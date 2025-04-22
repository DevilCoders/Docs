## YDB target

YDB как таргет можно использовать со всеми доступными типами источников.

### Настраиваем доступы

Для работы с YDB нужно указать 3 секрета:
- Эндпоинт
- База Данных
- Токен робота, который будет ходить в YDB.

Для репликации в YDB нужен робот. Вы можете использовать уже существующий свой или завести новый.
Про то, как завести робота, чуть ниже.

#### Как узнать эндпоинт и базу данных

Эндпоинт и база данных указаны на странице **Обзора** базы:

![YDB connections](../../docs/arcadia/_images/ydb_connections.png "YDB connections")

Положите их в отдельные секреты в стронгбокс. Используйте для них тип `freeform`.

[Стронгбокс секреты в админке](https://tariff-editor.taxi.yandex-team.ru/secrets)

#### Как завести робота

Завести робота можно:
* **с помощью тикета** в очередь `TAXIADMIN`.
[Пример](https://st.yandex-team.ru/TAXIADMIN-30870) такого тикета. В тикете надо указать, как получить
токен и в какой секрет его положить.

* **самомостоятельно** по [инструкции](https://wiki.yandex-team.ru/tools/support/zombik/).

#### Как получить токен

Токен можно получить по [инструкции](https://ydb.yandex-team.ru/docs/getting_started/start_auth#get_oauth_token),
предварительно залогинившись под роботом. Если у вас нет прав залогиниться под роботом,
то попросите это сделать админов. Также попросите положить токен
в секрет в стронгбоксе. Тип секрета для токена должен быть `api_token`.

{% note warning %}

В своей базе не забудьте выдать роботу `use` права.

{% cut "Кнопка выдачи прав" %}

![YDB robot rights](../../docs/arcadia/_images/ydb_robot_rights.png "YDB robot rights")

{% endcut %}

{% endnote %}

#### Добавляем секреты в секдист репликации

Секдист репликации расположен [здесь](https://tariff-editor.taxi.yandex-team.ru/services/38/edit/356018/secrets?service_name=replication).
Вам нужно добавить внутрь `ydb_settings` ключ вашего коннекта (придумайте его самостоятельно) и в соответствии
этому ключу указать свои 3 секрета. То есть, должно получиться так:
```
{
    "ydb_settings": {
        <connection_key>: {
            "database": "{{ YOUR_DATABASE_SECRET }}",
            "endpoint": "{{ YOUR_ENDPOINT_SECRET }}",
            "token": "{{ YOUR_TOKEN_SECRET }}"
        },
        ...
    },
...
}
```

### Описание формата таргета

Для YDB таргета доступны следующие опции:
* `path` _required_ - относительный путь к таблице. Если таблица партицируется, то это будет путь к директории.
* `connection` _required_ - ключ коннекта, который указан в секдисте (то что обозначено как `connection_key`
  в примере с указанием секретов в секдисте репликации).
* `link` _required_ - ссылка до таблицы в веб-интерфейсе YDB. Используется для быстрого перехода к таблице
из админки репликации. Можно указывать по окружениям в следующем виде:
    ```
    link:
        production: http://production/link
        testing: http://testing/link

    ```
  Если не указывать по окружениям, то в тестинге и в проде будет использована одна и та же ссылка.

### Описание схемы таблицы

Файл со схемой необходимо разместить в директории `ydb-targets` в корне директории скоупа Ваших правил
по пути, указанному в `path` в описании таргета. В файле со схемой необходимо указать следующее:

* `attributes` _required_ - список атрибутов.
  * `schema` _required_ - схема таблицы. Представляет собой список колонок:
    * `name` _required_ - имя колонки.
    * `type` _required_ - YDB тип колонки.
    * `primary_key` - является ли колонка ключевой. Выставьте `true`, если является.
  * `compression` - кодек сжатия. На выбор `lz4` или `none`. По умолчанию `lz4`.
* `description ` - описание таблицы.
* `partitioning` - набор полей, описывающих партицирование таблицы.
  * `type` _required_ - тип партицирования. На выбор один из трёх:
    * `by_days` - для партицирования по дням;
    * `by_months` - для партицирования по месяцам;
    * `by_years` - для партицирования по годам.
  * `field_name` _required_ - имя поля, по которому таблица будет разбиваться на партиции (неизменяемая дата).
  * `cast_to_date` - каст из типа `field_name` в utc дату. Доступные опции: **utc_from_timestamp**
    (по умолчанию), **utc_from_isostring**, **utc_from_microseconds**.

### Пример простого правила

YAML файл с правилом:

```
name: <rule_name>
replication_type: queue
source:
    ...
destinations:
  - <rule_name_ydb_target>:
        type: ydb
        mapper: <rule_name>/<rule_name_ydb_target>
        target:
            path: <rule_name>/<rule_name_ydb_target>
            connection: <connection_key>
            link:
                production: https://yc.yandex-team.ru/link/to/production/table
                testing: https://yc.yandex-team.ru/link/to/testing/table
```

YAML файл со схемой по пути `ydb-targets/<rule_name>/<rule_name_ydb_target>`:

```
attributes:
    schema:
      - name: id
        type: Uint64
        primary_key: true
      - name: created
        type: String
partitioning:
    type: by_months
    field_name: created
    cast_to_date: utc_from_isostring
```

### Ограничения

Репликация делает вставку с помощью BulkUpsert. Это накладывает ограничение: в YDB нельзя делать
BulkUpsert в таблицы со вторичными индексами. Если вам нужен вторичный индекс, то стоит сделать
отдельную таблицу, у которой все колонки - ключевые.
