report
===========

Count various stats about requests and responses.
Similar to [balancer report module](https://wiki.yandex-team.ru/balancer/cookbook/#tablicadostupnyxsignalov).

Syntax
------

Module has only one required param:
```
- report:
    uuid: my_uuid
```

Also optional params may be specified to collect additional stats:
```
- report:
    uuid: my_uuid
    outgoing_codes: [404, 501]
    time_ranges: [1ms, 5ms, 100ms, 1, 2, 3, 10s]
    backend_time_header: x-backend-processing-time
    connect_time_header: x-backend-connect-time
```
