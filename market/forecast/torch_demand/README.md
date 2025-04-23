# Инфра для прогноза спроса для msku

## Запуск

Для обучения заданной именованной модели:
```
./scripts/run_base_train.sh
```

Для ежедневного обновления прогнозов заданной модели:
```
./scripts/run_base_predict.sh
```

Для валидации нескольких моделей:
```
./scripts/run_validate.sh
```

## Описание проекта

Проект для обучения, сравнения и применения прогнозов спроса по какому-либо ключу.
Основной тип модели:
  - BASE – прогноз продаж по ключу `subkey` на основе исторических продаж 
    В качестве `subkey` можно взять листовую категорию `s0 = (msku)` или  `s1 = (msku, supplier_code, wh_id)`.
    
ПЛАНИРУЕТСЯ добавить два других типа модели (как в wh_load) 
  - ANAPLAN – прогноз средних значений скидок для каждой msku по запланированным promo_id's, 
    которые есть в таблицах anaplan-а.
  - FAIR – двухшаговый прогноз, который сначала применяет прогноз от модели ANAPLAN для каждой `msku`, 
    потом агрегирует прогнозируемые скидки по ключу `subkey`, полученные агрегаты использует 
    как фичи для итогового прогноза продаж по ключу `subkey`.
    
Проект построен как самодостаточный код, в котором есть возможность запускать графы 
  - обучения, 
  - валидации (сравнения моделей, выявление лучших)
  - прогноза

Графы берут исходные сырые данные из регулярных таблиц на YT и кладут результат на YT 
(сами обученные модели, прогнозы, результаты валидации).
    
На входе используются таблицы:
  - `//home/market/production/mstat/analyst/regular/cubes_vertica/fact_new_order_item_dict_flattened` – факты продаж
  - `//home/market/production/mstat/dictionaries/stock_sku/1d` – состояние стоков
  - `//home/market/production/mstat/analyst/regular/cubes_vertica/dim_ssku_flattened` – информация о мэппинге sku -> msku
  - `//home/market/production/mstat/analyst/regular/cubes_vertica/fact_unpublished_offers` – информация о скрытиях офферов

В модели **BASE** есть важные подварианты:
  - при обучении и тестировании на прошлых датах можно использовать фактические средние скидки 
    за таргетный период; это зависит от `feature_set`, если в имени `feature_set` есть суффикс 
    `future`, то полученный прогноз считается нечестным, и его качество дает оценку сверху 
    (в жизни такой прогноз невозможно использовать, так как точной информации о средней скидке
    для будущих дат для каждого значения key = (msku, supplier_code, wh_id) нет).
     - Варианты c`future` дают оптимистичную оценку того, какое будет качество прогноза, когда мы
       научимся очень хорошо прогнозировать средние скидки в будущем.
         - И здесь есть важный вариант, когда мы в прогнозе пред применением выставляем
           в фичах некоторые значения скидок, которые соответствуют минимальному фону без ПРОМО;
           Сейчас это делается выставлением future-фичей в 90%-квантильные значения 
           (в сторону маленьких скидок);
           Так получается прогноз **BASE_NO_PROMO** – cм. метод TrainBaseModelTask::do_no_promo_predict
     - Варианты без `future` показывают, какого качества можно достичь, если ничего не знать 
       о будущих скидках.


## Структура файлов

Для понимания модели BASE нужно посмотреть файлы
  - `lib/data_preparation/sql/build_base_dataset.sql` – файл с YQL кодом для получения датасета для BASE; 
    в нём используется стандартная библиотека forecast_utils/utils/sql/counters_lib.sql, а именно,
    subquery, генерирующий поток данных о продажах по заданному ключу (например, warehouse + msku) 
    с инфой про цены, скидки, OOS и др. Эта библиотека поддерживается и гарантируется работоспособность 
    это библиотеки, актуальность используемых таблиц и полей;
  - `lib/data_preparation/build_base_dataset_task.py` – нирвановская таска, которая запускает YQL выше;
  - `lib/data_preparation/train_base_model_task.py` – нирвановская таска, способная выполнять задачи обучения, 
    валидации (сравнения разных прогнозов) и прогноза на заданные даты;
  - `lib/cli_base.py` – файл с конфигурацией моделей для обучения, сравнения и применения

