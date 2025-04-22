# Биллинг хранения

## Предметная область

Поставщики поставляют товары на склады, где они хранятся до момента покупки.
Часть из этих складов принадлежит Маркету, а часть - партнерские. За хранение товаров на наших складах мы берем у поставщиков деньги.


## Сущности

*Поставщик* - тип партнера; в данном контексте это тот, кто поставил товар на склад (`supplier_id`).

*Товар* - уникальный товар конкретного поставщика (`supplier_id + shop_sku`, где `shop_sku` - это строковый идентификатор товара на стороне поставщика).
Одна и та же шариковая ручка "Brauberg I-Stick" от двух разных поставщиков - это два разных товара.

*Весогабаритные характеристики (ВГХ)* - длина, ширина, высота и масса товара (`supplier_id + shop_sku`, см. "товар").

*Поставка* - поставка товаров на склад (`request_id`). Одна поставка в общем случае содержит несколько товаров от разных поставщиков.

*Сток* - остаток товара на складе (`warehouse_id + supplier_id + shop_sku + date`).
Единицы одного и того же товара могут находиться на складе в разном статусе.
Например, шариковая ручка "Brauberg I-Stick" от поставщика "Рога и копыта" может лежать на складе в Санкт-Петербурге в количествах: 5 доступно для продажи, 1 бракована.


## Импорты { #imports }

### Типы партнеров { #imports_partner-types }

