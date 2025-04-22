`package` recipe
================

Приготовление пакета, являющегося результатом `ya make`.

## `build`

В build-параметре поддерживаются любые параметры sandbox-таски YA_MAKE.

## `compose`

В compose можно указать единственный необязательный параметр:
- `in_resource_path` - указывает путь к пакету, внутри собранного на build-стадии ресурса. Ожидается, что итоговый ресурс является директорией и целевой пакет может находится не в корне этого ресурса. Если опция не указана, то считается, что пакет располагается в корне ресурса.

## Пример конфигурации

```json
{
    "type": "package",
    "package": {
        "name": "@yandex-int/fei-17757-horizon-protos",
        "version": "1.0.0",
        "description": "horizon protos by npmify"
    },
    "build": {
        "arts": "serp/node_modules/horizon-protos",
        "checkout_arcadia_from_url": "arcadia:/arc/trunk/arcadia",
        "targets": "serp/node_modules/horizon-protos"
    },
    "compose": {
        "in_resource_path": "horizon-protos"
    }
}
```
