# Описание

s3-json-update.py обновляет https://s3.eu-central-1.amazonaws.com/tt3897/tt.json, который используется для обхода
блокировок в приложениях.

Файл зашифрован с помощью AES, и в расшиврованном виде представляет словарь:

```
{
    "timestamp": "2020-12-15T14:01:39.787040",
    "items": [
        {
            "addresses": [
                "80.239.201.74",
                "149.5.244.208"
            ],
            "fqdn": "mobileproxy.mobile.pssp.z5h64q92x9.net."
        },
        {
            "addresses": [
                "80.239.201.64",
                "149.5.244.49"
            ],
            "fqdn": "yandex.ru."
        },
        ...
    ],
}
```

# Детали

Изначальный таск, в рамках которого настраивалась работа схемы —
[TRAFFIC-3897](https://st.yandex-team.ru/TRAFFIC-3897).  
Некотоое общее описание схемы доступно
[по ссылке](https://wiki.yandex-team.ru/users/kfour/Jeksport-json-spiska-blokirovannyx-xostov-iz-s3/).

# Сборка

Для сборки docker-образа необходимо выполнить:

```
ya package noc/traffic/blockscheme/s3-json-dns/pkg.json --docker --docker-repository traffic
```

# Мониторинг

Описывает основные проверки для сервисов за обходом блокировок:

- ua_s3json: проверяет время обновления JSON файла в AWS облаке.

## Как добавляются проверки

Изначально необходимо создать bundle — см. директорию check-bundle и завести задачу на сборку бандла в
[sandbox](https://sandbox.yandex-team.ru/task/1232682587/view).  
Более подробно можно найти описание в [документации](https://docs.yandex-team.ru/juggler/client/bundles).

Параметры для сборки:
* Svn url for arcadia(checkout_arcadia_from_url): `arcadia:/arc/trunk/arcadia`
* Path to package file in Arcadia(package_path): `noc/traffic/blockscheme/s3-json-dns/check-bundle/bundle.json`
* Upload resulting resource to MDS(upload_to_mds): `false`
* Resource type to build(resource_type): `JUGGLER_CHECKS_BUNDLE`
* Force resource creation(force_resource): `false`
* Name of bundle(bundle_name): `s3-json-dns-check-bundle`

В описании конфигурации box в deploy.y-t необходимо включить juggler и добавить источник — ссылка на указанный выше
собранный бандл, например, `rbtorrent:b3df7d05fe405ac84645c086e326ed00edee8e33`.

Также необходимо в juggler доставить новое описание проверок:

    jsonnet juggler-checks.jsonnet | juggler-sdk load --force --dry-run
    jsonnet juggler-checks.jsonnet | juggler-sdk load
