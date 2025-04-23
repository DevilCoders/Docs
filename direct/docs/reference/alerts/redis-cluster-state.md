# redis-cluster-state


## Описание { #description }

Горящая проверка означает, что структура одного из наших redis-кластеров пришла в неожиданное состояние.

Ожидания от структуры:

- каждый диапазон ключей обрабатывается тремя репликами
- мастера живут на разных хостах
- все реплики живые

**Во время недоступности одного ppcback проверка ожидаемо загорается.**

Когда ppcback возвращается, надо запустить автопочинку по инструкции ниже.


## Диагностика { #diagnostics }

С ppcback смотрим состояния кластеров (имя кластера -- в параметре `-r`):

```
redis-check.py -r redis -vv -t
redis-check.py -r redis_cache -vv -t
```

Скрипт выводит текущий статус (первой строчкой) и табличку с диапазонами, серверами и мастерами.

Пример нормального состояния:

```
ppcback01f% redis-check.py -r redis -t          
0;OK;from:redis-check.py -r redis; more info: redis-check.py -r redis -vv -t
+-------------------------+--------+------------+-------------+-------+
|         dc\slots        | 0-5460 | 5461-10922 | 10923-16383 | Empty |
+-------------------------+--------+------------+-------------+-------+
| ppcback01e.da.yandex.ru |  6379  |    6380    |    *6381    |       |
|   ppcback01f.yandex.ru  | *6379  |    6381    |     6380    |       |
| ppcback01i.da.yandex.ru |  6379  |   *6380    |     6381    |       |
+-------------------------+--------+------------+-------------+-------+
X_X - dead
* - master
(L) - Dataset loading in memory
```

Пример проблемного состояния (два мастера на одной машине):

```
ppcback01f% redis-check.py -r redis_cache -t    
2;from:redis-check.py -r redis_cache; cluster state wrong; more info: redis-check.py -r redis_cache -vv -t
+-------------------------+--------+------------+-------------+-------+
|         dc\slots        | 0-5460 | 5461-10922 | 10923-16383 | Empty |
+-------------------------+--------+------------+-------------+-------+
| ppcback01e.da.yandex.ru |  6411  |    6413    |    *6412    |       |
|   ppcback01f.yandex.ru  |  6411  |    6412    |     6413    |       |
| ppcback01i.da.yandex.ru | *6411  |   *6412    |     6413    |       |
+-------------------------+--------+------------+-------------+-------+
X_X - dead
* - master
(L) - Dataset loading in memory
```


## Решение { #solution }

Скрипт умеет чинить типичные проблемы. 

Посмотреть, какие команды предлагает выполнить скрипт (в `-r` подставить нужный кластер):

```
ppcback01f% redis-check.py -r <redis|redis_cache> -t --repair
2;from:redis-check.py -r redis_cache; cluster state wrong; more info: redis-check.py -r redis_cache -vv -t
+-------------------------+--------+------------+-------------+-------+
|         dc\slots        | 0-5460 | 5461-10922 | 10923-16383 | Empty |
+-------------------------+--------+------------+-------------+-------+
| ppcback01e.da.yandex.ru |  6411  |    6413    |    *6412    |       |
|   ppcback01f.yandex.ru  |  6411  |    6412    |     6413    |       |
| ppcback01i.da.yandex.ru | *6411  |   *6412    |     6413    |       |
+-------------------------+--------+------------+-------------+-------+
X_X - dead
* - master
(L) - Dataset loading in memory

Failover commands:
redis-cli -h ppcback01f.yandex.ru -p 6411 cluster failover
After failover table should look like this:
+-------------------------+--------+------------+-------------+-------+
|         dc\slots        | 0-5460 | 5461-10922 | 10923-16383 | Empty |
+-------------------------+--------+------------+-------------+-------+
| ppcback01e.da.yandex.ru |  6411  |    6413    |    *6412    |       |
|   ppcback01f.yandex.ru  | *6411  |    6412    |     6413    |       |
| ppcback01i.da.yandex.ru |  6411  |   *6412    |     6413    |       |
+-------------------------+--------+------------+-------------+-------+
X_X - dead
* - master
(L) - Dataset loading in memory
```

Если все выглядит ожидаемо, то применить (к предыдущей команде добавить `--apply`):

```
ppcback01f% redis-check.py -r <redis|redis_cache> -t --repair --apply
2;from:redis-check.py -r redis_cache; cluster state wrong; more info: redis-check.py -r redis_cache -vv -t
+-------------------------+--------+------------+-------------+-------+
|         dc\slots        | 0-5460 | 5461-10922 | 10923-16383 | Empty |
+-------------------------+--------+------------+-------------+-------+
| ppcback01e.da.yandex.ru |  6411  |    6413    |    *6412    |       |
|   ppcback01f.yandex.ru  |  6411  |    6412    |     6413    |       |
| ppcback01i.da.yandex.ru | *6411  |   *6412    |     6413    |       |
+-------------------------+--------+------------+-------------+-------+
X_X - dead
* - master
(L) - Dataset loading in memory

Failover commands:
redis-cli -h ppcback01f.yandex.ru -p 6411 cluster failover
After failover table should look like this:
+-------------------------+--------+------------+-------------+-------+
|         dc\slots        | 0-5460 | 5461-10922 | 10923-16383 | Empty |
+-------------------------+--------+------------+-------------+-------+
| ppcback01e.da.yandex.ru |  6411  |    6413    |    *6412    |       |
|   ppcback01f.yandex.ru  | *6411  |    6412    |     6413    |       |
| ppcback01i.da.yandex.ru |  6411  |   *6412    |     6413    |       |
+-------------------------+--------+------------+-------------+-------+
X_X - dead
* - master
(L) - Dataset loading in memory

Starting failover...
Running ['redis-cli', '-h', 'ppcback01f.yandex.ru', '-p', '6411', 'cluster', 'failover']
OK
```

Проверить, что структура стала ожидаемой:

```
ppcback01f% redis-check.py -r <redis|redis_cache> -t    
```

## Ссылки { #links }
- Документация по redis-cluster: <https://redis.io/commands#cluster>
