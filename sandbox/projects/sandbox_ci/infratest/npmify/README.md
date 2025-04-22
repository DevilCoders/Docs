NPMIFY
======

Sandbox-таска для публикации произвольных артефактов из arcadia в npm.

Ввиду произвольности артефактов, существует необходимость описания произвольных же "рецептов" их сборки и композиции для последующей публикации в npm. По этой причине таска предоставляет фреймворк для описания новых рецептов приготовления npm-пакетов.

Поскольку таска реализована как бинарная, поддерживаются следующие возможности:
- поставка с произвольными не `py`-файлами
- доступ к произвольным библиотекам arcadia

## Рецепт

Рецепт состоит из 2-х компонент - builder и composer, выполняющих специфичные для сборки соответствующих артефактов шаги.

Примеры существующих рецептов можно посмотреть в соответствующей [директории](lib/recipes).

### builder

Назначение builder - запустить сопутствующие задачи для сборки необходимых артефактов на уровне sandbox, например, `YA_MAKE` и подготовить результаты сборки для composer. Ввиду sandbox-специфики (распределенный запуск подзадач, ожидание результатов подзадач, сопутствующая потеря контекста выполнения родительской таски при переходе в режим ожидания), builder реализует методы мемоизации контекста исполнения и сохранения состояния, предоставляя, по сути, интерфейс генератора (сопрограммы) со вкусом sandbox - только вместо `yield` используются `memoize_stage` + `return` + методы сохранения/восстановления состояния.

builder наследуется от базового класса [`BaseBuilder`](lib/base_builder.py). Единственный публичный метод объекта builder - `build`, и ожидается, что каждый return из этого метода будет возвращать sandbox-задачу или список sandbox-задач (возможно пустой), необходимых для дальнейших шагов. Для сигнализации об окончании работы, builder должен вызвать метод `done`, описываемый родительским классом, и передать в него произвольные результаты своей работы.

### composer

сomposer получает произвольный результат, который ему передает builder и формирует в некоторой рабочей директории готовый к публикации npm-пакет.

composer наследуется от базового класса [`BaseComposer`](lib/base_composer.py). Единственный публичный метод данного объекта - `compose`, который всегда должен возвращать путь до директории с готовым к публикации пакетом.

### Добавление нового рецепта

Для добавления нового рецепта необходимо:
- в директории [`lib/recipes`](lib/recipes) завести пакет/модуль под новый рецепт,
- в [`__init__`](lib/recipes/__init__.py) файле этой же директории проимпортировать этот пакет/модуль под необходимым для рецепта названием,
- в целевом пакете/модуле завести необходимые builder и composer, отнаследованные от базовых, и определить переменные `builder` и `composer`, указывающие на соответствующие классы.

Также, поскольку `NPMIFY` является бинарной таской, все составляющие ее исходные файлы должны быть указаны в макросе `PY_SRCS` в корневом [`ya.make`](ya.make) файле таски, в том числе и файлы новых рецептов.

## Конфигурация таски

Таска ожидает следующие параметры:

- `default_package_version` - версия пакетов по умолчанию
- `recipes` - список рецептов для сборки и публикации ([пример](#пример-конфигурации-recipes))
- `npm_username` - имя пользователя npm, от которого произовдится публикация
- `npm_password_vault_name` - название секрета в sandbox vault
- `npm_password_vault_owner` - владелец секрета в sandbox vault

### Конфигурация recipes

Каждый рецепт может иметь следующие поля:

- `type` - тип рецепта
- `package` - общая информация о пакете, часть которой добавляется в package.json результирующего пакета
- `build` - настройки builder'а, специфичные для данного рецепта
- `compose` - настройки composer'а, специфичные для данного рецепта
- `enabled` - флаг активности рецепта, по умолчанию `true`

#### Пример конфигурации recipes

С примерами для конкретных рецептов можно ознакомиться в README соответствующих рецептов.

```json
[
    {
        "enabled": false,
        "type": "package",
        "compose": {
            "in_resource_path": "horizon-protos"
        },
        "build": {
            "arts": "serp/node_modules/horizon-protos",
            "checkout_arcadia_from_url": "arcadia:/arc/trunk/arcadia",
            "targets": "serp/node_modules/horizon-protos"
        },
        "package": {
            "version": "1.0.0",
            "name": "@yandex-int/fei-17757-horizon-protos",
            "description": "horizon protos by npmify"
        }
    },
    {
        "type": "binding",
        "build": {
            "platforms": [
                {
                    "platform": "darwin",
                    "some": "custom attribute",
                    "params": {
                        "arts": "serp/ynode/extensions/flock/dynamic/libflock.node.dylib",
                        "target_platform": "darwin"
                    }
                },
                {
                    "platform": "linux",
                    "params": {
                        "arts": "serp/ynode/extensions/flock/dynamic/libflock.node.so"
                    }
                }
            ],
            "common_params": {
                "result_single_file": true,
                "checkout_arcadia_from_url": "arcadia:/arc/trunk/arcadia",
                "targets": "serp/ynode/extensions/flock/dynamic"
            }
        },
        "package": {
            "keywords": [
                "flock"
            ],
            "name": "@yandex-int/fei-17757-flock",
            "description": "flock binding by npmify"
        }
    },
    {
        "type": "binding",
        "build": {
            "platforms": [
                {
                    "platform": "darwin",
                    "params": {
                        "arts": "quality/logs/baobab/tamus/nodejs/lib/libtamus.node.dylib",
                        "target_platform": "darwin"
                    }
                },
                {
                    "platform": "linux",
                    "params": {
                        "arts": "quality/logs/baobab/tamus/nodejs/lib/libtamus.node.so",
                        "result_rt": "OTHER_RESOURCE"
                    }
                }
            ],
            "common_params": {
                "result_single_file": true,
                "checkout_arcadia_from_url": "arcadia:/arc/trunk/arcadia",
                "targets": "quality/logs/baobab/tamus/nodejs/lib"
            }
        },
        "package": {
            "keywords": [
                "tamus"
            ],
            "version": "1.0.0",
            "name": "@yandex-int/fei-17757-tamus",
            "description": "tamus binding by npmify"
        }
    }
]
```
