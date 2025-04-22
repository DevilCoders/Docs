# Генерация экспериментов для merge_ft_experiments

## Как добавить кастомное преобразование на yql

1. Пишем yql с заменой как в нирване через `{{}}` в виде библиотеки, в которой определен ACTION %%$postprocess_table($exp_id, $input, $output)%% (см. пример [simple.yql](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/ymapsdf/lib/merge_poi/yql/simple.yql) )
2. Доступные таблицы с именами смотрим [тут](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/ymapsdf/lib/merge_poi/merge_ft_experiment.py) в `spawn_experiment_generation_task`
3. Скрипт запускается и импортится (как %%data.sql%%) в двух местах :
   1. Для применения к "проду" (чистой таблице **ft**) через [apply_postprocessing](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/ymapsdf/lib/merge_poi/yql/apply_postprocessing.yql)
   2. Для применения к экспам (каждому из экспериментов в **ft_experiment**, кроме экспериментов с преффиксом %%postprocessing_%% - то есть полученных тем же способом) - через [apply_to_experiments](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/ymapsdf/lib/merge_poi/yql/apply_to_experiments.yql))
4. Если таблиц не хватает, можем добавить свою:
   1. Смотрим таблицы стадии merge_poi [https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/< timestamp >/cis1_yandex/merge_poi](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/)
   2. Описания таблиц: [основные](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/ymapsdf/garden/create) и [временные](https://a.yandex-team.ru/arcadia/maps/garden/modules/ymapsdf/lib/merge_poi/constants.py) (`FT_TEMP_TABLES`)
   3. Описание смыслов таблиц: https://docs.yandex-team.ru/garden/maps/garden/modules/ymapsdf/README#tablica2
   4. Берем понравившуюся, добавляем в `garden.Demands()` - слева имя, по которому таблица будет доступна в yql, справа `INPUT_STAGE.resource_name("table_name")`, где table_name - имя из списка на ыте
   5. Пишем yql скрипт с `{{table_name}}`
5. Подкладываем yql скрипт [в папку yql](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/ymapsdf/lib/merge_poi/yql)
6. Убеждаемся, что создаем сортированную таблицу с нужной схемой (см. пример simple.yql) и полем `experiment_id` со значением начинающимся на `postprocess`
7. Добавляем тест на синтаксис в [ya.make](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/ymapsdf/lib/merge_poi/yql/ya.make)
8. Добавляем скрипт в [ya.make](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/ymapsdf/lib/ya.make)
9. Регистрируем в [custom_transformations::POSTPROCESSING](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/ymapsdf/lib/merge_poi/custom_transformations.py):
   - Создаем объект типа %%TrasformationDescription%%
   - указываем список регионов, в которых хотим запускать свой эксп (РФ входит в **cis1**, **all** - все регионы)
   - в task кладем объек типа %%PostprocessTask%%
   - %%attach_file%% - ваш новый yql файлик с определенной %%$postprocess_table%%
   - %%exp_id%% имя эксперимента, не забудьте добавить префикс %%"postprocess_"%%
   - %%displayed_name%% отображается в графе и пригодится для тестирования
10. Имя `displayed_name` используем для тестирования https://docs.yandex-team.ru/garden/debug#lokalnyj-zapusk-zadach
11. Собираем модуль **ymapsdf** и деплоим в свой неймспейс для проверки полноценного запуска графа ([КАК?](https://docs.yandex-team.ru/garden/experiments)), проверяем работу **ymapsdf** и потом там же **renderer_denormalization**. Тут понадобится доступ с вашей разработческой машинки до Огорода, нужно завести правило в панчере, аналогичное [этому](https://puncher.yandex-team.ru/tasks?id=62b30a24f16202512997e30b).
12. Проходим ревью
13. Если все ок, с разрешения ответственных катим в дататестинг ([КАК?](https://docs.yandex-team.ru/garden/module-lifecycle#sedem))


## Как добавить кастомное преобразование на python

1. См. Пункты выше, разница заключается в том, что что в POSTPROCESSING надо подцепить код python. Менее дружественно, более гибко.
2. Если придется так делать, нужно предусмотреть также применение таска к экспериментам из ft_experiments, для этого надо определить у вашего таска %%get_exp_application_task%%

## [Не рекомендуется] Как добавить кастомное преобразование на с++

1. Через python binding см. mapreduce.pyx
2. Учтите замечания про  %%get_exp_application_task%%
