# Состояние начислений и выплат по заказу

## Штатные ситуации, когда может не быть выплаты за заказ
1. Не наступил статус Delivered
2. Не подошло расписание выплат для магазина
3. Команда на выплату (payment order) сформировалась, но не выплатилась в OEBS: для 610 есть непогашенный взаимозачет или рефанды по старой схеме, для 609 - не подписаны документы за прошлый месяц.
4. Для 1p (465852) и синего виртуального магазина (431782) не сохраняем payout.

## Инструменты для получения статуса начислений и выплат
1. Отчет Платежи в ПИ
2. [Дашборд](https://datalens.yandex-team.ru/vhaa0kwevhioo-dashbor-po-platezham-uv) по начислениям и платежам

## Чеклист для дежурного

Данный чеклист можно использовать для заказов, которые перешли в статус Delivered (или были в этом статусе).

1. Заказ переходил в статус DELIVERED.

    ``` sql
    Oracle

    select * from market_billing.cpa_order_status_history where status = 5 and order_id = :order_id;
    ```

2. Найти все платежи и рефанды по заказу (транзакции), которые пошли по новой схеме

    ``` sql
    Oracle

    select payment_id, refund_id, type from market_billing.orders_transactions ot join market_billing.cpa_order_transaction cot on ot.transaction_id = cot.id
    where ot.order_id = :order_id and mbi_control_enabled = 1;
    ```

    Если уже на этом этапе кажется, что здесь не все платежи/рефанды, надо траблшутить этот кейс отдельно.

3. Проверяем начисления: для каждого payment_id и refund_id в таблице market_billing.accrual_trantime должна быть запись со значением processed=1.
    ``` sql
    Oracle

    select * from market_billing.accrual_trantime where id in (:payment_id, refund_id);
    ```
4. Если в таблице market_billing.accrual_trantime есть все строки и они обработаны, проверяем таблицу market_billing.accrual (можно найти все строчки по order_id, а можно по checkouter_id - это либо payment_id, либо refund_id). Надо убедиться, все все строки есть, и у них флаг exported_to_tlog = true.
    ``` sql
    Postgres

    select * from market_billing.accrual where order_id = :order_id;
    select * from market_billing.accrual where checkouter_id in (:payment_id, :refund_id);
    ```

5. Проверяем создание payout по accrual. Если партнёр не 1p или виртуальный магазин и есть запись в таблице market_billing.order_payout_trantime, то для каждого начисления (accrual) должна быть создана соответствующая (1-к-1) запись в таблице market_billing.payout. 
    ``` sql
    Postgres

    select * from market_billing.payout where accrual_id = :accrual_id;
    ```

    При этом у accrual должен быть проставлен payout_status = 'PAID_OUT'
    ``` sql
    Postgres
    
    select payout_status from market_billing.accrual where id = :accrual_id;
    ```

    > Для 1p и виртуальных магазинов accrual создаётся сразу со статусом payout_status = 'IGNORED', для таких партнёров payout не создаются и дальше механизм выплат их игнорирует.

6. Проверяем выплаты дальше: в таблице market_billing.payout для заказа должны быть все платежи и рефанды. Надо проверить, что для строчки заполнено поле payout_group_id (которое означает, что payout собрался в драфт).
    ``` sql
    Postgres

    select * from market_billing.payout where order_id = :order_id;
    ```
7. Проверяем, выплатились ли драфты: в таблице market_billing.payment_order_draft поле processed должно быть true.
    ``` sql
    Postgres

    select * from market_billing.payment_order_draft
    where payout_group_id in (
        select payout.payout_group_id from market_billing.payout where order_id = :order_id
    );
    ```

    Если драфт не был выплачен, надо проверить, что у магазина должна была быть выплата по расписанию. Расписание магазина хранится в market_billing.client_payout_frequency, а дни для расписания хранятся в market_billing.payout_schedule).
8. Если драфт выплатился, надо найти его payment_order:
    ``` sql
    Postgres

    select po.id, po.trantime, po.service_id
    from market_billing.payout p
         join market_billing.payout_group_payment_order pgpo on p.payout_group_id = pgpo.payout_group_id
         join market_billing.payment_order po on pgpo.payment_order_id = po.id
    where p.order_id = :order_id;
    ```
    А затем проверить, есть ли платежное поручение (ПП) с этим payment_order:

    ``` sql
    Oracle

    select * from market_billing.bank_order bo join market_billing.bank_order_item boi on bo.payment_batch_id = boi.payment_batch_id
    where boi.payment_order_id = :payment_order_id;
    ```

    Если ПП есть, то магазин получил деньги. В довольно редких случаях это не так; бывает, что Банк сообщает, что ПП ушло успешно, а затем присылает статус, что ПП не отправлено. Для магазина это выглядит так, что деньги от Маркета он не получил, а мы в отчетах ему говорим, что деньги за заказы ему должны были прийти. Технические действия в этом случае не требуются, в течение 7 дней новый статус ПП автоматически придет из Балалайки в OEBS, а из OEBS в Market Billing.

