# CatBoost

## Действие PrepareCatboostPool (`prepare_catboost_pool`)    {#prepare_catboost_pool}

Готовим пул в [формате](https://docs.yandex-team.ru/catboost/concepts/input-data_values-file#native-catboost-in-yt), подходящем для обучения CatBoost.

**input:** Dataset или ListOf(Dataset).

**output:** Pool или ListOf(Pool) со столькими же пулами, сколько датасетов в inputs. Если входов и выходов больше одного, каждый входной датасет будет отдельно преобразован в соответствующий по порядку пул.

**parameters:**

* `column_description` (OrderedDict строка ➞ строка, обязательный) — отображение из имени колонки в [её тип для catboost](https://docs.yandex-team.ru/catboost/concepts/input-data_column-descfile#supported-column-types) (Label, Num, ... )
* `feature_order` (список строк, необязательный) — порядок, в котором в обученную модель надо подавать фичи. Если отсутствует, то используется порядок ключей из column_description.

### Детали реализации       {#prepare_catboost_pool_implementation}

Идейный код для nirvana и tape общий, находится в [ads/libs/tenfifty/plugins/catboost](https://a.yandex-team.ru/arc/trunk/arcadia/ads/libs/tenfifty/plugins/catboost). Для релиза обновления кода на nirvana используется [автоматическая паковка операций](https://docs.yandex-team.ru/vh3/usage/packing) из vh3.

## Действие TrainCatboostModel (`train_catboost_model`)    {#train_catboost_model}
Обучение модели CatBoost.

**input:**

* `train` — данные для обучения в виде пула, полученного от [PrepareCatboostPool](#prepare_catboost_pool).
* `test` — данные для валидации в виде пула, полученного от [PrepareCatboostPool](#prepare_catboost_pool).

**output:** одна Model.

**parameters** разделены на две группы - гиперпараметры модели и настройки процесса обучения.

*Гиперпараметры* (здесь перечислены только самые важные, подробнее - [см. в коде](https://a.yandex-team.ru/arc/trunk/arcadia/ads/libs/tenfifty/plugins/catboost/__init__.py?rev=r8817292#L243-326), и [в официальной документации CatBoost](https://docs.yandex-team.ru/catboost/references/training-parameters/)):

* `loss_function` - функция потерь, на минимизацию которой обучается модель (`Logloss`, `QueryCrossEntropy`, `RMSE`, etc.);
* `iterations` - число деревьев в модели;
* `border_count` - число корзинок для дискретизации вещественнозначных фичей;
* `learning_rate` - мультипликатор шага градиентного спуска;
* `l2_leaf_reg` - коэффициент `L2`-регуляризации;
* `ignored_features` - факторы, которые следует игнорировать при обучении.

С `ignored_features` сейчас дело обстоит так: в `PrepareCatboostPool` подаётся полный список фичей, которые индексируются положением в списке (начиная с нуля).
В `ignored_features` нужно подавать индексы фичей (`:`-разделённые), а не их имена (причём для подряд идущих индексов можно задавать интервалы).
Пример: в пуле фичи `[H, A, F, C, D, G, B, E]`, мы хотим заигнорить `H`, `F`, `D`, `G`, `B` - тогда в `ignored_features` подаём `0:2:4-6`.
В будущем это будет автоматизировано.

*Настройки обучения* (также только самые важные):

* `gpu_type` - версия `CUDA`, которую должна поддерживать GPU (до `CUDA_8_0`);
* `cpu_guarantee` - требуемая гарантия на количество ЦПУ;

Полученная модель хранит информацию об использованных для обучения фичах.

### Детали реализации       {#train_catboost_model_implementation}

В nirvana и tape обучение запускается на nirvana с помощью кубика TrainCatBoost из [ads/nirvana/blocks/matrixnet.py](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/blocks/matrixnet.py).


## Действие ApplyCatboostModel (`apply_catboost_model`)     {#apply_catboost_model}

Применяем обученную модель CatBoost.

**input:**

* `dataset`: Dataset, к которому применять, либо ListOf(Dataset).
* `model`: Model, полученная от [TrainCatboostModel](#train_catboost_model).

**output:** Dataset или ListOf(Dataset) — столько же датасетов, сколько в `inputs ➞ dataset`. Это будут копии входных датасетов с добавленной колонкой с именем из параметра `output_column`.

**parameters:**

* `output_column` (строка, обязательный) - имя колонки для записи предсказания
* `yt_memory_limit_gb` (число, необязательный) - лимит памяти для операции `run_map`
* `batch_size` (число, необязательный) - сколько примеров одновременно обрабатывать, проще понять по [коду](https://a.yandex-team.ru/arc/trunk/arcadia/ads/libs/tenfifty/plugins/catboost/__init__.py?rev=r8817292#L502-530)

**Замечание** (пока только для `NirvanaBackend`): если датасет для применения катбуста отсортирован - то в выходном датасете сортировка сохранится, однако операция замедлится (поскольку `ordered_map` дороже, чем `unordered`).

### Детали реализации       {#apply_catboost_model_implementation}

Идейный код для nirvana и tape общий, находится в [ads/libs/tenfifty/plugins/catboost](https://a.yandex-team.ru/arc/trunk/arcadia/ads/libs/tenfifty/plugins/catboost). Для релиза обновления кода на nirvana спользуется [автоматическая паковка операций](https://docs.yandex-team.ru/vh3/usage/packing) из vh3.

## Пример       {#example}

{% include notitle [train_catboost](../_includes/demonstration/train_catboost.md) %}
