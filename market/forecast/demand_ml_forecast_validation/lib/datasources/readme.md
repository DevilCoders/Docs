# Модуль Datasources

### yt_tables.yaml
Этот файл содержит все датасорсы, используемые в прогнозе.
```yaml
datasource_name:
    kind: monthly
```

После добавления к датасорсу можно обращаться в коде:
```python
from ..datasources import datasources
datasource = datasources.datasource_name
```

#### Атрибуты
| Название          | Формат                                        | Дефолт                           | Описание                                                                                                                                                                                                                                                                                   |
|-------------------|-----------------------------------------------|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| path              | string                                        | –                                | Обязательный параметр, путь к таблице, может содержать один плейсхолдер {date}.                                                                                                                                                                                                            |
| kind              | (daily, weekly, monthly)                      | –                                | Обязателен, если в пути есть плейсхолдер под дату.                                                                                                                                                                                                                                         |
| fallback_days     | int                                           | –                                | Количество дней фоллбека, если запрошенная таблица не найдена. Если отсутствует или равен 0, фоллбек не осуществляется.                                                                                                                                                                    |
| fallback_strategy | (reuse_last, use_only_existing)               | reuse_last                       | reuse_last cкопирует последнюю таблицу N раз за несуществующие даты.  use_only_existing игнорирует отсутствующие данные, использует только то, что есть.                                                                                                                                   |
| await_source      | bool                                          | False                            | Если True, при вызове сорса, если он не найден, скрипт будет ожидать его появления.                                                                                                                                                                                                        |
| await_params      | max_retries: int sleep_time: int (in seconds) | max_retries: 100 sleep_time: 300 | Параметры количества попыток и периода ожидания для await_source.                                                                                                                                                                                                                          |
| date_key          | string                                        | –                                | Ключ с датой в таблице, обязателен для weekly и monthly таблиц, поскольку по нему осуществляется фильтрация неполных периодов. Если такого нет, то можно указать use_whole_periods = True, но в таком случае в источник попадут данные за рамками запрошенного периода, если он не ровный. |
| validate          | bool                                          | True                             | Если указать False, таблица не будет никаким образом проверяться. Не стоит использовать в проде.                                                                                                                                                                                           |
| date_format       | string                                        | %Y-%m-%d                         | Для таблиц, формат названий которых не соответствует %Y-%m-%d, формат можно переопределить через этот параметр.                                                                                                                                                                            |
| first_week_day    | int (0 – Пн, 6 – Вс)                          | 0                                | Для weekly таблиц: день недели, в который формируется таблица.                                                                                                                                                                                                                             |
| use_whole_periods | bool                                          | False                            | Используется для работы с weekly и monthly таблицами, у которых нет столбца с датой, см. date_key.                                                                                                                                                                                         |

Пример использования await_params:
```yaml
datasource_name:
    path: //path/to/table
    await_source: True
    await_params:
        max_retries: 100
        sleep_time: 300  # 5 минут
```

### Использование в коде

Для таблиц без плейсхолдера, можно вызвать просто по названию:
```yaml
test_single_table:
    path: //path/to/table
```

```python
print(datasources.test_single_table)
# //path/to/table
```

Для таблиц с плейсхолдерами необходимо вызывать `for_period()` или `latest()`.
После этого доступны операции:
* `to_yql()`
* `to_clickhouse()`
* `to_nile()`
* `to_spark()`

#### for_period()
Можно инициализировать двумя способами:
* Через start_date и end_date (начало и конец периода данных, включительно)
* Через start_date, today и lag_days (внимание: lag_days сдвинет и начало, и конец)

Также можно при вызове переопределить конфиги date_format, kind, first_week_day и use_whole_periods, но делать это не рекомендуется

#### latest()
Обязательно указать параметр today, (будет взята последняя таблица на опеределенную дату)

#### Вызов данных
`to_yql()` и `to_clickhouse()` генерируют самостоятельные SQL куски (текст)
`to_nile(job=job)` и `to_spark(spark=spark)` генерируют объекты соответствующих библиотек, на вход обязательно подавать контекст

#### Примеры
```python
data = datasources.test_datasource.for_period(
    start_date='2020-01-01',
    end_date='2021-01-01'
).to_yql()

query = f"""
    select *
    from {data.to_yql()}
"""
```

```python
data = datasources.test_datasource.for_period(
    start_date='2020-01-01',
    end_date='2021-01-01'
).to_nile(job=job)  # Здесь необходим найловский объект job

data_processed = data.qb2(filters=[sf.nonzero('fit'))])
```

```python
data = datasources.test_datasource.latest(today='2021-01-01')

mskus = data.to_spark(spark=self.spark).select('msku')
```
