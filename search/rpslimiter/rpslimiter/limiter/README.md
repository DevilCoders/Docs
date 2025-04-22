rpslimiter
=====

Quota's storage
Returns true if consumed, else - fallback actions

Syntax
------

```yaml
- rpslimiter: default
  no-quota: false
  invalid-index: false
```
Options
-------

**no-quota** quota not found action
**invalid-index** index is invalid action
**limited** on limited action

**rpslimiter** (default="") quota storage id (quotas module required)
