## Где найти сервис
[тест и продакшен](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_sberlogtms/)

## Мониторинг
[Production](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dsberlogtms-production)<br>
**checkstalleduser** - [таска по обходу беков](https://a.yandex-team.ru/arc/trunk/arcadia/market/sberlog_tms/src/main/java/ru/yandex/market/sberlog_tms/scheduled/MigrateMarketidToPuidScheduled.java) по какой-то причине таска не выполнилась, например какой-то бекенд отдаёт не 200 и таска не может завершиться. Смотреть логи sberlog_tms и искать сломанный бекенд. Мониторинг можно погасить, если сходить в продовую базу и в табличке marketid_links для данного uid проставить 1 в islinked<br>
**checkrefreshreporttime** - [таска по выгрузки всех пользователей из базы в YT](https://a.yandex-team.ru/arc/trunk/arcadia/market/sberlog_tms/src/main/java/ru/yandex/market/sberlog_tms/scheduled/UploadUserToYtScheduled.java) данные выгружаются в markov(путь смотри ниже) и если данные давно не обновлялись загорится этот мониторинг, надо смотреть логи, искать почему не происходит выгрузка

## Сборка
[TSUM](https://tsum.yandex-team.ru/pipe/projects/sre/delivery-dashboard/sberlogtms)

## Документация
[Диаграмма связывания](https://wiki.yandex-team.ru/market/sberbank/sberbank-id-/sklejjka/arxitektura/diagramma-svjazyvanija-/)

[Общая архитектура](https://wiki.yandex-team.ru/Market/Sberbank/Sberbank-ID-/Arxitektura/Paritet/)

## YT
# Локальный YT
https://wiki.yandex-team.ru/yt/userdoc/localmode/
https://sandbox.yandex-team.ru/resources?type=YT_LOCAL

# locke
Для блокировки берётся лок через кипарис, сам лок можно найти [тут](https://yt.yandex-team.ru/locke/navigation?path=//home/market_sre/sberlog_tms)
далее по средам (testing|production)

# markov
Данные хранятся [тут](https://yt.yandex-team.ru/markov/navigation?path=//home/market)
далее по средам (testing|production)/sberlog

## TVM id
https://wiki.yandex-team.ru/Market/Sberbank/Sberbank-ID-/Arxitektura/Paritet/#apiv1
```
дев. стенд: https://sberlog-dev.tst.vs.market.yandex.net (tvm id 2011276)
тестовый стенд: https://sberlog.tst.vs.market.yandex.net (tvm id 2011264)
продакшен: https://sberlog.vs.market.yandex.net (tvm id 2011654)
```
