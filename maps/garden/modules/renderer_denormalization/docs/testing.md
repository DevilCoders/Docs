# Тестирование модуля renderer_denormalization

## Локальный запуск тестов

Запуск всех тестов модуля:
```
ya make -r -ttt maps/garden/modules/renderer_denormalization
```

Можно использовать тег `slow` для того чтобы отфильтровать медленные yt/yql тесты:
```
ya make -r -ttt maps/garden/modules/renderer_denormalization --test-tag -slow
```
Или для запуска только медленных тестов:
```
ya make -r -ttt maps/garden/modules/renderer_denormalization --test-tag +slow
```

Для запуска одного теста задачи можно использовать фильтрацию по названию теста:
```
ya make -r -ttt maps/renderer/denormalization/lib/tests -F sql_query_demands_tests::demands_test
ya make -r -ttt maps/renderer/denormalization/lib/tests/data_tests/ad_edge_tmp_test
```

## Тестирование в Огороде

- Создать огородный [эксперимент](https://docs.yandex-team.ru/garden/experiments).
- [Запустить](https://docs.yandex-team.ru/garden/experiments#start_local_module) локально собранный модуль.

Для визуальной проверки изменений:
- Запустить модуль renderer_denormalization_dump на собранном билде renderer_denormalization.
- Запустить модуль renderer_archive на собранном билде renderer_denormalization_dump. При создании билда в параметре renderer_map_stable_bundle нужно указать релиз из datatesting контура.
- Открыть в testing Картографе созданную ветку билда renderer_archive.

## Локальное тестирование на данных из Огорода

- Создать огородный [эксперимент](https://docs.yandex-team.ru/garden/experiments).
- Запустить в созданном эксперименте сборку модуля renderer_denormalization и дождаться ее завершения.
- Получить пути к таблицам модуля в YT: у собранного билда кликнуть `Open performance analyzer`, выбрать одну из задач (например, `BoundaryTask`), в `Demanded resources` найти путь к таблицам ymapsdf (кликнуть `ymapsdf_ft_cis1_yandex`, скопировать путь из `Url`), в `Created resources` найти путь к таблицам renderer_denormalization (кликнуть `renderer_denormalization_boundary_cis1_yandex`, скопировать путь из `Url`).  
  Путь к таблицам ymapsdf обычно вида `//home/maps/core/garden/datatesting/ymapsdf/20201202_524565_1935_203386748/cis1_yandex/final`, где `datatesting` - название огородного контура/эксперимента, `20201202_524565_1935_203386748` - свойство `shipping_date` билда, а `cis1_yandex` - собираемый регион.  
  Путь к таблицам renderer_denormalization обычно вида `//home/maps/core/garden/exp/eak1mov_y07/renderer_denormalization/20201202_524565_1935_203386748/cis1_yandex`, где `exp/eak1mov_y07` - название огородного контура/эксперимента, `20201202_524565_1935_203386748` - свойство `shipping_date` билда, а `cis1_yandex` - собираемый регион.
- Собрать и запустить тул renderer_denormalization на тестируемой задаче, используя пути к таблицам в YT, полученные в предыдущем пункте:
```
ya make -r maps/renderer/denormalization/bin

export YT_PROXY=hahn
export YT_TOKEN=`cat ~/.yt/token`

./maps/renderer/denormalization/bin/renderer_denormalization run AdEdgeTmpTask -i "//home/maps/core/garden/datatesting/ymapsdf/20201202_524565_1935_203386748/cis1_yandex/final" -o "//home/maps/core/garden/exp/eak1mov_y07/renderer_denormalization/20201202_524565_1935_203386748/cis1_yandex" -d
```

## Визуальная проверка изменений в локальном картографе

- Запустить тул renderer_denormalization на тестируемой задаче (см. `Локальное тестирование на данных из Огорода`).
- Обновить в `maps/renderer/libs/data_sets/denormalization_dump/config/shippings.yaml` пути к таблицам денормализации, созданным в огородном эксперименте.
- Запустить дамп:
```
ya make -r maps/renderer/libs/data_sets/denormalization_dump/bin
./maps/renderer/libs/data_sets/denormalization_dump/bin/denormalization_dump -s maps/renderer/libs/data_sets/denormalization_dump/config/shippings.yaml -l maps/garden/modules/renderer_denormalization_source_config/data/layers_yt.yaml -n 16 maps/renderer/cartograph/data/compiled
```
- (опционально) Скопировать схему данных:
```
mkdir -p maps/renderer/cartograph/data/schema
cp maps/doc/schemas/renderer/source/sources/map/0.x/source.json maps/renderer/cartograph/data/schema/map_source.json
```
- Запустить локальный рендерер картографа:
```
cd maps/renderer/cartograph
ya make -r bin
YCR_MODE=http:8080 YCR_THREADS=16 ./bin/renderer-cartograph
```
- Открыть в браузере `%host%:8080`.

## Визуальная проверка изменений в Картографе с помощью tilemill

- Запустить тул renderer_denormalization на тестируемой задаче (см. `Локальное тестирование на данных из Огорода`).

- Составить [рецепт](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/tilemill/libs/mill/README.md) tilemill для датасета денормализации:
  - заполнить `dataset_type: denormalization`,
  - заполнить `table_prefix` путем к выходным таблицам renderer_denormalization (из параметров запуска тула),
  - заполнить `layers` слоем из [layers_yt.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/renderer_denormalization_source_config/data/layers_yt.yaml).  

  Например, для задачи [FenceAreaTask](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/denormalization/lib/tasks/impl/fence_a/fence_a.cpp?rev=r9235962#L27) и слоя [fence_a](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/renderer_denormalization_source_config/data/layers_yt.yaml?blame=true&rev=r9286732#L73) рецепт будет таким:
  ```
  dataset_type: denormalization
  table_prefix: //home/maps/core/garden/exp/eak1mov_y07/renderer_denormalization/20201202_524565_1935_203386748/cis1_yandex
  layers:
  - id: fence_a
    type: polygon
    table: fence_a
    minzoom: 16
    properties:
    - tags
  ```

- Получить url схемы датасета денормализации:
  - открыть страницу билдов огородного модуля [renderer_denormalization_source_config](https://garden.maps.yandex-team.ru/datatesting/renderer_denormalization_source_config),
  - у первого билда кликнуть `Open performance analyzer`, выбрать задачу `UnpackSourceTask`, в `Created resources` выбрать ресурс `renderer_denormalization_source_config_schema`, скопировать `Url`.

- Запустить [sandbox задачу](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/tilemill/sandbox/README.md) tilemill:
  - открыть [testing шаблон](https://sandbox.yandex-team.ru/template/MAPS_CORE_RENDERER_TILEMILL_SANDBOX_TEMPLATE_TESTING) задачи MAPS_RENDERER_TILEMILL_TASK,
  - создать sandbox задачу кнопкой `Create new task`,
  - заполнить параметры задачи: название датасета, рецепт `recipe` и url схемы `schema_url` из предыдущих пунктов,
  - стартовать задачу и дождаться ее завершения.

- Проверить изменения в Картографе:
  - открыть testing Картограф,
  - создать новую ветку,
  - выбрать тестируемый слой,
  - заменить источник данных в слое: `Common` -> `Layer info` -> `Source`, выбрать вместо `map` название датасета из sandbox задачи,
  - визуально проверить корректность изменений.
