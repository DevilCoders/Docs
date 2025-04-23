## MSSQL
* [Как добавить секрет yav](../../docs/arcadia/secrets.md#how_to_add_yav)
* [Как добавить секрет strongbox](../../docs/arcadia/secrets.md#how_to_add_strongbox)
* [Как использовать секрет в правиле](../../docs/arcadia/secrets.md#how_to_use_secret)
<br>
<br>
* `connection`:
    * `secret` — алиас секрета в config.yaml
* `replicate_by` — поле, по которому нужно реплицировать.
  Это должно быть поле, хранящее дату и выставляющееся в БД.
  Также для корректной работы по этому полю необходимо иметь индекс.
* `table` — имя таблицы.
* `primary_key` — список имен ключевых колонок.
* `timezone` — по умолчанию `UTC`. Нужно явно выставить иную в случае,
если поле `replicate_by` по каким-то причинам выставляется не в `UTC`.

Пример:
```(yaml)
name: mssql_test
source:
    type: mssql
    replication_type: queue
    connection:
        secret: secret_alias
    table: test.test
    primary_key:
      - ID
    replicate_by: utc_updated_dttm
destinations:
  - mssql_test_raw:
        mapper: $raw
        target:
            raw_settings:
                yt_columns_info:
                  - name: id
                    input_column: ID
                    type: string
                    description: ID
                    sort_order: ascending
            cluster_groups:
              - map_reduce
            path: raw/test/test
        type: yt
```
