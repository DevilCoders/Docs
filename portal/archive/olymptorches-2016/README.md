# olymptorches_2016
Global map with fire-points

#### Ручка для клика
```
/portal/olymptorch/add
```
Она задается в экспорте **covers_v14** id_event=olymprio json_animate

#### Конфиг для скриптов
В нем можно настраивать хост базы данных, дистанцию поиска ближайшей точки и метод подключения к монге
```
etc/Conf.pm
```

#### Парсер лога и обновление базы кликов
Этот скрипт должен работать на всех машинках бэкенда. Он читает лог бэкенда ```/var/log/www/olymptorch.log.yyyymmdd```, парсит его, и записывает данные в MongoDB

```--debug=3``` включает режим [developerdebug]
```
* *  *  *  *  www-data /opt/www/olymptorches_2016/scripts/push.pl -l >>/var/log/www/export_torches_push.log 2>&1
```

Последняя обработанная позиция лога записывается в файл ```/var/log/www/olymptorch.pos.yyyymmdd``` в формате filename:pos

#### Генератор json-файлов с результатами
Должен работать на экспортящих машинках
```
* *  *  *  *  www-data /opt/www/olymptorches_2016/scripts/fetch.pl >>/var/log/www/export_torches_fetch.log 2>&1
```

В коде заданы три типа файлов. Координаты сортируются по уникальным хитам и выбирается топ
```perl
    my $files = {
        sm => 1000,
        md => 3000,
        lg => 5000,
    };
```
Плюс к этому еще файл со счетчиком и файл all, куда пишутся все координаты, где есть клики.

В результате получается 4 файла, которые раскладываются на весь кластер нативным механизмом экспортов:
```
/var/exports/wrk/torches_md.json
/var/exports/wrk/torches_lg.json
/var/exports/wrk/torches_sm.json
/var/exports/wrk/torches_all.json
/var/exports/wrk/torches_cn.json
```

Ссылка на файл с результатами задается в экспорте **covers_v14** id_event=olymprio json_animate
```
BaseUrl : https://www.yandex.ru/portal/torches/
Sizes: { sm: "sm.json", md: "md.json", lg: "lg.json", cn: "cn.json" }
```

  * sm - small
  * md - medium
  * lg - large
  * all - all
  * cn - total counter only

Адрес на файл формируется из BaseUrl + Size, чтобы получилось https://www.yandex.ru/portal/torches/sm.json

### Заливка точек с нуля

./tools/whitelist_reload.pl tools/geo_min.pl
либо для использование для оригинальных точк
./tools/whitelist_reload.pl

### madm options
  * torches_stop_pushing=1 - остановить парсер скрипта и запись данных в базу
  * torches_turnoff_spam_check=1 - отключить проверку на спам
  * torches_stop_fetching=1 - отключить получение данных и генерацию json

### nginx

```
location ~ ^/portal/torches/(sm|md|lg|cn|all).json$ {
    root /var/exports/wrk;
    set $file "torches_$1.json";
    try_files "/${file}" =404;
}

location ~ ^/portal/olymptorch/.* {
    limit_except    GET { deny all; }
    fastcgi_pass    unix:/tmp/morda-v21d3.sock;
}

```

### utils
`./tools/uniq_drop.pl` - поудалять коллекции с униками

`./tools/whitelist_reload.pl` - загрузить whitelist (данные лежат в tools/whitelist_dataset.pl)

### Juggler-проверки
#### torches_count_t
```
/usr/bin/jctl add check -host portal_wfront -service torches_count_t -methods GOLEM -children
/usr/bin/jctl add active -host portal_wfront -service torches_count_t -module graphite -kwargs '{"CRIT": "metric < 10", "WARN": "metric < 10", "metric": "movingAverage(transformNull(sumSeries(servers.portal.wfront.torches.*.torches_count_t)), \"15mins\")", "base_url": "http://graphite.wdevx.yandex.net"}'
```

#### torches_count_u
```
/usr/bin/jctl add check -host portal_wfront -service torches_count_u -methods GOLEM -children
/usr/bin/jctl add active -host portal_wfront -service torches_count_u -module graphite -kwargs '{"CRIT": "metric < 10", "WARN": "metric < 10", "metric": "movingAverage(transformNull(sumSeries(servers.portal.wfront.torches.*.torches_count_u)), \"15mins\")", "base_url": "http://graphite.wdevx.yandex.net"}'
```



