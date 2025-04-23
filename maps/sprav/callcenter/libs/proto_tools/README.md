Позволяет парсить `pqxx::result`, `pqxx::row` в протобуф и обратно.
Что умеет:
 * json, бинарные протобуфы, бинарные протобуфы пожатые snappy <-> вложенные протобуфы ('message_format').
 * для колонок в которых могут лежать разные типы данных маппинг в oneof (надо явно указывать тип данных в отдельной колонке и через опцию 'type_column')
 * строки и числовые типы <-> enum ('enum_format')
 * timestamp without time zone <-> числовые типы ('timestamp_format', для парсинга в результате select'а должен получаться unix-таймстемп в секундах: extract(epoch from ..), см 'util.cpp')
 * array <-> repeated

## Пример
Опишем таблицу протобафом:
```protobuf
message TableRow {
    message TestMessage {
        optional string inner_string = 1;
        optional int64 inner_int = 2;
    };

    message TestMessage2 {
        optional double inner_double = 1;
    };

    enum TestEnum {
        FIRST = 0;
        SECOND = 1;
    };

    optional int64 int_field = 1;
    optional string string_field = 2;
    optional TestEnum enum_int_field = 3 [(enum_format) = INT];
    optional TestEnum enum_string_field = 4 [(enum_format) = STRING];
    optional double timestamp_field = 5 [(timestamp_format) = SECONDS];
    repeated string repeated_string_field = 6;
    optional TestMessage message_json_field = 7 [(message_format) = JSON];
    optional TestMessage message_proto_field = 8 [(message_format) = PROTOBUF];

    oneof oneof_field {
        option (type_column) = "oneof_type_field";

        TestMessage oneof_first = 10 [(message_format) = PROTOBUF];
        TestMessage2 oneof_second = 11 [(message_format) = PROTOBUF];
    };
};
```

Теперь чтобы распарсить табличку нам достаточно написать:
```cpp
    pqxx::result result;
    std::vector<TableRow> parsedResult = parseQueryResult<Table>(result);
```

Или, если мы ожидаем не более одной строки в результате:
```cpp
    pqxx::result result;
    std::optional<TableRow> parsedResult = parseSingleQueryResult<Table>(result);
```

Или чтобы создать запрос для записи данных обратно:
```cpp
    maps::wiki::query_builder::InsertQuery query;
    TableRow data;
    formatModifyQuery(data, query);
```

Можно распарсить результат любого запроса, не обязательно чтения из таблички, при условии совпадения названий полей в результате запроса и в протобуфе.

```protobuf
message Point {
    optional int64 lat = 1;
    optional int64 lon = 2;
};
```

```cpp
    auto row = tx->exec1(
        "SELECT lat.value as lat, lon.value as lon "
        "FROM proto_test.lat JOIN proto_test.lon USING(id)"
    );
    auto point = parseRow<proto::Point>(row);
```
