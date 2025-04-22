rpslimiter
=====

Quota's storage sync

Syntax
------

```yaml
- quota-sync: default
  host: {{ HOST_ID }}
  path: /state.sync
  remote:
    host1: { proxy: http://127.0.0.1:8080 }
    host2: { proxy: http://127.0.0.1:8081 }
  interval: 10ms
  streams: 1
  full: false
```
Options
-------

**quota-print** (default="") quota storage id (fetcher module required)
**host** (required) local host id
**method** (default=POST) fetch action method.
**path** (default=/) fetch action path.
**remote** remote instances map (hostId -> action)
**interval** (default=50ms) sync interval
**streams** (default=1) streams, parallel requests per remote host
**full**  (default=false) sync full state