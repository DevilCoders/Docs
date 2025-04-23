# threads_connected*
Проверки: threads_connected, threads_connected_ppcmonitor.  
[Juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=(host%3Ddirect.prod_ppcdata%7Chost%3Ddirect.prod_mysql)%26service%3Dthreads_connected*).


## Описание { #description }
Проверяется наличие большого количества подключений к БД. Может служить сигналом о проблемах с железом у самой БД или проблемах у соседних шардов(порождается куча параллельных запросов в разные шарды).


## Диагностика { #diagnostics }
Зайти на указанную машину с базой. Для примера это будет ppcdata1-01i.yandex.ru с инстансом ppcdata1.

### Вариант 1
Смотрим через innotop и ищем долгие транзации, запоминаем conection_id(слева):
```sh
lm ppcdata1 innotop
```

### Вариант 2
Зайти в БД и поискать запросы через PROCESSLIST:
```sh
lm ppcdata1 -A
```
Откроется mysql-клиент в интерактивном режиме. Выполнить:
```sql
mysql> pager grep -v Sleep | less; SHOW FULL PROCESSLIST;
```

### Вариант 3
- Смотрим графики CPU/Memmory/Disk на серверах: [graphite/overview](https://ppcgraphite.yandex.ru/grafana/dashboard/db/common-systems-per-host?orgId=1)
- Смотрим графики CPU/Memmory/Disk на серверах(для MDB): [solomon/overview](https://solomon.yandex-team.ru/?cluster=internal-mdb_dom0&dc=by_cid_container&host=by_cid_container&project=internal-mdb&service=dom0&dashboard=internal-mdb-porto-instance&l.container=man-9uld86zjwpre3gwh.db.yandex.net&b=1h&e=)
- Смотрим графики PMM: [graphite/pmm-overview](https://ppcgraphite.yandex.ru/grafana/dashboard/db/pmm-mysql-overview?orgId=1)
- Смотрим графики метрик mysql(для MDB): [solomon/mysql-overview](https://solomon.yandex-team.ru/?project=internal-mdb&cluster=mdb_mdb2ktk8f8nilm6c8b8i&service=mdb&host=*&graph=auto&stack=false&dc=by_host&hideNoData=true&b=7d&e=&l.sensor=mysql_Threads_running)

## Решение { #solution }
Если известно, что выполняется на указанной базе какая-то работа — можно поставить downtime.

В остальных случаях:
- понять что это за транзакции и откуда они
- узнать, действительно ли они могут так долго работать
- оценить, можно ли их прибивать и не приведет ли это к поломке
- определить есть ли проблемы на других базах(не работают, тормозят)
- если можно прибивать запросы - прибить транзакцию

[Пример тикетов](https://st.yandex-team.ru/DIRECT-131356).
