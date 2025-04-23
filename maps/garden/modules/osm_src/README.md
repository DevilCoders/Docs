# osm_src

## Общее описание модуля

Source-модуль, который регистрирует RemoteDirResource с url для скачивания OSM-данных в PBF-формате.

## Старт модуля и входные данные

На вход модулю должен подаваться файл в формате PBF:

1. Скачать OSM PBF файл:
  * [Планета](https://planet.openstreetmap.org/)
  * [Континенты и страны](https://download.geofabrik.de/)
2. Залить скаченный файл в Sandbox. Например (`ttl` можно не указывать):
```bash
ya upload <скаченный PBF файл> -T MAPS_GARDEN_OSM_PBF -A shipping_date="<дата>" -A region="<region>" -A vendor="osm" --owner MAPS_GARDEN --ttl 30 -d '<комментарий к файлу>'
```

Имя региона должно присутствовать в [файле](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/osm_src/defs/__init__.py).
Если нужного региона нет в списке, то его можно добавить и зарелизить модули `osm_src`, `osm_to_yt`, `ymapsdf_osm`.

В модуле работает сканер ресурсов, который каждые 15 минут проверяет свежие ресурсы в Sandbox и добавляет их в Огород.

Если нужно запустить билд с файлом, который лежит не в Sandbox, то это можно сделать через POST-запрос в API Огорода.

**data.json**
```json
{
    "contour": "datatesting",
    "foreign_key": {
        "sandbox_resource_id": "2490779955"
    },
    "resources": [
        {
            "name": "osm_pbf_url_africa_osm",
            "version": {
                "properties": {
                    "shipping_date": "20211012",
                    "region": "africa",
                    "vendor": "osm",
                    "file_list": [
                        {
                            "name": "osm_data.pbf",
                            "url": "https://proxy.sandbox.yandex-team.ru/2490779955",
                            "md5": "e3cb756051142426985f384b24b5940b"
                        }
                    ]
                }
            }
        }
    ]
}
```

**POST запрос**
```bash
curl -X POST -H "Authorization: OAuth <token>" -H "Content-Type: application/json" http://garden.maps.yandex-team.ru/modules/osm_src/builds/ --data @data.json
```
