# Hotel suggest build pipeline

A python-glue app that do all the steps to build and publish hotels suggest dictionary resource.

## Dev run

Before fresh run you must do some preparations:

```shell script
ya make ${ARCADIA_ROOT}/travel/hotels/suggest/builder/bin && ln -sf ${ARCADIA_ROOT}/travel/hotels/suggest/builder/bin/hotels_suggest_builder hotels_suggest_builder
ya make ${ARCADIA_ROOT}/quality/trailer/suggest/data_builder && ln -sf ${ARCADIA_ROOT}/quality/trailer/suggest/data_builder/suggest-data-builder suggest-data-builder
```

After dependencies are built and symbolic links imitates package you can run pipeline locally:

```shell script
ya make . && ./hotels-suggest-build-pipeline --yql-token $(cat ~/.yql/token) --yt-token $(cat ~/.yt/token)
```

This command will not build sandbox resource and can be safely used for development purposes.


## Production run

To build dictionary for production environment run:

```shell script
ya make . && ./hotels-suggest-build-pipeline --yql-token $(cat ~/.yql/prod_token) --yt-token $(cat ~/.yt/prod_token) --publish --sandbox-token $(cat ~/.sandbox/token)
```

This command will build dictionaries as production user, build sandbox resource and publish it to sandbox.

## Build package

```shell script
ya package package/package.json
```

## Autobuild and autodeploy

Pipeline package are built with [Test Env job](https://beta-testenv.yandex-team.ru/project/travel-trunk/job/TRAVEL_PACKAGE_HOTELS_SUGGEST_BUILD_PIPELINE/history).

Pipeline will run each day with sandbox planner job (TODO: Add link).

Dictonaries builded with pipeline will be published as sandbox resource `SUGGEST_DICT` with owner `TRAVEL` and attribute `name=hotels`.
[Link to sandbox](https://sandbox.yandex-team.ru/resources?owner=TRAVEL&type=SUGGEST_DICT&limit=20&attrs=%7B%22name%22%3A%22hotels%22%7D&created=6_months).

Resource with such parameters will be loaded on [suggest multi testing](https://nanny.yandex-team.ru/ui/#/services/catalog/suggest_multi_r1/)

And if deploy was successful to [production](https://nanny.yandex-team.ru/ui/#/services/catalog/suggest_multi/)

In case of corrupted resource such resource must be deleted from sandbox.

## Manual build

In case of manual build run folowing commands

```shell script
ya package package/package.json
ya upload --token $(cat ~/.sandbox/token) --ttl inf --type TRAVEL_HOTELS_SUGGEST_BUILD_PIPELINE --owner TRAVEL --description "Manual upload of TRAVEL_HOTELS_SUGGEST_BUILD_PIPELINE by $(whoami)" <PACKAGE_FILE>
```
