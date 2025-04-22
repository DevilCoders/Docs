# Stock restore

Приложение восстанавливает сток за интервал дат, применяя записанные в аудит изменения стоков к (корректным) стокам за определенную предшествующую дату.

## Как запустить

Для запуска надо собрать приложение через `ya make`.
Приложение запускается скриптом `stock-restore.sh`.
При запуске без аргументов выводится справка.

Минимальный набор параметров для расчета в кластере YT "Hahn":
* `--trusted-stock-directory` — папка, в которой хранится корректный сток;
* `--restored-stock-directory` — папка, в которой будет выполняться расчет;
* дата, на которую сток считаем корректным
* дата, на которую сток надо рассчитать

### Пример

```
./stock-restore.sh \
    --trusted-stock-directory=//home/market/production/mstat/dwh/staging/stock_sku \
    --restored-stock-directory=//home/market/production/wms/stockstorage/recalculated \
    2030-01-01 \
    2030-01-02
```

## Общее описание схемы работы

При запуске утилита выполняет обработку в YT в три фазы:

1. загрузка (если необходимо) корректного стока в кластер, где будет выполняться расчет;
1. загрузка событий аудита из ClickHouse в YT;
1. запуск map-reduce задачи, которая упорядочит по дате поток событий из двух предыдущих пунктов и сформирует сток на целевую дату.

### Восстановления стока по данным аудита и корректному (исходному) стоку

Для расчета стока по заданной SKU на дату X, берется запись по данной SKU в исходном стоке на дату Y.
Затем к ней начинают "применяться" изменения стока из аудита в порядке их создания (колонка `updated_at`).
Так как в аудите пишется только новое значение стока, то применение изменений в порядке их создания важно.

Хотя в записи восстановленного стока будут присутствовать все колонки исходного стока, обновляться из аудита будут только следующие значения:
 * fit
 * freezed
 * defect
 * defect_freezed
 * expired
 * expired_freezed
 * quarantine
 * quarantine_freezed
 * surplus
 * surplus_freezed
 * updated_at

На практике изредка возникает ситуация, при которой по заданной SKU приходит несколько обновлений стока в одну миллисекунду. В такой ситуации установить исходный порядок изменений невозможно, поэтому восстановленный сток может отличаться от фактического.

[Пример обработки](docs/processing_example.md)

## Восстановление работы при ошибках

Приложение по возможности восстанавливает прогресс при перезапуске.
Это полезно на этапе загрузки событий аудита, так как сервер отдает события очень нестабильно и часто это приводит к зависанию потоков, загружающих данные из ClickHouse.
Помогает только рестарт приложения.

## Просмотр расхождений между исходным и восстановленным стоком

Для просмотра различий между исходными значениями стока и его восстановленной версией, можно использовать этот запрос в YQL:

```sql
USE hahn;

SELECT
    r.sku_id AS sku_id,
    o.updated_at AS `updated_at (dwh)`,
    r.updated_at AS `updated_at (restored)`,
    o.fit AS `fit (dwh)`,
    r.fit AS `fit (restored)`,
    o.freezed AS `freezed (dwh)`,
    r.freezed AS `freezed (restored)`,
    o.surplus AS `surplus (dwh)`,
    r.surplus AS `surplus (restored)`,
    o.surplus_freezed AS `surplus_freezed (dwh)`,
    r.surplus_freezed AS `surplus_freezed (restored)`,
    o.quarantine AS `quarantine (dwh)`,
    r.quarantine AS `quarantine (restored)`,
    o.quarantine_freezed AS `quarantine_freezed (dwh)`,
    r.quarantine_freezed AS `quarantine_freezed (restored)`,
    o.expired AS `expired (dwh)`,
    r.expired AS `expired (restored)`,
    o.expired_freezed AS `expired_freezed (dwh)`,
    r.expired_freezed AS `expired_freezed (restored)`,
    o.defect AS `defect (dwh)`,
    r.defect AS `defect (restored)`,
    o.defect_freezed AS `defect_freezed (dwh)`,
    r.defect_freezed AS `defect_freezed (restored)`
FROM `//home/market/production/mstat/dwh/staging/stock_sku/<исходный сток>` AS o
FULL OUTER JOIN `//home/market/production/wms/stockstorage/recalculated/<восстановленный сток>` AS r ON
    r.sku_id = o.sku_id
WHERE 1 = 1
    --AND r.updated_at <= '2022-05-29 23:00:00'
    AND (
        r.fit != o.fit
        OR r.surplus_freezed != o.surplus_freezed
        OR r.surplus != o.surplus
        OR r.quarantine_freezed != o.quarantine_freezed
        OR r.quarantine != o.quarantine
        OR r.freezed != o.freezed
        OR r.expired_freezed != o.expired_freezed
        OR r.expired != o.expired
        OR r.defect_freezed != o.defect_freezed
        OR r.defect != o.defect
    );
```

К запросу можно добавить отсечку стока, по которому были обновления после 23 часов заданных суток.
С очень большой вероятностью по нему будет расхождение, так как выгрузка исходных стоков из StockStorage начинается ранее конца суток и может не "захватить" изменения, которые поступили после ее начала.
Обычно данные расхождения начинают быстро расти с 23 часов, но они могут возникать и при более ранних обновлениях, хотя их и будет меньше.

Дополнительно просмотреть данные аудита по заданной SKU можно в YQL этим запросом.
Диапазон дат лучше расширить на 1 день относительно того, за который восстанавливался сток.
```sql
USE marketclickhouse;

SELECT toDateTime(event_timestamp / 1000), event_timestamp, *
FROM market.stock_storage_stock_events
WHERE target_id = '<sku_id>'
AND date BETWEEN '2022-05-28' AND '2022-05-30'
ORDER BY timestamp DESC;
```
