Драйвера автомобильного маршрутизатора.

Данный сервис является обслуживающим  [автомобильный маршрутизатор][маршрутизатор].
Он генерирует датасеты yandex-maps-l6a-jams-diff-auto, yandex-maps-l6a-jams-diff-taxi, yandex-maps-l6a-jams-diff-truck, которые затем с помощью экстатика загружаются в маршрутизатор.
Балансеров у данного сервиса нет, т.к. он ни с кем не взаимодействует по HTTP(S).

## General information
| Key | Value |
|---|---|
| Ответственные разработчики | Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev) <br/>  Алексеев Андрей [(@alekseev-a-v)](https://staff.yandex-team.ru/alekseev-a-v) <br/> Александр Агафонов [(@lokken)](https://staff.yandex-team.ru/lokken) |
| Ответственные SRE | Вадим Мазаев [(@vmazaev)](https://staff.yandex-team.ru/vmazaev) <br/> Константин Ша́льнев [(@kshalnev)](https://staff.yandex-team.ru/kshalnev)|
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/driver/ |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-driving-driver/ |
| CI (TestEnv) - Покомитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_DRIVING_DRIVER_DOCKER |


## Потребители
Роутер: a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/README.md

## Панель сервиса
https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps_core_driving_driver/

## Что произойдет, если сломается
Перестанет генерироваться датасет yandex-maps-l6a-jams-diff, у роутера возрастет возраст пробок

## Monitorings
https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_driving_driver_stable

## Ecstatic datasets
Потребляет:<br/>
yandex-maps-graph-*<br/>
yandex-maps-jams-speeds<br/>
yandex-maps-jams-speeds-external<br/>
yandex-maps-jams-closures<br/>
<br/>
Генерирует:<br/>
yandex-maps-l6a-jams-diff-auto<br/>
yandex-maps-l6a-jams-diff-taxi<br/>
yandex-maps-l6a-jams-diff-truck<br/>

## Graphics
| Environment | URL |
|---|---|
| stable | https://yasm.yandex-team.ru/template/panel/maps-core-driving-driver-stable-panel-main/ |
| datatesting | https://yasm.yandex-team.ru/template/panel/maps-core-driving-driver-datatesting-panel-main/ |
| testing | https://yasm.yandex-team.ru/template/panel/maps-core-driving-driver-testing-panel-main |
| datavalidation | https://yasm.yandex-team.ru/template/panel/maps-core-driving-driver-datavalidation-panel-main/ |
| dataprestable | https://yasm.yandex-team.ru/template/panel/maps-core-driving-driver-dataprestable-panel-main/ |
| datatestingprestable | https://yasm.yandex-team.ru/template/panel/maps-core-driving-driver-datatestingprestable-panel-main/ |
| datatestingvalidation | https://yasm.yandex-team.ru/template/panel/maps-core-driving-driver-datatestingvalidation-panel-main/ |
| unstable | https://yasm.yandex-team.ru/template/panel/maps-core-driving-driver-unstable-panel-main/ |

## Instances
| Environment | URL |
|---|---|
| stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_driver_stable |
| datatesting | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_driver_datatesting |
| testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_driver_testing |
| datavalidation | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_driver_datavalidation |
| dataprestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_driver_dataprestable |
| datatestingprestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_driver_datatestingprestable |
| datatestingvalidation | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_driver_datatestingvalidation |
| unstable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_driving_driver_unstable |

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
  * /var/spool/yandex/maps/graph - хардлинки на графы из экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## Firewall macroses
| staging | URL |
|---|---|
| testing | [ \_MAPS_CORE_DRIVING_DRIVER_TESTING_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_DRIVER_TESTING_RTC_NETS_ ) |
| datatesting | [ \_MAPS_CORE_DRIVING_DRIVER_DATATESTING_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_DRIVER_DATATESTING_RTC_NETS_ ) |
| stable | [ \_MAPS_CORE_DRIVING_DRIVER_STABLE_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_DRIVER_STABLE_RTC_NETS_ ) |
| datavalidation | [ \_MAPS_CORE_DRIVING_DRIVER_DATAVALIDATION_RTC_NETS\_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_DRIVING_DRIVER_DATAVALIDATION_RTC_NETS_ ) |

## Logs
Файловые логи искать в контейнерах в сервисах Няни.

| Name | Path |
|---|---|
| Driver | /var/log/yandex/maps/driver/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| Roquefort | /var/log/yandex/roquefort/* |

[маршрутизатор]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router/README.md
