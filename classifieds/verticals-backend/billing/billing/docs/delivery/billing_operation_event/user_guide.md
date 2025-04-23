# Основное руководство пользователя для лога операций биллинга

## Предоставляемая информация
Текущая поставка предоставляет информацию:
1. О списаниях на стороне биллинга. По ней можно найти с кого, сколько и главное за что мы списали.
2. О перерасходах на стороне биллинга. Непосредственно события о перерасходе не поставляется, **НО** вычислить сумму перерасхода можно на основе [expected](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto#L441) и [actual](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto?rev=r9558371L442).
Перерасход возникает когда у пользователя недостаточно денег, чтобы оплатить оказанную услугу. Такая ситуация возникает из-за нескольких архитектурных особенностей: биллинг не быстро превращает события в транзакции и сервисы не могут хорошо прогнозировать траты клиентов.
В общем случае биллинг ничего не делает с перерасходами. Только при переобилливании в случае наличия достаточной суммы перерасход может быть уменьшен вплоть до нуля.
3. О пополнениях баланса на стороне биллинга. По ней можно найти кто, когда и на сколько пополнил баланс.
4. О коррекциях проведенных на стороне биллинга. По ней можно найти кто, когда, на какую сумму и по какой причине провел коррекцию.
5. О предоставленных скидках на стороне биллинга. По ней можно найти кто, когда, на какую сумму и по какой причине предоставил скидку.
6. О транзакции на стороне биллинга связанную с событием. [Информация в схеме](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto?rev=r9558371L431).
7. О состоянии заказа на стороне биллинга на момент создания события. [Информация в схеме](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto?rev=r9558371L430).

В схеме можно посмотреть информацию поставляемую вместе с [пополнениями](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto#L460), [списаниями](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto#L438), [коррекциями](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto#L456) и [скидками](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto?rev=r9558371L463).

Запросы которые часто используют можно посмотреть в [разделе с запросами](#примеры-запросов).

## Структура лога
Лог структурирован и имеет следующую [схему](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto?rev=r9558371L411).

## Поставки
Данные поставляются в yt и кафку. Гарантия at-least-once delivery распространяется на обе поставки.

[id](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto?rev=r9558371L426) является уникальным идентификатором операции.
Соответственно по этому полю нужно избавляться от дублей и находить актуальное состояние используя операцию с максимальным `timestamp`.

[Подробнее о поставках](./detailed_info.md#поставки)

### Поставка в кафку
Данные можно найти в топике `broker-billing-billing-raw-operation-event`

[Подробнее о поставке в кафку](./detailed_info.md#поставка-в-кафку)

### Поставка в yt
Данные можно найти в таблице [billing_operation_event](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d).

[Подробнее о поставке в yt](./detailed_info.md#поставка-в-yt).

## Партиционирование в yt
Партиционирование происходит по полю [operation_timestamp](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto?rev=r9558371L429).

[Подробнее о партиционировании в yt](./detailed_info.md#поставка-в-yt)

## Построение запросов в yt
Предлагается следующий подход для вычленения актуального состояния операции:
```sql
use hahn;

SELECT
    *
FROM (
    SELECT MAX_BY(TableRow(), `timestamp`)
    FROM RANGE('home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d', '2020-12-01', '2020-12-24')
    -- <тут место для своих фильтров>
    GROUP BY `id`
) FLATTEN COLUMNS;
```

## Примеры запросов
### Сумма списаний за определенный день в разрезе продуктов в домене AUTORU

<details>
<summary>Запрос</summary>
<p>

```sql
use hahn;

SELECT
    product_name,
    SUM(withdraw_payload.actual) as actual,
    SUM(withdraw_payload.expected) as expected,
    SUM(withdraw_payload.expected - withdraw_payload.actual) as overdraft
FROM (
    SELECT MAX_BY(TableRow(), `timestamp`)
    FROM `home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d/2020-12-24`
    WHERE domain = "AUTORU" AND withdraw_payload is not null
    GROUP BY `id`
) FLATTEN COLUMNS
GROUP BY withdraw_payload.product.name as product_name;
```

</p>
</details>

### Сумма списаний за звонки за определенный день в домене AUTORU
<details>
<summary>Запрос</summary>
<p>

```sql
use hahn;

SELECT
    SUM(withdraw_payload.actual) as actual,
    SUM(withdraw_payload.expected) as expected,
    SUM(withdraw_payload.expected - withdraw_payload.actual) as overdraft
FROM (
    SELECT MAX_BY(TableRow(), `timestamp`)
    FROM `home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d/2020-12-24`
    WHERE domain = "AUTORU" AND withdraw_payload.product.name = "call"
    GROUP BY `id`
) FLATTEN COLUMNS;
```

</p>
</details>

### Количество звонков за определенный день с разбивкой по статусам в домене AUTORU
<details>
<summary>Запрос</summary>
<p>

```sql
use hahn;

SELECT
    detailed_status,
    SUM(withdraw_payload.actual) as actual,
    SUM(withdraw_payload.expected) as expected,
    SUM(withdraw_payload.expected - withdraw_payload.actual) as overdraft
FROM (
    SELECT MAX_BY(TableRow(), `timestamp`)
    FROM `home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d/2020-12-24`
    WHERE domain = "AUTORU" AND withdraw_payload.product.name = "call"
    GROUP BY `id`
) FLATTEN COLUMNS
GROUP BY withdraw_payload.call_fact.detailed_status as detailed_status;
```

</p>
</details>

### Сумма транзакций в разрезе по типу в домене AUTORU
<details>
<summary>Запрос</summary>
<p>

```sql
use hahn;

SELECT
    tr_type,
    SUM(transaction_info.amount) as amount
FROM (
    SELECT MAX_BY(TableRow(), `timestamp`)
    FROM `home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d/2020-12-24`
    WHERE domain = "AUTORU"
    GROUP BY `id`
) FLATTEN COLUMNS
GROUP BY transaction_info.type as tr_type;
```

</p>
</details>

### Список списаний средств за услуги по конкретному офферу в домене AUTORU
<details>
<summary>Запрос</summary>
<p>

```sql
use hahn;

SELECT
    *
FROM (
    SELECT MAX_BY(TableRow(), `timestamp`)
    FROM `home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d/2020-12-24`
    WHERE domain = "AUTORU" and withdraw_payload.raw_event.offer_id = "cars-autoru-1050286016"
    GROUP BY `id`
) FLATTEN COLUMNS;
```

</p>
</details>

### Услуги за день по клиенту в домене AUTORU
<details>
<summary>Запрос</summary>
<p>

```sql
use hahn;

SELECT
    product_name,
    SUM(withdraw_payload.actual) as actual,
    SUM(withdraw_payload.expected) as expected,
    SUM(withdraw_payload.expected - withdraw_payload.actual) as overdraft
FROM (
    SELECT MAX_BY(TableRow(), `timestamp`)
    FROM `home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d/2020-12-24`
    WHERE domain = "AUTORU" AND transaction_info.customer_id.client_id = 6767510 -- balance client id
    GROUP BY `id`
) FLATTEN COLUMNS
GROUP BY withdraw_payload.product.name as product_name;
```

</p>
</details>

### Результат обилливания конкретного звонка в домене AUTORU
<details>
<summary>Запрос</summary>
<p>

```sql
use hahn;

SELECT
    *
FROM (
    SELECT MAX_BY(TableRow(), `timestamp`)
    FROM `home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d/2020-12-24`
    WHERE domain = "AUTORU" AND withdraw_payload.call_fact.call_fact.id IN ("--Kb5rTzc_g", "--TmL8kYMgE", "-0XItwRljXs")
    GROUP BY `id`
) FLATTEN COLUMNS;
```

</p>
</details>
