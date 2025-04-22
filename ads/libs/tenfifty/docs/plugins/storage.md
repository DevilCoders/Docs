# Storage

## Действие UploadToYt (`upload_to_yt`)
Загружает артефакт или несколько артефактов на Yt.

**input:** Dataset или Model, или список таковых. В будущем, возможно, будут поддержаны и другие типы артефактов. Список из разных типов (например, один Dataset и две Model) на данный момент не допускается (из-за возможных изменений в будущем).

**output:** отсутствует.

**parameters:** `directory` или `path` (но не оба одновременно).

* Если указан параметр `directory` (путь на YT в виде строки), все артефакты (один или больше) загружаются в указанную директорию под своими именами.
* Параметр `path` может быть указан одним из тремя способов:
  * Путь на YT (строка) — артефакт загружается по указанному пути. Допускается только если в `input` один артефакт.
  * Путь на YT (строка), содержащий вставки (одну или несколько) `$$input` — артефакты будут загружаться по путям, полученным путём замены вставок `$$input` на имя соответствующего входного артефакта.
  * Словарь вида «имя входного артефакта (строка) → путь на Yt (строка)». В этом случае каждый артефакт сохраняется по своему пути. Вставка `$$input` в этих путях тоже обрабатывается.
* Параметр `ignore_input_mask` (булево значение, по умолчанию `False`) — если `True`, то указанная вставка `$$input` никак не обрабатывается. Таким образом, параметр позволяет писать пути с комбинацией символов `$$input`, если они вам зачем-то нужны.

{% note warning %}

Конкретно строка `$$input` может в ближайшем будущем быть заменена на другую.

{% endnote %}

### Детали реализации
UploadToYt — композитное действие, разлагающееся, в зависимости от типов входных артефактов, на другие действия, которые пока что не документированы.

## Действие UploadModelToMlStorage (`upload_model_to_ml_storage`)
Загружает catboost или tlm модель в [ML Logos Storage](https://logos.yandex-team.ru/docs/ml_logos/storage/about).

**input:** Model

**output:** отсутствует.

**parameters:** `key`, `version`, `owner`, `environment_type`, `attributes` соответсвующие параметрам Push'а [клиентов ML Storage](https://logos.yandex-team.ru/docs/ml_logos/storage/clients/python23)

Пример использования в yaml-таске:
```yaml
    upload_model_to_ml_storage:
        action: upload_model_to_ml_storage
        do_after: train_model
        input: model
        parameters:
          key: sameg_test_catboost_model
          version: 2022-03-11T00:00:00
          owner: AUTOBUDGET
          environment_type: development
          attributes:
            task_id: train_catboost_tenfifty_test
```

## Действие FetchCatboostModelFromYt (`fetch_catboost_model_from_yt`)
Берет catboost модель с YT.

**input:** отсутствует.

**output:** Model.

**parameters:** `path` - путь до директории с моделью (//home/.../my_model).

### Детали реализации
На нирване используются кубики загрузки файлов (GetMRFile, MRDownloadFileAsTSV, YTDownloadBinaryFile).
