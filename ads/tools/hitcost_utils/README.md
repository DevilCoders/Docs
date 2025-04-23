# Некоторые пайплайны для хиткоста

1. Как выполнить препроцессинг хиткоста:
    1. Записать в `ads/tools/simulator/conf.yml`:
        - В `start_date` и `end_date` временной промежуток,
        - В `preprocessed_table` название таблицы на выходе,
        - В `testids` `null` и в `sample_ratio` 273.
    2. Запустить симулятор с опцией `--preprocess`.
2. Как посчитать метрики набора хиткостов:
    1. Заполнить все поля в `ads/tools/simulator/conf.yml` как описано в [readme](simulator/README.md).
    2. Запустить симулятор со всеми опциями командной строки кроме `--compare`.
    3. Скопировать датафреймы из `dataframe_folder` на локальную машину.
    4. Построить графики с помощью ноутбука в `junk/broccoliman/useful`.
3. Как обучить DSSM:
    1. Выполнить препроцессинг при помощи пункта 1 или таска в логосе.
    2. Поджойнить таблицу на выходе с царями при помощи `junk/broccoliman/tsar_multijoining`.
    3. Применить к таблице сначала `junk/broccoliman/useful/dssm_preprocessing`,
    4. а затем `junk/broccoliman/useful/dssm_mappers` с опцией `--train`.
    5. Обучить DSSM на получившейся таблице с помощью [таска](https://a.yandex-team.ru/arc/trunk/arcadia/yabs/utils/learn-tasks2/broccoliman/DSSM/dssm_extra.yml).
4. Как применить DSSM:
    1. Выполнить шаги 1-3 из предыдущего пункта.
    2. Применить `junk/broccoliman/dssm_mappers` с опцией `--apply`.
    3. Применить обученную модель к таблице любым удобным способом, например, например, взяв за основу [этот инстанс](https://nirvana.yandex-team.ru/flow/6dd9bb8d-7181-4e4c-b915-5f50b8b3a70e/2b248a59-7cb0-40e0-8565-bd3bdb866d2c/graph).
