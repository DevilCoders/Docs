=== How to debug ===
```
$ ya make -tt --test-stderr --test-param DEBUG_PORT=8031 --test-disable-timeout -F test_tech.py::test_debug
```
Then
```
$ curl 'http://localhost:8031/yandsearch?...'
```
