## Сборка

Сборка docker-образа с использованием ya-tool:

    ya package noc/traffic/blockscheme/blocklist-monitoring/package.json --docker --docker-repository mnt-traf

## Как добавляются проверки

Изначально необходимо создать bundle — см. директорию check-bundle и завести задачу на сборку бандла в
[sandbox](https://sandbox.yandex-team.ru/task/1238793388/view).  
Более подробно можно найти описание в [документации](https://docs.yandex-team.ru/juggler/client/bundles).

Параметры для сборки:
* Svn url for arcadia(checkout_arcadia_from_url): `arcadia:/arc/trunk/arcadia`
* Path to package file in Arcadia(package_path): `noc/traffic/blockscheme/blocklist-monitoring/check-bundle/bundle.json`
* Upload resulting resource to MDS(upload_to_mds): `false`
* Resource type to build(resource_type): `JUGGLER_CHECKS_BUNDLE`
* Force resource creation(force_resource): `false`
* Name of bundle(bundle_name): `blocklist-monitoring-check-bundle`

Также необходимо в juggler доставить новое описание проверок:

    jsonnet juggler-checks.jsonnet | juggler-sdk load --force --dry-run
    jsonnet juggler-checks.jsonnet | juggler-sdk load