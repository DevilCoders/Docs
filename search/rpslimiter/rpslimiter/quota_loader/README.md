rpslimiter
=====

Quota's storage

Syntax
------

```yaml
- quotas: default
  test1:
    by:
      user: true
      service: false
    by-key:
      user:
        admin: 10000
        robot: 10
    tags:
    - user
    quota: 1000
    interval: 1000
    sync: true
  test2: { quota: 1000 }
```
Options
-------

**quotas** (default=""): global quota-storage id
**by-key**: custom quota values for specific keys
    key:
      value: quota-value
  A key must be `export`ed in a router to be used here
  If multiple keys are exported and their values match the quota,
  any of the quotas will be used, which one exactly is undefined.
  You can override only quota value here, but not interval or other options.
**(everything else)**: quota configuration
  **by**: map quota index field (string) to required flag(bool)
  **tags**: unistat tags list
  **interval** (default=1000): quota's interval milliseconds
  **quota**: quota limit per interval
  **sync** (default=true): quota sync required
