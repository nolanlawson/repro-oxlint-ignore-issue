# repro oxlint ignore issue

This repos an issue with oxlint where files are not ignored in certain cases, despite being specified in `"ignorePatterns"`.

Quick repro:

```bash
npm i
npm run lint
```

Here is what's happening. `"ignorePatterns"`:

```json
  "ignorePatterns": [
    "foo.js",
    "a/bar.js"
  ],
```

This works, and ignores both files:

```bash
oxlint -c .oxlintrc.json --fix
```

However, adding `.` to the end of the command causes `bar.js` to no longer be ignored:

```bash
oxlint -c .oxlintrc.json --fix .
```

If you run this second command, you'll see that `foo.js` is correctly ignored, but `a/bar.js` is not:

```diff
--- a/a/bar.js
+++ b/a/bar.js
@@ -1,2 +1,2 @@
-debugger
+
 console.log("Don't lint me!!")
```