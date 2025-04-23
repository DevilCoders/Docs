Библиотека для выполнения рассчётов на YQL
===

Это обёртка над [yql/library/python](/arc/trunk/arcadia/yql/library/python), упрощающая её использование.

Пример
===
Собираемый пример можно посмотреть тут: [example/select.sql](example/select.sql), [example/main.py](example/main.py) (там лежат py2 и py3 бинарники, которые можно запустить).

Hint: если пример запустить так: `Y_PYTHON_ENTRY_POINT=:repl example/py3/example`, то получишь `IPython` с уже загруженным туда yql-модулем под именем `yql`.

Удобнее всего класть класть запросы в ресурсы (`RESOURCE`). Положим такой запрос в `query.sql`:
```sql
declare $table as string; -- declare query param
declare $bounds as Struct<low:Double, high:Double>; -- struct with named fields

select count(*) as cnt from $table
where value between $bounds.low and $bounds.high;
```

Добавим в `ya.make` соотв директиву:
```make
RESOURCE(query.sql /query)
```

Теперь можно выполнить этот запрос и получить результат:
```python
import maps.analyzer.pylibs.yql as yql

def test():
    [table1, table2] = yql.run_query(
        yql.get_query('/query'),
        host='hahn',
        params=yql.create_params(
            table='//path/to/table',
            bounds=yql.Struct(low=0.0, high=100.0),
        ),
    )
    print(table1[0]['cnt'])
```

Как правило, можно обойтись основным модулем `maps.analyzer.pylibs.yql` и несколькими функциями оттуда: `run_query`, `wait_results`, `get_query`, `create_params`.

`run_query`:
  * `query` — текст запроса, строка; можно воспользоваться `get_query` для загрузки из ресурса
  * `host` — хост, м.б. как в кратком виде `hahn`/`banach`, так и в полном: `hahn.yt.yandex.net`/`banach.yt.yandex.net`
  * `token` — YQL-токен, если не указан, то используется значение по умолчанию:
        - переменная окружения `ALZ_API_YQL_TOKEN`
        - содержимое файла `~/.yql/token`
  * `params` — параметры запроса, создаются функцией `create_params`, где каждый keyword-аргумент - параметр
  * `wait` — ожидать ли завершения запроса; если нет, то вернётся request-объект, на котором можно дождаться результатов функцией `wait_results`
  * `as_list` — вернуть строки таблицы как списки, а не как словари (в словаре ключи — имена колонок)
  * `no_raise` — не кидать исключение в случае ошибки выполнения запроса

Описание
===

Все функции представляют собой тонкие обёртки над стандартной библиотекой YQL и во многих местах возвращают/принимают в качестве аргументов те же объекты. Но это знание для использования не нужно.<br>
Модули:
  * [query](query.py) — easy-to-use фунцкии для разового выполнения запроса.
  * [client](client.py) — создание клиента. YQL-токен по умолчанию берётся из `~/.yql/token`, либо может быть указан явно. В качестве хоста можно указать как базу (`hahn`), так и URL (`hahn.yt.yandex.net`), это сделано для того, чтобы можно было передать туда `ytc.config['proxy']['url']`.
  * [request](request.py) — создание/выполнение/ожидание запроса. При выполнении можно указать параметры запроса.
  * [params](params.py) — создание параметров для запроса.
  * [results](results.py) — получение результатов выполнения. Возвращается список с данными для каждой результирующей таблицы, где в качестве записей таблицы может быть как список (значения колонок), так и словарь (имя колонки => значение соответствующей колонки)

В [example](example) лежит собираемый пример использования, считающий медиану, минимум и максимум для последовательности чисел. Его также можно запустить с `Y_PYTHON_ENTRY_POINT=:repl`, чтобы получить `IPython` с подгруженной библиотекой, и позапускать что-нибудь.
