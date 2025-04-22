## API
Схему ручки заливки данных можно посмотреть по [ссылке](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Backend-py3/replication/api/api/#datareplication_rule_name).
Помимо этого, нужно заказать доступы к машинке репликации (укажите сервис `replication`) с машинки, которая будет пушить данные
и прописать правила для выписки тикетов TVM ([инструкция](https://wiki.yandex-team.ru/taxi/backend/architecture/tvm2/#jaxochupodpisyvatzaprosyvstoronnijjserviskotoryjjprinimaettikety).
Кроме того, для доступа к самой ручке надо прописать роль по шаблону `put_data-{имя_правила}` в конфиг **SERVICE_ROLES** ключ `replication`:
[testing](https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/SERVICE_ROLES?name=SERVICE_ROLES) |
[production](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/SERVICE_ROLES?name=SERVICE_ROLES)
и указать в списке TVM-сервис машинки, с которой будут пушиться данные.

* `replicate_by` — поле с бизнес-датой, которая будет отображаться в админке.
Стоит учитывать, что выставляться в стейтах оно будет строго с учетом монотонного возрастания.
Также, в этом случае нужно указать каст этого поля в дату: `replicate_by_cast`
* `replicate_by_cast` — Доступные опции лучше смотреть в [коде](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/backend-py3/services/replication/replication/custom_models/datetime_cast.py).
* `replicate_by_empty_reason` — Комментарий о причине, по которой не указано поле `replicate_by`.
* `plugin_parameters` — тут доступна опция `personal_transform` для обработки персональных данных.
Данные будут подменяться на id в сервисе ПД.
Правил **rules** может быть более одного. Задаётся так:
```yaml
plugin_parameters:
  - name: personal_transform
    parameters:
        rules:
          - personal_type: phones
            json_path: path.to.value
            normalize: phone_add_plus
            json_path_type: default
```
* Схема `rules`:
    * `json_path` — **path.to.value** — путь к персональному значению в исходном документе.
    В данном случае это словарь с вложенными
    элементами, точка обозначает вложенность.
    * `personal_type` — тип [персональных данных](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/backend-py3/services/replication/replication/plugins/personal/client.py#L20).
    * `normalize` (optional) — способ нормализации значения.
    Доступные типы стоит смотреть [тут](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/backend-py3/services/replication/replication/plugins/personal/normalization.py),
    также здесь нужно добавлять новые.
    Чтобы они стали доступны в правилах репликации требуется выкатить сервис **replication**.
    * `json_path_type` (optional) — смотреть [тут](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/backend-py3/services/replication/replication/plugins/personal/json_path.py#L7).
    Режим по умолчанию **default** справится с извлечением значений из документов в большинстве случаев,
    другие режимы помогут со сложными случаями, подробнее смотри [тесты](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/backend-py3/services/replication/test_replication/plugins/personal/test_json_path_zendesk.py).

## Queue Mongo
Очередь - это внутренний тип источника, явно его указывать не нужно, но некоторые настройки доступны в `queue_data`.
