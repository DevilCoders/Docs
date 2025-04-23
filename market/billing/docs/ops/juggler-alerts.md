# Juggler-проверки (и нотификации)

**Цель статьи:** упорядочить знания о проверках и нотификациях вообще и Маркет-Биллинговой специфике в частности.
Если совсем ничего не знаешь про Juggler, лучше почитать что-нибудь более нацеленное на новичков. TODO: полезные ссылки на этот случай.

## Цикл жизни проверок и нотификаций

### 1. Сырые события в Juggler

Могут поступать из Solomon, Sentry, Голована. Или джобы/таски/сервисы/программы могут отсылать события сами.

Искать и смотреть сырые события на вкладке `Raw events` в juggler-е: <https://juggler.yandex-team.ru/raw_events/>.
Координаты сырого события &mdash; `host` и `service`. Это могут быть на самом деле имена какого-то хоста и какого-то сервиса, а могут быть и произвольные строчки.

### 2. Настройки проверок в Juggler

Проверки = агрегатные проверки = агрегаты.

Искать и смотреть агрегаты на вкладке `Agregates`: <https://juggler.yandex-team.ru/aggregate_checks/>

Откуда могут появляться проверки:
* можно создать вручную (кнопка `Create check`)
* можно написать конфиг в маркетном конфигураторе, см. в ссылках Малек
* может создавать какая-нибудь джоба

Про настойки проверок см. документацию Juggler.

### 3. Нотификации

Нотификации можно настраивать:
* в параметрах агрегатной проверки &mdash; устаревший способ, не надо так делать
* создавать правила нотификаций (Notification rule) &mdash; хороший, рекомендуемый способ

Смотреть правила нотфикаций на соответствующей вкладке Juggler: <https://juggler.yandex-team.ru/notification_rules>

Создавать правила нотификаций вручную в интерфейсе Juggler.


### 4. Дашборды

В Juggler можно делать дашборды. Ссылки на доку и на главный дашборд Биллинга Маркета см. в ссылках.


## Полезные ссылки

* Документация Juggler, раздел про агрегаты: <https://docs.yandex-team.ru/juggler/aggregates/basics>
* Маркетный конфигурато алертов ("Малек"), здесь подробное README: <https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/market-alerts-configs>
* Неймспейс Биллинга Маркета в Juggler: `market.mbi_money`, <https://juggler.yandex-team.ru/namespaces/?query=namespace=market.mbi_money>
* Конфиги juggler-проверок Биллинга Маркета
  * <https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/market-alerts-configs/configs/market_mbi_billing.yaml>
  * <https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/market-alerts-configs/configs/market-billing.yaml>
  * Тарифница?
* Дашборд с проверками Биллинга Маркета: <https://juggler.yandex-team.ru/dashboards/market-billing/>
* Документация Juggler, раздел про дашборды: <https://docs.yandex-team.ru/juggler/dashboards/overview>
* Звонящие проверки Биллинга Маркета: <https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dmarket-billing-phone>
* Важные правила нотификаций Биллинга Маркета:
  * Звонки: <https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5e6f89752c7c4400763aeff8>
  * Tg для звонящих проверок: <https://juggler.yandex-team.ru/notification_rules/?query=rule_id=610bf5c55c233bfc5b199908>
* Код про проверки
  * <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/model/MonitorItems.java>
  * <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/AggregateGroupsCreationExecutor.java>
  * <https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/monitor/JobsAggregateCreationExecutor.java>