Структура графов для обучения, сравнения и прогноза задана в `lib/graph.py`.
Доступны такие графы (команды):
- **validate** – сравнение моделей заданного типа с заданным subkey (опции `--model_type`, `--subkey`),
  `model_type` – `base`, `analan`, или `fair`, `subkey` – `s1` или `s0`; 
  также есть опция `--target`, чтобы задать колонку, которую нужно прогнозировать; есть такие варианты:
    -  BASE:
        - `r_target_d1_items` – продажи в один день, смещённый на `target_lag + 1` относительно `forecast_date`
        - `r_dn_target_d1_items` – продажи в один день, смещённый на `dn_target_lag + target_lag + 1` относительно `forecast_date`
        - `vec_target_d14_shift_items` – тензорный таргет размерности 14, продажи за 14 дней, где первый день 
          смещённый на `target_lag + 1` относительно `forecast_date`
- **train_base** – обучение BASE модели
- **predict_base** – применение BASE модели 

## Добавление новой фичи

Шаги добавления новых фичей:
  - добавить поля в YT-таблицу c датасетом (если фича основана на новых данных) и добавить их в список `BASE_DATASET_COLS`
    загружаемых колонок в [util_my.py][util_base_columns]
  - добавить новые фичи в новый `feature_set` в [feature_sets_base.py][features]
  - добавить варианты конфигураций обучений с новыми фичами в [cli_base.py][cli_config] 
    и указать их в списке проверяемых моделей [cli_base.py][cli_validate_models] 
  - запустить `run_validate.py`
  - посмотреть результат в таблице [cross_val][cross_val]; 
    если результат по метрикам лучше, чем текущий прод, то нужно дать новому конфигу имя 
    и добавить модель в словарь именованных моделей `predict_base_model_tasks` в [cli_base.py][cli_named_models].
    Именованные модели могут использоваться в командах `train` и `predict` для прода.

Есть несколько вариантов добавления фичи:
  - **Новая фича на базе тех колонок, которые уже есть:**
    
    Здесь нужно просто дописать строчки на питоне типа `dataset["new_feature"] = ..` 
    в метод `enhance_base_dataset`; см., например, как добавляются фичи
    - [target_weekday] – номер дня недели 
    - [norm_d28_sum_sq_price] – нормализованный вариант среднего квадрата продаж за 28 дней

  - **Новая фича в рамках библиотеки `counters_lib.sql`:**
    
    Здесь нужно написать нужный новый тип агрегатора, 
    по какой либо величине в [counters_lib.sql]; 
    можно добавлять фичи типа "cреднее типа X для величины Y за окно дней длины N";
    вот [пример коммита][hist_max] как в 17 строк добавить фичу "исторический максимум продаж";
    
    Тут могут быть разные средние – средние арифметические, квадратические, максимум, минимум, квантили и др.
    А сами величины – это продажи в штуках, в деньгах, дни оффстока, отмены, сумма скидок и др.

  - **Новая фича на базе новых данных:** 
    - вот [пример][ref_prices] добавления нескольких фичей про референсные цены в рамках похожего проекта lastic
    
   Здесь, если действовать только через YQL, можно добавить `SUBQUERY $my_new_features` в `build_base_dataset.sql` 
   и приджойнить это `SUBQUERY` внутри `$save_dataset`.

Также можно сделать отдельную таску для сбора фичи в отдельную таблицу и добавить запуск этой таски в метод 
[define_create_base_dataset_graph][define_create_base_dataset_graph] в `graph.py`. 
И тогда в `build_base_dataset.sql` нужно будет добавить `left join` этой таблицы в определении
[data_with_dn_target][new_feature_line], используя то условия для join, которое нужно
(или msku, или msku + forecast_date или msku + wh_id + forecast_date).
   

## Поиск оптимальных гиперпарамметров

Чтобы подбирать гиперпараметры нужно использовать методы `models_for_change` и `models_for_product`.
С их помощью генерируются списки моделей, которые нужно протестировать.

