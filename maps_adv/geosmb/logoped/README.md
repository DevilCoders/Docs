## Logoped
Сервис по работе с формами слов.

#### Testing
api: http://logoped.tst.geosmb.maps.yandex.net

#### Production
api: http://logoped.geosmb.maps.yandex.net

#### Полезные ссылки
* [ABC](https://abc.yandex-team.ru/services/maps-adv-clients-logoped/)
* [CD](https://a.yandex-team.ru/ci/maps-adv-clients-logoped/releases/timeline?dir=maps_adv%2Fgeosmb%2Flogoped%2Fserver&id=stable-release)
* [Sandbox resources](https://sandbox.yandex-team.ru/resources?type=GEOSMB_LOGOPED)
* [Deploy](https://deploy.yandex-team.ru/projects/geosmb-logoped)
* Awacs [testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.tst.geosmb.slb.maps.yandex.net/show/) [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.geosmb.slb.maps.yandex.net/show/)
* Solomon [админка](https://solomon.yandex-team.ru/admin/projects/geosmb)


## API

#### Получение лемм для каждого слова произвольного текста

`POST /v1/extract-lemmas/`

input:
```json
{
    "input": "Онотола, онотолб. Онотолв? Онотолг! онотолд; Онотоле..."
}
```

output:
```json
[
    {"input": "Онотола", "lemmas": ["онотол", "онотоле"]},
    {"input": "онотолб", "lemmas": ["онотол", "онотоле"]},
    {"input": "Онотолв", "lemmas": ["онотол", "онотоле"]},
    {"input": "Онотолг", "lemmas": ["онотол", "онотоле"]},
    {"input": "онотолд", "lemmas": ["онотол", "онотоле"]},
    {"input": "Онотоле", "lemmas": ["онотол", "онотоле"]},
]
```