### release
Собирается как всегда через **make release**

**package** =  portal-morda-olymptorches2016

**teamcity** = http://quigon.yandex.ru/viewType.html?buildTypeId=PortalMorda_PortalMordaOlymptorches2016

**conductor** = https://c.yandex-team.ru/packages/portal-morda-olymptorches2016

**deps** = libmongodb-perl =0.702.2-3~portal (https://metacpan.org/pod/release/FRIEDO/MongoDB-0.702.2/lib/MongoDB.pm)

### MongoDB

#### Схема бд

**whitelist** - белый список координат. count_t - общий счетчик кликов, count_u - счетчик уникальных кликов. Json-файлы для отрисовки карты строятся по **count_u**.

**uniq_NN** - партишены для учета уников по yandexuid. Если такой yandexuid еще не кликал, тогда в whitelist'e у нужных координат обновится счетчик count_u

**counters** - дневные счеткики
ключ
type : 'all' | 'country' | 'district' | 'city'
geoid : '10000' ,// или geoid региона

запись хранить в себе общий счетчки count_u + YYYYDDMM дневной счетчик
на базе которого создается top для сводок

стоит сделать db.counters.drop() перд запуском в прод


#### Настройка бд
Если проблема ```Failed global initialization: BadValue Invalid or no user locale set. Please ensure LANG and/or LC_* environment variables are set correctly.``` Сделать:
```
echo 'export LC_ALL=C' >> ~/.bashrc && . ~/.bashrc
```
#### Понижение версии authSchema у монги
Для работы libmongodb-perl-0.702.2-3~portal с монгой нужно понизить версию authSchema (драйвер умеет работать с 3 версией, на наших же монгах по-умолчанию 5 версия):
```
> use admin
switched to db admin

> db.grantRolesToUser ( "root", [{ role: "__system", db: "admin" } ] )

> db.getSiblingDB("admin").system.version.update({ _id: "authSchema" },{ $set: { currentVersion: 3 } });
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
```
Проверяем:
```
> db.system.version.find()
{ "_id" : "authSchema", "currentVersion" : 3 }
```
Затем нужно перезапустить все монги и пересоздать пользователей.

#### cheatsheet
найти запись уника по yandexuid
```
db.uniq_95.find({"yuid": "4952238391469134816"});
```

найти point по _id
```
db.whitelist.find({"_id" : ObjectId("5790ebf1600468e050000000")}).pretty();
```

найти точки, ближайшие к заданной координате coordinates:[ lon, lat ]
```
db.whitelist.find({lon_lat: {$near: { $geometry: { type : "Point", coordinates : [ 134.93, 45.95 ] }, $maxDistance: 1000 }}} );
```

добавить точку в whitelist coordinates:[lon,lat]
```
db.whitelist.insert({"lon_lat": {"type":"Point", "coordinates":[134.93, 45.95]}, "name_ru":'test', "geoid":"0"});
```

посчитать, сколько всего уников
```
db.whitelist.aggregate([{$group:{"_id":null, "total": {$sum: "$count_u" } } }])
```

получить 5 топ точек, где количество хитов больше 1
```
db.whitelist.find({"count_u":{$gt:1}}).sort({"count_u":-1}).limit(5);
```

обновить каунтер уникальных хитов у всех точек
```
db.whitelist.updateMany({},{$set:{"count_u":2}});
```

накрутить счетчик уников для точки по _id, которую надо предварительно найти
```
db.whitelist.update({"_id":ObjectId("5792212ed5490333fd987df0")},{$set:{"count_u":10}});
```

удалить точку по geoid
```
db.whitelist.remove({'geoid':'0'});
```

удалить точку по _id
```
db.whitelist.remove({"_id":ObjectId("5790ebf1600468e050000000")});
```

создать 2dsphere-индекс
```
db.whitelist.createIndex({"lon_lat" : "2dsphere"}, { unique: true });
```


просмотреть дневные счетчики
```
db.counters.find({})
```
