# Signs detector

## Overview
* [ABC service](https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-signsdetector/).
* [Per commit build task](https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_SIGNSDETECTOR).
* [Dashboard](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps-core-nmaps-mrc-signsdetector/).

As map-reduce operation it loads photos of mrc service and detects signs. The found signs are used to validate the road graph. Error hypotheses are sent to the social service as a feedback.

## Instances, graphics, monitorings
| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_mrc_signsdetector_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_signsdetector_stable/) | [ core-nmaps-mrc-signsdetector.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-signsdetector-stable-panel-main/) | [ maps_core_nmaps_mrc_signsdetector_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_signsdetector_stable) |
| Testing | [maps_core_nmaps_mrc_signsdetector_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_signsdetector_testing/) | [ core-nmaps-mrc-signsdetector.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-signsdetector-testing-panel-main/) | [ maps_core_nmaps_mrc_signsdetector_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_signsdetector_testing) |

[Monitorings all (tag=a_prj_maps-core-nmaps-mrc-signsdetector)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-mrc-signsdetector)

## Ecstatic Datasets
| Stable | Testing |
| ------ | ------- |
| [yandex-maps-coverage5-geoid](http://ecstatic.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) | [yandex-maps-coverage5-geoid](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) |
