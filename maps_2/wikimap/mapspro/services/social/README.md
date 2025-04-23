# wiki-social

Социальная часть Народной карты:
* модерация правок и фидбека
* комментарии к объектам, фидбеку и общение на Народной Карте
* инволвменты - периоды совместного редактирования пользователями
* фидбек
* фиды правок:
  * пользовательские
  * по области
  * по зоне подписки
* рейтинг пользователя
* профиль пользователя

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Алексей Пономарев ( ponomarev@yandex-team.ru ) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/social |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-social/ |
| Проект в CI | [maps-core-nmaps-social](https://a.yandex-team.ru/projects/maps-core-nmaps-social/ci/actions/launches?dir=maps/wikimap/mapspro/services/social) |

## Instances

Сервисы в Няне:
- [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_nmaps_social/)
- [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_stable/)
- [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_testing/)
- [unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_unstable/)
- [load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_social_load/)

## Documentation

Схема: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/schemas/social

[Инструкция](https://docs.yandex-team.ru/nmaps/services/social/add_feedback_type) по добавлению нового типа фидбека

## Known clients

https://puncher.yandex-team.ru/?destination=core-nmaps-social.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination

wiki-social -> `_PGAASINTERNALNETS_`:6432

`_SEARCHPRODNETS_`,`_MAPSPRODQNETS_`,`_CMSEARCHNETS_`, `_MAPS_DEV_RTC_NETS_`

## What happens when service is down

Не работает социальная часть Народной карты - см. описание сервиса


## Как проверить, что сервис работает

Открыть какой-нибудь фидбек в НК [пример](https://n.maps.yandex.ru/#!/feedback/tasks/14664210?z=16&ll=38.957822%2C45.133232&l=nk%23sat)

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | default | [core-nmaps-social.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-nmaps-social.maps.yandex.net/) | [core-nmaps-social.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,vla;fqdn=core-nmaps-social.maps.yandex.net;prj=core-nmaps-social-maps;signal=service_total;) | [rtc_balancer_core-nmaps-social_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-social_maps_yandex_net_sas) <br>[rtc_balancer_core-nmaps-social_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-nmaps-social_maps_yandex_net_vla) |
| Testing | common_default | [core-nmaps-social.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-nmaps-social.common.testing.maps.yandex.net"}) | [core-nmaps-social.common.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.testing.maps.yandex.net;prj=common.testing.maps.yandex.net;signal=core-nmaps-social_common_testing_maps_yandex_net;) | [rtc_balancer_common_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_sas) <br>[rtc_balancer_common_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_man) <br>[rtc_balancer_common_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_vla) |
| Unstable | common_default | [core-nmaps-social.common.unstable.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.unstable.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-nmaps-social.common.unstable.maps.yandex.net"}) | [core-nmaps-social.common.unstable.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.unstable.maps.yandex.net;prj=common.unstable.maps.yandex.net;signal=core-nmaps-social_common_unstable_maps_yandex_net;) | [rtc_balancer_common_unstable_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_sas) <br>[rtc_balancer_common_unstable_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_man) <br>[rtc_balancer_common_unstable_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_unstable_maps_yandex_net_vla) |

## Мониторинги

| Type | URL |
|---|---|
| Juggler (Production) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_social_stable |
| Juggler (Testing) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_social_testing |
| Juggler (Development) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_social_unstable |
| Juggler (Load) | https://juggler.yandex-team.ru/?query=host%3Dmaps_core_nmaps_social_load |

## Создание мониторингов

https://wiki.yandex-team.ru/users/romankh/SEDEM-Kak-zapuskat/

## Графики
| Staging | Golovan panel URL |
|---|---|
| Stable | [maps-core-nmaps-social-stable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-social-stable-panel-main) |
| Testing | [maps-core-nmaps-social-testing-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-social-testing-panel-main) |
| Unstable | [maps-core-nmaps-social-unstable-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-social-unstable-panel-main) |
| Load | [maps-core-nmaps-social-load-panel-main](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-social-load-panel-main) |
| mapspro_core | [mapspro_core](https://yasm.yandex-team.ru/panel/chikunov.mapspro_core/) |
| mapspro_social | [mapspro_social](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb6od92oiks2maqel86;dbname=mapspro_social) |

## SLA

Нет

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| wiki-social | /var/log/yandex/maps/wiki-social/* |
| nginx | /var/log/nginx/* |
| yacare| /var/log/yandex/maps/yacare/* |
| supervisord | /var/log/supervisor/* |
| syslog (unfiltered) | /var/log/syslog |

## Regression Stress Testing Configurations

- [Shootings](https://lunapark.yandex-team.ru/regress/NMAPS?service=Social)
- [Scheduler for imbalance shootings](https://sandbox.yandex-team.ru/scheduler/13971/view)
- [Scheduler for timing shootings](https://sandbox.yandex-team.ru/scheduler/13973/view)

## Патч в DNS

### для UI
core-nmaps-social.load.maps.yandex.net is an alias for **YP-POD from maps_core_nmaps_social_load**

Можно получить динамически из [API Няни](https://nanny.yandex-team.ru/v2/services/maps_core_nmaps_social_load/current_state/instances/)

### Для отстающих (landing page)
host social.um.maps.yandex.net
social.um.maps.yandex.net is an alias for core-nmaps-social.maps.yandex.net.
