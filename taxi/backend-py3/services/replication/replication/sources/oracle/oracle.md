## Oracle
* [Как добавить секрет yav](../../docs/arcadia/secrets.md#how_to_add_yav)
* [Как добавить секрет strongbox](../../docs/arcadia/secrets.md#how_to_add_strongbox)
* [Как использовать секрет в правиле](../../docs/arcadia/secrets.md#how_to_use_secret)
<br>
<br>
* `connection`:
    * `secret` — алиас секрета в config.yaml
* `replicate_by` — поле, по которому нужно реплицировать. Это должно быть поле, хранящее дату и выставляющееся в БД.
  Также для корректной работы по этому полю необходимо иметь индекс.
* `table` — имя таблицы.
* `primary_key` — список имен ключевых колонок.
* `timezone` — по умолчанию `UTC`. Нужно явно выставить иную в случае,
если поле `replicate_by` по каким-то причинам выставляется не в `UTC`.
* `raw_select` - поле, в котором можно указать кастомные запросы для получения данных из базы. В этом случае движение
  по курсору происходит с шагом `time_chunk_size` от результата запроса `min_replicate_by` до
  результата запроса `max_replicate_by`. Если за очередной шаг в источнике данных нет, то пытаемся получить
  слещующий документ выполняя `min_replicate_by` с добавлением условия, что `replicate_by` больше чем значение этого
  поля у последнего полученного из источника документа.
    * `data` — полный запрос для получения данных из базы (поле для репликации и первичный ключ должны
      обязательно быть в списке выбранных колонок).
    * `min_replicate_by` — полный запрос для получения минимального значения поля репликации в базе.
    * `max_replicate_by` — полный запрос для получения максимального значения поля репликации в базе.
    * `data_query_has_conditions` — обязательный булевый флаг. Нужно указать, содержатся ли
      условия в кастомном запросе данных.
* `time_chunk_size` — размер временного окна в секундах для чанка. По умолчанию 10 минут. Используется только в
  инкрементаальных загрузках с `raw_select`

Note:
В данный момент репликатор умеет обращаться к столбцам по имени строго в том формате, который возвращает схема.
В oracle это имена полей в UPPER_CASE, это нужно учитывать при указании полей `primary_key`, `replicate_by`

Пример:
```(yaml)
name: oracle_test
replication_type: queue
source:
    type: oracle
    connection:
        secret: config_yaml_secret_alias
    table: test.test
    primary_key:
      - ID
    replicate_by: UPDATED_AT
    timezone: Europe/Moscow
destinations:
  - oracle_test_raw:
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

### Время и таймзоны в Oracle

На данный момент используемый драйвер для Oracle (cx_Oracle) не умеет корректно работать
с колонками типа `TIMESTAMP WITH LOCAL TIME ZONE` и `TIMESTAMP WITH TIME ZONE`.
Таймзона просто отбрасывается (см. [примечание 2 под таблицей в документации](https://cx-oracle.readthedocs.io/en/latest/user_guide/sql_execution.html?highlight=timestamp#fetch-data-types)).

На GitHub висит [тикет](https://github.com/oracle/python-cx_Oracle/issues/13).
Но пока движения по нему нет.

Если требуется сохранять временную зону в поле со временем, то можно извлекать
ее в формате ISO8601-строки с преобразованием на стороне Oracle
(создав view или используя raw_select).

```sql
select to_char(tz_column,'YYYY-MM-DD"T"HH24:MI:SS.FFTZHTZM') as tz_column_
```
