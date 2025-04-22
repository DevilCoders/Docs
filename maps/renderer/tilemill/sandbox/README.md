Бинарная Sandbox задача для создания тайлсета из таблиц в YT или из geojson датасета.

#### Как создать тайлсет:
- получить роль `Пользователь` в сервисе [maps-core-renderer-tilemill](https://abc.yandex-team.ru/services/maps-core-renderer-tilemill/),
- открыть [шаблон задачи MAPS_RENDERER_TILEMILL_TASK](https://sandbox.yandex-team.ru/template/MAPS_CORE_RENDERER_TILEMILL_SANDBOX_TEMPLATE_STABLE),
- создать sandbox задачу кнопкой `Create new task`,
- заполнить обязательные параметры задачи: название датасета и рецепт,
- стартовать задачу.

Описание формата рецепта см. в [libs/mill/README.md](../libs/mill/README.md).

Для удаления тайлсета нужно в sandbox задаче нажать `Release` -> выбрать `cancelled` -> нажать `Release`.

#### Как настроить регулярное обновление тайлсета:
- однократно создать тайлсет с помошью sandbox задачи `MAPS_RENDERER_TILEMILL_TASK`,
- получить `cartograph_dataset_id` из секции `Custom header` страницы sandbox задачи,
- добавить датасет в список планировщиков в [add_datasets](task/datasets.py),  
  заполнить `cartograph_dataset_id` значением из предыдущего пункта,
- добавить планировщик в [sedem_config](sedem_config/__all__.yaml),
- закоммитить изменения,
- зарелизить sandbox планировщик с помощью sedem:  
  `ya tool sedem release start maps/renderer/tilemill/sandbox rNNNNNNN`  
  `ya tool sedem release step maps/renderer/tilemill/sandbox vNNN.N stable`
- в sandbox настроить регулярность запуска созданного планировщика и стартовать его.

[Sandbox планировщики](https://sandbox.yandex-team.ru/schedulers?task_type=MAPS_RENDERER_TILEMILL_TASK):
[mapsearch_stable](https://sandbox.yandex-team.ru/scheduler/698347),
[mapsearch_testing](https://sandbox.yandex-team.ru/scheduler/698345).  
Sandbox шаблоны: [stable](https://sandbox.yandex-team.ru/template/MAPS_CORE_RENDERER_TILEMILL_SANDBOX_TEMPLATE_STABLE), [testing](https://sandbox.yandex-team.ru/template/MAPS_CORE_RENDERER_TILEMILL_SANDBOX_TEMPLATE_TESTING).

[Monitorings all (tag=a_prj_maps-core-renderer-tilemill-sandbox)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-renderer-tilemill-sandbox&project=maps)

#### Как откатить тайлсет на предыдущую версию:
- перейти в sandbox на страничку с ресурсами типа [MAPS_RENDERER_TILEMILL_TILESET_INFO](https://sandbox.yandex-team.ru/resources?type=MAPS_RENDERER_TILEMILL_TILESET_INFO&state=READY&limit=20&attrs=%7B%22cartograph_dataset_id%22%3A%2288b1e80b-5fa3c6c4-c52a2c71-53126c50%22%7D),
- отфильтровать ресурсы по значению атрибута `cartograph_dataset_id` нужного датасета,
- перейти на страницу задачи, создавшей предыдущую версию ресурса,
- нажать `Release` -> выбрать `stable` -> нажать `Release`.

#### Локальная сборка и создание sandbox задачи:
```
cd maps/renderer/tilemill/sandbox/task
ya make -r .
./MAPS_RENDERER_TILEMILL_TASK run --type MAPS_RENDERER_TILEMILL_TASK --enable-taskbox --create-only
```
[Документация](https://docs.yandex-team.ru/sandbox/dev/binary-task) на бинарные sandbox задачи.  
