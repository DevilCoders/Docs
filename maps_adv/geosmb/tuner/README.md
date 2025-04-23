## Tuner
Сервис управления настройками организации.

#### Testing
api: http://tuner.tst.geosmb.maps.yandex.net
tvm: 2024625

#### Production
api: http://tuner.geosmb.maps.yandex.net
tvm: 2024745

#### Полезные ссылки
* [ABC](https://abc.yandex-team.ru/services/maps-adv-clients-tuner/)
* Yav [testing](https://yav.yandex-team.ru/secret/sec-01ep784p21rxweedqh5msme6aa/) [production](https://yav.yandex-team.ru/secret/sec-01ep786zpm02v18284vd5vya16/)
* [CD](https://a.yandex-team.ru/ci/maps-adv-clients-tuner/releases/timeline?dir=maps_adv%2Fgeosmb%2Ftuner%2Fserver&id=stable-release)
* [Sandbox resources](https://sandbox.yandex-team.ru/resources?type=GEOSMB_TUNER)
* [Deploy](https://deploy.yandex-team.ru/projects/geosmb-tuner)
* Awacs [testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.tst.geosmb.slb.maps.yandex.net/show/) [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.geosmb.slb.maps.yandex.net/show/)
* [YC](https://yc.yandex-team.ru/folders/akubhk590b41g8csg0dl/)
* Solomon [админка](https://solomon.yandex-team.ru/admin/projects/maps-adv-clients)

## API
Протоколы живут в `./proto/`.

#### Получение настроек организации

`POST /v1/fetch_settings/`

input: **settings.FetchSettings**

output:
* **HTTP 200, settings.Settings** - успех.
    Если принесён новый biz_id, то для него создаются дефолтные настройки.
* **HTTP 400, Error.VALIDATION_ERROR** - ошибка валидации входящих данных

#### Обновление настроек организации

`POST /v1/update_settings/`

input: **settings.UpdateSettings**

output:
* **HTTP 200, settings.Settings** - успех
* **HTTP 400, Error.VALIDATION_ERROR** - ошибка валидации входящих данных
* **HTTP 400, Error.UNKNOWN_BIZ_ID** - данные по переданному biz_id не найдены

#### Получение параметра general_schedule_id настроек организации

`POST /v1/fetch_settings/general_schedule_id/`

input: **settings.FetchSettings**

output:
* **HTTP 200, settings.GeneralScheduleIdSetting** - успех.
    Если принесён новый biz_id, то для него создаются дефолтные настройки.
* **HTTP 400, Error.VALIDATION_ERROR** - ошибка валидации входящих данных

#### Обновление параметра general_schedule_id настроек организации

`POST /v1/update_settings/general_schedule_id/`

input: **settings.UpdateGeneralScheduleIdSetting**

output:
* **HTTP 200, settings.GeneralScheduleIdSetting** - успех
* **HTTP 400, Error.VALIDATION_ERROR** - ошибка валидации входящих данных
* **HTTP 400, Error.UNKNOWN_BIZ_ID** - данные по переданному biz_id не найдены
