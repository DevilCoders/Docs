## Description
Для всех сервисов фронтенда используется общий шаблон для алертов (`maps-front-common`).

### Список модулей
| название | описание |
| --- | --- |
| **common** | |
| `maps-front-common-application-alerts` | базовый (универсальный) шаблон алертов для сервисов |
| `maps-front-awacs` | шаблон алертов для балансеров |
|  **common block** | |
| `maps-front-common-block-app` | алерты по кастомным логам |
| `maps-front-common-block-http` | основные алерты по http сигналам |
| `maps-front-common-block-infra` | инфраструктурные мониторинги |
| `maps-front-common-block-raw` | полностью кастомные алерты, на основе сырых сигналов |
| `maps-front-common-block-tvm` | алерты по tvm-квотам бекендов |

## Работа с шаблонами алертов

* **create** - `curl -d '{"key": "<template_name>", "owners": [<devops_list>]}' 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/create'`
* **update** - `curl --data-binary @<template_name>.jinja2 'https://yasm.yandex-team.ru/srvambry/tmpl/alerts/update/content?key=<template_name>'`
* **apply** - `curl -XPOST https://yasm.yandex-team.ru/srvambry/tmpl/alerts/apply/<template_name>`
* **render** - `curl -XPOST https://yasm.yandex-team.ru/srvambry/tmpl/alerts/render_json/<template_name>`
* **delete** - `curl -XPOST -d '{"key": "<template_name>"}' /srvambry/tmpl/alerts/delete`
