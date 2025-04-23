# Аркадийные py-модули для yql-запроса

Собрать и подключить в запросе:
```
PRAGMA File('word_utils.so', 'https://proxy.sandbox.yandex-team.ru/731608850');
PRAGMA udf('word_utils.so');
```

Импорты в python-udf:
```python
import clemmer
import _hiliter
import advq.generation.common.queries
```

Пример python-udf можно посмотреть в example_udf.py.
Подключение udf в запросе:
```
$criteria_num_words = CustomPython::criteria_num_words(
    "(Utf8)->Uint8?",
    FileContent("example_udf.py")
);
$query_num_words = CustomPython::query_num_words(
    "(Utf8, Utf8)->Uint8?",
    FileContent("example_udf.py")
);
$get_hl_nhl = CustomPython::get_hl_nhl(
-- (criteria, query, snippet)
    @@(Utf8, Utf8, Utf8) -> 
        Struct<
          criteria:Utf8,
          query:Utf8,
          snippet:Utf8,
          hl:List<Utf8>?,
          nhl:List<Utf8>?
        >@@,
    FileContent("example_udf.py")
);
```

blinkov@: "Если не хочется свою so'шку постоянно с собой таскать, то можно добавить PEERDIR вот сюда https://a.yandex-team.ru/arc/trunk/arcadia/yql/udfs/common/python/python_arc/ya.make и после очередного релиза YQL оно станет доступно в ArcPython::"
