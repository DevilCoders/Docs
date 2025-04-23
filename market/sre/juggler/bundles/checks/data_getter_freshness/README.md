## data_getter_freshness
Проверки свежести ресурсов от облачного data-getter в контейнерах RTC. 

### Как настроить
1. Включаем генерацию `meta.json` для ресурсов геттера. За это отвечает `create_meta_file` в параметрах запуска `RUN_MARKET_DATA_GETTER`, [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/sandbox-data-getter/datacamp-controllers.yaml?rev=r9501986#L15).
2. Проверяем, что бинарник добавлен в juggler-bundle вашего сервиса
3. Создаем алерт в мальке, [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/market-alerts-configs/configs/datacamp/market.rtc.datacamp-piper.yaml?rev=r9507720#L81-91)
