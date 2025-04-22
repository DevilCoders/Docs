# Состояние ежедневных выплат магазинам

## Сумма подготовленных выплат (сколько лежит в драфтах и ждёт наступления даты выплаты)
Надо указать сегодняшнюю дату в [YQL запросе](https://yql.yandex-team.ru/Operations/Yr1Y5pfFt1QnZCJU6OaQwc0dyBZGX0gMnOFV7vwqLJM=)

## Суммы payment_order 

1. Сводная статистика по дням:
``` sql
select date(trantime), round(sum(amount)/100) as sum, count(distinct contract_id) as contract_count, count(*) as po_count, org_id, platform 
from market_billing.payment_order po
where exported_to_tlog
and contract_id not in (select contract_id from shops_web.supplier_contract where supplier_id in (465852, 431782))
group by date(trantime), org_id, platform order by date(trantime) desc ;
```

2. По конкретному партнеру (договору партнера):
``` sql
select date(trantime), round(sum(amount)/100) as sum, count(distinct contract_id) as contract_count
from market_billing.payment_order po
where exported_to_tlog
and contract_id in (select contract_id from shops_web.supplier_contract where partner_id = :1)
group by date(trantime) order by date(trantime) desc;
```

## Суммы в т-логе на YT
Надо указать сегодняшнюю дату в [YQL запросе](https://yql.yandex-team.ru/Operations/Ytpa0AVK8LDTxWnPg4TiuElYaesgIHodRniuXYr9wKE=)

## Статусы платежей для указанной даты

Надо указать сегодняшнюю дату в [YQL запросе](https://yql.yandex-team.ru/Operations/YhT0jbq3k4C_kp9pF1eSRxh8l1dazVD3NYzUFsIFMgo=) и запустить его. 

Как читать результат запроса:
* Поле report_type
    * MARKETPLACEBLUE - это 609 сервис, он всегда идет не через Фактор 
    * MARKETPAYSBLUE - это 610 сервис, старая схема (до УВ)
    * MARKETPAYSBLUE_PAY - это 610 сервис, новая схема (УВ)
* Поле factor 
    * RAIFFEISEN - платеж пошел через Банк-Фактор 
    * null - платеж пошел с наших счетов (Сбербанк и Райффайзен Банк)
* Поле payment_status 
    * CREATED - платеж сформировался, но еще не передан в Балалайку
    * TRANSMITTED - платеж передан в Балалайку 
    * RECONCILED - платеж успешно ушел в Банк получателя (магазин получил деньги)
    * RETURNED - платеж несколько дней назад успешно ушел в Банк, но в течение 7 дней из Банка пришел отказ
    * VOIDFACTOR - платеж был отклонен Банком-Фактором 

