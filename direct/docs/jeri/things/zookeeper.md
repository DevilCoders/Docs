# ZooKeeper

## Общее { #general }

ZooKeeper — распределенное key-value хранилище для небольших данных (конфиги, промежуточные состояния долгоживущих процессов и т.п.).

Также через него можно реализовывать распределенные блокировки.

Часто ZK используется как "распределенно-синхронизованная подсистема"
в более крупных системах.
Например, Clickhouse использует Zookeeper, чтобы хранить информацию о репликах в кластере.
В Директе через ZK синхронизуется запуск perl-скриптов на разных серверах (`switchman`).


## Структура данных { #data-model }

Именованная единица данных в ZK — нода. Ноды организованы в древовидную структуру, как файлы в файловой системе.
Отличие от файлов: каждая нода одновременно может быть родительской для других нод **И** содержать какой-то контент.

```
direct-zkcli -H ppctest-zookeeper01i.sas.yp-c.yandex.net ls -R /direct/release-state/testing
/direct/release-state/testing/direct
/direct/release-state/testing/oneshot
/direct/release-state/testing/test
/direct/release-state/testing/java-recom-tracer
/direct/release-state/testing/ess-router
/direct/release-state/testing/canvas
/direct/release-state/testing/java-logviewer
/direct/release-state/testing/steps
/direct/release-state/testing/java-api5
/direct/release-state/testing/java-jobs
/direct/release-state/testing/java-web
/direct/release-state/testing/lb-moderation
/direct/release-state/testing/db-schema
/direct/release-state/testing/lb-alw
/direct/release-state/testing/java-b2yt
/direct/release-state/testing/java-intapi
/direct/release-state/testing/java-alw
/direct/release-state/testing/binlogbroker
/direct/release-state/testing/b2clh
/direct/release-state/testing/mysql2yt-full
```


## Ссылки { #links }

- [как потыкать наши ZooKeeper-ы](../guide/zk-operations.md)
- [Apache Zookeeper](https://zookeeper.apache.org/)
- TODO: про switchman (короткое концептуальное описание)
- TODO: про zk-delivery (короткое концептуальное описание)
- TODO: zk-sync (коротко концепцию + инструкцию)
- [Справочник: важные данные в Директовых ZooKeeper](../reference/zk-data.md)



