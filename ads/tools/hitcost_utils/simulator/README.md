# Симулятор для применения хиткоста и подсчёта его метрик в оффлайне

**Что происходит:**
1. Из логов строится `preprocessed_table`
2. `preprocessed_table` подготавливается к применению хиткостов и записывается в `joined_output_table`.
3. К `joined_output_table` по одной применяются модели.
4. После этого над `joined_output_table` рассчитываются метрики.
5. Можно напрямую сравнить две модели и получить оценку различия их метрик.

**Опции командной строки:**
- `--yql_token` - токен от YQL
- `--conf` - путь к конфигу
- `--preprocess` - надо ли строить с нуля `preprocessed_table` для применения хиткоста (шаг 1)
- `--prepare` - надо ли создавать `joined_output_table` (шаг 2)
- `--apply` - надо ли применять хиткосты (шаг 3)
- `--eval` - надо ли рассчитывать метрики (шаг 4)
- `--compare` - надо ли выполнять сравнение двух моделей (шаг 5)

**Опции в конфиге:**
- `dates`:
    - `start_date`, `end_date` - даты начала и конца промежутка, за который надо считать метрики, включительно. Нужны только для этапа `preprocess`.
- `tables`:
    - `preprocessed_table` - таблица на выходе препроцессора
    - `joined_output_table` - таблица, к которой можно применять хиткосты
    - `dataframe_folder` - путь к папке, в которую складывать датафреймы с метриками
    - `dump_folder` - путь к папке, в которую складывать дампы моделей с помощью `fetch_dump`
    - `mw_table` - промежуточная таблица, которую можно использовать для сравнения моделей
- `params`:
    - `result_suffix`: str - такой суффикс прибавится к названию директории с результатами и графику на Datalens
    - `thresholds_to_mark`: Dict[str, float] - по задумке должна давать ставить разные пороги для отдельных ссп, но сейчас еще может не работать
    - `sspid_exclusion_run`: bool - считает метрики для всего лога - указанные sspids
    - `sspids`: List[int] - можно указать отдельные sspid и по ним отдельно посчитаются метрики
    - `testids`: List[int] - По каким `ActiveTestIds` брать логи
    - `sample_ratio`: int - доля хитов для семплирования
    - `markup`: str - задает X ось графика. Сначала идет тип разметки может быть `p` - percentiles или `t` - thresholds, далее через одинарный пробел идут разделенные `:` значения начала, конца и шага, эти параметры передаются в функцию np.arange
    - `mw_bucket_count` - на сколько бакетов разбивать хиты при сравнении экспериментов. Дефолтное значение должно давать нормальные результаты
    - `condint_alpha` - уровень значимости доверительного интервала, для которого считать разницу экспериментов
- `mannwhitney`:
    - `etalon` и `exp` - названия моделей, значения которых записаны в `joined_output_table` и которые нужно сравнить.
    - `etalon_threshold` и `exp_threshold` - пороги, для которых выполнять сравнение.
- `models`: здесь должен находиться набор моделей в следующем формате:
    - `название модели:`
        - `lm` - какую линейку подавать на вход
        - `hitcost` - дамп модели
        - `readable_name` - так модель будет называться на графике лучше пользоваться ASCII символами, иначе в даталензе все будет записано кодами юникода
        - `threshold_to_mark` - порог для модели. Предполагается отказаться в пользу `thresholds_to_mark` из `param`, не отмечается в datalens
        - `mx_factors` - список полей, которые нужно подавать на вход хиткосту помимо факторов из `HitCostFactors`. Добавятся в конец.
