`binding` recipe
================

Приготовление пакета, со сборкой биндингов под разные платформы.

## `build`

В build-параметре ожидается объекст с полями:
- `platforms` - массив словариков со следующими полями:
    - `platform` - значение `process.platform` node.js, соответствующее целевой платформе
    - `params` - любые параметры sandbox-таски YA_MAKE
- `common_params` - необязательный параметр, устанавливающий дефолтные значения для поля `params` каждой платформы.

Дополнительно, на каждом таком словарике могут быть установлены произвольные поля, которые прорастут в атрибуты целевых ресурсов.

Также, рецепт распознает тип целевого ресурса, если он был переопределен через `params.result_rt`. По умолчанию целевые ресурсы имеют тип `ARCADIA_PROJECT`.

## `compose`

compose стадия не имеет параметров.

## Пример конфигурации

```json
{
    "type": "binding",
    "package": {
        "name": "@yandex-int/fei-17757-flock",
        "version": "1.0.0",
        "description": "flock binding by npmify",
        "keywords": [
            "flock"
        ]
    },
    "build": {
        "common_params": {
            "checkout_arcadia_from_url": "arcadia:/arc/trunk/arcadia",
            "targets": "serp/ynode/extensions/flock",
            "result_single_file": true
        },
        "platforms": [
            {
                "platform": "darwin",
                "params": {
                    "target_platform": "darwin",
                    "arts": "serp/ynode/extensions/flock/dynamic/libflock.node.dylib",
                },
                "some": "custom attribute"
            },
            {
                "platform": "linux",
                "params": {
                    "arts": "serp/ynode/extensions/flock/dynamic/libflock.node.so",
                }
            }
        ]
    }
}
```
