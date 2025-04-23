# Выгрузки по гео

Для работы `globe` используется выгрузки по регионам и станциям метро.

## S3

Выгрузки обновляются на s3 руками по требованию.  

### Testing
 - [regions](https://classified-test.s3.mds.yandex.net/geo/regions) 
 - [metro](https://classified-test.s3.mds.yandex.net/geo/metro) 
 
### Production
 - [regions](https://classified.s3.mds.yandex.net/geo/regions) 
 - [metro](https://classified.s3.mds.yandex.net/geo/metro)

## Выгрузка данных по регионам/городам
В качестве источника используется геобаза. 

### UI

https://geoadmin.yandex-team.ru.

### XML-экспорт
```
curl http://geoexport.yandex.ru/\?types\=_all_\&format\=xml\&fields\=id,name,type,parent,tz_offset,ru_name,uk_name,tr_name,en_name,latitude,longitude,ru_prepositional,ru_preposition,chief_region,population
```

## Выгрузка данных по метро
Берется у [фронтенда](https://github.com/YandexClassifieds/frontend-metro/blob/master/export/metro.json)
