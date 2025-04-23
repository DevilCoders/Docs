
# Core Renderer Stylerepo

Хранилище дизайнов для множества сервисов, использующих карты. Предоставляет минимальную функциональность систем контроля версий. Доступ к хранилищу осуществляется с помощью API.

**Table of Contents**
[[toc]]

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Вадим Бенкевич (vbenkevich@yandex-team.ru)<br> Дмитрий Шаханович (shakhanovich@yandex-team.ru) |
| Отвественные SRE | Вадим Бенкевич (vbenkevich@yandex-team.ru)<br> Дмитрий Шаханович (shakhanovich@yandex-team.ru) |
| Исходники | [maps/renderer/stylerepo](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/stylerepo) |
| Сервис в ABC | [maps-core-renderer-stylerepo](https://abc.yandex-team.ru/services/maps-core-renderer-stylerepo/)|
| CI (TestEnv) - Покоммитный | [https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_RENDERER_STYLEREPO](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_RENDERER_STYLEREPO)


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_renderer_stylerepo_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_stylerepo_stable/) | [ core-renderer-stylerepo.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-stylerepo-stable-panel-main/) | [ maps_core_renderer_stylerepo_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_stylerepo_stable) |
| Testing | [maps_core_renderer_stylerepo_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_renderer_stylerepo_testing/) | [ core-renderer-stylerepo.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-renderer-stylerepo-testing-panel-main/) | [ maps_core_renderer_stylerepo_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_renderer_stylerepo_testing) |


[Monitorings all (tag=a_prj_maps-core-renderer-stylerepo)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-renderer-stylerepo)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [core-renderer-stylerepo.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-renderer-stylerepo.maps.yandex.net/) | [core-renderer-stylerepo.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-renderer-stylerepo.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla;prj=core-renderer-stylerepo-maps;signal=service_total) | [rtc_balancer_core-renderer-stylerepo_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-renderer-stylerepo_maps_yandex_net_sas)<br>[rtc_balancer_core-renderer-stylerepo_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-renderer-stylerepo_maps_yandex_net_vla) |
| Testing | common | | | [maps-core-renderer-stylerepo-testing-slb](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-core-renderer-stylerepo-testing-slb) |
| Testing | maps common | [core-renderer-stylerepo.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-renderer-stylerepo.common.testing.maps.yandex.net"}) | [core-renderer-stylerepo.common.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.testing.maps.yandex.net;prj=common.testing.maps.yandex.net;signal=core-renderer-stylerepo_common_testing_maps_yandex_net;) | [rtc_balancer_common_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_sas) <br>[rtc_balancer_common_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_man) <br>[rtc_balancer_common_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_vla) |

### URLs

| Staging | FQDN |
|--|--|
| Stable | core-renderer-stylerepo.maps.yandex.net |
| Tesing | core-renderer-stylerepo.testing.maps.n.yandex.ru |

### MDB Postgres clusters

| Staging | MDB cluster |
| ------- | ----------- |
| testing | [cluster](https://yc.yandex-team.ru/folders/foomip3v3f690c6rip9o/managed-postgresql/cluster/b091f9fe-8d11-4f5a-8773-a1e1823f169d) |
| stable | [cluster](https://yc.yandex-team.ru/folders/foomip3v3f690c6rip9o/managed-postgresql/cluster/mdblivka01fpspsmouuu) |
  
## Deployment

  
После коммита в maps/renderer/stylerepo запускается сборка контейнера в [TestEnv](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_RENDERER_STYLEREPO).
Для выкладки используется `maps/renderer/stylerepo$ ya tool sedem info/start/step .`
  [Подробнее про sedem](https://docs.yandex-team.ru/docs/sedem/releases#2.2-release-commands)
  
## What happens when service is down

Не работает сервис Картограф, нельзя разрабатывать и публиковать дизайны для подложки и слоев в картах.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Смотреть логи:

    /var/log/yandex/maps/stylerepo/*
    /var/log/supervisor/supervisord.log

## Documentation

### Доступы

Для возможности публикации дизайна из карторграфа необходима роль `Дизайн-менеджер` в abc-сервисе [Пользователи Картографа](https://abc.yandex-team.ru/services/cartographusers/). После добавления пользователя в abc-сервис [idm](https://idm.yandex-team.ru/system/stylerepo) автоматически сообщит stylerepo о новой роли. В тестовом окружении публикация дизайнов доступна всем.

### Wiki
 - https://wiki.yandex-team.ru/users/vbenkevich/factory
 - https://wiki.yandex-team.ru/users/avlasyuk/Stylerepo-bundle-release
 - https://wiki.yandex-team.ru/users/vbenkevich/experiments
 - https://wiki.yandex-team.ru/users/avlasyuk/User-data-set-API/#stylerepo
 - https://wiki.yandex-team.ru/users/ivpeschinskiy/stylerepo-db-migration/

## Known clients
- https://cartograph.maps.yandex-team.ru
- https://cartograph.tst.c.maps.yandex-team.ru
- Огород – выкачивает дизайны и иконки для tilesgen'а

## Persistent Volumes

* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_RENDERER_STYLEREPO_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_RENDERER_STYLEREPO_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_RENDERER_STYLEREPO_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_RENDERER_STYLEREPO_TESTING_RTC_NETS_ ) |
