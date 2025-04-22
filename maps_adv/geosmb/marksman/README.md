## Marksman
Сервис для работы с CDP-сегментами бизнеса.

#### Testing
api: http://marksman.tst.geosmb.maps.yandex.net
tvm: 2026830

#### Production
api: http://marksman.geosmb.maps.yandex.net
tvm: 2026832

#### Полезные ссылки
* [ABC](https://abc.yandex-team.ru/services/maps-adv-clients-marksman/)
* Yav [testing](https://yav.yandex-team.ru/secret/sec-01f0h5hq7e8bt0schdz9p182q2/explore/versions) [production](https://yav.yandex-team.ru/secret/sec-01f0hbcckty8073r9z7ypdccx1/explore/versions)
* [CD](https://a.yandex-team.ru/ci/maps-adv-clients-logoped/releases/timeline?dir=maps_adv%2Fgeosmb%2Flogoped%2Fserver&id=stable-release)
* [Sandbox resources](https://sandbox.yandex-team.ru/resources?type=GEOSMB_MARKSMAN)
* [Deploy](https://deploy.yandex-team.ru/projects/geosmb-marksman)
* Awacs [testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.tst.geosmb.slb.maps.yandex.net/upstreams/list/geosmb-marksman-testing/show/) [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.geosmb.slb.maps.yandex.net/upstreams/list/geosmb-marksman-production/show/)
* [YC](https://yc.yandex-team.ru/folders/aku88pi3sdoq5gla0dkj)
* Solomon [админка](https://solomon.yandex-team.ru/admin/projects/geosmb)

## API

#### Добавление бизнеса в синхронизацию

`POST /v1/business/`

input:
```json
{
  "biz_id": 123
}
```

output:
В случае успеха - код 201 и пустое тело.

В случе ошибки:
```json
{
  "error": "ERROR_DESC"
}
```

На месте `ERROR_DESC` могут быть:
- `BIZ_NOT_FOUND` - неизвестный biz_id;
- `NO_ORG_INFO` - не удалось найти информациб об организации;
- `NO_COUNTER` - у организации нет пылесосного счётчика.


#### Получение информации о CDP сегментах бизнеса

`GET /v1/business/segments_data/`
Параметры:
biz_id (int, обязательный) - идентификатор бизнеса

output:
```json
{
  "biz_id": 123,
  "permalink": 456,
  "counter_id": 789,
  "segments": [
    {
      "segment_name": "ACTIVE",
      "cdp_id": 12345,
      "cdp_size": 1000
    },
    {
      "segment_name": "PROSPECTIVE",
      "cdp_id": 12346,
      "cdp_size": 2000
    }
  ],
  "labels": [
    {
      "label_name": "UPLOADED",
      "cdp_id": 12347,
      "cdp_size": 1000
    },
    {
      "label_name": "DOWNLOADED",
      "cdp_id": 12348,
      "cdp_size": 2000
    }
  ]
}
```