Например:
```python
train_s1_model_tasks_b5_mq = models_for_change(
    model_cls=TrainBaseModelTask,
    **{
        'net_type': ['dn1'],
        'flt_feature_set': ['f2', 'f3'],
        'cat_feature_set': ['c1', 'c2', 'c3'],
        'mid_size': [20, 18, 16],
        'loss': ['smq'],
        'loss_args': [
            {'qxs': 'high_1', 'beta': 0.1}
        ],
        'target_transform': ['log_0.5'],
        'epochs': [20, 15],
        'shuffle_epochs': [4],
        'batch_size': [3000],
        'learn_rate': [0.001]
    }
)
```
Каждый аргумент здесь должен быть списком вариантов "на попробовать".
Первый элемент в каждом списке называется базовым. Модель задаваемая базовыми параметрами назовём базовой.
Метод `models_for_change` сгенерирует модели, который отличаются от базовой только в одном гиперпараметре,
в данном случае список `train_s1_model_tasks_b5_mq` будет содержать 2 + 3 + 3 + 2 моделей 
(2 варианта `flt_feature_set`, 3 варианта `cat_feature_set`, 3 варианта `mid_size` и 2 варианта `epochs`).

Если же написать `models_for_product`, то будет сгенерировано 2 * 3 * 3 * 2 моделей.
Обычно `models_for_product` используется с аргументом `max_size`, который означает, что из прямого произведения
вариантов нужно взять `max_size` случайных.

Полученный список или списки моделей нужно добавить в список моделей
для валидации [train_base_model_tasks][cli_validate_models] и запустить граф валидации `./scripts/run_validate.sh`.

## Модель FAIR
       
Модель **FAIR** (ПОКА В ПЛАНАХ) является целевой – она должна достичь хорошего качества при максимально точной 
и полной информации о будущих промо в таблицах anaplan. 
В будущем можно переделать на любые другие подобные anaplan таблицы,
в которых будет информация о promo_id: даты проведения, тип промо и размер, ассортимент промо, 
условия на срабатывание промо, факты наличия промоушена на главных экранах, в телевизоре, наружней рекламы и др. 

[target_weekday]: https://a.yandex-team.ru/arc/trunk/arcadia/market/forecast/torch_demand/lib/data_preparation/torch_lib/util_my.py?rev=r9229680#L140
[norm_d28_sum_sq_price]: https://a.yandex-team.ru/arc/trunk/arcadia/market/forecast/torch_demand/lib/data_preparation/torch_lib/util_my.py?rev=r9229680#L192
[counters_lib.sql]: https://a.yandex-team.ru/arc/trunk/arcadia/market/forecast/forecast_utils/utils/sql/counters_lib.sql?rev=r9229680
[hist_max]: https://a.yandex-team.ru/review/2378544/files/1
[ref_prices]: https://a.yandex-team.ru/arc/trunk/arcadia/market/forecast/lastic/lib/data_preparation/sql/build_msku_dataset.sql?rev=r9229680#L114
[util_base_columns]: https://a.yandex-team.ru/arc/trunk/arcadia/market/forecast/torch_demand/lib/data_preparation/torch_lib/util_my.py?rev=r9229680#L32
[features]: https://a.yandex-team.ru/arc/trunk/arcadia/market/forecast/torch_demand/lib/data_preparation/feature_sets_base.py?rev=r9229680#L90
[cli_config]: https://a.yandex-team.ru/arc/trunk/arcadia/market/forecast/torch_demand/lib/cli_base.py?rev=r9229680#L253
[cli_validate_models]: https://a.yandex-team.ru/arc/trunk/arcadia/market/forecast/torch_demand/lib/cli_base.py?rev=r9229680#L284
[cross_val]: https://yql.yandex-team.ru/Operations/Yh9rltJwbFJB9lmkIB6NkywIRSj_igl1C_u3d8rU-nQ=
[cli_named_models]: https://a.yandex-team.ru/arc/trunk/arcadia/market/forecast/torch_demand/lib/cli_base.py?rev=r9229680#L272
[define_create_base_dataset_graph]: https://a.yandex-team.ru/arc/trunk/arcadia/market/forecast/torch_demand/lib/graph.py?rev=r9229680#L221
[new_feature_line]: https://a.yandex-team.ru/arc/trunk/arcadia/market/forecast/torch_demand/lib/data_preparation/sql/build_base_dataset.sql?rev=r9229680#L138