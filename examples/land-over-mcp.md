# Landing a site your assistant built

Your assistant holds the files. This publishes them.

## 1 · Check it first (no account needed)

```bash
curl -X POST https://api.promptswing.com/api/assess \
  -H 'content-type: application/json' \
  -d '{"files":[{"path":"index.html","content":"<html>…</html>"}]}'
```

Fix anything it reports `missing`. Findings marked `not_run` are checks that
could not run on what you sent — they are not passes.

## 2 · Connect

The merchant authorises PromptSwing from their own account. **Hosting requires an
active subscription; `land_site` refuses without one and says so.**

## 3 · Land

```
land_site({ files: [...] })
```

If a store is already live this does **not** publish on the first call. It
returns what would be replaced, a confirmation, and **every file that would stop
being served** — a landing publishes exactly what it is sent. Read that list,
then call again with the confirmation.

## 4 · Change it later, without rebuilding

```
read_site()                        → the files that are live
update_page({ path, content })     → change one, leave the rest untouched
add_page / delete_page             → one file at a time
revert_site({ release })           → put it back
```

`update_page` publishes as a **patch**, which cannot delete what it was not
shown: images, the favicon and every other page survive an edit that never
mentioned them.
