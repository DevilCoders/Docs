# Onfoot Processor

Processes objects made in Mobile NMaps application (Mobile Map Editor) in the walking mode:
* Checks photos content.
* Publishes photos in the dashcam snapshots layer.
* Creates feedback objects in NMaps.


## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Сухов (quoter@yandex-team.ru) |
| Отвественные SRE | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) <br> Дмитрий Сухов (quoter@yandex-team.ru) |
| Исходники | [maps/wikimap/mapspro/services/mrc/onfoot-processor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/onfoot-processor) |
| Сервис в ABC | [maps-core-nmaps-mrc-onfoot-processor](https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-onfoot-processor/)|
| CI (TestEnv) - Покоммитный | [BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_ONFOOT_PROCESSOR](https://beta-testenv.yandex-team.ru/project/maps_tests/job/BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_ONFOOT_PROCESSOR/history?limit=20) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_mrc_onfoot_processor_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_onfoot_processor_stable/) | [ core-nmaps-mrc-onfoot-processor.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-onfoot-processor-stable-panel-main/) | [ maps_core_nmaps_mrc_onfoot_processor_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_onfoot_processor_stable) |
| Testing | [maps_core_nmaps_mrc_onfoot_processor_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_onfoot_processor_testing/) | [ core-nmaps-mrc-onfoot-processor.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-onfoot-processor-testing-panel-main/) | [ maps_core_nmaps_mrc_onfoot_processor_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_onfoot_processor_testing) |


[Monitorings all (tag=a_prj_maps-core-nmaps-mrc-onfoot-processor)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-mrc-onfoot-processor)

## How it Works

Onfoot Processor performs following operations for objects with status `pending` uploaded by the Mobile NMaps:
* Downloads a photo from MDS.
* Calculates photo's size and orientation.
* Checks that the photo does not contain any forbidden content.
* If a photo is okay then feedback is created and object's status is changed to `published`.
* Otherwise object's status is changed to `discarded`.

In case of any errors object's status is changed to `failed`.

If a photo is created on a territory where it is prohibitted to show photos then corresponding feedback is hidden.


## How to fix fired up monitorings

**onfoot-processor-failed-objects-count**

1. Enter the docker container in Nanny and check the logs `/var/log/yandex/maps/onfoot-processor/*`
to find out what went wrong.
2. If the problem is caused by an external service unavailability then move the failed objects to the pending queue:
```
psql postgresql://maps_mrc:<password>@c-117eed12-3358-4c5e-b713-6cbf1d57e54e.rw.db.yandex.net:6432/maps_mrc
=> BEGIN;
=> UPDATE signals.walk_object SET status='pending' WHERE status='failed';
=> COMMIT;
```
3. If the problem is caused by the damaged data then consider removing the data from the database.


## What Happens When the Service is Down?

Feedback from Mobile NMaps (walking mode) is not being delivered to NMaps.


## Other services

DBaaS
* [Stable](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=117eed12-3358-4c5e-b713-6cbf1d57e54e;dbname=maps_mrc)
* [Testing](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=dcddf4d9-6276-4f2a-9e11-3c07cab2ccd1;dbname=maps_mrc_testing)

MDS
* [Stable](https://yasm.yandex-team.ru/template/panel/mds-ns-space/prj=maps_mrc/?range=604800000)

wiki-social
* [Stable](https://grafana.yandex-team.ru/d/3wXHxtDik/maps-wiki-social?orgId=1)



### Logs

All logs can be found in Nanny's containers in the following directories.

| Name                | Path                                      |
|---------------------|-------------------------------------------|
| onfoot-processor    | `/var/log/yandex/maps/onfoot-processor/*` |
| supervisord         | `/var/log/supervisor/*`                   |
| syslog (unfiltered) | `/var/log/syslog`                         |
