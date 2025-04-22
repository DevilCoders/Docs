# Темплейтный подход к SQL

При формировании сложных SQL часто используют различные SQL-конструкторы, которые
имеют низкую наглядность и большой порог вхождения.

Так же существует проблема работы с SQL из кода python. Включения SQL в виде строк
приводят к смешению кода SQL и Python что не делает код читабельным.

Данный проект пытается решить обе проблемы:

1. Раскладка SQL по файликам в заданной директории
2. Простая генерация SQL

Для генерации SQL используется темлейтный язык, базирующийся на jinja2.

Пример:

```sql
SELECT
    *
FROM
    "users"
WHERE
        "group_id" = {{ group }}
    {% if filter.name %}
        AND "name" = {{ filter.name }}
    {% endif %}
```

## Особенности

Все вставки кода `{{ code }}` прогоняются через штатный механизм кодирования.
Таким образом данный
решается проблема SQL-инжекшенов при такой же наглядности как f-строки.

Доступны все возможности jinja2 по формированию блоков, циклов, итп.

## Дополнительные фильтры

Иногда надо вставить кусок кода без енкодинга (например имена таблиц),
можно использовать фильтр `|i` (от слова immediately). В этом случае
вставка текста будет непосредственной.

Так же есть фильтр `|q`, он по умолчанию добавляется ко всем
вставкам `{{ code }}`, однако может использоваться для наглядности.

Еще можно использовать фильтр `|vlist`. Использование этого фильтра
имеет смысл только с массивами.

Например:

```sql
SELECT
    *
FROM
    "table"
WHERE
    "id" IN ({{ ids |vlist }})
```

Если `ids = (1,2,3)`, то SQL будет приведен к виду:

```sql
SELECT
    *
FROM
    "table"
WHERE
    "id" IN ($1, $2, $3)
```

А список переменных для bind будет содержать значения `1,2,3`.


## Низкоуровневый API

Низкоуровневый API не включает в себя интеграцию с собственно коннектором Pg,
а только раскладку SQL по директориям и работу с темлейтом.

```python

import dbtpl
import postgresql

db = postgresql.open('pq://test:test@localhost:5432/test')
agent = dbtpl.agent(sqldir)


sql, bindargs = agent('my/select.sql', { 'id': 123 })
rows = db.query.rows(sql, *bindargs)

```

## Надстройка для модуля asyncgpg

Реализован наследник и врапперы для функций connect и `create_pool`:


```python
import dbtpl.asyncpg

# установление коннекта
db = await asyncpg.connect('postgresql://postgres@localhost/test', sql_dir='.')

# Типовая схема работы
row = await db.single('myfile1.sql', {'id': 10, 'login': 'vasya'})
rows = await db.select('myfile2.sql', {'group': 'bla'})
boolresult = await db.perform('myfile3.sql', {'foo', 'bar'})


# иногда всё-таки нужно написать SQL прямо в коде. Тогда через .inline
row = await db.inline.single("SELECT {{a}}", {'a': 123})
rows = await db.inline.select('SELECT generate_series(1,5), {{a}}', {'a': 123})
boolresult = await db.inline.select('DROP TABLE {{ tbl |i }}', {'tbl': 'users'})


# работа с пулами
pool = await asyncpg.create_pool('postgresql://postgres@localhost/test', sql_dir='.')

# взятие коннектора из пула и работа с ним
async with pool.acquire() as db:
    row = await db.single('myfile1.sql', {'id': 10, 'login': 'vasya'})
    rows = await db.select('myfile2.sql', {'group': 'bla'})
    boolresult = await db.perform('myfile3.sql', {'foo', 'bar'})
```

## Надстройка для модуля postgresql

```python

import dbtpl.pg


db = dbtpl.pg.connect('pq://localhost:5432/test', 'my/sql/dir')

admins = db.select('user/list.sql', {'filter': {'role':'admin'} })

```

Модуль определяет три метода и два свойства:

* `connection.agent` - экземпляр dbtpl (ro свойство)
* `connection.db` - экземпляр postgresql (ro свойство)

* `connection.perform` - метод для выполнения запросов не возвращающих значения (`create table` итп)
* `connection.single` - метод для выполнения запроса возвращающего одну строку
* `connection.select` - метод для выполнения запроса возвращающего выборку 0+ строк
