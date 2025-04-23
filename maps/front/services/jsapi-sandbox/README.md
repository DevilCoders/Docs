# jsapi-sandbox

Проект представляет из себя составную часть [сайта технологий Яндекса](https://yandex.ru/dev/). И генерирует блоки `html`-кода (со всеми необходимыми ресурсами `css`, `js`), которые врезаются в страницы сайта.

Существует возможность получение песочницы в двух разных форматах:

* **full** — основной, когда песочница является основной частью страницы.
* **widget** — песочница отдается в виде небольшого виджета для вставки в документацию.

По умолчанию отдается песочница в основном формате, для получения виджета необходимо отправлять запрос по url'у: `/widget`.

Песочница умеет обрабатывать три GET-параметра:

* `lang` — язык, на котором должна быть отдана песочница/виджет (`ru`, `en`, `tr`, по умолчанию `ru`).
* `version` — версия API Яндекс.Карт, пример для которой необходимо получить (по умолчанию `2.1`).
* `id` — идентификатор примера, фактически это имя папки с примером [yandex/mapsapi-examples-ru](https://github.com/yandex/mapsapi-examples-ru) (по умолчанию выбирается первый из списка `menu`).
* `namespace` — неймспейс проекта, который прибавляется к началу относительных ссылок (по-умолчанию пустая строка).

## General information

| Key | Value |
|---|---|
| ABC | [maps-front-jsapi-sandbox](https://abc.yandex-team.ru/services/maps-front-jsapi-sandbox/) |
| CI | [Trendbox CI](https://github.yandex-team.ru/search-interfaces/trendbox-ci/) |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-jsapi-sandbox |
| Tanker | [maps-sandbox](https://tanker.yandex-team.ru/?project=maps-sandbox&branch=master) |

## Instances

| Environment | URL |
|---|---|
| Testing | https://tst.sandbox.api.maps.yandex.ru/ |
| Testing Tech | https://l7test.yandex.ru/dev/maps/jsbox/2.1/ |
| Production | https://sandbox.api.maps.yandex.net/ |
| Production Tech | https://yandex.ru/dev/maps/jsbox/2.1/ |

## Known clients

* [Yandex Tech](https://yandex.ru/dev/maps/jsbox/2.1/)

## What happens when service is down

* User cannot see examples for JS API.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-jsapi-sandbox_production.app |
| Golovan | https://yasm.yandex-team.ru/template/alert/maps-front-jsapi-sandbox-production-app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-jsapi-sandbox_production |
| Balancer (porto metrics) | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-jsapi-sandbox.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-jsapi-sandbox.slb.maps.yandex.net/ |
| Balancer (requests) | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-jsapi-sandbox.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-jsapi-sandbox.slb.maps.yandex.net/ |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | https://deploy.yandex-team.ru/stages/maps-front-jsapi-sandbox_production/logs |
| Supervisor | `/var/log/supervisor/` |
| YT | `tskv_format=maps-front-jsapi-sandbox_app` |

### Example in [YQL](https://yql.yandex-team.ru/)

```sql
SELECT *
FROM hahn.[logs/maps-log/1d/2021-01-07]
WHERE tskv_format == 'maps-front-jsapi-sandbox_app';
```

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
