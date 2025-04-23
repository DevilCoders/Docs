# Описание
Создает и монтирует дин. таблицы для данных свечек для `stock_service`


# Использование
1. `create_dyn_tables --config ./config.json`
1. создать `_yql_proto_field_data` аттрибуты как указано в [доке](https://yql.yandex-team.ru/docs/yt/misc/schema#_yql_proto_field)
    ```bash
    export ARCADIA_PATH=~/arcadia
    for cluster in ("hahn" "arnold"); do
        for table in ("daily_candles" "candles"); do
            ya yql proto_field -c $cluster -t "//home/search-verticals/stocks_service/${table}" -p extsearch/stocks_service/common/proto/candle.proto -m TCandle -n data --arcadia-path $ARCADIA_PATH
        done
    done
    ```
    т.к. конфиг протобафный можно генерить только тулой или из C++ этой [штукой](https://a.yandex-team.ru/svn/trunk/arcadia/library/cpp/protobuf/yql)
