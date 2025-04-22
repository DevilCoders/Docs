# http-geobase [![Build Status](https://drone.yandex-team.ru/api/badges/project-stub/node-http-geobase/status.svg)](https://drone.yandex-team.ru/project-stub/node-http-geobase) [![OKO health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/packages/node-http-geobase&vcs=arc)](https://oko.yandex-team.ru/repo/toolbox/node-http-geobase)

> Удобный интерфейс к HTTP геобазе

Используется в паре с [http-geobase](https://github.yandex-team.ru/floatdrop/http-geobase).

## Install

```
$ npm install --save http-geobase
```


## Usage

```ts
import HttpGeobase from 'http-geobase';

const geobase = new HttpGeobase('geobase.qloud.yandex.ru');

geobase.regionById(213).then(region => {
    console.log(region.name); // => Москва
});
```

## API

### HttpGeobase(api, [options])

##### api
Type: String

Адрес HTTP API геобазы.

##### options

###### cacheTimeout
Type: `Number`
Default: `60 * 60 * 1000`

Таймаут кеша.

###### cacheSize
Type: `Number`
Default: `500`

Размер кеша.

###### cache
Type: `LRU кеш`
Default: `LRU({ maxAge: options.cacheTimeout, max: options.cacheSize });`

Кеш для обращений к геобазе.

* `Number` - создается LRU кеш с опциями `{maxAge: cache, max: 500}`
* `Object` - ваш кеш. Должен поддерживать методы `get`, `set` и `del`

### geobase.[asset](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/asset)(ip, [opts])

### geobase.[calculatePointsDistance](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/calculate_points_distance)(alon, alat, blon, blat, [opts])

### geobase.[chiefRegionId](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/chief_region_id)(id, [opts])

### geobase.[children](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/children)(id, [opts])

### geobase.[findCountry](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/find_country)(id, [opts])

### geobase.[idIn](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/id_in)(id, id, [opts])

### geobase.[ipIn](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/ip_in)(ip, id, [opts])

### geobase.[linguisticsForRegion](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/linguistics_for_region)(id, lang, [opts])

### geobase.[parentId](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/parent_id)(id, [opts])

### geobase.[parents](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/parents)(id, [opts])

### geobase.[pinpointGeolocation](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/pinpoint_geolocation)(query, [opts])

### geobase.[regionById](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/region_by_id)(id, [opts])

### geobase.[regionByIp](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/region_by_ip)(ip, [opts])

### geobase.[regionId](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/region_id)(ip, [opts])

### geobase.[regionIdByLocation](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/region_id_by_location)(lat, lon, [opts])

### geobase.[regionsByType](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/regions_by_type)(type, [opts])

### geobase.[reliabilitiesByIp](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/reliabilities_by_ip)(ip, [opts])

### geobase.[subtree](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/subtree)(id, [opts])

### geobase.[supportedLinguistics](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/supported_linguistics)([opts])

### geobase.[timezone](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/timezone)(id, [opts])

### geobase.[tzinfo](https://beta.wiki.yandex-team.ru/http-geobase/api-v1/#/v1/tzinfo)(name, [opts])

### geobase.[traitsByIp](https://wiki.yandex-team.ru/http-geobase/api-v1/#get/v1/gettraitsbyip)(ip, [opts])

##### opts

- `nocache` - по умолчанию `true` для методов, которые работают с IP адресами

#### Транслокальность

Для передачи параметра `crimeaStatus` добавьте его в `opts`:

```ts
geobase.findCountry(146).then(country => {
    console.log(country); // => 225
});

geobase.findCountry(146, {
    crimeaStatus: 'ua'
}).then(country => {
    console.log(country); // => 187
});
```

## License

MIT © [Vsevolod Strukchinsky](http://github.com/floatdrop)
