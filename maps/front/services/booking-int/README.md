# `booking-int`

Service for booking integration with partners

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-booking-int/ |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-booking-int |
| Reactor | https://reactor.yandex-team.ru/browse?selected=9347439 |
| Statistics | https://datalens.yandex-team.ru/uabzmviqpj2en-bronirovaniya |

## Instances

| Environment | URL |
|---|---|
| Testing | https://booking-int.tst.c.maps.yandex.net |
| Production | https://booking-int.maps.yandex.net |

## Storage

 * MDS: https://mds.yandex-team.ru/avatars/namespaces/yandex-bookings/overview
 * YT: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/booking-int

## Database

| Environment | URL |
|---|---|
| Testing | https://yc.yandex-team.ru/folders/akukb1gf9soala0c61ci/managed-postgresql/cluster/mdbtfrv2s9l2khrffh2f |
| Production | https://yc.yandex-team.ru/folders/akukb1gf9soala0c61ci/managed-postgresql/cluster/mdb9jltbsqllnpqog8vn |
| Data transfer (YT) | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/booking-int/production/data-transfer |

## Balancers

| Environment | URL |
|---|---|
| Production | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-booking-int.slb.maps.yandex.net/show/ |

## Known clients

[`Yandex Desktop Maps`](https://abc.yandex-team.ru/services/maps-front-maps/)
[`Yandex Mobile Maps`](https://abc.yandex-team.ru/services/mobilemaps/)

## What happens when service is down

No bookings will be available at desktop and mobile maps apps.

## Monitorings

| Type | URL |
|---|---|
| Juggler | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps.front-booking-int.production.app |
| Solomon | https://solomon.yandex-team.ru/admin/projects/maps-front-booking-int |

## Dashboards

| Name | URL |
|---|---|
| Custom | https://yasm.yandex-team.ru/panel/front-booking-int |
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-booking-int_production;mode=full |
| Balancer | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/fqdn=front-booking-int.slb.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=front-booking-int.slb.maps.yandex.net; |
| Active bookings | https://monitoring.yandex-team.ru/projects/maps-front-booking-int/dashboards/mononskvtjkqfhv826cn?range=1d&refresh=60 |
| DB Cluster | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb9jltbsqllnpqog8vn;dbname=production |

## Logs

| Name | URL/path |
|---|---|
| NodeJS | `/porto_log_files/app_workload_stdout.portolog`, `/porto_log_files/app_workload_stderr.portolog` <br/> https://deploy.yandex-team.ru/stage/maps-front-booking-int_production/logs |
| Nginx,Juggler Client, Push client | /var/log/supervisor/ |
| YT (nginx access-log) | `hahn.[home/logfeller/logs/maps-front-production-log]` [yql example](https://yql.yandex-team.ru/Operations/YWPoedjKSy11tiDBbYSppuoTfUfU7sLgyma_QOSwBj4=) |
| YT (nodejs) | `` arnold.`logs/deploy-logs/` `` [yql example](https://yql.yandex-team.ru/Operations/YWPolNjKSy11tiD5yGUeyq9sOG1PLtu2Oql-E7g4sc4=) |

## Vault

https://yav.yandex-team.ru/?search=front-booking-int

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

## Troubleshooting

If [scheduler](https://reactor.yandex-team.ru/browse?selected=9493972) has done something wrong you can run `PREV_TABLE_PATH=<path> make restore-snippets`, where path is like `//home/maps/front/booking-int/production/companies/data/<YYYY-mm-dd>` from [companies data](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/front/booking-int/production/companies/data).

Do not forget to restore symlinks if generated data is not correct:

```sh
yt link //home/maps/front/booking-int/production/companies/data/<YYYY-mm-dd> //home/maps/front/booking-int/production/companies/data/latest
yt link //home/maps/front/booking-int/production/partner-feed/<partner name>/data/<YYYY-mm-dd> //home/maps/front/booking-int/production/partner-feed/<partner name>/latest
```
