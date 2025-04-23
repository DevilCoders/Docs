## Description
Для всех сервисов фронтенда используется общий шаблон для голована (`maps-front-common`).

### Параметры
Для настройки некоторых параметров (например, графиков для балансеров), для каждого приложения необходимо указывать дополнительные параметры. Все эти параметры собираются шедулером и чаще всего их не нужно указывать, но можно переопределить при желании.

| назвние | описание |
| --- | --- |
| `slb` | название балансера |
| `srcTvmId` | tvmId приложения конкртеного приложения |
| `cid` | айди кластера базы из MDB |
| `mode` | режим показа дополнительной информации на панели \<full|basic\> |

### Список модулей
| название | описание |
| --- | --- |
| **common** | |
| `maps-front-common` | базовый (универсальный) шаблон графиков для сервисов |
| **generated block** | |
| `maps-front-colors-style` | блок с цветами для графиков |
|  **common block** | |
| `maps-front-common-block-app-log` | график по кастомным логам |
| `maps-front-common-block-extended-graph` | графики по "ручкам" |
| `maps-front-common-block-http` | основные графики (http_codes, request_time) |
| `maps-front-common-block-mdb` | графики по кластеру БД |
| `maps-front-common-block-network` | графики сетевой подсистемы приложения |
| `maps-front-common-block-infra` | графики по осноными ресурсам (CPU, RAM, Disk) приложения |
| `maps-front-common-block-slb` | графики по балансеру (Qloud only) |
| `maps-front-common-block-tvm-quota` | графики потребления квоты у бекендов Карт |
| `maps-front-common-block-notify` | блок отвечающий за настройки нотификаций в Алертах (используется только в алертах) |

## Работа с шаблонами панелей

* **create** - `curl -d '{"key": "<template_name>", "owners": [<devops_list>]}' 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/create'`
* **update** - `curl --data-binary @<template_name>.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=<template_name>'`
* **render** - `curl https://yasm.yandex-team.ru/srvambry/tmpl/panels/render_json/<template_name>`
* **delete** - `curl -d '{"key": "<template_name>"}' 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/delete'`

## Использование
```
https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=<DEPLOY_STAGE | QLOUD_ENVIRONMENT_ID>
```
где
* `<DEPLOY_STAGE>` - название стейджа из Deploy `<abc-slug>_<environment>`
* `<QLOUD_ENVIRONMENT_ID>` - название окружения из Qloud `<project>.<application>.<environment>`
* `mode` - `full` или пустое значение,

## Пример

https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-maps_production/
https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps.front-redirect.production;mode=full/
