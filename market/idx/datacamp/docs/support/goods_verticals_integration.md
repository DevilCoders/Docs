## Траблшутинг интеграции ЕОХ с Товарными Вертикалями

## Схема интеграции

Подробная схема находится здесь [https://st.yandex-team.ru/MARKETTECH-1957#60f3545f7576672e3746e1f6](https://st.yandex-team.ru/MARKETTECH-1957#60f3545f7576672e3746e1f6)

Товарные вертикали приносят в хранилище свои офферы + "заказывают" себе часть из тех чужих, что уже есть в ЕОХ. Для заказа чужого оффера на него проставляется флаг [vertical\_approved](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r8766613#L150). Конфигурация флагов поставляется через [таблицы на yt](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/etc/env/production.united?rev=r8799549#L214) и применяется [scanner-ом](../components/scanner.md).

Товарные вертикали имеют свой отдельный индексатор (turbo) и репорт. Необходимое (но не достаточное) условие попадания оффера в индекс: `vertical_approved(offer) && vertical_share(shop)`. Первый флаг хранится в оффере, второе - настройка магазина в `mbi` (допустимость появления на вертикальной выдаче), которую можно проверить в шопсдат или таблице информации о партнерах.

В контексте траблшутинга можно рассмотреть некоторую приближенную схему:

@startuml
cloud "Parser"
cloud "RTHub"
cloud "Miner"
cloud "Indexer"
cloud "Report"

(ecom-export snapshot) as ecom

database "DataCamp State" as DB

collections "Generation Input" as GenInp
note left
turbo_out
blue_turbo_out
end note


[Parser] --> [DB] : Feed offers
[RTHub] --> [DB] : WildWeb offers
[Miner] <-right-> [DB] : Enrich

[DB] --> [ecom] : ecom-export routine
[DB] --> [GenInp] : dumper routine

[GenInp] --> [Indexer]
[Indexer] --> [Report]
[DB] --> [Report] : Fast pipelines (prices, hidings)
@enduml

## Дебаг на стадии Источник => ЕОХ

Первая половина расследования заключается в том, чтобы понять, доехали ли данные до стейта Офферного Хранилища. Сделать это можно двумя способами:
* [YQL](https://yql.yandex-team.ru/Operations/YYKS_9jKS7TyWeLiHUnsPz3FnxOCDEW5wBjPSetRcx8=)
* [http-ручка](../components/stroller-api.md#list-offers-with-filters) (если вам нужен один оффер, пользуйте ручку - будет быстрее)

Если нужных данных в стейте нет, в соответствии с картинкой выше, надо смотреть приходил ли такой апдейт в хранилище:
* [логфеллер топика от rthub-а](https://yt.yandex-team.ru/arnold/navigation?path=//logs/rthub-datacamp-offers-log)
* [раз](https://yt.yandex-team.ru/arnold/navigation?path=//logs/market-united-datacamp-qoffers-direct-log), [два](https://yt.yandex-team.ru/arnold/navigation?path=//logs/market-united-datacamp-qoffers-log), [три](https://yt.yandex-team.ru/arnold/navigation?path=//logs/market-datacamp-qoffers-log) логфеллера топика от парсера. первый для директовых и чисто-ТВ фидов, оставшиеся два - для маркетных

Если оффер по каким-то причинам не приехал из парсера, стоит посмотреть логи парсинга в [фид-архиве](http://idxapi.vs.market.yandex.net:29334/v1/feed_archives/get?shop_id=1207490). Нужен один из трех cgi-параметров: `feed_id=...`(история парсинга конкретного фида), или `shop_id=...`(все фиды шопа), или `business_id=...`(фиды бизнеса).

Если же нужные измения есть в стейте, они могли не успеть доехать на вход индексатору / до экспортных ecom-выгрузок. Понять это поможет соотнесение таймстемпа ну нужном поле во внутреннем стейте и названия таблички со снапшотом (например `20211111_1200`).

## Дебаг на стадии ЕОХ => Индексатор
Если оффер не попал в индекс или попал, но у него не хватает какого-то важного поля, то стоит проверить следующие места:
* Найти его в [выгрузках для индексатора](../model/tables.md#datacamp-out)
* Поискать в выхлопе компоненты индексатора под названием full-maker [YQL](https://yql.yandex-team.ru/Operations/YYKWKQVK8IhSIAsOIYt_Zg5JYXUKKD9BNcE5lg22LDo=)
* Поискать в генлогах (логах поколения) [YQL](https://yql.yandex-team.ru/Operations/YYKWb65OD9giQvvTz0Tg4_TfIjRpO_SPtkPA_ycjduw=)

Что делать дальше:
* Если ожидания расходятся с реальностью на стадии 1, скорее всего вам надо смотреть на канал поставки данных в ЕОХ (грепать логфеллер)
* Возможно, что каких-то данных на оффере не хватает из-за того, что он еще не поучаствовал в процессе майнинга (стоит обратить внимание на `tech_info` - там записано время последнего майнинга)
* Сам факт майнинга не обязательно значит, что оффер попадет в индекс. Как правило, если майнер нашел какие-то ошибки, он заполняет поле [resolution](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/DataCampOffer.proto?rev=r8780389#L73) у оффера. Пояснения к кодам ошибок можно найти в [этом README](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/feeds/README.md#2-feedparser-error-codes).
* Если проблемы между первой и второй стадией, надо читать код [dumper-а](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/tasks/dumper/dumper.cpp?rev=r8795792#L986) (регулярная джоба, собирающая выгрузки для индексатора)
* Если проблема после запуска full-maker, стоит поискать конкретные mr-операции от имени робота и посмотреть их stderr (в его логах мало информации, но иногда там бывает полезное)
* Если оффер отсутствует в генлогах (т.е. и правда не попал в поколение), причина его отсутствия может быть указана в [process-log](//home/market/production/indexer/turbo.stratocaster/mi3/main/last_complete/process_log)
