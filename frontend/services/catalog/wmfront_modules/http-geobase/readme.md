# http-geobase [![Build Status](http://drone-beta.haze.yandex.net/api/badges/project-stub/node-http-geobase/status.svg)](http://drone-beta.haze.yandex.net/project-stub/node-http-geobase)

> Удобный интерфейс к HTTP геобазе

Используется в паре с [http-geobase](https://github.yandex-team.ru/floatdrop/http-geobase).

## Install

```
$ npm install --save http-geobase
```


## Usage

```js
const HttpGeobase = require('http-geobase');
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

###### cache
Type: `Number` / `Object`  
Default: `60 * 60 * 1000`

Кеш для обращений к геобазе.

* `Number` - создается LRU кеш с опциями `{maxAge: cache, max: 500}`
* `Object` - ваш кеш. Должен поддерживать методы `get` и `set`

### geobase.[asset](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/asset)(ip, [opts])

### geobase.[calculatePointsDistance](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/calculate_points_distance)(alon, alat, blon, blat, [opts])

### geobase.[chiefRegionId](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/chief_region_id)(id, [opts])

### geobase.[children](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/children)(id, [opts])

### geobase.[findCountry](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/find_country)(id, [opts])

### geobase.[idIn](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/id_in)(id, id, [opts])

### geobase.[ipIn](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/ip_in)(ip, id, [opts])

### geobase.[linguisticsForRegion](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/linguistics_for_region)(id, [opts])

### geobase.[parentId](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/parent_id)(id, [opts])

### geobase.[parents](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/parents)(id, [opts])

### geobase.[pinpointGeolocation](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/pinpoint_geolocation)(query, [opts])

### geobase.[regionById](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/region_by_id)(id, [opts])

### geobase.[regionByIp](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/region_by_ip)(ip, [opts])

### geobase.[regionId](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/region_id)(ip, [opts])

### geobase.[regionIdByLocation](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/region_id_by_location)(lat, lon, [opts])

### geobase.[reliabilitiesByIp](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/reliabilities_by_ip)(ip, [opts])

### geobase.[subtree](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/subtree)(id, [opts])

### geobase.[supportedLinguistics](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/supported_linguistics)([opts])

### geobase.[timezone](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/timezone)(id, [opts])

### geobase.[tzinfo](https://beta.wiki.yandex-team.ru/http-geobase/api-v0/#/v0/tzinfo)(name, [opts])

##### opts

- `nocache` - по умолчанию `true` для методов, которые работают с IP адресами

#### Транслокальность

Для передачи параметра `crimea_status` добавьте в `opts` поле `query`:

```js
geobase.findCountry(146).then(country => {
	console.log(country); // => 225
});

geobase.findCountry(146, {
	query: {
		crimea_status: 'ua'
	}
}).then(country => {
	console.log(country); // => 187
});
```

## License

MIT © [Vsevolod Strukchinsky](http://github.com/floatdrop)
