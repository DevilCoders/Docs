# geo_position_master_*
Проверки: geo_position_master, geo_position_master_ppcmonitor.  
[Juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=(host%3Ddirect.prod_ppcdata%7Chost%3Ddirect.prod_mysql)%26service%3Dgeo_position_master*).


## Описание { #description }
Проверяется географическое расположение мастера. Если мастер оказывается в Финляндии(MAN), то загорается лампочка. Переключение мастеров в MDB происходит в автоматическом режиме. Нахождение мастера в Финляндии - это крайний случай. При работе из этого ДЦ, время ответа запросов возрастает в 2-3 раза, поэтому переключать такие мастера надо на другие доступные реплики. Допускается короткое время работы на таких машинах во время учений или поломки соседних реплик.


## Диагностика { #diagnostics }
Зайти на указанный инстанс и посмотреть имя сервера, либо посмотреть мастера в yc.yandex-team.ru, либо в обсерваториуме.

### Вариант 1
Заходим на ppcback* или ppcdev*, подключаемся к БД и смотрим её имя:
```sh
dbs-sql pr:ppc:1 'SELECT @@hostname'
```

### Вариант 2
Зайти в MDB облако и посмотреть текущего мастера:

1. [yandex cloud](https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/managed-mysql)
2. зайти в нужный инстанс
3. щелкнуть слева по вкладке "Хосты"

### Вариант 3
Зайти на Observatorium и найти нужный инстанс:  

[replication_schema](https://observatorium.common.yandex.ru/storages/replication_schema)

## Решение { #solution }
Если известно, что выполняется на указанной базе какая-то работа — можно поставить downtime.

В остальных случаях:
- попробовать переключить мастер на другую реплику(в "Хосты" слева сверху будет "Переключить мастер") 
- обратиться за помощью к DirectAdmin дежурному

