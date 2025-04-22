RpsLimiter
===========

Build
------

```
ya m -r --checkout
```

Run
------

```
./rpslimiter -c ./rpslimiter.config
```

Test
-------

```
curl "localhost:9091/quota.acquire?quota=test"
curl "localhost:9091/quota.acquire?quota=test&test2=1"
```