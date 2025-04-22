# design_bundles

## Module description
This module creates map designs for different services and uploads ecstatic datasets:
- yandex-maps-jams-design
- yandex-maps-road-events-design
- yandex-maps-streetview-design
- yandex-maps-mrc-design

Each dataset contains a production design, a design testing (release candidate) and experimental branches of design.

## How to test module
1. Deploy the module to testing.
2. Publish a design in [Cartograph Testing](https://cartograph.tst.c.maps.yandex-team.ru).
3. Check tiles of traffic jams and road events, street panoramas, mirrors in datatesting:
    - https://l7test.yandex.ru/maps?l=trf,trfe&renderer_experimental_datatesting=1
    - To see design testing add `experimenal_{layer}_design=testing` parameters: [link](https://l7test.yandex.ru/maps?l=trf,trfe&renderer_experimental_datatesting=1&renderer_experimental_trf_design=testing&renderer_experimental_trfe_design=testing&renderer_experimental_stv_design=testing&renderer_experimental_mrc_design=testing)

WARN: [streetview datatesting](https://a.yandex-team.ru/arc/trunk/arcadia/maps/streetview/renderer/readme.md) is not ready in April 2021.

## How to update canonical test data
Call `YA_MAPS_CANONIZE_TESTS=1 ya make -t` to update canonical test data.
