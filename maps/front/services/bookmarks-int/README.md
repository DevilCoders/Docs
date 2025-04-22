# `bookmarks-int`

Provides REST API for the shared bookmarks lists management.

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-bookmarks-int |
| Deploy | https://deploy.yandex-team.ru/projects/maps-front-bookmarks-int |
| MDB | https://yc.yandex-team.ru/folders/foonquium8istgt59qca/managed-postgresql?section=list |

## Instances

| Environment | URL |
|---|---|
| Testing | https://bookmarks-int.tst.c.maps.yandex.net/ |
| Production | https://bookmarks-int.maps.yandex.net/ |

## Documentation

API method documentation and API entities description can be found in [docs](docs) directory or on [Swagger UI webpage](https://bookmarks-int.tst.c.maps.yandex.net/v1/api_docs/)

## Known clients

* Yandex Web Maps
* Yandex Maps Mobile app

## What happens when service is down

All known clients will be unable to update the shared bookmarks lists and gather new updates.
It means that the user couldn't be able to send the updates of his bookmarks lists to the subscribers and receive the updates of the lists he subscribed on.

## How to fix common problems

### Contacts

| Name | URL |
|---|---|
| Emergency chat with MDB | https://t.me/joinchat/CCDG-0Dje_KWvyMQ-bFMtA |

### Restart service

```sh
# supervisorctl restart app
```

### Database
- If the database cannot handle the load (e.g. high CPU wait on the `Production PG Cluster (golovan)` dashboard), you should
  contact the MDB Emergency duty and ask for a fast 2x scale-up of the cluster.

## Monitorings

| Type | URL |
|---|---|
| [Golovan](https://yasm.yandex-team.ru/) | https://yasm.yandex-team.ru/template/alert/maps-front-bookmarks-int-production-app |
| [Juggler](https://juggler.yandex-team.ru/) | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps-front-bookmarks-int_production.app |

## Dashboards

| Name | URL |
|---|---|
| Main | https://yasm.yandex-team.ru/template/panel/maps-front-common/full_env_name=maps-front-bookmarks-int_production |
| Deploy | https://yd.yandex-team.ru/stage/maps-front-bookmarks-int_production/monitoring |
| Production PG Cluster (golovan) | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbvj64kc1kqctu95ud9;dbname=bookmarks_int/ |
| Production PG Cluster (solomon) | https://solomon.yandex-team.ru/?project=internal-mdb&cluster=mdb_mdbvj64kc1kqctu95ud9&service=mdb&dashboard=internal-mdb-cluster-postgres |

## Logs

| Name | URL/path |
|---|---|
| Deploy | `/porto_log_files/app_workload_stdout.portolog`, `/porto_log_files/app_workload_stderr.portolog` <br/> https://deploy.yandex-team.ru/stages/maps-front-bookmarks-int_production/logs |
| Nginx, Juggler Client, Push client | `/var/log/supervisor/` |
| YT (maps) | `hahn.[home/logfeller/logs/maps-front-production-log]` [yql example](https://yql.yandex-team.ru/Operations/YVrcbQVK8P1EcSwbjb7u4TfKrWRfajmMQi39gVcPP9k=) |
| YT (Y.Deploy) | `` arnold.`logs/deploy-logs/` `` [yql example](https://yql.yandex-team.ru/Operations/YVreQa5ODy4UKEuAG36uVF5iMy3ZqwsUo3VKwP_bKxo=) |

## Vault

| Type | URL |
|---|---|
| Production | https://yav.yandex-team.ru/secret/sec-01fg1rvajq6t72a3ya7xta9njr/ |
| Testing | https://yav.yandex-team.ru/secret/sec-01f20zn1r5t7zjd7tbd6mncsn7/ |
| Stress | https://yav.yandex-team.ru/secret/sec-01f8sgq75stj0f8bftyfrfz2qz/ |
| Development | https://yav.yandex-team.ru/secret/sec-01ff7nzg89mqwhw1jfrr2jpz4h/ |
| bookmarks-int-test-user | https://yav.yandex-team.ru/secret/sec-01f127w43gq06wz4r2fxe0xf7m/ |

## Developing

Checkout [CONTRIBUTING.md](CONTRIBUTING.md) for tips on how to use the included dev scaffolding.

*Based on [http-api-stub](https://a.yandex-team.ru/arc_vcs/maps/front/tools/http-api-stub)*
