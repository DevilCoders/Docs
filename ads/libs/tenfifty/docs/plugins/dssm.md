# DSSM

Плагин для работы с DSSM-моделями.
**N.B.** Пока что все действия отсюда реализованы на `NirvanaBackend`, а на `TapeBackend` -- только `GetDssmModelFromYt`.


## Действие GetDssmModelFromYt (`get_dssm_model_from_yt`)   {#get_dssm_model_from_yt}

Скачивает готовую модель из YT.

**output:** `DssmModel` - бинарный файл DSSM-модели.

**parameters:**

* `path` (строка) — полный путь к модели на YT.


## Действие ApplyDssmModel (`apply_dssm`)   {#apply_dssm}

Применяет обученную DSSM-модель на датасете.

**input:**

* `dataset` — `Dataset`, self-explanatory;
* `model` — `DssmModel`, бинарный файл DSSM-модели.


**output:** один `Dataset`.

**parameters:**

* `columns` (непустой список строк) - поля в датасете, к которым применяется DSSM;
* `header` (непустой список строк) - поля в датасете, на которых училась DSSM (свойство модели, поля из `header` матчатся один к одному к полям из `columns`);
* `result_column` (непустая строка) - название поля, в которое запишется результат применения DSSM;
* `columns_to_output` (непустой список строк) - список полей, которые следует оставить в итоговой таблице (`result_column` должен быть в их числе, иначе граф не соберётся);
* `output_mode` (строка, одно из `{"single_float", "vector", "tab_separated", "space_separated"}`) - формат вывода, почти всегда стоит использовать `"single_float"` (по умолчанию);
* `model_type` (строка, одно из `{"dssm3", "nn_applier"}`) - метод обучения DSSM (при применении должен совпадать с методом, по которому модель училась);

Параметры дальше задают настройки MR-джобов или партиционирование данных, на итоговый результат не влияют.
У них есть разумные дефолты, и шатать их стоит только если вы уверены, что в вашем случае они существенно хуже оптимальных.

* `batch_size` (положительное целое, по умолчанию 1024) - размер батча подаваемых на вход DSSM данных;
* `memory_limit` (положительное целое, по умолчанию 64 GiB) - максимальная выделяемая под маппер память на хосте (MiB);
* `threads_count` (положительное целое, по умолчанию 4) - число тредов на один ЦПУ;
* `cpu_limit` (положительное целое, по умолчанию 16) - максимальное используемое число ЦПУ на хосте;
* `data_size_per_job` (положительное целое, по умолчанию 512 MiB) - рекомендуемый размер данных на одну Map-джобу (MiB).

На `NirvanaBackend` также поддержаны [стандартные параметры](https://a.yandex-team.ru/arcadia/ads/libs/tenfifty/docs/backends/nirvana.md#BackendParameters)


### Детали реализации       {#apply_dssm_implementation}

Код применения DSSM лежит [тут](https://a.yandex-team.ru/arcadia/quality/nirvana_tools/conveyor_operations/train_dssm/dssm/yt_apply/lib/dssm_pool_apply_map.h?rev=r9711370#L10).


## Пример       {#example}

{% include notitle [apply_dssm](../_includes/demonstration/apply_dssm.md) %}
