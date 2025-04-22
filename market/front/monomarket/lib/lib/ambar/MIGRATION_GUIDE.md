# 0.8.x to 0.9.x

- `mergeLeft` was renamed to `mergeRight` (to follow ramda semantics)
Replace all usages of `mergeLeft ` to `assign` or `mergeRight`.

- `prop` is now less paranoid to combination of keys and sources. Now it checks keys only.
If you have used following trait (which is very unlikely), check source and throw exception manually.
