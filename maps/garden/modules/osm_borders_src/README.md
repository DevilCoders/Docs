# osm_borders_src

## Общее описание модуля

Source-модуль, который регистрирует python-ресурс, содержащий в себе url для скачивания OSM данных с границами стран.
Дальше из OSM данных извлекаются данные об административных границах стран.
На основании полученных границ формируется coverage-файл для стран и coverage-файл для используемых в ymapsdf регионов.

## Старт модуля и входные данные

На вход модулю должен подаваться файл в подходящем для библиотеки libosmium формате,
в котором имеются все административные границы стран.

Залить файл с границами в Sandbox. Например (`ttl` можно не указывать):
```bash
ya upload <скаченный файл с OSM данными> -T MAPS_GARDEN_OSM_BORDERS -A shipping_date="<дата>" -A vendor="osm" --owner MAPS_GARDEN --ttl inf -d '<комментарий к файлу>'
```

Если нужно запустить билд, то это можно сделать через POST-запрос в API Огорода.
Пример:

**data.json**
```json
{
    "contour": "datatesting",
    "foreign_key": {
        "sandbox_resource_id": "2834691858"
    },
    "resources": [
        {
            "name": "osm_borders_url",
            "version": {
                "properties": {
                    "file_list": [
                        {
                            "name": "osm_data.pbf",
                            "url": "https://proxy.sandbox.yandex-team.ru/2834691858",
                            "md5": "e1155fe4d5d529137ffca5740633f7b4"
                        }
                    ],
                    "shipping_date": "20220301",
                    "vendor": "osm",
                    "enable_countries_number_validation": false
                }
            }
        }
    ]
}
```
Примечание: `enable_countries_number_validation` может не указываться и по умолчанию установлен в `true`.

**POST запрос**
```bash
curl -X POST -H "Authorization: OAuth <token>" -H "Content-Type: application/json" http://garden.maps.yandex-team.ru/modules/osm_borders_src/builds/ --data @data.json
```

## Выходные данные:

* Таблица с геометрией стран
* Таблица с геометрией регионов (объединение сухопутных и водных регионов)
* Файл `water_regions_coverage` покрытия водных регионов (соответствует тем, которые представлены на https://npro.maps.yandex.ru)
* Файл `regions_coverage` покрытия сухопутных регионов (на основании OSM данных с границами стран)

## Колонии

На данный момент принято решение вырезать из геометрии стран геометрию колоний, которые не попали в соответствующие
водные регионы. Список проверяемых стран и соответствующих им водных регионов прописано [здесь](lib/extract_countries.h).
