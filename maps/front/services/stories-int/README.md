# stories-int

API for Maps stories

[![OKO status][badge:oko]][link:oko]

## General information

| Key              | Value                                                                                                |
| ---------------- | ---------------------------------------------------------------------------------------------------- |
| ABC              | <https://abc.yandex-team.ru/services/maps-front-stories-int/>                                        |
| Deploy           | <https://deploy.yandex-team.ru/projects/maps-front-stories-int>                                      |
| YT Data Transfer | <https://yc.yandex-team.ru/folders/akup8864d28sftk1m682/data-transfer/transfer/dttm5antlpsb9ngg6183> |
| MDB cluster      | <https://yc.yandex-team.ru/folders/akup8864d28sftk1m682/managed-postgresql>                          |

## Monitorings

| Type    | URL                                                                                                   |
| ------- | ----------------------------------------------------------------------------------------------------- |
| Juggler | <https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-stories-int_production.app> |

## Dashboards

| Name                | URL                                                                                                                                                                                                                                                                                |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Dashboard           | <https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-stories-int_production;mode=full>                                                                                                                                                           |
| DataLens            | <https://datalens.yandex-team.ru/dc7vtwj72hp67-dashbord-po-storis-i-novostyam?tab=7J>                                                                                                                                                                                              |
| MDB cluster Yasm    | <https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbh24jhca3j533davai;dbname=stories-int>                                                                                                                                                                    |
| MDB cluster Solomon | <https://solomon.yandex-team.ru/?project=internal-mdb&cluster=mdb_mdbh24jhca3j533davai&service=mdb&dashboard=internal-mdb-cluster-postgres>                                                                                                                                        |
| YT Data Transfer    | <https://solomon.yandex-team.ru/?project=data-transfer&cluster=rtc-prod&dashboard=transfer_dashboard&l.resource_id=*dttm5antlpsb9ngg6183&l.source_type=pg&l.target_type=yt&l.source_id=mdbh24jhca3j533davai&l.target_id=hahn--home-maps-front-stories-int-production-stories&b=1h> |

## Instances

| Environment | URL                                          |
| ----------- | -------------------------------------------- |
| Testing     | <https://stories-int.tst.c.maps.yandex.net/> |
| Production  | <https://stories-int.c.maps.yandex.net/>     |

## Database data

| Environment | URL                                                                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| Production  | <https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/maps/front/stories-int/production/stories/stories> |

## How to fix common problems

[How to detach instance from balancer][link:wiki:detach]

### In case of data transfer alert

-   Check data transfer [status][link:data-transfer] and and error messages
-   Get support: [Data Transfer Support Chat][link:dt-support-chat]

### Restart instance

SSH into container, then:

```sh
supervisorctl restart app
```

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

_Based on [http-api-stub][link:http-api-stub]_

[badge:oko]: https://oko.yandex-team.ru/badges/repo.svg?repoName=maps/front/services/stories-int&vcs=arc
[link:oko]: https://oko.yandex-team.ru/arc/maps/front/services/stories-int
[link:wiki:detach]: https://wiki.yandex-team.ru/maps/dev/ui/deploy/devops/#kakotkljuchitodininstansotbalansera
[link:http-api-stub]: https://github.yandex-team.ru/mapsapi/http-api-stub
[link:dt-support-chat]: https://t.me/joinchat/AqxpCBURpBhW79Uwq6Pcjw
[link:data-transfer]: https://yc.yandex-team.ru/folders/akup8864d28sftk1m682/data-transfer/transfer/dttm5antlpsb9ngg6183
