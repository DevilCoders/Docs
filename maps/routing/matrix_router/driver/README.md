Драйвера матричного маршрутизатора.

Данный сервис является обслуживающим [матричный маршрутизатор][маршрутизатор].
Он генерирует датасет yandex-maps-l6a-matrix-jams-diff, который затем с помощью экстатика загружается в маршрутизатор.
Балансеров у данного сервиса нет, т.к. он ни с кем не взаимодействует по HTTP(S).

## General information
| Key | Value |
|---|---|
| Ответственные разработчики | Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev) <br/> Александр Игнатьев [(@asi81)](https://staff.yandex-team.ru/asi81) |
| Ответственные SRE | Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev)|
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/matrix_router/driver/ |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-matrix-driver/ |
| CI (TestEnv) - Покомитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_MATRIX_DRIVER_DOCKER |


## Потребители
Матричный Роутер: a.yandex-team.ru/arc/trunk/arcadia/maps/routing/matrix_router/README.md

## Панель сервиса
https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_matrix_driver/

## Что произойдет, если сломается
Перестанет генерироваться датасет yandex-maps-l6a-matrix-jams-diff, у матричного роутера упадёт качество предсказания eta

## Monitorings
https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_matrix_driver_stable

## Ecstatic datasets
Потребляет:
yandex-maps-graph-speed-profiles<br/>
yandex-maps-jams-speeds<br/>
yandex-maps-jams-speeds-external<br/>
yandex-maps-jams-closures<br/>
<br/>
Генерирует:<br/>
yandex-maps-l6a-matrix-jams-diff


## Graphics
Stable: https://yasm.yandex-team.ru/template/panel/maps-core-matrix-driver-stable-panel-main/<br/>
Testing: https://yasm.yandex-team.ru/template/panel/maps-core-matrix-driver-testing-panel-main/<br/>
Datatesting: https://yasm.yandex-team.ru/template/panel/maps-core-matrix-driver-datatesting-panel-main/

## Instances
| Environment | URL |
|---|---|
| stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_matrix_driver_stable |
| datatesting | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_matrix_driver_datatesting |
| testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_matrix_driver_testing |

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
  * /var/spool/yandex/maps/graph - хардлинки на графы из экстатика
* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_MATRIX_DRIVER_STABLE_RTC_NETS__\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MATRIX_DRIVER_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_MATRIX_DRIVER_TESTING_RTC_NETS_\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MATRIX_DRIVER_TESTING_NETS_ ) |
| datatesting | [ \_MAPS_CORE_MATRIX_DRIVER_DATATESTING_RTC_NETS_\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MATRIX_DRIVER_DATATESTING_RTC_NETS_ ) |
| datavalidation | [ \_MAPS_CORE_MATRIX_DRIVER_DATAVALIDATION_RTC_NETS_\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_MATRIX_DRIVER_DATAVALIDATION_RTC_NETS_ ) |


## Logs
Файловые логи искать в контейнерах в сервисах Няни.

| Name | Path |
|---|---|
| Driver | /var/log/yandex/maps/driver/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Roquefort | /var/log/yandex/roquefort/* |

[маршрутизатор]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/matrix_router/README.md
