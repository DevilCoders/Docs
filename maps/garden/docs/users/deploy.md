# Деплой данных

В Огороде обычно разделяют по разным модулям варку данных и деплой данных. Пример: `road_graph_build` варит данные, а `road_graph_deployment` - деплоит данные.

Это позволяет иметь сваренные датасеты за несколько последних дней, и отдельно контролировать, какой именно датасет активирован в продакшене, и при необходимости откатывать на предыдущий датасет. Данные могут вариться в любое время, а деплоиться в заданные часы (например, в рабочее время).

Модули, которые выполняют деплой данных, должны иметь тип `deployment` в трейтах:

```json
"type": "deployment"
```

Также принято выставлять лимит 1 на [количество билдов](build_limits.md):

```json
"build_limits": [
    {
        "max": 1,
        "remove_on_exceed": true
    }
]
```

## Шаги деплоя

Один и тот же датасет может деплоиться на разные группы-хостов (в разные Няня-сервисы). В простых случаях можно деплоить сразу на все группы-хостов. В более сложных - нужно деплоить последовательно с дополнительными проверками данных и паузами.

В Картах обычно (но не обязательно) данные деплоятся через [экстатик](https://wiki.yandex-team.ru/maps/dev/core/ecstatic/). В [конфиге экстатика](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ecstatic/stable) указывается, какой датасет на какие машины деплоится. Пример:

```
@testing deploy yandex-maps-coverage5-geoid to rtc:maps_core_meta_datavalidation (tolerance 1)
@prestable deploy yandex-maps-coverage5-geoid to rtc:maps_core_meta_dataprestable (tolerance 1)
@stable deploy yandex-maps-coverage5-geoid to rtc:maps_core_meta_stable (tolerance 1)
```

Чтобы настроить процесс выкатки данных, используется группировка Няня-сервисов по веткам. В примере выше 3 ветки: `testing`, `prestable`, `stable`. Заливать и активировать датасеты можно по отдельности в разные ветки.

Концептуальная модель деплоя описана на [странице](data_deploy.md).

Для управления деплоем данных в Огороде вводится понятие "шаг деплоя". Шаг деплоя - это свойство билда, которое пробрасывается в задачи модуля через ресурс `build_params`. Если модуль деплоит данные через экстатик, то шаг деплоя - это ветка экстатика.

Шаги деплоя в интерфейсе Огорода:

![](img/deploy_steps.png)

### Как включить шаги деплоя для модуля

Нужно вписать названия возможных шагов деплоя в трейты модуля, выставить лимит на количество билдов и настроить пробрасывание шага деплоя в ресурс `build_params`:

```json
"deploy_steps": [
    "testing",
    "prestable",
    "stable"
],
"build_limits": [
    {
        "max": 1,
        "remove_on_exceed": true,
        "builds_grouping": ["deploy_step"]
    }
],
"build_params_args": {
    "deploy_step": {
        "from_build": "{0.extras[deploy_step]}"
    }
},
```

Имена шагов деплоя могут быть произвольными. Но при использовании экстатика рекомендуется, чтобы их имена соответствовали веткам экстатика.

# Как использовать в задачах

Граф задач, который формируется в функции `fill_graph` - общий на все шаги деплоя. Если какая-то из задач не должна выполняться на определённом шаге, то это нужно проверить явно в коде задачи.

Пример задачи:

```py
class MyTask(Task):
    def __call__(self, build_params, input_resource, output_resource):
        if build_params.deploy_step == "testing":
            # Do something
        elif build_params.deploy_step == "stable":
            # Do something else
```

Типовой сценарий - активация датасета в экстатике с помощью задачи `ActivateTask`:

```py
graph_builder.task(
    ActivateTask(
        allowed_deploy_steps=[
            ecstatic_const.TESTING_BRANCH,
            ecstatic_const.PRESTABLE_BRANCH,
            ecstatic_const.STABLE_BRANCH,
        ]
    )
).creates(
    output_resource,
).demands(
    input_resource_name,
    build_params=BUILD_PARAMS_RESOURCE_NAME,
)
```

# Как запускать билды

## UI

Через интерфейс Огорода можно запустить деплой данных в любом шаге деплоя. Можно запускать деплой одновременно в нескольких шагах деплоя.

## Автостартеры

При автоматическом запуске в коде функции автостартера нужно указать шаг деплоя:

```py
def start_build(trigger_build: autostart.Build, build_manager: autostart.BuildManager):
    build_manager.create_build(
        source_ids=[trigger_build.full_id],
        properties={"deploy_step": "testing"}
    )
```

Автостартеры сейчас не позволяют запустить деплой одного датасета сразу в несколько шагов деплоя. Деплоить нужно последовательно: `testing` -> `prestable` -> `stable`.

Но возможен случай, когда параллельно идёт деплой нескольких версий датасета:
* завершается деплой в `testing` и триггерит деплой в `prestable`;
* в это время завершается варка новой версии датасета и триггерит деплой в `testing`.

Разные сценарии можно разрешить или запретить, если написать кастомный автостартер для модуля.

## API

Через API Огорода запросом на ручку `POST /modules/<module_name>/builds/`:

```json
{
    "contour": "datatesting",
    "sources": [
        {
            "name": "road_graph_build",
            "version": "build_id:123"
        }
    ],
    "properties": {
        "deploy_step": "testing"
    }
}
```

В последних двух примерах `deploy_step` - это обязательное свойство билда, иначе он не запустится.
