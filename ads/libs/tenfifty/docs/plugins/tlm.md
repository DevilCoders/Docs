# TLM

## Действие TrainTlmModel (`train_tlm_model`)    {#train_tlm_model}
Обучает TLM.

**input:**

* `train` — Dataset с данными для обучения.
* `test` — Dataset с данными для валидации.

**output:** одна Model.

**parameters** представляют собой словарь со сложной структурой, б́о́льшая часть которой передаётся TLM и обрабатывается уже там.

Таск для обучения tlm задаётся в `parameters ➞ tlm_task`. Это тот самый
таск, который задаётся для кубика TLMTrain в Nirvana, или для [lm_run](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/tlm/lm_run)
О том, какие параметры можно задать, можно прочитать на [официальной вики](https://wiki.yandex-team.ru/users/stepych/tlm/) tlm.

### Детали реализации

{% list tabs %}

- Nirvana

    Используется кубик [tlm nirvana](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/blocks/tlm.py#L27)

    Если `task_id` не задан, то он будет равен `"tlm_model_" + '_nirvana_{meta.owner}_{meta.operation_uid}'`

- Tape

    Tape реализация для Train использует реализацию из [lm_run](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/tlm/lm_run)
    В `parameters->cmd_params` можно задать параметры командной строки(такие же, как в `lm_run`)

    Если `task_id` не задан, то он будет равен `"tlm_model_" + ("_".join(str(self.tape_task.uid).split())`

    После обучения дамп модели в формате `.tar.gz` будет находиться в папке под названием `TrainTlmModelTapeImpl.DUMP_NAME` (`model.tar.gz`)

{% endlist %}


## Действие ApplyTlmModel (`apply_tlm_model`)
Применение обученной модели TLM.

**input:**

* `dataset`: один Dataset, к которому применять.
* `model`: Model, полученная от [TrainTlmModel](#train_tlm_model).

**output:** Dataset, копия входного датасета с добавленной колонкой с именем из параметра `prediction_field`.

**parameters:**

* `prediction_field` (строка, обязательный) — название колонки, куда будет писаться предсказание TLM-модели.

### Детали реализации

{% list tabs %}

- Nirvana

    Реализовано через `VWApplyMapperBlock` и `MrDoMap`, это кубики из [библиотеки](https://a.yandex-team.ru/arc/trunk/arcadia/ads/nirvana/blocks)

- Tape

    На данный момент ApplyTlm реализован через вызовы кубиков Nirvana. На вход ожидается путь до папки, где лежит дамп модели в формате `.tar.gz` (как в Нирвана реализации)
    Название дампа должно быть равно `TrainTlmModelTapeImpl.DUMP_NAME` (`model.tar.gz`)

{% endlist %}

## Пример

{% include notitle [train_tlm](../_includes/demonstration/train_tlm.md) %}


## Действие GetTlmModelFromYt (`get_tlm_model_from_yt`)   {#get_tlm_model_from_yt}

Скачивает готовую модель из YT.

**output:** `TlmModel` - архив с дампом TLM-модели.

**parameters:**

* `path` (строка) — полный путь к модели на YT.
