# mysql-slowlog-parser - Библиотека для парсинга записей slow query лога mySQL 5.7 с перконовскими расширениями

### Что делает
Парсит запись mySQL slow query лога версии 5.7 с [расширениями percona](https://www.percona.com/doc/percona-server/5.7/diagnostics/slow_extended.html). Такая запись выглядит примерно так:
```
# Time: 2021-10-07T00:06:25.879595+03:00
# User@Host: ppc[ppc] @ direct-perl-scripts-man-yp-1.man.yp-c.yandex.net [2a02:6b8:c0b:1996:0:648:fa3:0]  Id: 37856411
# Schema: ppc  Last_errno: 1260  Killed: 0
# Query_time: 10.561406  Lock_time: 0.000286  Rows_sent: 203733  Rows_examined: 4375576  Rows_affected: 0
# Bytes_sent: 13023285  Tmp_tables: 3  Tmp_disk_tables: 1  Tmp_table_sizes: 16384
# InnoDB_trx_id: 0
# QC_Hit: No  Full_scan: Yes  Full_join: No  Tmp_table: Yes  Tmp_table_on_disk: Yes
# Filesort: No  Filesort_on_disk: No  Merge_passes: 0
#   InnoDB_IO_r_ops: 0  InnoDB_IO_r_bytes: 0  InnoDB_IO _r_wait: 0.000000
#   InnoDB_rec_lock_wait: 0.000000  InnoDB_queue_wait: 0.000000
#   InnoDB_pages_distinct: 8191
SET timestamp=1633554385;
...QUERY...
```
В результате парсинга выдает объект класса SlowLogRecord с типизированными полями.

Примеры команд для получения slow query логов через yc cloud api (смотреть поле `raw` в ответе):
```shell
export IAM_TOKEN=$(yc iam create-token)
curl -H "Authorization: Bearer ${IAM_TOKEN}" "https://gw.db.yandex-team.ru:443/managed-mysql/v1/clusters/mdb2809bjdkkb5faglq1:logs?serviceType=MYSQL_SLOW_QUERY&fromTime=2022-04-13T05:00:00.000Z&pageSize=5"
```
