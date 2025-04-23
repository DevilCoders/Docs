# podrick-int

Проект автоматизации рабочих процессов команды Карт.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-podrick-int |
| CI | https://sandbox.yandex-team.ru/tasks?owner=MAPS_FRONT&desc_re=maps%2Fpodrick-int&forPage=tasks |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-podrick-int |

## Instances

| Environment | URL |
|---|---|
| Testing | https://podrick.tst.c.maps.yandex-team.ru |
| Production | https://podrick.c.maps.yandex-team.ru |

## Balancer

Balancer: [front-podrick-int.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-podrick-int.slb.maps.yandex.net/show/).

## Secrets

| Secret | URL |
|---|---|
| Testing | https://yav.yandex-team.ru/secret/sec-01cjz1zmeqzc10c3kjr0vjrdw5 |
| Production | https://yav.yandex-team.ru/secret/sec-01cjz1hw16ymy62e9f917k8gdk |

## Documentation

Новые проекты следует заводить в отдельной директории в `./server/projects/`. Всё что лежит выше этой директории можно переиспользовать.

Текущие проекты:

* [startrek-manager](./server/projects/startrek-manager) — управление статусами задач в startrek.
* [mocks](./server/projects/mocks) — моки для автотестов.
* [version-controller](./server/projects/version-controller) — автоматизация работы с версиями в startrek.
* [translate](./server/projects/translate) — автоматизация переводов при релизе.
* [devops](./server/projects/devops) — автоматизация по дежурству (self-service или девопсизация).
* [proxy](./server/projects/proxy) — прокси для доступа к ipv6 адресам из докер контейнера.
* [notify](./server/projects/notify) — уведомления о выкладке.
* [static](./server/projects/static) — выкладка статики в S3.

## Known clients

* Webhooks:
    * Практически все репозитории в [maps](https://a.yandex-team.ru/arcadia/maps/front/services/maps)
    * Обработка хуков от Трекера

## What happens when service is down

* Не будут работать автоматические задачи, такие как:
    * Перевод статусов тасок
    * Создание новых версий в трекере
    * Автозапуск тестов
* Автотесты будут падать, т.к. придут реальные данные, а не замоканные
* etc...

### production

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/?query=host%3Dmaps-front-podrick-int_common.app |

## Dashboards

| Name | URL |
|---|---|
| Main | [common](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-podrick-int_common), [static](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-podrick-int_static), [mocks](https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-podrick-int_mocks) |
| S3 | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-mocks;owner=2365/ |
| S3 (testing) | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-mocks;owner=2365;ctype=testing/ |
| Balancer | [portoinst metrics](https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-podrick-int.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-podrick-int.slb.maps.yandex.net/), [requests](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=front-podrick-int.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-podrick-int.slb.maps.yandex.net/) |

## Logs

**Deploy**: https://deploy.yandex-team.ru/stage/maps-front-podrick-int_common/logs

**YT**: `hahn.[//home/logfeller/logs/maps-front-production-log/1d/YYYY-MM-DD]`, [example in YQL](https://yql.yandex-team.ru/Operations/XUw2hWHljjuEJlFSi_-xor_fmjdvUiDtWgqTCydfo6w=)

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.
