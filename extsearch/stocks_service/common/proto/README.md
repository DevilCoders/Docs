# Обновление схемы дин.таблиц YT

```bash
export ARCADIA_PATH=~/arcadia
for cluster in ("hahn" "arnold"); do
    for table in ("daily_candles" "hourly_candles"); do
        ya yql proto_field -c $cluster -t "//home/search-verticals/stocks_service/${table}" -p extsearch/stocks_service/common/proto/candle.proto -m TCandle -n data --arcadia-path $ARCADIA_PATH
    done
done
```