Источник:
- подневные таблицы с типами партнеров: [hahn.//home/market/production/mstat/dictionaries/partner_types](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/market/production/mstat/dictionaries/partner_types)
  - `id` - id поставщика (`supplier_id`)
  - `type` - тип партнера, нам интересен `SUPPLIER` ("поставщик")

Типы партнеров не импортируются, но используются для фильтрации при импорте стоков и ВГХ в YQL-запросах.


### Остатки товаров на складах (стоки) { #imports_stocks }

Источники:
- подневные снепшоты остатков на складах: [hahn.//home/market/production/mstat/dwh/staging/stock_sku](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/market/production/mstat/dwh/staging/stock_sku)
  - `warehouse_id` - id склада (строка описывает остатки на конкретном складе)
  - `supplier_id` - id поставщика
  - `shop_sku` - id товара в контексте поставщика
  - `fit` - количество товара, котовое к продаже (используется для биллинга)
  - `expired` - количество просроченных товаров (используется для биллинга)
  - `defect` - количество бракованных товаров (используется для биллинга)
  - `quarantine` - потерянное/перемещенное количество
  - `freezed` - заморожено на время заказа
  - `lifetime` - срок годности в днях
- типы партнеров (см. [Типы партнеров](#imports_partner-types)).

Целевая таблица в Postgres: [shops_web.stocks_new](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/db/src/liquibase/shops_web/stocks_new.sql).

Джоба: [DailyImportStocksExecutor](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/stocks/DailyImportStocksExecutor.java).

В исходной таблице отражаются остатки на складах на какой-то момент времени в рамках соответствующей даты. Обычно это примерно конец суток.
Для корректности взаиморасчетов важно, чтобы это условие соблюдалось. Если в табличке за дату X будет отражено состояние за дату X - 1 ли X + 1,
то мы можем неправильно посчитать, сколько денег нам должен партнер.

Джоба импортирует только те записи, у которых тип партнера - "поставщик" и есть положительный биллимый остаток (`fit + defect + expired > 0`).


### Весогабаритные характеристики (ВГХ) { #imports_stock_sku_infos }

Источники:
- подневные снепшоты актуального состояния ВГХ из MDM: [hahn.//home/market/production/mdm/dictionaries/reference_item/1d](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/market/production/mdm/dictionaries/reference_item/1d)
  - `supplier_id` - id поставщика
  - `shop_sku` - id товара в контексте поставщика
  - `complete_item` - yson-поле с данными о товаре, в том числе ВГХ
- типы партнеров (см. [Типы партнеров](#imports_partner-types)).

Целевая таблица в Postgres: [shops_web.shop_sku_info](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/db/src/liquibase/shops_web/shop_sku_info.sql).

Джоба: [DailyImportShopSkuInfoExecutor](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/stocks/DailyImportShopSkuInfoExecutor.java).

Джоба импортирует только те записи, у которых тип партнера - "поставщик" и для которых удалось извлечь необходимые данные из `complete_item`.

Особенность данного импорта состоит в том, что в нашей базе хранятся характеристики без привязки к дате, только их актуальное состояние.
Однако, при этом мы импортируем не последний доступный день (`/latest`), а каждый день по порядку, явно подставляя дату.

Весогабаритные характеристики могут приходить как от партнера при поставке, так и замеряться непосредственно на нашем складе.
При этом, характеристики конкретных товаров могут изменяться со временем.</br>
Известные причины изменения характеристик:
- поставщик сам изменил характеристики
- перезамеры на нашем складе по регулярным проверкам качества
- некорректный замер на нашем складе (редко и решается в тикетах)

Для некоторых товаров могут отсутствовать ВГХ. Обычно таких немного (< 1%). Основная причина: поставка товаров без ВГХ.
В этом случае товар замеряется на складе, но у склада пропускная способность замеров ограничена.


### Поставки на склады { #imports_supplies }

Источник:
- актуальное состояние всех поставок за всю историю: [hahn.//home/market/production/mstat/dictionaries/fulfillment_shop_request/1d/latest](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/market/production/mstat/dictionaries/fulfillment_shop_request/1d/latest).
  - `id` (он же `request_id`) - уникальный id поставки
  - `type_name` - тип поставки
  - `status_name` - актуальный на момент формирования таблицы статус поставки
  - `created_at` - время создания поставки
  - `updated_at` - время изменения поставки (её состояние в таблице соответствует этому времени)

Целевая таблица в Postgres: [market_billing.fulfillment_supply](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/db/src/liquibase/market_billing/fulfillment_supply.sql).

Джоба: [DailyImportSupplyExecutor](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/supplies/DailyImportSupplyExecutor.java).

Джоба импортирует только записи с подходящими типами `type_name` и подходящими статусами `status_name`. Перед импортом джоба полностью очищает таблицу в Postgres.

Поставка в общем случае содержит несколько различных товаров от разных поставщиков.
 Данные о товарах в поставке (id поставщика, количество...), хранятся в другой таблице (см. [Товары в поставках](#imports_supply-items)).


### Товары в поставках { #imports_supply-items }

Источник:
- актуальное состояние товаров в поставках за всю историю: [hahn.//home/market/production/mstat/dictionaries/fulfillment_request_item/1d/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/fulfillment_request_item/1d/latest)
  - `request_id` - идентификатор поставки, к которой относится товар
  - `supplier_id` - id поставщика
  - `article` (он же `shop_sku`) - id товара в контексте поставщика
  - `name` - название товара на стороне поставщика
  - `count` - количество единиц товара в поставке
  - `fact_count` - количество единиц товара, которое приняли на склад (доступ)
- дополнительная информация о товарах из MBO: [hahn.//home/market/production/mstat/dictionaries/mbo/mboc_offers/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbo/mboc_offers/latest)
  - `supplier_id` - id поставщика
  - `shop_sku` - id товара в контексте поставщика
  - `category_id` - категория товара
- актуальное состояние всех поставок за всю историю (см. [Поставки на склады](#imports_supplies)).

Целевая таблица в Postgres: [market_billing.fulfillment_supply_item](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/db/src/liquibase/market_billing/fulfillment_supply_item.sql).

Джоба: [DailyImportSupplyExecutor](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/supplies/DailyImportSupplyExecutor.java).

Джоба импортирует только записи, которые относятся к поставкам с подходящими типами `type_name` и подходящими статусами `status_name`.
 Перед импортом джоба полностью очищает таблицу в Postgres.


## Биллинг (актуально с 1ого июня 2022года) { #new-billing }

Сам биллинг состоит из 2‑х вещей: [агрегация](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/StorageByCategoryAggregationExecutor.java) и [самого обиливания](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/StorageByCategoryBillingExecutor.java)

Суть биллинга - вычислить оборачиваемость (рассчитывается как среднесуточный объем товаров деленный на среднесуточный объем проданных товаров),
относительно оборачиваемости выбрать ставку и эту ставку помножить на сумматный объем стока в пределах отчетного периода (календарный месяц)

Среднесуточные данные агрегируются до департамента (категории, у которой родитель = 90401 (Все товары)).
Таким образом, если для `shopSku1` и `shopSku2` общим департаментом является `Departament1`, то эти 2 shopSku будут считаться вместе.

### Что такое агрегация данных и зачем она нужна
Агрегация нужна для того, чтобы биллинг каждый день не считал одно и тоже.
Если бы агрегации не было, то биллинг на день `X` расчитывал среднесуточные объемы за день `Х-1`. За день `X+1` надо было бы расчитать среднесуточные объемы на даты `Х` и `Х-1`.
Но чтобы 2 раза не считать объемы за дату `Х-1` - для этого и нужна агрегация.

**Агрегация** - один раз посчитали и используем эти значения.

### Как рассчитывается агрегация
Основной запрос [тут](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/stocks/StockDao.java?rev=r9641310#L96)

Запрос для переданного дня рассчитывает, какой был объем стока и какой был объем проданых товаров на определенный день.
Что он делает:
* Выбираем все стоки из **shops_web.stocks_new** за переданную дату (cte `skus`)
* На основе этих стоком, мы рассчитываем, какие `shop sku` надо биллить, а какие нет. (cte `skus_with_date_of_presence`)
    <p>Рассчитываем так: если shop_sku лежит больше 30 дней, то мы считаем, что эту shop sku надо биллить

   {% note alert %}

   Текущий расчет признака обиливаемости работает неправильно (не так как в оферте). Его надо поменять

   {% endnote %}

* Далее для каждой sku находим ее категорию (cte `skus_with_categoreis`) на основе данных по поставкам

   {% note alert %}

   **Проблема:** для поставки может не быть категории. В таком случае, если в этот день не было продаж,
    то мы не сможем вообще обилить данную shop sku, потому что мы не будем знать, к какому департаменту относится данная shop sku (см ниже объяснение)

   {% endnote %}

* Считаем на нужную дату объем стока по каждый shop_sku по каждому партнеру на каждую дату (cte `stock`)
    <p>Объем считаем в литрах. Объем = общее количество стока по конкретной `shop sku`, помноженного на объем одной `shop sku`.
    <p>Общее количество стока = `available + expired + defect`
    <p>Объем одной shop_sku в литрах = `max(length, 1) * max(width, 1) * max(height, 1) * * 0.001`

{% note info %}

`max` нам нужен, потому что мы импортируем к себе данные в **ЦЕЛЫХ** см, с округлением [вниз](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/imports/shopsku/DailyImportShopSkuInfoExecutor.java?rev=r9590551#L200).
<p> Таким образом, если, например, `length` в источниках будет равен 5мм (т.е. 0.5см), то мы импортируем это как 0
<p> И чтобы учитывать такие стоки правильно (они же занимают объем), то мы берем 1см.
<p> </p>Возможно, правильнее брать честную длину в мм, но это уже другая история.
<p> На 0.001 домножаем, потому что перемножение 3х измерений мы получаем **кубические см**, а **1 литр** = **1 кубическому дециметру**.
<p> В свою очередь **1 кубичесий дециметр = 1000 кубическим см**.

{% endnote %}

* Считаем проданный объем каждой shop sku на конкретную дату (cte `sold`)

    <p>Считаем по табличкам **cpa_order_status_history**, **cpa_order_item**
    <p>По истории понимаем, когда был доставлен заказ, а по **coi** понимаем, что за **shop sku** была продана

{% note info %}

Внимательный читатель запроса увидит интересную вещь:

`max(coi.cat_id)` - мы могли бы группировать по категории, а не брать max, но так не пройдет, потому что у одной и той же
`shop sku` для одного и того же партнера, заказ которой был в один и тот же день может иметь разные категории.

Пример: coi.id = 179368584 и 178522631

{% endnote %}

Так же считаем проданный объем для конкретной `shop sku`:
    <p> Общее количество * объем одной `shop sku`.
    <p> Общее количество = `coi.item_count`,
    <p> Объем = `max(mdm.length, checkouter.length, 1) * max(...) * 0.001`.
    <p> Мы сначала пытаемся взять длину(ширину/глубину) из mdm, если там нет - то берем из чекаутерных данных (менее правдивые)

{% note info %}

<p> Есть забавная shop_sku - москитная сетка для детского кресла (shop_sku = УТ000001268, partner = 977584)
<p> По данным из mdm там валидные данные (20см * 10см * 4см). А по данным чекаутера - сетка имеет размеры 100см * 100см * 100см с весом 1кг :)
<p> пример: coi.id = 173811495

Вывод: - доверять чекаутерным вгх не стоит

{% endnote %}

* На послднем этапе мы делаем full join 2х табличек: `stock` и `sold` по партнеру, shop_sku и дате,
и выбираем поля (проданный объем, объем на складе, признак обиливаемости, етц) через `coalesce`

    <p> Full join нужен затем, чтобы не пропустить ситуации, когда был сток и не было продаж (либо наоборот)
    <p> coalesce нужен по той же самой причине (если не было стока, то возьмем shop_sku из проданных товаров)
    <p> Именно поэтому в п3 мы не сможем обилить, если было stock с категорией null и не было продаж: `coalesce(null, null)` нам вернет null

* Ну и из всего этого мы явно фильтруем **беру 465852**

    <p>Полученную агрегацию сохраняем в табличку **market_billing.storage_by_category_volumes**, откуда данные подтянет биллинг

### Как работает биллинг

1. Для каждой даты в течение месяца забираются агрегированные данные по `partner_id + shop_sku + category_id`
2. Для каждой shop_sku мы получаем департамент (если возможно), и данные складываем в `Map<SupplierToDepartment, Boolean>` (в коде это [supplierDepartmentIsBillable](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/StorageByCategoryBillingService.java?rev=r9663134#L159))
<p>где ключом является `partner_id + departament`, а значением - признак обиливаемости (надо ли обиливать данный департамент для партнера или нет)
<p>Таким образом, у нас каждая shop sku попадает в общий ключ `SupplierToDepartment` с общим признаком обиливаемости (мы же биллим по департаменту)
3. Далее, если данный департамент нужно обилить, мы суммируем объем стока и объем продаж в данном департаменте на текущую дату,
собираем все в `Map<SupplierToDepartment, StockAndSoldVolumes>`(в коде это [volumesSum](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/StorageByCategoryBillingService.java?rev=r9663134#L148))
<p> где ключ = `partner_id + departament`, а значение = `stock_volume + sold_volume`
4. Затем, для каждого ключа мы рассчитываем `CalculationInfo` ([вот тут](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/StorageByCategoryBillingService.java?rev=r9663134#L197)).
<p> CalculationInfo хранит такие данные, как среднесуточный объем товаров на стоке, среднесуточный объем проданных товаров, оборачиваемость и тариф
<p> Эти данные собираем в `Map<SupplierToDepartment, CalculationInfo> departmentTariffs`
5. И только лишь затем, для каждого ключа из `departamentTariffs` мы рассчитываем, сколько поставщик нам должен за хранение = тариф * общий сток в литрах в пределах отчетного периода
6. Полученные значения сохраняем в **market_billing.storage_by_category_billing**
На этом биллинг на текущий день закончился.

### Как работает месячный биллинг
Все те же самые пункты 1-5 выше, только:
1. месячный биллинг работает 1 раз в месяц (1ого числа считаем предыдущий месяц)
2. данные складываем в табличку **market_billing.storage_by_category_monthly**, которые дальше уезжают в тлог

Таким образом
```sql
select *
from market_billing.storage_by_category_billing
where billing_date = last_day_of_month
```
это то же самое, что и
```sql
select *
from market_billing.storage_by_category_monthly
where billing_date = last_day_of_month
```

(за любые другие даты это не работает)

## Биллинг (актуально до 1 июня 2022года)

Джоба: [StorageBillingExecutor](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/billing/storage/StorageBillingExecutor.java).

Таблица с результатами биллинга в Postgres: [market_billing.storage_billing](https://a.yandex-team.ru/arc/trunk/arcadia/market/billing/db/src/liquibase/market_billing/storage_billing.sql).

За одну итерацию джоба работает с одной датой. За эту дату рассчитывает стоймость хранения каждого товара (`supplier_id` + `shop_sku`) за один день хранения.

Краткое описание алгоритма:
- Для каждого товара суммируются остатки на ограниченном списке складов, которые принадлежат Маркету (не партнерские).
- Для каждого товара рассчитывается период хранения, так как а) есть бесплатный период и б) он влияет на применяемый к тарифу коэффициент.
  1. поставки перебираются последовательно в порядке от самой свежей к наиболее давней
  2. рассчитывается сумма для того количества товара, которое было в очередной поставке, а срок хранения для этого количества товара рассчитывается как количество дней между датой поставки и текущей обилливаемой датой (не включительно)
  3. из общего числа остатка на складах вычитается обсчитанное на предыдущем шаге количество товара
  4. если осталось не обсчитанное количество товара, то переходим к следующей поставке (шаг 2), в противном случае завершаем расчет для данного товара и переходим к следующему

Данный алгоритм не учитывает следующий кейс. Проще всего его понять на примере:
- Обилливаем 1 ноября 2021 года.
- 1 августа 2021 года (3 месяца назад) товар X был поставлен на склад в Санкт-Петербург в количестве 1 штуки и до сих пор там хранится.
- 29 октября 2021 года (3 дня назад) этот же товар был поставлен на склад в Екатеринбург в количестве 1 штуки.
- 31 октября 2021 года (1 день назад) товар ушел со склада в Екатеринбурге покупателю.
- На текущую дату мы имеем остаток товара в количестве 1 штуки.
- При расчете срока хранения мы возьмем последнюю поставку в Екб, и срок будет равен 2 дням, хотя товар хранится в Спб уже 3 месяца.

