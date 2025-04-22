# Teacup

[RTC: сервис для тестирования базового образа (GEOINFRA-832)](https://st.yandex-team.ru/GEOINFRA-832)

Карточная кружка. Принимает трафик от карточного чайника [maps/infra/teapot](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/teapot).

## General information

| Key | Value |
|---|---|
| Сервис в ABC | [maps-core-teacup](https://abc.yandex-team.ru/services/maps-core-teacup) |
| Исходники | [maps/infra/teacup](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/teacup) |
| CI (TestEnv) покоммитная сборка| [BUILD_MAPS_CORE_TEACUP](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_MAPS_CORE_TEACUP) |
| Tracker Queue | <https://st.yandex-team.ru/GEOINFRA> |

## Instances

| Environment | URL |
|---|---|
| Stable | <https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_teacup_stable/> |
| Testing | <https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_teacup_testing/> |

| Dashboard |
|---|
| <https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_teacup> |

## Monitorings

| Staging | Juggler panel |
|---|---|
| Stable | <https://juggler.yandex-team.ru/?query=host%3Dmaps_core_teacup_stable> |
| Testing | <https://juggler.yandex-team.ru/?query=host%3Dmaps_core_teacup_testing> |

## Logs

Логи сервиса искать в контейнерах в Няне.

| | |
|---|---|
| Yacare application | `/var/log/yandex/maps/teacup/*` |
| Nginx | `/var/log/nginx/*` |
| Supervisord | `/var/log/supervisor/*` |
| YT | <https://yql.yandex-team.ru> `SELECT * FROM hahn.[logs/maps-log/1d/2019-03-05] WHERE tskv_format='teacup'` |

## Balancers

#### Production - core-teacup.maps.yandex.net
* L3
  * L3-manager: <https://l3.tt.yandex-team.ru/service/5355>
  * Racktables: <https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=6669>
  * Awacs: <https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-teacup.maps.yandex.net/l3-balancers/list/>
  * Grafana: <https://grafana.yandex-team.ru/d/6zOl5Fjiz/l3-vs-core-teacup-maps-yandex-net>
* L7
  * Awacs: <https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-teacup.maps.yandex.net/show/>
  * Графики
    * Common metrics: <https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-teacup.maps.yandex.net;prj=core-teacup-maps;ctype=prod;timelines=0.2,0.4,0.7,1,2,10/>
    * Portoinst metrics: <https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-teacup.maps.yandex.net;prj=core-teacup-maps;ctype=prod/>
  * Мониторинги: <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drtc_balancer_core-teacup_maps_yandex_net_man%7Chost%3Drtc_balancer_core-teacup_maps_yandex_net_vla%7Chost%3Drtc_balancer_core-teacup_maps_yandex_net_sas&statuses=WARN%2CCRIT%2COK>
  * Фаервол: <https://puncher.yandex-team.ru/?destination=core-teacup.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination>

#### Testing - core-teacup.testing.maps.yandex.net
* L3
  * L3-manager: <https://l3.tt.yandex-team.ru/service/5355>
  * Racktables: <https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=6669>
  * Awacs: <https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-teacup.testing.maps.yandex.net/l3-balancers/list/>
  * Grafana: <https://grafana.yandex-team.ru/d/PHpnQDjik/l3-vs-core-teacup-testing-maps-yandex-net>
* L7
  * AWACS: <https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-teacup.testing.maps.yandex.net/show/>
  * Графики
    * Common metrics: <https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-teacup.testing.maps.yandex.net;prj=core-teacup-testing-maps;ctype=prod;timelines=0.2,0.4,0.7,1,2,10/>
    * Portoinst metrics: <https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=core-teacup.testing.maps.yandex.net;prj=core-teacup-testing-maps;ctype=prod/>
  * Мониторинги: <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drtc_balancer_core-teacup_testing_maps_yandex_net_man%7Chost%3Drtc_balancer_core-teacup_testing_maps_yandex_net_vla%7Chost%3Drtc_balancer_core-teacup_testing_maps_yandex_net_sas&statuses=WARN%2CCRIT%2COK>
  * Фаервол: <https://puncher.yandex-team.ru/?destination=core-teacup.testing.maps.yandex.net&rules=exclude_rejected&values=all&sort=destination>
