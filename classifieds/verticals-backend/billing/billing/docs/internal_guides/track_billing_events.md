## Отслеживание событий в биллинге

### Продукты auto.ru и realty_commercial, применяемые к офферу: размещения и васы (поднятие в поиске, спецпредложение, ...)

Пусть нужно отследить путь оплаты продукта placement, применённого 8 января 2022 к офферу с id = 1105781313-ba90c0d8, через биллинг.

1. В yt/event_to_pay размещения сейчас не пишутся, так что там найти размещение не получится.
2. Находим id события в таблице сырых событий в [базе vs_bill_storage](https://nda.ya.ru/t/MWSjfYBw4j6Prw) (здесь и далее можно селектить и другие поля, если нужно):
```sql
MySQL [vs_bill_storage]>
-- или realty_commercial_ru_offer_indexing для Недвижки
select id from autoru_ru_offer_indexing
where timestamp between '2022-01-08' and '2022-01-09'
-- или data_string->'$.offer_id' для Недвижки
and data_string->'$."service.payload.offerId"' = '1105781313-ba90c0d8'
and data_string->'$."billing.header.product.goods@0.custom.id"' = 'placement';
+----------------------------------+
| id                               |
+----------------------------------+
| e8fae888badee1e4f7c679105d3b0178 |
+----------------------------------+
1 row in set (1.212 sec)
```
NB: условие по timestamp нужно для поиска по индексу, а также для поиска конкретной оплаты. В целом, можно искать и без него.

<a name="get_transaction_id">
3. Находим id транзакции в таблице обилленных событий:
</a>

```sql
-- или realty_commercial_ru_offer_indexing_billed_event для Недвижки
MySQL [(none)]> select tr_id from autoru_ru_offer_indexing_billed_event where event_id = 'e8fae888badee1e4f7c679105d3b0178';
+------------------+
| tr_id            |
+------------------+
| 6488da0b03ee0e1d |
+------------------+
1 row in set (2.811 sec)
```
4. Находим транзакцию по id в базе [billing_autoru](https://nda.ya.ru/t/FB5Dv6B94j6PhJ) или [billing_realty_commercial](https://nda.ya.ru/t/UCTb-7U54j8kKd) (нет индекса по id, но для разового запроса ок):
```sql
MySQL [billing_autoru]> select id from order_transaction where id = '6488da0b03ee0e1d';
+------------------+
| id               |
+------------------+
| 6488da0b03ee0e1d |
+------------------+
1 row in set (19.138 sec)
```
5. Находим события в [yt/billing_operation_event](https://yql.yandex-team.ru/Operations/Yd0buNJwbNxvlkoYfQ_3eYxGwyOZNYKvsr1qJxxiamI=):
```sql
SELECT *
FROM hahn.`home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d/2022-01-08`
-- или REALTY_COMMERCIAL для Недвижки
WHERE domain = 'AUTORU'
AND withdraw_payload.raw_event.id = 'e8fae888badee1e4f7c679105d3b0178';
```
NB: нужно заменить prod на test для поиска событий в тестинге.

### Продукты auto.ru, покупаемые клиентом не к офферу: заявки на кредит, квоты, отчёты по VIN, ...

Пусть нужно отследить путь оплаты продукта quota:placement:cars:new, применённого 8 января 2022 клиентом с id = 45120 (на auto.ru), через биллинг.

1. Находим событие в [yt/event_to_pay](https://yql.yandex-team.ru/Operations/Yd1l5i3DcAOgZR1AgXQIWmC5ed77WICKO5PGTqTxH40=):
```sql
$GetValue = ($tuples, $key) -> {
    RETURN ListHead(ListFilter($tuples.`values`, ($tuple) -> { RETURN $tuple.key = $key; })).value;
};

SELECT *
FROM hahn.`home/verticals/broker/prod/warehouse/billing/event_to_pay/1d/2022-01-08`
WHERE $GetValue(`tuple`, 'billing.header.product.goods@0.custom.id') = 'quota:placement:moto'
AND   $GetValue(`tuple`, 'service.payload.serviceClientId') = '45120';
```
2. Находим id события в таблице сырых событий в [базе vs_bill_storage](https://nda.ya.ru/t/MWSjfYBw4j6Prw):
```sql
MySQL [vs_bill_storage]>
select id from autoru_ru_offer_indexing
where timestamp between '2022-01-08' and '2022-01-09'
and data_string->'$."service.payload.serviceClientId"' = '45120'
and data_string->'$."billing.header.product.goods@0.custom.id"' = 'quota:placement:moto';
+----------------------------------+
| id                               |
+----------------------------------+
| 7656fd2927afdd18bdc87267a0dd065c |
+----------------------------------+
1 row in set (1.202 sec)
```
3. Далее пункты 3, 4, 5 из гайда для продуктов, применяемых к офферу (см. [выше](#get_transaction_id)).

### Звонки

Пусть нужно отследить путь оплаты звонка с id = lrDpeP1vFUI, произошедшего 10 января 2022, через биллинг.

NB: если не знаем id звонка в телепони, но знаем id звонка в коллцентре, узнать id звонка в телепони можно так:
```sql
MySQL [(none)]> select id from callfact where call_center_call_id = 'TK-977244';
+-------------+
| id          |
+-------------+
| 0ApsXNj0q7U |
+-------------+
1 row in set (0.431 sec)
```

Запрос делается в базу сервиса ([billing_autoru](https://nda.ya.ru/t/FB5Dv6B94j6PhJ), [billing_realty](https://nda.ya.ru/t/eXp5YW4l4j8jv6) или [billing_realty_commercial](https://nda.ya.ru/t/UCTb-7U54j8kKd)).

1. Находим звонок в таблице callfact в базе сервиса ([billing_autoru](https://nda.ya.ru/t/FB5Dv6B94j6PhJ), [billing_realty](https://nda.ya.ru/t/eXp5YW4l4j8jv6) или [billing_realty_commercial](https://nda.ya.ru/t/UCTb-7U54j8kKd)):
```sql
MySQL [(none)]> select id from callfact where id = 'lrDpeP1vFUI';
+-------------+
| id          |
+-------------+
| lrDpeP1vFUI |
+-------------+
1 row in set (0.015 sec)
```
2. Находим id транзакции в таблице обилленных событий в [базе vs_bill_storage](https://nda.ya.ru/t/MWSjfYBw4j6Prw):
```sql
-- если надо, заменяем autoru на другой домен
MySQL [(none)]> select tr_id from autoru_ru_phone_show_billed_event where callfact_id = 'lrDpeP1vFUI';
+------------------+
| tr_id            |
+------------------+
| eac5763187b1bcf6 |
+------------------+
1 row in set (0.047 sec)
```
3. Находим транзакцию по id в базе сервиса (нет индекса по id, но для разового запроса ок):
```sql
MySQL [(none)]> select id from order_transaction where id = 'eac5763187b1bcf6';
+------------------+
| id               |
+------------------+
| eac5763187b1bcf6 |
+------------------+
1 row in set (19.139 sec)
```
4. Находим события в [yt/billing_operation_event](https://yql.yandex-team.ru/Operations/Yd2FPy3DcAOgZVR24m5hf-UEAPQ0AcUYFdg_LgTzpjY=):
```sql
-- если надо, заменяем AUTORU на другой домен
SELECT *
FROM hahn.`home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d/2022-01-10`
WHERE domain = 'AUTORU'
AND withdraw_payload.call_fact.call_fact.id = 'lrDpeP1vFUI';
```
