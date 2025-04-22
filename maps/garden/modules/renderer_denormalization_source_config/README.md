# renderer_denormalization_source_config

Модуль renderer_denormalization_source_config импортирует [layers.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/renderer_denormalization_source_config/data/layers_yt.yaml) и [schema.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/renderer/source/sources/map/0.x/source.json) в Огород.

[CI модуля](https://a.yandex-team.ru/projects/maps-core-renderer-cartograph/ci/actions/launches?dir=maps%2Fgarden%2Fmodules%2Frenderer_denormalization_source_config&id=build)

## Сборка архива с layers.yaml и schema.json

Архив собирается CI задачей [BUILD_RENDERER_DENORMALIZATION_SOURCE_CONFIG_PACKAGE](https://a.yandex-team.ru/svn/trunk/arcadia/maps/garden/modules/renderer_denormalization_source_config/a.yaml?rev=r9586515#L26), которая:
- покоммитно следит за изменениями layers.yaml и schema.json,
- собирает с помощью ya package [архив source-config.sandbox.tar.gz](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/renderer_denormalization_source_config/src_pkg.json),
- загружает его в sandbox как ресурс типа [MAPS_RENDERER_DENORMALIZATION_SOURCE_CONFIG](https://a.yandex-team.ru/svn/trunk/arcadia/sandbox/projects/garden/renderer_denormalization_source_config/__init__.py?rev=r9481463#L4).  

[Текущий статус сборки в CI](https://a.yandex-team.ru/projects/maps-core-renderer-cartograph/ci/actions/launches?dir=maps%2Fgarden%2Fmodules%2Frenderer_denormalization_source_config&id=build-renderer-denormalization-source-config-package), там же можно получить ссылку на sandbox ресурс.

То же самое можно сделать локально:
```
$ ya package src_pkg.json
$ ya upload -T=MAPS_RENDERER_DENORMALIZATION_SOURCE_CONFIG -A="svn_revision=5105554" source-config.sandbox.tar.gz
```

## Импорт layers.yaml и schema.json в огород

Sandbox ресурсы типа `MAPS_RENDERER_DENORMALIZATION_SOURCE_CONFIG` автоматически [сканируются и импортируются](https://docs.yandex-team.ru/garden/scan_resources) Огородом.  
Ручной запуск сканирования (например, для экспериментального контура) описан [тут](https://docs.yandex-team.ru/garden/scan_resources#dopolnitelnye-vozmozhnosti).

Для выкатывания ресурса в stable огород нужно у задачи созданного sandbox ресурса кликнуть "Release" -> "stable" -> "Release". Ссылку на sandbox задачу можно получить из ci (см. выше).

<!--
Ручное импортирование ресурса:
```
cat <<EOF > /tmp/resource.json
{
    "contour": "<contour_name>",
    "foreign_key": {
        "sandbox_resource_id": "1027214638"
    },
    "resources": [
        {
            "version": {
                "properties": {
                    "file_list": [
                        {
                            "url": "https://proxy.sandbox.yandex-team.ru/1027214638",
                            "name": "source-config.sandbox.tar.gz",
                            "md5": "5d0c1b3108e118e6299b12e7ddb53344"
                        }
                    ],
                    "release_name": "2019.07.11-12:36-r5292289",
                    "shipping_date": "2019-07-11T12:36:45Z",
                    "svn_revision": "5292289",
                    "sandbox_resource_id": 1027214638
                }
            },
            "name": "renderer_denormalization_source_config"
        }
    ]
}
EOF

curl -i --request POST \
  --url "http://core-garden-server.maps.yandex.net/modules/renderer_denormalization_source_config/builds/" \
  --header "Content-Type: application/json" \
  --header "Authorization: OAuth <OAuth-token>" \
  --data @/tmp/resource.json
```
-->
