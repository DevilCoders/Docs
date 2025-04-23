# RAFT leader

ORLY use etcd under the hood, which in it's turn, use RAFT.

Etcd become slow (RTT damn it) when RAFT leader goes to MAN, so leader must be moved back:

1. See where it is and pick ID for SAS candidate:

```
root@nhkxeclli2ovmwr2:/place/db/iss3/instances/nhkxeclli2ovmwr2_production_orly_ICf9elEjK1K# /opt/etcd/etcdctl  --write-out=table --endpoints http://nhkxeclli2ovmwr2.vla.yp-c.yandex.net:2379,http://cplptii2dg7qig4j.man.yp-c.yandex.net:2379,http://jyd2fsnhbktrkq6u.sas.yp-c.yandex.net:2379,http://pbsocv2ek76juvuk.vla.yp-c.yandex.net:2379,http://b3blcwjmcm2kbhpk.sas.yp-c.yandex.net:2379 endpoint status
+--------------------------------------------------+------------------+------------+---------+-----------+------------+-----------+------------+--------------------+--------+
|                     ENDPOINT                     |        ID        |  VERSION   | DB SIZE | IS LEADER | IS LEARNER | RAFT TERM | RAFT INDEX | RAFT APPLIED INDEX | ERRORS |
+--------------------------------------------------+------------------+------------+---------+-----------+------------+-----------+------------+--------------------+--------+
| http://nhkxeclli2ovmwr2.vla.yp-c.yandex.net:2379 | 5c088115d80c4867 | 3.4.0-rc.0 |  163 MB |     false |      false |    196720 |  494460502 |          494460502 |        |
| http://cplptii2dg7qig4j.man.yp-c.yandex.net:2379 | 6dc8722e1c039d69 | 3.4.0-rc.0 |  163 MB |      true |      false |    196720 |  494460504 |          494460504 |        |
| http://jyd2fsnhbktrkq6u.sas.yp-c.yandex.net:2379 | 787c439c00866395 | 3.4.0-rc.0 |  163 MB |     false |      false |    196720 |  494460505 |          494460505 |        |
| http://pbsocv2ek76juvuk.vla.yp-c.yandex.net:2379 | 4c6c7aa0ecb1a849 | 3.4.0-rc.0 |  163 MB |     false |      false |    196720 |  494460505 |          494460505 |        |
| http://b3blcwjmcm2kbhpk.sas.yp-c.yandex.net:2379 | f88803642a04701e | 3.4.0-rc.0 |  163 MB |     false |      false |    196720 |  494460506 |          494460506 |        |
+--------------------------------------------------+------------------+------------+---------+-----------+------------+-----------+------------+--------------------+--------+
root@nhkxeclli2ovmwr2:/place/db/iss3/instances/nhkxeclli2ovmwr2_production_orly_ICf9elEjK1K#
```

2. Move leader back to SAS instance:

```
root@nhkxeclli2ovmwr2:/place/db/iss3/instances/nhkxeclli2ovmwr2_production_orly_ICf9elEjK1K# /opt/etcd/etcdctl move-leader 787c439c00866395 --endpoints http://nhkxeclli2ovmwr2.vla.yp-c.yandex.net:2379,http://cplptii2dg7qig4j.man.yp-c.yandex.net:2379,http://jyd2fsnhbktrkq6u.sas.yp-c.yandex.net:2379,http://pbsocv2ek76juvuk.vla.yp-c.yandex.net:2379,http://b3blcwjmcm2kbhpk.sas.yp-c.yandex.net:2379
Leadership transferred from 6dc8722e1c039d69 to 787c439c00866395
root@nhkxeclli2ovmwr2:/place/db/iss3/instances/nhkxeclli2ovmwr2_production_orly_ICf9elEjK1K#
```
