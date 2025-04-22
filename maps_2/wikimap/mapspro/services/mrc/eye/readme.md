# Eye of providence
![logo](https://proxy.sandbox.yandex-team.ru/1383246244)

## Overview
The services and the set of tools for road object detection and map validation. The architecture description can be found [here](https://wiki.yandex-team.ru/users/dasimagin/sd2/), which is migrating to the [tech docs](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/doc/).

## Instances, graphics, monitorings
Temporarily **eye** shares environment with [signs_detector](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/signs_detector) and will replace it in the future.
* [ABC service](https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-signsdetector/)
* [Per commit build task](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_SIGNSDETECTOR)
* [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps-core-nmaps-mrc-signsdetector/)
* [Monitoring](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-mrc-signsdetector)

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_mrc_signsdetector_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_signsdetector_stable/) | [ core-nmaps-mrc-signsdetector.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-signsdetector-stable-panel-main/) | [ maps_core_nmaps_mrc_signsdetector_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_signsdetector_stable) |
| Testing | [maps_core_nmaps_mrc_signsdetector_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_signsdetector_testing/) | [ core-nmaps-mrc-signsdetector.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-signsdetector-testing-panel-main/) | [ maps_core_nmaps_mrc_signsdetector_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_signsdetector_testing) |

## Services
### Frame
* [import_mrc](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/bin/import_mrc)

### Recognition
* [detect_object](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/bin/detect_object)
* [detect_panel](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/bin/detect_panel)
* [manage_recognition_task](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/bin/manage_recognition_task)
* [sync_detection](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/bin/sync_detection)

### Object
* [object_manager](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/bin/object_manager)

### Hypothesis
* [generate_hypothesis](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/bin/generate_hypothesis)
* [push_feedback](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/bin/push_feedback)

### Monitoring
* [check_queue_size](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/bin/check_queue_size)
* [check_run_time](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/bin/check_run_time)

### Tool
* [import_mrc/monitoring](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/bin/import_mrc/monitoring)
* [import_detection](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/tool/import_detection)
* [test_feature_location](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/tool/test_feature_location)
* [upload_mrc_feature](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/tool/upload_mrc_feature)
