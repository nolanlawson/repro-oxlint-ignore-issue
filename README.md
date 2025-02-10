# repo oxlint ignore issue

This repos an issue with oxlint where files are not ignored in certain cases, despite being specified in `"ignorePatterns"`.

`"ignorePatterns"`:

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
oxlint -c .oxlintrc.json --fix
```