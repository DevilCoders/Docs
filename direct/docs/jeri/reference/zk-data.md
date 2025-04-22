# Важные данные в ZooKeeper

## Продакшен-ZooKeeper { #zk-prod }

`ppcback*`

### /direct/versions

Продакшеновые версии Директовых приложений.
Записываются и читаются скриптами `direct-version-set`, `direct-version-get`

### /direct/db-config.json

Продакшеновый db-config


### /direct/direct-apps.conf.yaml

Реестр приложений


### ... more to come ... { #more-p }


## Непродакшен-ZooKeeper { #zk-np }

`ppctest-zookeeper01i.sas.yp-c.yandex.net`, `ppctest-zookeeper01f.myt.yp-c.yandex.net`, `ppctest-zookeeper01v.vla.yp-c.yandex.net`

### /direct/release-state

Здесь `direct-release` хранит состояния релизов.

### и другое... { #more-np }

## Ссылки { #links }

- [Самое главное, что надо знать о ZooKeper](../things/zookeeper.md)
- [Руководство: разовые операции с ZK](../guide/zk-operations.md)
