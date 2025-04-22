## Cleaner

Сервис, удаляющий/чистящий данные для нужд GDPR.

#### Testing
api: http://cleaner.tst.geosmb.maps.yandex.net
tvm: 2025880

#### Production
api: http://cleaner.geosmb.maps.yandex.net
tvm: 2025882

#### Полезные ссылки
* [ABC](https://abc.yandex-team.ru/services/maps-adv-clients-cleaner/)
* Yav: [testing](https://yav.yandex-team.ru/secret/sec-01ewn5e0w8mkhfzhxg50pz07a6), [production](https://yav.yandex-team.ru/secret/sec-01ewn5hzx0k5rygec59t7fzk3s)
* [CD](https://a.yandex-team.ru/ci/maps-adv-clients-cleaner/releases/timeline?dir=maps_adv%2Fgeosmb%2Fcleaner%2Fserver&id=stable-release)
* [Sandbox resources](https://sandbox.yandex-team.ru/resources?type=GEOSMB_CLEANER)
* [Deploy](https://deploy.yandex-team.ru/projects/geosmb-cleaner)
* Awacs (коммунальный) [testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.tst.geosmb.slb.maps.yandex.net/show/) [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.geosmb.slb.maps.yandex.net/show/)
* YC [PostgreSQL](https://yc.yandex-team.ru/folders/akuko14ll6s7jvdk0f6i/managed-postgresql)
* Solomon [админка](https://solomon.yandex-team.ru/admin/projects/geosmb)
* [внешняя документация](https://wiki.yandex-team.ru/lentil-of-everything/podderzhka-gdpr/) про поддержку GDPR



## API
Делалось по [этим](https://wiki.yandex-team.ru/users/yakushevsky/takeoutrequirements/) требованиям.

#### Удаление данных пользователя

`POST /1/takeout/delete/`

input: service/user TVM tickets in headers

output:
* success
```json
{
    "status": "ok"
}
```

* error
```json
{
    "status": "error",
    "errors": [
        {"code": "missed_user_ticket", "message": "TVM user ticket is missed"}
    ]
}
```

#### Получение статуса пользователя

`GET /1/takeout/status/`

input: service/user TVM tickets in headers

output:
* success
```json
{
    "status": "ok",
    "data": [
        {
            "id": "1",
            "slug": "all",
            "state": "empty",
            "update_date": "2020-01-01T00:00:00+00:00"
        }
    ]
}
```

* error
```json
{
    "status": "error",
    "errors": [
        {"code": "missed_user_ticket", "message": "TVM user ticket is missed"}
    ]
}
```