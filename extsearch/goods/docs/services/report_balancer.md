# Балансер репорта

Main:
  - Прод [goods-warehouse-report.vs.market.yandex.net](goods-warehouse-report.vs.market.yandex.net)
  - Хамстер [goods-warehouse-report.pre.vs.market.yandex.net](goods-warehouse-report.pre.vs.market.yandex.net)
  - Тестинг [goods-warehouse-report.tst.vs.market.yandex.net](goods-warehouse-report.tst.vs.market.yandex.net)

Parallel: [goods-parallel-report.vs.market.yandex.net](goods-parallel-report.vs.market.yandex.net)

Конфиги балансеров лежат в аркадии. Например, конфиг [прода](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/slb-haproxy/prod/etc/haproxy/values-available/38395-goods_warehouse_report.market_slb-report-stable.yaml?rev=8952369). Остальные по поиску можно найти (по названию файла).

Чтобы поменять что-то в балансере проще всего завести тикет в очередь [CSADMIN](https://st.yandex-team.ru/CSADMIN). Можно и руками поменять конфиг, подождать какое-то время, пока он раскатится (хз как смотреть статус). И потом пойти в чат [CSADMIN-HOTLINE](https://telegram.me/joinchat/ByTNYD79mq1FOGJkLYsq5A) и попросить дежурного перезапустить нужный балансер.
