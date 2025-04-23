# Сверка начислений

Тикет: [MARKETBILLING-3488](https://st.yandex-team.ru/MARKETBILLING-3488)

Документация на wiki (аналогичная): [Сверка начислений](https://wiki.yandex-team.ru/market/billing/docs/sverki/accrual-checker)

Запись видео с демо: [demo_accrual_payout_checker.mp4](https://jing.yandex-team.ru/files/rhrrd/demo_accrual_payout_checker-4.mp4)

## Описание

Если вы интересуетесь сверкой начислений, то возможно Вас заинтересует и [{#T}](payout-checker.md).

Хочется понимать, как идут начисления через все участвующие системы, не просыпаем ли мы что-то. Если просыпаем, то какие именно суммы и на каком участке пути.

Поток начислений через системы выглядит так:
**Чекаутер** - **Начисления Маркет Биллинга** - **Тлог Маркет Биллинга** - **Начисления в OEBS**

{% note info %}

Между Тлогом Маркет Биллинга и OEBS есть еще Баланс, который игнорировать в этой схеме нельзя, но в явном виде все же обозначать его не будем, но пару слов про него будет по тексту ниже.

{% endnote %}

## Общий алгоритм сверок
{% cut "" %}

Будем сверять данные **не** между первой (Чекаутер) и последней системой (OEBS), а между двумя соседними системами на пути потока начислений. Почему именно так? Потому что в противном случае сверка будет гореть всегда, и чего-то полезного из такой сверки не получить.

Алгоритм сверки между системой А и системой Б состоит из пунктов:
- выбираем из системы А данные, подходящие под критерии
- к этим данным джойним данные из системы Б
- получаем результат для анализа. Такую сверку будем называть прямой
- выбираем из системы Б данные, подходящие под критерии
- к этим данным джойним данные из системы А
- получаем результат для анализа. Такую сверку будем называть обратной

Почему алгоритм именно такой, почему нельзя было сделать более стандартно - выбираем по критериям данные из системы А, выбираем данные по критериям из системы Б, делаем join между ними, смотрим разницу?

Дело в том, что данные из разных систем нельзя сравнивать между собой напрямую. Сначала нужно их нетривиально преобразовать, чтобы иметь возможность сделать нужный join. Подробности про каждую сверку можно найти ниже.

{% endcut %}

## Используемые выгрузки

{% cut "" %}

- Общее аналитическое
    - [//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_dict](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_dict) - таблица с позициями заказов ("старая" выгрузка)
    - [//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_item_dict](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_item_dict) - таблица с позициями заказов ("новая" выгрузка)

- Чекаутер
    - [//home/market/production/checkouter/dictionaries/payment/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/payment/latest) - платежи
    - [//home/market/production/checkouter/dictionaries/refund/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/refund/latest) - возвраты
    - [//home/market/production/checkouter/dictionaries/receipt/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/receipt/latest) - чеки
    - [//home/market/production/checkouter/dictionaries/receipt_item/late](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/receipt_item/latest) - позиции чеков

- Маркет Биллинг
    - [//home/market/production/billing/dictionaries/accrual](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/accrual) - начисления
    - [//home/market/production/billing/tlog/payouts/expenses](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/tlog/payouts/expenses) - транзакционный лог платежей расходных сервисов
    - [//home/market/production/billing/tlog/payouts/payments](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/tlog/payouts/payments) - транзакционный лог платежей доходных сервисов

- OEBS
    - [//home/bi/stable/dwh/outbox/external/oebs_oracle/XXYA/XXAP_AGENT_REWARD_DATA/MARKET/XXAP_AGENT_REWARD_DATA](https://yt.yandex-team.ru/hahn/navigation?path=//home/bi/stable/dwh/outbox/external/oebs_oracle/XXYA/XXAP_AGENT_REWARD_DATA/MARKET/XXAP_AGENT_REWARD_DATA))
    - [//home/bi/stable/dwh/outbox/external/oebs_oracle/OKE/OKE_K_HEADERS/MARKET/OKE_K_HEADERS)](https://yt.yandex-team.ru/hahn/navigation?path=//home/bi/stable/dwh/outbox/external/oebs_oracle/OKE/OKE_K_HEADERS/MARKET/OKE_K_HEADERS)

{% endcut %}

## Чекаутер <-> Начисления Маркет Биллинга

{% cut "" %}

В этой сверке хотим сравнить данные по начислениям со стороны Чекаутера и начисления со стороны Маркет Биллинга.

Текущий вариант сверки-импорта в Чекере:

Название |                                Описание                                |                                                       Ссылка                                                       | Расписание
:---: |:----------------------------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------:| :---:
Accrual_Checkouter_dashborad | Ежедневная сверка начислений за все время Чекаутера с Маркет Биллингом | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=529&schedulerTypeForCardView=IMPORT) | 0 0 6 * * ? *

Обработка результатов в виде YQL-запроса - [Accrual_Checkouter_dashborad_Result](https://yql.yandex-team.ru/Operations/YoIKBa5OD2sulU4EFNMdGXvwOUuzsSppV7JNevcEDXE=)

### Откуда читаем:

- [//home/market/production/billing/dictionaries/accrual](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/accrual) - начисления
- [//home/market/production/checkouter/dictionaries/payment/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/payment/latest) - платежи
- [//home/market/production/checkouter/dictionaries/refund/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/refund/latest) - возвраты
- [//home/market/production/checkouter/dictionaries/receipt/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/receipt/latest) - чеки
- [//home/market/production/checkouter/dictionaries/receipt_item/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/receipt_item/latest) - позиции чеков
- [//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_dict](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_dict) - таблица с позициями заказов ("старая" выгрузка)
- [//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_item_dict](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_item_dict) - таблица с позициями заказов ("новая" выгрузка)


### Куда пишем:

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/checkouter_accrual_left_market_billing_accrual](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/checkouter_accrual_left_market_billing_accrual) - результат прямой сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
ch_amount | double | сумма начисления в копейках из таблиц чекаутера
ch_fact_shipped_items | int64 | итоговое количество item-ов (если 0, то товар удален из заказа) из таблиц чекаутера
ch_partner_id | int64 | id партнера из таблиц чекаутера
ch_payment_goal | int64 | тип платежа из таблиц чекаутера
ch_status_updated_at | string | дата/время последнего изменения статуса из таблиц чекаутера
checkouter_id | int64 | id платежа или рефанда из чекаутера
checkouter_type | string | платеж или возврат
entity_id | int64 | id товара в заказе или id доставки
entity_type | string | товар в заказе или доставка
mb_acc_trantime | string | время события начисления
mb_amount | int64 | сумма начисления в копейках из таблиц маркет биллинг
mb_partner_id | int64 | id партнера из таблиц маркет биллинг
mb_paysys_type_cc | string | тип платежной системы из таблиц маркет биллинг
mb_product | string | тип продукта для начисления из таблиц маркет биллинг
order_id | int64 | id заказа
service_id | int64 | id сервиса в Балансе

Поля, начинающиеся на префикс _ch__ относятся к таблицам Чекаутера; на префикс _mb__ относятся к таблицам Маркет Биллинга. Все остальные - это общие поля. По ним идет join между выборками для сравнения, поэтому оставлено только одно поле.

Как читать результат? Чтобы найти записи, которые есть только в Чекаутере, то надо сделать выборку с условием `mb_amount is null` (не обязательно именно с этим полем). Чтобы найти записи, которые есть и в Чекаутере и в Маркет Биллинге, надо сделать выборку с обратным условием `mb_amount is not null`. Чтобы найти записи, с отличающимися суммами - с условием `mb_amount is not null and mb_amount <> ch_cmount`.

{% endcut %}

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/checkouter_accrual_right_market_billing_accrual](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/checkouter_accrual_right_market_billing_accrual) - результат обратной сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
ch_amount | double | сумма начисления в копейках из таблиц чекаутера
ch_partner_id | int64 | id партнера из таблиц чекаутера
ch_payment_goal | int64 | тип платежа из таблиц чекаутера
ch_status_updated_at | string | дата/время последнего изменения статуса из таблиц чекаутера
checkouter_id | int64 | id платежа или рефанда из чекаутера
checkouter_type | string | платеж или возврат
entity_id | int64 | id товара в заказе или id доставки
entity_type | string | товар в заказе или доставка
mb_acc_trantime | string | время события начисления
mb_amount | int64 | сумма начисления в копейках из таблиц маркет биллинга
mb_partner_id | int64 | id партнера из таблиц маркет биллинга
mb_paysys_type_cc | string | тип платежной системы из таблиц маркет биллинга
mb_product | string | тип продукта для начисления из таблиц маркет биллинга
order_id | int64 | id заказа
service_id | int64 | id сервиса в Балансе

В выгрузке результата поля, начинающиеся на префикс _ch__ относятся к таблицам Чекаутера; на префикс _mb__ относятся к таблицам Маркет Биллинга. Все остальные - это общие поля. По ним идет join между выборками для сравнения, поэтому оставлено только одно поле.

Как читать результат? Чтобы найти записи, которые есть только в маркет биллинге, то надо сделать выборку с условием `ch_amount is null` (не обязательно с этим полем). Чтобы найти записи, которые есть и в Чекаутере и в Маркет Биллинге, надо сделать выборку с обратным условием `ch_amount is not null`. Чтобы найти записи, с отличающимися суммами - с условием `ch_amount is not null and mb_amount <> ch_cmount`.

{% endcut %}

### Прямая сверка

Получаем заказы для сверки из помесячных таблиц-выгрузок. Не очевидный момент: может быть ситуация, когда заказ был сильно в прошлом периоде, а refund по такому заказу случился в интересующем нас периоде. Для обхода этого кейса смотрим на заказы на год назад.

Выбираем данные по начислениям из Чекаутера фильтрами:
- флаг mbi_control_enabled = true
- payment заказа в статусе CLEARED/refund заказа в статусе SUCCESS
- payment_goal в списке (ORDER_PREPAY, SUBSIDY, ORDER_POSTPAY, TINKOFF_CREDIT, VIRTUAL_BNPL, TINKOFF_CESSION)
- status_updated_at в нужном периоде

При этом данные выбираются отдельно по payment-ам и refund-ам. Кроме того отдельно и по item и по delivery. Это связано с нетривиальным определением supplier_id для delivery в случае 1p/3p поставщиков.

К этим данным джойним данные из Маркет Биллинга, в независимости от периода и других фильтров - для учета ситуации, когда начисление должно было быть в одном периоде, а случилась в другом.

{% note info %}

- при выборке данных из Чекаутера не фильтруем записи для 1p и виртуального поставщиков (465852, 431782, 2652811), т.к. начисления в Маркет Биллинге для них создаются
- в записи с entity_type = delivery в поле entity_id прорастает order_id, а на delivery_id

{% endnote %}

### Обратная сверка

Выбираем данные по начислениям из Маркет Биллинга фильтрами:
- accrual.trantime в нужном мериоде
- org_id = 64554

К этим данным джойним данные из Чекаутера. При этом при выборке данных из Чекаутера действуют те же фильтры, что и для прямой сверки, а именно:
- флаг mbi_control_enabled = true
- payment заказа в статусе CLEARED/refund заказа в статусе SUCCESS
- payment_goal в списке (ORDER_PREPAY, SUBSIDY, ORDER_POSTPAY, TINKOFF_CREDIT, VIRTUAL_BNPL, TINKOFF_CESSION)
- ~~status_updated_at в нужном периоде~~

Отличие только в отсутствии фильтра по status_update_at.

{% endcut %}

## Начисления Маркет Биллинга <-> Тлог Маркет Биллинга

{% cut "" %}

В этой сверке хотим сравнить начисления Маркет Биллинга и транзакционный лог с начислениями Маркет Биллинга.

Текущий вариант сверки-импорта в Чекере

Название |                      Описание                      |                                                       Ссылка                                                       | Расписание
:---: |:--------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------:| :---:
Accrual_Tlog_dashboard | Ежедневная сверка за все время начислений с тлогом | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=526&schedulerTypeForCardView=IMPORT) | 0 0 6 * * ? *

Обработка результатов в виде YQL-запроса - [Accrual_Tlog_Checker_Result](https://yql.yandex-team.ru/Operations/YoI4CVZ1OzMCM01h36msetWragAzPglJfjYhKwsE0oM=)

### Откуда читаем:

- [//home/market/production/billing/dictionaries/accrual](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/accrual) - начисления
- [//home/market/production/billing/tlog/payouts/expenses](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/tlog/payouts/expenses) - транзакционный лог платежей расходных сервисов
- [//home/market/production/billing/tlog/payouts/payments](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/tlog/payouts/payments) - транзакционный лог платежей доходных сервисов

### Куда пишем:

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/market_billing_accrual_left_tlog](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/market_billing_accrual_left_tlog) - результат прямой сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
acc_amount | int64 | сумма начисления в копейках
acc_entity_id | int64 | id товара в заказе или id доставки
acc_entity_type | string | товар в заказе или доставка
acc_id | int64 | id начисления
acc_order_id | int64 | id заказа
acc_partner_id | int64 | id партнера
acc_paysys_type_cc | string | тип платежной системы
acc_product | string | тип продукта для начисления
acc_service_id | int32 | id сервиса в Балансе
acc_transaction_type | string | платеж или возврат
acc_trantime | string | время события начисления
tlog_accrual_id | int64 | id начисления из тлога
tlog_amount | double | сумма начисления в копейках из тлога
tlog_checkouter_id | int64 | id платежа или рефанда из чекаутера
tlog_client_id | string | id клиента в Балансе
tlog_contract_id | int64 | id контракта в Балансе
tlog_entity_id | int64 | id товара в заказе или id доставки
tlog_entity_type | string | товар в заказе или доставка
tlog_event_time | string | время события
tlog_order_id | int64 | id заказа
tlog_partner_id | int64 | d партнера
tlog_paysys_type_cc | string | тип платежной системы
tlog_product | string | тип продукта для начисления
tlog_service_id | int64 | id сервиса в Балансе
tlog_service_transaction_id | string | id транзакции на стороне маркет биллинга
tlog_transaction_id | int64 | id транзакции
tlog_transaction_type | string | платеж или возврат

В выгрузке результата поля, начинающиеся на префикс _acc__, относятся к таблицам начислений; на префикс _tlog__ относятся к таблицам транзакционного лога. Т.к. связь идет через accrual-id, то возможно общие поля (order_id, entity_id и т.д.) оставлены из обеих таблиц для возможности их сравнения.

{% endcut %}

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/market_billing_accrual_right_tlog](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/market_billing_accrual_right_tlog) - результат обратной сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
acc_amount | int64 | сумма начисления в копейках
acc_entity_id | int64 | id товара в заказе или id доставки
acc_entity_type | string | товар в заказе или доставка
acc_id | int64 | id начисления
acc_order_id | int64 | id заказа
acc_partner_id | int64 | id партнера
acc_paysys_type_cc | string | тип платежной системы
acc_product | string | тип продукта для начисления
acc_service_id | int32 | id сервиса в Балансе
acc_transaction_type | string | платеж или возврат
acc_trantime | string | время события начисления
tlog_accrual_id | int64 | id начисления из тлога
tlog_amount | double | сумма начисления в копейках из тлога
tlog_checkouter_id | int64 | id платежа или рефанда из чекаутера
tlog_client_id | string | id клиента в Балансе
tlog_contract_id | int64 | id контракта в Балансе
tlog_entity_id | int64 | id товара в заказе или id доставки
tlog_entity_type | string | товар в заказе или доставка
tlog_event_time | string | время события
tlog_order_id | int64 | id заказа
tlog_partner_id | int64 | d партнера
tlog_paysys_type_cc | string | тип платежной системы
tlog_product | string | тип продукта для начисления
tlog_service_id | int64 | id сервиса в Балансе
tlog_service_transaction_id | string | id транзакции на стороне маркет биллинга
tlog_transaction_id | int64 | id транзакции
tlog_transaction_type | string | платеж или возврат

В выгрузке результата поля, начинающиеся на префикс _acc__, относятся к таблицам начислений; на префикс _tlog__ относятся к таблицам транзакционного лога. Т.к. связь идет через accrual-id, то возможно общие поля (order_id, entity_id и т.д.) оставлены из обеих таблиц для возможности их сравнения.

{% endcut %}

### Прямая сверка

К начислениям с фильтрами по org_id = 64554 и периоду джойним записи из транзакционного лога (отдельно для расходного и отдельно для доходного) через accrual_id (в тлоге поле service_transaction_id имеет вид accrual-:id) и record_type = 'accrual'.

### Обратная сверка

К записям из транзакционного лога (отдельно для расходного и отдельно для доходного) с фильтрами по org_id, дате и record_type = 'accrual', джойним начисления через accrual_id (в тлоге поле service_transaction_id имеет вид accrual-:id).

{% endcut %}

## Тлог Маркет Биллинга <-> Начисления в OEBS

{% cut "" %}

В этой сверке хотим сравнить транзакционный лог Маркет Биллинга с начислениями OEBS.

{% note info %}

- сравнивать будем только 610 сервис, т.к. начисления по 609 в Балансе собираются в акты накопительным итогом, и там нетривиальная логика проверки
- 1p поставщики (465852, 431782, 2652811) не участвуют в сверке, т.к. не прорастают в OEBS

{% endnote %}

Текущий вариант сверки-импорта в Чекере

Название |                                                                                  Описание                                                                                  |                                                     Ссылка                                                     | Расписание
:---: |:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------:| :---:
Accrual_Tlog_Oebs_dashboard | Ежедневная сверка за все время начислений тлога с OEBS | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=525&schedulerTypeForCardView=IMPORT) | 0 0 6 * * ? *

Обработка результатов в виде YQL-запроса - [Accrual_Tlog_Oebs_dashboard_Result](https://yql.yandex-team.ru/Operations/YoI6cdJwbLysvnzkuXEd0sRMvw-NL0z7bOnk6J_JGt0=)

### Откуда читаем:

- [//home/bi/stable/dwh/outbox/external/oebs_oracle/XXYA/XXAP_AGENT_REWARD_DATA/MARKET/XXAP_AGENT_REWARD_DATA](https://yt.yandex-team.ru/hahn/navigation?path=//home/bi/stable/dwh/outbox/external/oebs_oracle/XXYA/XXAP_AGENT_REWARD_DATA/MARKET/XXAP_AGENT_REWARD_DATA)
- [//home/bi/stable/dwh/outbox/external/oebs_oracle/OKE/OKE_K_HEADERS/MARKET/OKE_K_HEADERS](https://yt.yandex-team.ru/hahn/navigation?path=//home/bi/stable/dwh/outbox/external/oebs_oracle/OKE/OKE_K_HEADERS/MARKET/OKE_K_HEADERS)
- [//home/market/production/billing/tlog/payouts/payments](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/tlog/payouts/payments) - транзакционный лог платежей доходных сервисов

### Куда пишем:

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/market_billing_tlog_left_oebs](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/market_billing_tlog_left_oebs) - результат прямой сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
ard_accrual_id | int64 | распарсенный id начисления из service_order_id из таблиц oebs
ard_agent_type_code | string | agent_type_code из таблиц oebs
ard_amount | double | сумма начисления в копейках из таблиц oebs
ard_contract_id | int64 | id контракта в Балансе из таблиц oebs
ard_creation_date | string | creation_date из таблиц oebs
ard_k_alias | string | номер договра в балансе из таблиц oebs
ard_k_header_id | int64 | k_header_id из таблиц oebs
ard_org_id | int64 | Операционная единица, через которую осуществляется работа из таблиц oebs
ard_paysys_type_id | int64 | paysys_type_id из таблиц oebs
tlog_accrual_id | int64 | id начисления из тлога
tlog_amount | double | сумма начисления в копейках из тлога
tlog_checkouter_id | int64 | id платежа или рефанда из чекаутера
tlog_client_id | string | id клиента в Балансе
tlog_contract_id | int64 | id контракта в Балансе
tlog_entity_id | int64 | id товара в заказе или id доставки
tlog_entity_type | string | товар в заказе или доставка
tlog_event_time | string | время события
tlog_order_id | int64 | id заказа
tlog_partner_id | int64 | d партнера
tlog_paysys_type_cc | string | тип платежной системы
tlog_product | string | тип продукта для начисления
tlog_service_id | int64 | id сервиса в Балансе
tlog_service_transaction_id | string | id транзакции на стороне маркет биллинга
tlog_transaction_id | int64 | id транзакции
tlog_transaction_type | string | платеж или возврат

В выгрузке результата поля, начинающиеся на префикс _ard__, относятся к таблицам OEBS; на префикс _tlog__ относятся к таблицам транзакционного лога. Т.к. связь идет через service_transaction_id = SERVICE_ORDER_ID, то возможно общие поля (order_id, entity_id и т.д.) оставлены из обеих таблиц для возможности их сравнения.

{% endcut %}

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/market_billing_tlog_right_oebs](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/accrual/dashboard/market_billing_tlog_right_oebs) - результат обратной сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
ard_accrual_id | int64 | распарсенный id начисления из service_order_id из таблиц oebs
ard_agent_type_code | string | agent_type_code из таблиц oebs
ard_amount | double | сумма начисления в копейках из таблиц oebs
ard_contract_id | int64 | id контракта в Балансе из таблиц oebs
ard_creation_date | string | creation_date из таблиц oebs
ard_k_alias | string | номер договра в балансе из таблиц oebs
ard_k_header_id | int64 | k_header_id из таблиц oebs
ard_org_id | int64 | Операционная единица, через которую осуществляется работа из таблиц oebs
ard_paysys_type_id | int64 | paysys_type_id из таблиц oebs
tlog_accrual_id | int64 | id начисления из тлога
tlog_amount | double | сумма начисления в копейках из тлога
tlog_checkouter_id | int64 | id платежа или рефанда из чекаутера
tlog_client_id | string | id клиента в Балансе
tlog_contract_id | int64 | id контракта в Балансе
tlog_entity_id | int64 | id товара в заказе или id доставки
tlog_entity_type | string | товар в заказе или доставка
tlog_event_time | string | время события
tlog_order_id | int64 | id заказа
tlog_partner_id | int64 | d партнера
tlog_paysys_type_cc | string | тип платежной системы
tlog_product | string | тип продукта для начисления
tlog_service_id | int64 | id сервиса в Балансе
tlog_service_transaction_id | string | id транзакции на стороне маркет биллинга
tlog_transaction_id | int64 | id транзакции
tlog_transaction_type | string | платеж или возврат

В выгрузке результата поля, начинающиеся на префикс _ard__, относятся к таблицам OEBS; на префикс _tlog__ относятся к таблицам транзакционного лога. Т.к. связь идет через service_transaction_id = SERVICE_ORDER_ID, то возможно общие поля (order_id, entity_id и т.д.) оставлены из обеих таблиц для возможности их сравнения.

{% endcut %}

### Прямая сверка

К транзакционному логу доходного сервиса с фильтрами:
- tlog.event_time в нужном периоде
- org_id = 64554
- partner_id not in (465852, 431782, 2652811)
- record_type = 'accrual'

через service_transaction_id джойним данные из OEBS (в ard поле SERVICE_ORDER_ID).

### Обратная сверка

К данным из OEBS с фильтрами:
- ard.CREATION_DATE в нужном периоде
- org_id = 64554
- SERVICE_ORDER_ID like 'accrual-%'

через SERVICE_ORDER_ID  джойним транзакционной лог доходного сервиса (поле service_transaction_id).

{% endcut %}

## Результаты

{% cut "" %}

### Сверки в Чекере

Вся деятельность выше родилась из потребности на ежемесячной основе проводить сверку начислений. Чтобы по итогу создавался тикет (или тикеты), куда будут призываться люди, которые будут анализировать результаты сверок.
Получились следующие сверки в Чекере:

Название | Описание                                                   |                                                      Ссылка                                                       | Расписание
:--- |:-----------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------:| :---:
Accrual_Checkouter_Accrual_monthly | Ежемесячная сверка начислений Чекаутера с Маркет Биллингом | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=531&schedulerTypeForCardView=CHECK) | 0 0 8 3 * ? *
Accrual_Checkouter_monthly | Ежемесячная сверка начислений Маркет Биллинга c Чекаутером | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=532&schedulerTypeForCardView=CHECK) | 0 0 8 3 * ? *
Accrual_Tlog_monthly | Ежемесячная сверка начислений с тлогом                     | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=522&schedulerTypeForCardView=CHECK) | 0 0 8 3 * ? *
Accrual_Tlog_Oebs_monthly | Ежемесячная сверка начислений тлога с OEBS                 | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=523&schedulerTypeForCardView=CHECK) | 0 0 8 3 * ? *

Сверки запускаются 3 числа в 8 утра за предыдущий месяц. По итогу создаются тикеты, в которые призываются люди для анализа расхождений.

### Дашборд

Выгрузки с результатами сверки, конечно, хорошо, но не очень наглядно. Поэтому появился дашборд в DataLens с подробными результатами. Дашброд строится на основе сверок-импортов в Чекере выше.

Ссылка на дашборд в DataLens с результатами сверки - [CATE_dashboard](https://datalens.yandex-team.ru/kyidipr6uxqkc-cate-dashboard)

#### Описание дашборда

Название представляет собой ~~попытку~~ акронима:
- **C**heckouter
- **A**ccrual
- **T**log
- O**E**BS

Сам дашборд разбит на 5 вкладок:
- Общая сводка
- Чекаутер LEFT JOIN Маркет Биллинг Accrual
- Маркет Биллинг Accrual LEFT JOIN Чекаутер
- Маркет Биллинг Accrual JOIN Маркет Биллинг Tlog
- Маркет Биллинг Tlog JOIN OEBS

{% list tabs %}

- Общая сводка

  На вкладке собрана общая информация со всех остальных вкладок. Важно отметить, что это не исчерпывающая информация. То есть, если на этой вкладке будет расхождение 0 между какими-то системами, это не будет означать, что расхождений совсем нет. Надо перейти на интересующую вкладку и посмотреть результат сверки там.

  На этой вкладке можно увидеть:
  - Общая сумма accrual в Чекаутере _- данные из Чекаутера из прямой сверки_
  - Общая сумма accrual недоехавших до Маркет Биллинга _- данные из Чекаутера, отсутствующие в Маркет Биллинге, из прямой сверки_
  - Общая сумма проблемных accrual между МБ и Чекаутером _- данные из Маркет Биллинга, отсутствующие в Чекаутере, из обратной сверки_
  - Общая сумма accrual в Маркет Биллинге _- данные Маркет Биллинга из прямой сверки с Тлогом_
  - Общая сумма accrual в тлоге Маркет Биллинга _- данные Тлога маркет Биллинга из обратной сверки с Маркет Биллингом_
  - Общая сумма accrual в OEBS (610 сервис без 1p) _- данные из OEBS из обратной сверки с Маркет Биллингом_
  - Общая сумма accrual недоехавших до OEBS (610 сервис) _- данные из Маркет Биллинга, отсутствующие в OEBS, из прямой сверки_

  Также на вкладке присутствуют фильтры для выборки диапазона периода сверки и максимальные и минимальные даты записей в сверках. По умолчанию они не заполнены, т.е. период, который отображается при пустых фильтрах, является максимальным периодом сверки.

  Как интерпретировать информацию, на какие числа в первую очередь обращать внимание?
  - суммы, выделенные зеленым цветом, а именно: _общая сумма в Чекаутере, общая сумма в Маркет Биллинге и общая сумма в OEBS_, **не** стоит сравнивать между собой. Они скорее приведены для масштаба
  - суммы: _Общая сумма accrual в Маркет Биллинге и Общая сумма accrual в тлоге Маркет Биллинга_ можно сравнивать между собой. Если там будут расхождения, то это повод сразу пойти разбираться
  - в первую очередь стоит смотреть на суммы, выделенные красным цветом. В идеале они должны равняться 0

- Чекаутер LEFT JOIN МБ Accrual

  На вкладке представлены подробные результаты **прямой сверки** начислений между Чекаутером и Маркет Биллингом. Помимо периода сверки (_min(status_update) и max(status_update)_), данные представлены в виде таблиц
  - Нет данных в Маркет Биллинге. Группировка по типу и сервису _- сгруппированные данные из Чекаутера, отсутствующие в Маркет Биллинге. В таблице представлена как сумма в рублях, так и количество записей сверки_
  - Отличающиеся суммы. Группировка по типу и сервису _- сгруппированные пересекающиеся начисления из Чекаутера и Маркет Биллинга, у которых отличаются суммы_
  - Общие данные. Группировка по типу и сервису _- сгруппированные общие начисления из Чекаутера и Маркет Биллинга_
  - Нет данных в Маркет Биллинге. Группировка по партнеру _- сгруппированные данные по партнеру из Чекаутера, отсутствующие в Маркет Биллинге. В таблице приведена сумма в рублях и количество отсутствующих записей_
  - Нет данных в Маркет Биллинге _- все данные по всем начислениям Чекаутера, отсутствующим в Маркет Биллинге, из прямой сверки_
  - Разные суммы _- все данные по всем пересекающимся начислениям из Чекаутера и Маркет Биллинга, у которых отличаются суммы_

  графика
  - Нет данных в Маркет Биллинге. Суммы по status_updated_at _- суммы начислений Чекатера, отсутствующих в Маркет Биллинге, из прямой сверки, сгруппированной по времени обновления статуса payment-а/refund-а_

  фильтров
  - status_updated _- фильтр по дате последнего обновления статуса payment-а/refund-а в Чекаутере_
  - partner_id _- фильтр по id партнера_
  - order_id _- фильтр по id заказа_
  - entity_id _- фильтр по id товара/id доставки_
  - entity_type _- фильтр по item/delivery_
  - checkouter_type _- фильтр по payment/refund_
  - checkouter_id _- фильтр по id payment-а/refund-а_
  - service_id _- фильтр по id сервиса в Балансе_
  - payment_goal _- фильтр по типу платежа из Чекаутера_

- МБ Accrual LEFT JOIN Чекаутер

  На вкладке представлены подробные результаты **обратной сверки** начислений между Чекаутером и Маркет Биллингом. Помимо периода сверки (_min(accrual_trantime) и max(accrual_trantime)_), данные представлены в виде таблиц
  - Нет данных в Чекаутере. Группировка по типу и сервису _- сгруппированные данные из Маркет Биллинга, отсутствующие в Чекаутере. В таблице представлена как сумма в рублях, так и количество записей сверки_
  - Отличающиеся суммы. Группировка по типу и сервису _- сгруппированные пересекающиеся начисления из Чекаутера и Маркет Биллинга, у которых отличаются суммы_
  - Общие данные. Группировка по типу и сервису _- сгруппированные общие начисления из Чекаутера и Маркет Биллинга_
  - Нет данных в Чекаутере. Группировка по партнеру _- сгруппированные данные по партнеру из Маркет Биллинга, отсутствующие в Чекаутере. В таблице приведена сумма в рублях и количество отсутствующих записей_
  - Нет данных в Чекаутере _- все данные по всем начислениям Маркет Биллинга, отсутствующим в Чекаутере, из прямой сверки_
  - Разные суммы _- все данные по всем пересекающимся начислениям из Чекаутера и Маркет Биллинга, у которых отличаются суммы_

  графиков
  - Нет данных в Чекаутере. Суммы по accrual_trantime _- суммы начислений Маркет Биллинга, отсутствующих в Чекаутере, из обратной сверки, сгруппированной по времени события начисления accrual_trantime_
  - Общие данные. Суммы по accrual_trantime _- суммы пересекающихся начислений Маркет Биллинга и Чекаутера, из обратной сверки, сгруппированной по времени события начисления accrual_trantime_

  фильтров
  - accrual_trantime _- фильтр по времени события начисления в Маркет Биллинге_
  - partner_id _- фильтр по id партнера_
  - order_id _- фильтр по id заказа_
  - entity_id _- фильтр по id товара/id доставки_
  - entity_type _- фильтр по item/delivery_
  - checkouter_id _- фильтр по id payment-а/refund-а_
  - checkouter_type _- фильтр по payment/refund_
  - product _- фильтр по продукту начисления Маркет Баллинга_
  - paysys_type_cc _- фильтр по типу платежной системы начисления Маркет Биллинга_
  - service_id _- фильтр по id сервиса в Балансе_

- МБ Accrual JOIN МБ Tlog

  На вкладке представлены подробные результаты как **прямой** так и **обратной** сверок начислений между Маркет Биллингом и Тлогом Маркет Биллинга. Вкладка условно поделена на левую и правую половины. На левой - результаты прямой сверки, на правой - обратной.

  Результаты прямой сверки представлены в виде периода сверки (_min(accrual_trantime) и max(accrual_trantime)_), общей суммы начислений в Маркет Биллинге за этот период, а также таблиц
  - Нет данных в транзакционном логе _- все данные по всем начислениям Маркет Биллинга, отсутствующими в Тлоге Маркет Биллинга, из прямой сверки_
  - Есть данные в транзакционном логе. Суммы отличаются _- все данные по всем пересекающимся начислениям Маркет Биллинга и Тлога Маркет Биллинга, у которых отличаются суммы_
  - Общие данные. Группировка по сервису и типу _- сгруппированные пересекающиеся начисления из Маркет Биллинга и Тлога Маркет Биллинга. В таблице представлена сумма в рублях_

  графика
  - Общие данные. Суммы по accrual_trantime _- суммы пересекающихся начислений Маркет Биллинга и Тлога Маркет Биллинга, из прямой сверки, сгруппированной по времени события начисления accrual_trantime_

  фильтров
  - accrual_trantime _- фильтр по времени события начисления в Маркет Биллинге_
  - accrual_partner_id _- фильтр по id партнера_
  - accrual_service_id _- фильтр по id сервиса в Балансе_

  Результаты обратной сверки представлены в виде периода сверки (_min(tlog_event_time) и max(tlog_event_time)_), общая сумма начислений в Тлоге Маркет Биллинга за этот период, а также таблиц
  - Нет данных в accrual _- все данные по всем начислениям Тлога Маркет Биллинга, отсутствующими в Маркет Биллинга, из обратной сверки_
  - Есть данные в accrual. Суммы отличаются _- все данные по всем пересекающимся начислениям Маркет Биллинга и Тлога Маркет Биллинга, у которых отличаются суммы_
  - Общие данные. Группировка по сервису и типу _- сгруппированные пересекающиеся начисления из Маркет Биллинга и Тлога Маркет Биллинга. В таблице представлена сумма в рублях_

  графика
  - Общие данные. Суммы по tlog_event_time _- суммы пересекающихся начислений Маркет Биллинга и Тлога Маркет Биллинга, из обратной сверки, сгруппированной по времени события tlog_event_time_

  фильтров
  - tlog_event_time _- фильтр по времени события Тлога Маркет Биллинга_
  - tlog_partner_id _- фильтр по id партнера_
  - tlog_service_id _- фильтр по id сервиса в Балансе_

- МБ Tlog JOIN OEBS

  На вкладке представлены подробные результаты как **прямой** так и **обратной** сверок начислений между Тлогом Маркет Биллинга и OEBS.

  Результаты сверой представлены в виде периода сверки (_min(oebs_creation_date) и max(oebs_creation_date)_) из обратной сверки, общей суммы accrual в OEBS (610 сервис без 1p) за этот период из обратной сверки, общей суммы accrual недоехавших до OEBS (610 сервис) из прямой сверки, а также таблиц
  - Маркет Биллинг Tlog LEFT JOIN OEBS. Общие данные. Отличающиеся суммы _- все данные по всем пересекающимся начислениям Тлога Маркет Биллинга и OEBS, у которых отличаются суммы, из прямой сверки_
  - Маркет Биллинг Tlog RIGHT JOIN OEBS. Общие данные. Отличающиеся суммы _- все данные по всем пересекающимся начислениям Тлога Маркет Биллинга и OEBS, у которых отличаются суммы, из обратной сверки_
  - Маркет Биллинг Tlog RIGHT JOIN OEBS. Нет данных в Маркет Биллинг _- все данные по всем начислениям OEBS, отсутствующими в Тлоге Маркет Биллинга, из обратной сверки_
  - Маркет Биллинг Tlog LEFT JOIN OEBS. Нет данных в OEBS _- все данные по всем начислениям Тлога Маркет Биллинга, отсутствующими в OEBS, из прямой сверки_

  графика
  - Сумма начислений по oebs_creation_date _- суммы начислений из OEBS по дате creation_date из обратной сверки_

  фильтра
  - oebs_creation_date _- фильтр по дате creation_date из OEBS_

{% endlist %}

{% endcut %}
