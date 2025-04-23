Solomon Services
================

Source code of all micro-services located in this folder.

Ports
-----

To prevent ports collisions we use next scheme to choose port number:

```
+---+---+---+---+
| a | b | c | d |
+---+---+---+---+
```

Where:

  * **a.** API type

    4 - private

    5 - public for yandex

    6 - cloud public for all users

  * **b.** protocol type

    5 - HTTP

    6 - HTTPS (previously MessageBus, not used now)

    7 - gRPC

  * **cd.** service type

    00 - Stockpile

    10 - Coremon
    
    15 - Metabase

    20 - Fetcher

    30 - Alerting

    40 - Gateway

    50 - Dumper

    60 - Ingestor

    70 - DataProxy

    80 - MemStore/ProjectManager

    90 - NameResolver/YasmGateway

NOTE: ports starting from `8*` are considered legacy and will be removed.

**Examples:**

  * _5700_ - public gRPC API of Stockpile

  * _4540_ - private HTTP API of Gateway

  * _4720_ - private gRPC API of Fetcher

