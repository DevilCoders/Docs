# Core factory maintenance

Этот сервис предназначен для мониторинга инфраструктуры, от которой зависит функционирование спутниковой фабрики:
- PostgreSQL
- S3MDS

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Сухов (quoter@yandex-team.ru) |
| Отвественные SRE |  |
| Исходники | [maps/factory/services/maintenance](https://a.yandex-team.ru/arc/trunk/arcadia/maps/factory/services/maintenance) |
| Сервис в ABC | [maps-core-factory-maintenance](https://abc.yandex-team.ru/services/maps-core-factory-maintenance/)|
| CI (TestEnv) - Покоммитный | https://beta-testenv.yandex-team.ru/project/maps_tests/job/BUILD_DOCKER_MAPS_CORE_FACTORY_MAINTENANCE/history?limit=20 |


## Service infrastructure

### Instances, graphics, monitorings

| Deploy unit | Nanny service | Graphics panel | Monitoring checks |
| ----------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_factory_maintenance_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_maintenance_stable/) | [ core-factory-maintenance.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-maintenance-stable-panel-main/) | [ maps_core_factory_maintenance_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_maintenance_stable) |
| Testing | [maps_core_factory_maintenance_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_factory_maintenance_testing/) | [ core-factory-maintenance.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-factory-maintenance-testing-panel-main/) | [ maps_core_factory_maintenance_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_factory_maintenance_testing) |

[Monitorings all (tag=a_prj_maps-core-factory-maintenance)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-factory-maintenance)

### Firewall macroses

| staging | URL |
|---|---|
| Stable | [ \_MAPS_CORE_FACTORY_MAINTENANCE_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_MAINTENANCE_STABLE_RTC_NETS_ ) |
| Testing | [ \_MAPS_CORE_FACTORY_MAINTENANCE_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_FACTORY_MAINTENANCE_TESTING_RTC_NETS_ ) |


## How to fix common problems

### PostgreSQL

| Environment | Cluster name | Cluster id | YASM | Solomon | Console |
| ----------- | ------------ | ---------- | ---- | ------- | ------- |
| stable | mapsfactory | `mdb21a98mrqnui16ep26` | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb21a98mrqnui16ep26;dbname=mapsfactory | https://solomon.yandex-team.ru/?cluster=mdb_mdb21a98mrqnui16ep26&project=internal-mdb&service=mdb&dashboard=internal-mdb-cluster-postgres | https://yc.yandex-team.ru/folders/foodm3beso73dkd7am00/postgresql_cluster/cluster/mdb21a98mrqnui16ep26?section=monitoring |
| testing | mapsfactory_testing | `mdbh6cqv98bv2p8igsqc` | https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdbh6cqv98bv2p8igsqc;dbname=mapsfactory | https://solomon.yandex-team.ru/?cluster=mdb_mdbh6cqv98bv2p8igsqc&project=internal-mdb&service=mdb&dashboard=internal-mdb-cluster-postgres | https://yc.yandex-team.ru/folders/foodm3beso73dkd7am00/postgresql_cluster/cluster/mdbh6cqv98bv2p8igsqc?section=monitoring |


### S3MDS

| Environment | S3 bucket | Graphics | Request logs |
| ----------- | --------- | -------- | ------------ |
| stable      | maps-sat-dem | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat-dem;owner=3543 | https://s3-int.chv.yandex-team.ru/projects/maps-sat-cog |
| stable      | maps-sat-push-digital-globe | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat-push-digital-globe;owner=3543 | https://s3-int.chv.yandex-team.ru/projects/maps-sat-dem |
| stable      | maps-sat-source | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat-source;owner=3543 | https://s3-int.chv.yandex-team.ru/projects/maps-sat-source |
| stable      | maps-sat-rgb-source | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat-rgb-source;owner=3543 | https://s3-int.chv.yandex-team.ru/projects/maps-sat-rgb-source |
| stable      | maps-sat-cog | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat-cog;owner=3543 | https://s3-int.chv.yandex-team.ru/projects/maps-sat-cog |
| testing     | maps-sat-dem-tiles-testing | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat-dem-tiles-testing;owner=3543 | https://s3-int.chv.yandex-team.ru/projects/maps-sat-tiles-testing |
| testing     | maps-sat-tiles-testing | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat-tiles-testing;owner=3543 | https://s3-int.chv.yandex-team.ru/projects/maps-sat-tiles-testing |
| testing     | maps-sat-push-digital-globe-testing | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat-push-digital-globe-testing;owner=3543 | https://s3-int.chv.yandex-team.ru/projects/maps-sat-push-digital-globe-testing |
| testing     | maps-sat-rgb-source-testing | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat-rgb-source-testing;owner=3543 | https://s3-int.chv.yandex-team.ru/projects/maps-sat-rgb-source-testing |
| testing     | maps-sat-source-testing | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat-source-testing;owner=3543 | https://s3-int.chv.yandex-team.ru/projects/maps-sat-source-testing |
| testing     | maps-sat-cog-testing | https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat-cog-testing;owner=3543 | https://s3-int.chv.yandex-team.ru/projects/maps-sat-cog-testing |

