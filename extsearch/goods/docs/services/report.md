# Репорт

В тестинг через граф поход
[Дашборд](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/goods-report) для наших репортов.

Сервисы:

{% list tabs %}

- Main
  - Тестинг: [sas](https://nanny.yandex-team.ru/ui/#/services/catalog/test_report_goods_warehouse_sas) [man](https://nanny.yandex-team.ru/ui/#/services/catalog/test_report_goods_warehouse_man) [vla](https://nanny.yandex-team.ru/ui/#/services/catalog/test_report_goods_warehouse_vla) (сейчас работает только vla)
  - Престейбл: [sas](https://nanny.yandex-team.ru/ui/#/services/catalog/prep_report_goods_warehouse_sas) [man](https://nanny.yandex-team.ru/ui/#/services/catalog/prep_report_goods_warehouse_man) [vla](https://nanny.yandex-team.ru/ui/#/services/catalog/prep_report_goods_warehouse_vla)
  - Прод: [sas](https://nanny.yandex-team.ru/ui/#/services/catalog/prod_report_goods_warehouse_sas) [man](https://nanny.yandex-team.ru/ui/#/services/catalog/prod_report_goods_warehouse_man) [vla](https://nanny.yandex-team.ru/ui/#/services/catalog/prod_report_goods_warehouse_vla)

- Parallel
  - Тестинг: [sas](https://nanny.yandex-team.ru/ui/#/services/catalog/test_report_goods_parallel_sas) [man](https://nanny.yandex-team.ru/ui/#/services/catalog/test_report_goods_parallel_man) [vla](https://nanny.yandex-team.ru/ui/#/services/catalog/test_report_goods_parallel_vla)
  - Престейбл: [sas](https://nanny.yandex-team.ru/ui/#/services/catalog/prep_report_goods_parallel_sas) [man](https://nanny.yandex-team.ru/ui/#/services/catalog/prep_report_goods_parallel_man) [vla](https://nanny.yandex-team.ru/ui/#/services/catalog/prep_report_goods_parallel_vla)
  - Прод: [sas](https://nanny.yandex-team.ru/ui/#/services/catalog/prod_report_goods_parallel_sas) [man](https://nanny.yandex-team.ru/ui/#/services/catalog/prod_report_goods_parallel_man) [vla](https://nanny.yandex-team.ru/ui/#/services/catalog/prod_report_goods_parallel_vla)

{% endlist %}

В няне напрямую бинарь и другие ресурсы не найти (кроме архива моделек). Нужно идти на машинку и выкачивать с неё.

В тестинг можно сходить или напрямую в курлом, или через srcrwr. Пример: [https://yandex.ru/products/search/?text=телефон&srcrwr=MARKET_REPORT_PROXY:vla3-2401-f97-vla-market-prep--216-17050.gencfg-c.yandex.net:17060](https://yandex.ru/products/search/?text=телефон&srcrwr=MARKET_REPORT_PROXY:vla3-2401-f97-vla-market-prep--216-17050.gencfg-c.yandex.net:17060)

Аппхост ходит в репорт через балансер. В престейбл ходят запросы как с хамстера (hamster.yandex.ru/products?...), так и с прода (скорее баг, чем фича). В prod сервисы только из прода (через балансер http://goods-warehouse-report.vs.market.yandex.net/yandsearch?) 

Конфиг репорта генерится [скриптом](https://a.yandex-team.ru/arc/trunk/arcadia/market/report/runtime_cloud/report_config/market_report.py)

### Как достать запрос
[https://yandex.ru/products?text=велокуртка+зеленая&json_dump_requests=MARKET_REPORT_PROXY](https://yandex.ru/products?text=велокуртка+зеленая&json_dump_requests=MARKET_REPORT_PROXY)
[https://yandex.ru/products?text=котики&json_dump_requests=MARKET_REPORT_PROXY&debug=da#MARKET_REPORT_PROXY/requests/0/decoded_protobuf](https://yandex.ru/products?text=котики&json_dump_requests=MARKET_REPORT_PROXY&debug=da#MARKET_REPORT_PROXY/requests/0/decoded_protobuf)

Полученным запросом можно стрельнуть или в балансер, или напрямую в машинку в 17051 порт.
