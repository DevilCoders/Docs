# Секция mdb

- [Секция databases](#секция-databases)
- [Секция alertsets](#секция-alertsets)
    - [Алиасы для сигналов](#алиасы-для-сигналов)
- [Нюансы](#нюансы)
- [Где взять путь до кластера](#где-взять-путь-до-кластера)

Пример:
```yaml
mdb:
  databases:
    postgresql:maps_cloud.maps_folder.maps_pg_cluster: default
    mongodb:maps_cloud.maps_folder.maps_mongo_cluster: default
    clickhouse:maps_cloud.maps_folder.maps_clickhouse_cluster: default
    redis:maps_cloud.maps_folder.maps_redis_cluster: default

  alertsets:
    default:
      settings:
        notifications: [chat, team]  # Кому отправлять уведомления
      alerts:
        cpu_load:
          signal: '%cpu_perc'  # Процент потребления CPU
          warn: 50
          crit: 85
          tier: master  # Только на мастере
```

## Секция databases

Определяет соответствие `кластер БД` -> `набор алертов`.
Формат: `<тип_базы>:<имя_облака>.<имя_каталога>.<имя кластера>: <имя_алертсета>`

`<тип_базы>` может быть один из: `postgresql`, `mongodb`, `clickhouse`, `redis`.
Как где взять остальные компоненты, можно прочитать [ниже](#где-взять-путь-до-кластера).

Пример:
```yaml
databases:
  posgtresql:meta-search.locdoc-dev.daas: first
  mongodb:mdb-junk-cloud.mdb-junk.testcluster: second
  clickhouse:mdb-junk-cloud.mdb-junk.vgtest: third
  redis:mdb-junk-cloud.mdb-junk.test: fifth
```

## Секция alertsets

Базовый формат описан [тут](./common.md#Секция-alertsets).

Внутри алерта добавлено необязательное поле `tier`, которое ограничивет тип инстанса базы, с которого собираются метрики.
Возможные значения:

* `master` - учитываются только значения с мастера
* `replica` - учитываются только значения с реплик

По умолчанию учитываются данные со всех инстансов. Поле игнорируется для ClickHouse.

Для удобства в Monitorado заведены алиасы для наиболее полезных сигналов.
Их названия начинаются с символа `%`.

### Алиасы для сигналов

#### Общие для всех типов

Алиас | Сигнал | Описание
--------|---------|---------
%cpu_perc | perc(portoinst-cpu_usage_cores_tmmv, portoinst-cpu_guarantee_cores_tmmv) | Процент потребления CPU относительно гарантированного лимита
%max_cpu_perc | perc(portoinst-cpu_usage_cores_txxx, portoinst-cpu_guarantee_cores_txxx) | Процент потребления CPU относительно гарантированного лимита (максимальный по инстансам)
%mem_anon_perc | perc(portoinst-anon_usage_gb_tmmv, portoinst-memory_guarantee_gb_tmmv) | Процент потребления памяти (anon) относительно гарантированного лимита
%max_mem_anon_perc | perc(portoinst-anon_usage_gb_txxx, div(portoinst-memory_guarantee_gb_tmmv, counter-instance_tmmv)) | Процент потребления памяти (anon) относительно гарантированного лимита (максимальный по инстансам)
%mem_perc | perc(portoinst-memory_usage_gb_tmmv, portoinst-memory_guarantee_gb_tmmv) | (НЕ рекомендуется использовать, см. %mem_anon_perc) Процент потребления памяти относительно гарантированного лимита **с учетом файловых кэшей**
%net_perc | perc(portoinst-net_mb_summ, portoinst-net_guarantee_mb_summ) | Процент портребления сети относительно гарантированного лимита
%cpu_wait | portoinst-cpu_wait_cores_tmmv | Время ожидания процессов в очереди
%used_space_perc | push-disk-used_bytes_/var/lib/{type}_tmmx, push-disk-total_bytes_/var/lib/{type}_tmmx) | Процент занятого места на диске (`{type}` заменяется на тип базы)
%replica_lag_avg | зависит от типа базы (см. ниже) | Среднее отставание реплик от мастера, либо задержка репликации таблиц для Clickhouse (сек)

#### Специфичные для PostgreSQL

Алиас | Сигнал | Описание
--------|---------|---------
%statm_avg | or(push-pooler-avg_query_time_tmmx, 0) | Среднее время выполнения отдельных стейтментов (мс)
%statm_p95 | or(push-pooler-query_0.95_tmmx, 0) | 95-ый перцентиль времени выполнения отдельных стейтментов (мс)
%statm_p99 | or(push-pooler-query_0.99_tmmx, 0) | 99-ый перцентиль времени выполнения отдельных стейтментов (мс)
%trans_avg | or(push-pooler-avg_xact_time_tmmx, 0) | Среднее время выполнения транзакций (мс)
%trans_p95 | or(push-pooler-transaction_0.95_tmmx, 0) | 95-ый перцентиль времени выполнения транзакций (мс)
%trans_p99 | or(push-pooler-transaction_0.99_tmmx, 0) | 99-ый перцентиль времени выполнения транзакций (мс)
%replica_lag_avg | div(push-postgres-replication_lag_tmmx, push-postgres-is_replica_tmmx) | Среднее отставание реплик от мастера (сек)

#### Специфичные для MongoDB

Алиас | Сигнал | Описание
--------|---------|---------
%conn_perc | perc(push-server_status_admin_connections.current_tmmx, sum(push-server_status_admin_connections.current_tmmx, push-server_status_admin_connections.available_tmmx)) | Процент количества установленных соединений относительно лимита
%replica_lag_avg | div(push-replset_status-replicationLag_tmmx, push-server_status_admin_repl.secondary_tmmx) | Среднее отставание реплик от мастера (сек)

#### Специфичные для ClickHouse

Алиас | Сигнал | Описание
--------|---------|---------
%query_avg | div(div(push-ch_system_events_QueryTimeMicroseconds_rate_tmmx, push-ch_system_events_Query_rate_tmmx), 1000)  | Среднее время выполнения запроса (мс)
%replica_lag_avg | div(push-ch_replication-max_absolute_delay_tmmx, counter-instance_tmmv) | Средняя задержка репликации таблиц (сек)
%zk_query_avg | push-zk_avg_latency_tmmx | Среднее время выполнения запроса в ZooKeeper (мс)
%zk_used_space_perc | perc(push-disk-used_bytes_/var/lib/zookeeper_tmmx, push-disk-total_bytes_/var/lib/zookeeper_tmmx) | Процент занятого места на диске в ZooKeeper

#### Специфичные для Redis

Алиас | Сигнал | Описание
--------|---------|---------
%connected_clients | push-redis_connected_clients_tmmx | Количество клиентских подключений
%ops_per_sec | push-redis_instantaneous_ops_per_sec_tmmx | Количество обработанных команд в секунду
%miss_rate| div(mul(diff(counter-instance_tmmv, push-redis_hit_rate_tmmx), 100), normal()) | Средний процент неудачных поисков ключей в главном словаре
%replica_lag_avg | div(push-redis_master_last_io_seconds_ago_tmmx, counter-instance_tmmv) | Среднее отставание реплик от мастера (сек)

## :warning: Нюансы

1. Для алертов на `%cpu_perc`, `%mem_perc`, `%net_perc` и `%cpu_wait` имеет смысл выставлять `tier: master`, чтобы не мерять среднюю температуру по больнице.

1. Если после срабатывания алерта на `%used_space_perc` вы почистили базу, на сигнал это отразится не сразу.
   Можно включить даунтайм у созданного чека в Juggler на пару дней, либо (в случае PostgreSQL) руками запустить команду [VACUUM FULL](https://postgrespro.ru/docs/postgresql/10/sql-vacuum) на нужных таблицах.

## Где взять путь до кластера

1. Открываем [внутренний интерфейс Облака](https://yc.yandex-team.ru)
1. Выбираем нужное облако (cloud) и каталог (folder) с помощью переключалки в верхнем правом углу
   ![](https://jing.yandex-team.ru/files/nikshel/Yandeks.Oblako_2019-04-02_14-01-31.png)
1. Находим наш кластер
  ![](https://jing.yandex-team.ru/files/nikshel/Yandeks.Oblako_2019-04-02_14-07-26.png)
1. Склеиваем имена через точку

Для кластера со скриншотов путь будет `mdb-junk-cloud.mdb-junk.bugatron`.
