# Maps-Auto-Store-Internal
Хранит и управляет информацией о доступных для обновления прошивках, а также их раскаткой на головные устройства

## General information

| Key | Value |
|---|---|
| Кому звонить | https://staff.yandex-team.ru/oklimin |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-auto-store-internal/ |
| Tracker Queue | https://st.yandex-team.ru/YCARBACKEND |
| Tanker | https://tanker.yandex-team.ru/?project=yandexauto&branch=master |
| CI | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_STORE_INTERNAL |
| OAuth | https://oauth.yandex-team.ru/client/e69c563865e54e6486590f134489a619 |
| IDM | https://idm.yandex-team.ru/system/maps-auto-store-internal |
| IDM (для testing) | https://idm.yandex-team.ru/system/maps-auto-store-internal-testing |

## Instances

| Environment | URL |
|---|---|
| Сервисы в няне | |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_store_internal_testing/ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_store_internal_prestable/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_store_internal_stable/ |

## Documentation
https://wiki.yandex-team.ru/users/oklimin/auto/deploy/auto-store/firmware-ota/

## What happens when service is down
Не будет возможности добавлять/удалять пакеты, прошивки, изменять метаданные пакетов и прошивок.
auto-updater после перезапуска не получит информацию о пакетах и прошивках.

## How to fix common problems
TODO

## SLA
TODO

## Monitorings
TODO

## Balancers

| Testing | URL |
|---|---|
| Host | auto-store-internal.testing.maps.n.yandex.ru |
| Nanny | https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-auto-store-internal-testing-slb |

| Stable | URL |
|---|---|
| Host | auto-store-internal.maps.yandex.net |
| Nanny | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-store-internal.maps.yandex.net/show/ |

## Dashboards

| Environment | Link |
|---|---|
| Golovan (testing) | https://yasm.yandex-team.ru/template/panel/maps-auto-store-internal-testing-panel-main |
| Golovan (stable) | https://yasm.yandex-team.ru/template/panel/maps-auto-store-internal-stable-panel-main |

## Logs

Файловые логи искать в контейнерах в сервисах Няни.

| Name | URL/path |
|---|---|
| [YT](https://yql.yandex-team.ru)  | `SELECT * FROM hahn.[home/logfeller/logs/maps-log/1d/2019-03-13] WHERE tskv_format = 'auto-store-internal'` |
| auto-store-internal | `/var/log/yandex/maps/auto-store-internal/` |
| nginx | `/var/log/nginx/` |
| roquefort | `/var/log/yandex/maps/roquefort/` |
| yacare | `/var/log/yandex/maps/yacare/` |
| supervisord | `/var/log/supervisor/` |
| syslog (unfiltered) | `/var/log/syslog` |
| juggler | `/juggler/logs/` |

## Regression Stress Testing Configurations
TODO

## S3 MDS
| S3 bucket | Purpose | Monitoring |
|---|---|---|
| maps-auto-store-internal | EXTERNAL, Firmware images and packages, downloadable from head unit | [YASM](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-auto-store-internal) |
| maps-auto-store-internal-incoming | Incoming firmware images and packages | [YASM](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-auto-store-internal-incoming) |
| maps-auto-store-internal-metadata | Obsolete (was: Firmware metadata, rollout configs, etc.) | |
| maps-auto-store-internal-testing | EXTERNAL, Firmware images and packages, downloadable from head unit, testing env | |
| maps-auto-store-internal-incoming-testing | Incoming firmware images and packages, testing env | |
| maps-auto-store-internal-metadata-testing | Obsolete (was: Firmware metadata, rollout configs, etc., testing env) | |

## Postgres database
| Environment| YandexCloud link |
|---|---|
| Testing | https://yc.yandex-team.ru/folders/fooeu9titknicj7pqrd0/managed-postgresql/cluster/mdbg9aohhcq6cvmnt4j1 |
| Stable  | https://yc.yandex-team.ru/folders/fooeu9titknicj7pqrd0/managed-postgresql/cluster/mdbs0pjbqc1tei49va73 |

### Robot credentials 
https://staff.yandex-team.ru/robot-maps-auto-s3
https://yav.yandex-team.ru/secret/sec-01d54vrz0f6k6vqjadm4kmbgsr/explore/versions

## SECAUDIT
TODO
