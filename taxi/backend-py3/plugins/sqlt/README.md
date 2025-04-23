# Генератор sql-запросов из jinja2-шаблонов

По умолчанию escape'ит от инжекшенов все `{{ вставки }}`

Пример использования:

```python

query, binds = context.sqlt('path/select.sqlt', {'id': 123})
rows = context.postgresql(query, *binds)

```

Если `'path/select.sqlt'` содержит нечто вроде:

```sql
SELECT
    *
FROM
    "table"
WHERE
    "id" = {{ id }}
```

То на выходе получится `query`:

```sql
SELECT
    *
FROM
    "table"
WHERE
    "id" = $1
```

И `binds`:

```python
(
    123
)
```

Плагин использует модуль `dbtpl`, который определяет несколько дополнительных
фильтров для jinja2:

1. Сознательный injection  `|i`:

```sql
SELECT
    *
FROM
    "{{ tablename |i }}"
WHERE
    "id" = {{ id }}
```

Подходит для передачи имен таблиц.

2. Список значений `|vlist`, разворачивающийся в список параметров.

```sql
SELECT
    *
FROM
    "users"
WHERE
    "id" IN ({{ ids |vlist }})
```

Если `ids` содержит список `(1,2,3)`, то получится

```sql
SELECT
    *
FROM
    "users"
WHERE
    "id" IN ($1, $2, $3)
```

А значения `ids` попадут в соответствующие элементы `binds`.
