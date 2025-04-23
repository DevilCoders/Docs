# osm_coastlines_src

## Общее описание модуля

Source-модуль, который регистрирует python-ресурс, содержащий в себе url для скачивания OSM данных с береговыми линиями.
TODO(gzagon): дополнить описание

## Старт модуля и входные данные

На вход модулю должен подаваться файл, содержащий в себе береговые линии.

Залить файл с границами в Sandbox. Например (`ttl` можно не указывать):
```bash
ya upload <скаченный файл с данными> -T MAPS_GARDEN_OSM_COASTLINES -A shipping_date="<дата>" -A vendor="osm" --owner MAPS_GARDEN --ttl inf -d '<комментарий к файлу>'
```

Если нужно запустить билд, то это можно сделать через POST-запрос в API Огорода.
Пример:

**data.json**
```json
{
    "contour": "datatesting",
    "foreign_key": {
        "sandbox_resource_id": "2843455000"
    },
    "resources": [
        {
            "name": "osm_coastlines_url",
            "version": {
                "properties": {
                    "file_list": [
                        {
                            "name": "water_polygons.shp",
                            "url": "https://proxy.sandbox.yandex-team.ru/2843455000"
                        },
                        {
                            "name": "water_polygons.shx",
                            "url": "https://proxy.sandbox.yandex-team.ru/2843464959"
                        }
                    ],
                    "shipping_date": "20211012",
                    "vendor": "osm"
                }
            }
        }
    ]
}
```

**POST запрос**
```bash
curl -X POST -H "Authorization: OAuth <token>" -H "Content-Type: application/json" http://garden.maps.yandex-team.ru/modules/osm_coastlines_src/builds/ --data @data.json
```

## Источники данных:

[water polygons](https://osmdata.openstreetmap.de/data/water-polygons.html)
[earth_polygons](https://daylightmap.org/coastlines.html)