9. ПП в OEBS может не формироваться из-за взаимозачета (если пришло много рефандов или начался новый месяц и есть непогашенный долг по 612 актам за услуги). 

    Убедиться, что ПП действительно не формируется из-за взаимозачета, можно [YQL](https://yql.yandex-team.ru/Operations/YlWiULq3k1JYYBYGHoxIk1CyCGeiJLSzOWnEpW6sfjk=) запросом. В этом случае последнее сообщение будет "Итоговая сумма по договору ID остается отрицательной!".
10. Стоит проверить, что в заказе нет 613 рефандов с некорректными удержаниями без корректировок (см. [инструкцию](https://a.yandex-team.ru/arc_vcs/market/billing/docs/reference/architecture/payment-control/order-status.md?edit=true#nekorrektnye-uderzhaniya-po-613-refandam-i-ih-korrektirovki)).

## Известные проблемы
### Некорректные удержания по 613 рефандам и их корректировки


> Рефанды по 613 сервису используются вместо обычных рефандов для следующих методов оплаты: постоплата, Тинькофф кредит, Тинькофф переуступка.

#### Теория

Проблема возникает в двух случаях:

1. Платеж был поклирен, но заказ отменился до доставки.
2. Платеж был поклирен и заказ был доставлен, но покупатель оформил возврат.

Выражается проблема в следующем: у магазина возникает лишний возврат по старой схеме, и он получает меньше выплат (или может не получать их совсем).

Проблему еще не починили и такие кейсы продолжают возникать. Раз в 2 недели мы по таким заказам создаем корректировки.

#### Проверить состояние 613 рефанда и корректировки

Как проверить, что данный рефанд прошел по 613 сервису (поле using_cash_refund_service должно быть равно 1)

``` sql
Oracle

select
    refund_id,
    using_cash_refund_service
from
    market_billing.orders_transactions ot
    join market_billing.cpa_order_transaction cot on ot.transaction_id = cot.id
where
    ot.order_id = :order_id
    and refund_id is not null
```

Исходный платеж должен идти по УВ. Проверить можно запросом

``` sql
Oracle

select
    payment_id,
    mbi_control_enabled
from
    market_billing.cpa_order_transaction cot
where
    payment_id = :payment_id
```

Проверить, что в ARD действительно создалось некорректное удержание, можно [YQL запросом](https://yql.yandex-team.ru/Operations/Yg0QaLq3k9WElbDxQXfGVAs42BAQhWEh4gKZXQ2xAJk=).

Проверить, была ли создана корректировка для некорректного удержания:


``` sql
Postgres

select *
from market_billing.payout_correction
where order_id = :order_id
```
Стоит внимательно посмотреть, на все ли товары и доставку были созданы корректировки.

Проверить, выплатились ли корректировки, можно [по инструкции (п. 7)](https://docs.yandex-team.ru/market-billing/reference/architecture/payment-control/order-status#cheklist-dlya-dezhurnogo), только payout_group_id надо взять из таблицы payout_correction.

В целом, на каждый заказ с некорректным удержанием должны быть созданы корректировки. Почему их может еще не быть:

1. 613 рефанд перешел в статус Success менее, чем 2 недели назад
2. Для заказа есть баги в Чекаутере (или других системах), и заказ отложили для ручного разбора. Все такие заказы мы собираем в [тикете](https://st.yandex-team.ru/MARKETBILLING-2225).

Если 1) и 2) не применимы к заказу, то корректировку для заказа надо запланировать на следующую итерацию корректировок.

## Про платежное поручение

В конечном итоге команда на выплату должна попасть в платежное поручение (п/п). Именно это является реальным переводом денег поставщику за заказ.

> **NOTE:** Само платежное поручение формирует **не** биллинг.

Найти, в какое п/п попал заказ, можно таким `YQL` запросом:
 ``` sql
 YQL

use hahn;

select
       p.order_id,
       p.entity_id,
       p.entity_type,
       p.partner_id,
       po.id as payment_order_id,
       po.trantime,
       po.service_id,
       po.client_id,
       po.contract_id,
       bo.payment_batch_id,
       bo.bank_order_id,
       bo.eventtime,
       boi.sum,
       boi.transaction_type
from `home/market/production/billing/dictionaries/payout/latest` as p
    join `home/market/production/billing/dictionaries/payout_group_payment_order/latest` as pgpo
on p.payout_group_id = pgpo.payout_group_id
    join `home/market/production/billing/dictionaries/payment_order/latest` as po on pgpo.payment_order_id = po.id
    left join `home/market/production/mstat/dictionaries/mbi_bank_order_item/latest` as boi on pgpo.payment_order_id = boi.payment_order_id
    left join `home/market/production/mstat/dictionaries/mbi_bank_order/latest` as bo on boi.payment_batch_id = bo.payment_batch_id
where p.order_id = :order_id
 ```
Запрос вернет по заказу номер п/п, в которое попала команда на выплату, в которую вошел нужный заказ.

Но может быть ситуация, когда с нашей стороны команда ушла, но деньги еще не выплатились (т.е. п/п нет).
Что делать в этом случае? Можно убедиться, что п/п действительно нет.

Для этого надо запросить детализацию платежей и комиссии по договору на [странице поддержки баланса](https://wiki.yandex-team.ru/otdelsoprovozhdeniya/dokument/avtomatformi/detalisation/).
По результату будет сформирован тикет, в который автоматически прорастет excel файл детализации. Если напротив нужной команды на выплату нет номера и даты п/п,
то значит оно еще не сформировано и вопросы **не** к биллингу.
