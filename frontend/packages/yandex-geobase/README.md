# yandex-geobase

Это обертка над N-API биндингом `@yandex-int/geo` для geobase версии 6.

## Important

Поставить данные для работы геобазы можно с помощью debian-пакета p2p-distribution-geodata{version}-config,
которые по умолчанию упадут в `/var/cache/geobase/geodata{version}.bin` или скачать sandbox-ресурс (GEODATA5BIN_STABLE или GEODATA6BIN_STABLE).

## Install

Set your npm registry server to `http://npm.yandex-team.ru` then `npm install yandex-geobase`.

## Usage

Документация и описание API геобазы – [doc.yandex-team.ru/lib/libgeobase5](https://doc.yandex-team.ru/lib/libgeobase5/concepts/interfaces-nodejs.xml).

```ts
import geobase, { geobase6 } from 'yandex-geobase';

const lookup: geobase6.GeobaseLookup = geobase.v6({
    geobaseData: '/var/cache/geobase/geodata6.bin'
});

const region = lookup.getRegionById(213);

if (region) {
    console.log(region.name);
}
```

## API

### yandex-geobase.v6([options])

Возвращает инстанс GeobaseLookup шестой версии геобазы.

### options

#### geobaseData

Type: `String` Default: `/var/cache/geobase/geodata6.bin`

Абсолютный путь к файлу данных или конфига.
