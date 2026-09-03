# Attaching files to a Linear issue

Read this when the request supplies a screenshot, image, log, or document, and when a
supplied file has no path on disk.

- [Find the file first](#find-the-file-first)
- [Upload procedure](#upload-procedure)
- [Verify](#verify)

## Find the file first

A supplied file is not always on disk. Work through these in order, and only report a
missing file after all of them fail.

1. **A path in the request.** Use it directly.
2. **A pasted image.** A screenshot pasted into the chat is stored as base64 in the
   session transcript, not as a file. Extract it:

   ```bash
   python3 - <<'PY'
   import json, base64, hashlib
   f = "<session transcript>.jsonl"   # ~/.claude/projects/<project-slug>/<session-id>.jsonl
   def walk(o):
       if isinstance(o, dict):
           if o.get("type") == "image" and isinstance(o.get("source"), dict) and o["source"].get("data"):
               yield o["source"]
           for v in o.values():
               yield from walk(v)
       elif isinstance(o, list):
           for v in o:
               yield from walk(v)
   seen = set()
   for line in open(f):
       line = line.strip()
       if not line:
           continue
       try:
           rec = json.loads(line)
       except ValueError:
           continue
       for src in walk(rec):
           raw = base64.b64decode(src["data"])
           h = hashlib.sha256(raw).hexdigest()[:12]
           if h in seen:
               continue
           seen.add(h)
           name = f"attach-{h}." + src.get("media_type", "image/png").split("/")[-1]
           open(name, "wb").write(raw)
           print(name, len(raw))
   PY
   ```

   The same paste can appear more than once in the transcript. De-duplicate by hash, as
   above, or the issue gets the same image twice.
3. **Open each extracted file and look at it.** A transcript can hold images from earlier,
   unrelated messages. Confirm the file is the one the request refers to before you upload
   it.

If no file is found, say which locations were searched. Do not ask the operator to attach
it until the transcript has been checked.

## Upload procedure

Linear takes three steps per file. Complete all three for one file before starting the
next, because the signed URL expires in 60 seconds.

1. `prepare_attachment_upload` with `issue`, `filename`, `contentType`, and the exact byte
   `size`. A wrong size fails the upload.
2. `PUT` the raw bytes to `uploadRequest.url` with `curl --data-binary @<path>`. Send every
   header from `uploadRequest.headers` verbatim, including letter case. A missing or
   changed header returns HTTP 403. Do not base64-encode the body. Expect HTTP 200.
3. `create_attachment_from_upload` with the `assetUrl` from step 1. This step only creates
   the attachment record; it uploads nothing.

Give each attachment a `title` that names what it is, and a `subtitle` that names the
source, for example "Supplied by <person> in Slack — visual reference only".

## Verify

Re-read the issue with `get_issue` and confirm the file is in `attachments`. A 200 on the
PUT is not proof that the attachment exists.
