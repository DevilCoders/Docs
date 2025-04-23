# Сверка выплат

Тикет: [MARKETBILLING-3195](https://st.yandex-team.ru/MARKETBILLING-3195)

Документация на wiki (аналогичная): [Сверка выплат](https://wiki.yandex-team.ru/market/billing/docs/sverki/payout-checker)

Запись видео с демо: [demo_accrual_payout_checker.mp4](https://jing.yandex-team.ru/files/rhrrd/demo_accrual_payout_checker-4.mp4)

## Описание

Если вы интересуетесь сверкой выплат, то возможно Вас заинтересует и [{#T}](accrual-checker.md).

Хочется понимать, как идут выплаты через все участвующие системы, не просыпаем ли мы что-то. Если просыпаем, то какие именно суммы и на каком участке пути.

Поток выплат через системы выглядит так:
**Чекаутер** - **Драфты Маркет Биллинга** - **Команды на выплату Маркет Биллинга** - **Команды на выплату OEBS**

{% note info %}

Полная схема : Чекаутер - Выплаты Маркет Биллинга - Драфты Маркет Биллинга - Команды на выплату Маркет Биллинга - Тлог Маркет Биллинга - Баланса - Команды на выплату OEBS
но в текущей сверке полную схему учитывать не будем.

{% endnote %}

## Общий алгоритм сверок

{% cut "" %}

Будем сверять данные **не** между первой (Чекаутер) и последней системой (OEBS), а между двумя соседними системами на пути потока выплат. Почему именно так? Потому что в противном случае сверка будет гореть всегда, и чего-то полезного она говорить не будет.

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
    - [//home/market/production/mstat/analyst/regular/cubes_vertica/fact_order_statuses](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/analyst/regular/cubes_vertica/fact_order_statuses) - таблица со статусами заказов

- Чекаутер
    - [//home/market/production/checkouter/dictionaries/payment/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/payment/latest) - платежи
    - [//home/market/production/checkouter/dictionaries/refund/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/refund/latest) - возвраты
    - [//home/market/production/checkouter/dictionaries/receipt/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/receipt/latest) - чеки
    - [//home/market/production/checkouter/dictionaries/receipt_item/late](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/receipt_item/latest) - позиции чеков

- Маркет Биллинг
    - [//home/market/production/billing/dictionaries/payout/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/payout/latest) - выплаты
    - [//home/market/production/billing/dictionaries/payment_order_draft/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/payment_order_draft/latest) - драфты команд на выплату
    - [//home/market/production/billing/dictionaries/payout_group_payment_order/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/payout_group_payment_order/latest) - связь групп выплат с командами на выплату
    - [//home/market/production/billing/dictionaries/payment_order/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/payment_order/latest) - команды на выплату

- OEBS
    - [//home/bi/stable/dwh/outbox/external/oebs_oracle/XXYA/XXAP_AGENT_REWARD_DATA/MARKET/XXAP_AGENT_REWARD_DATA](https://yt.yandex-team.ru/hahn/navigation?path=//home/bi/stable/dwh/outbox/external/oebs_oracle/XXYA/XXAP_AGENT_REWARD_DATA/MARKET/XXAP_AGENT_REWARD_DATA))
    - [//home/bi/stable/dwh/outbox/external/oebs_oracle/OKE/OKE_K_HEADERS/MARKET/OKE_K_HEADERS)](https://yt.yandex-team.ru/hahn/navigation?path=//home/bi/stable/dwh/outbox/external/oebs_oracle/OKE/OKE_K_HEADERS/MARKET/OKE_K_HEADERS)

{% endcut %}

## Чекаутер <-> Драфты Маркет Биллинга

{% cut "" %}

В этой сверке хотим сравнить данные на стороне Чекаутера и Драфты команд на выплату со стороны Маркет Биллинга.

Текущий вариант сверки-импорта в Чекере:

Название |                                Описание                                |                                                     Ссылка                                                     | Расписание
:---: |:----------------------------------------------------------------------:|:--------------------------------------------------------------------------------------------------------------:| :---:
Payout_Checkouter_dashborad | Ежедневная сверка выплат за все время Чекаутера с Маркет Биллингом| [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=530&schedulerTypeForCardView=IMPORT) | 0 0 6 * * ? *

Обработка результатов в виде YQL-запроса - [Payout_Checkouter_dashborad_Result](https://yql.yandex-team.ru/Operations/YoJPbrq3k_b8KgteoNkcUGzZPHZ_vNUvAHukJdGXtwk=)

### Откуда читаем:

- [//home/market/production/billing/dictionaries/payout/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/payout/latest) - выплаты
- [//home/market/production/billing/dictionaries/payment_order_draft/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/payment_order_draft/latest) - драфты команд на выплату
- [//home/market/production/checkouter/dictionaries/payment/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/payment/latest) - платежи
- [//home/market/production/checkouter/dictionaries/refund/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/refund/latest) - возвраты
- [//home/market/production/checkouter/dictionaries/receipt/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/receipt/latest) - чеки
- [//home/market/production/checkouter/dictionaries/receipt_item/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/dictionaries/receipt_item/latest) - позиции чеков
- [//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_dict](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_dict) - таблица с позициями заказов ("старая" выгрузка)
- [//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_item_dict](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/analyst/regular/cubes_vertica/cube_order_item_dict) - таблица с позициями заказов ("новая" выгрузка)
- [//home/market/production/mstat/analyst/regular/cubes_vertica/fact_order_statuses](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/analyst/regular/cubes_vertica/fact_order_statuses) - таблица со статусами заказов

### Куда пишем:

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/checkouter_payout_left_market_billing_payout](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/checkouter_payout_left_market_billing_payout) - результат прямой сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
ch_amount | double | сумма выплаты в копейках из таблиц чекаутера
ch_datetime | string | дата и время перехода заказа в статус DELIVERED
ch_fact_shipped_items | int64 | итоговое количество item-ов (если 0, то товар удален из заказа; если -1, то это delivery) из таблиц чекаутера
ch_partner_id | int64 | id партнера из таблиц чекаутера
ch_payment_goal | int64 | тип платежа из таблиц чекаутера
ch_paysys_type_cc | string | тип платежной системы из таблиц чекаутера
ch_status_updated_at | string | дата/время последнего изменения статуса из таблиц чекаутера
checkouter_id | int64 | id платежа или рефанда из чекаутера
checkouter_type | string | платеж или возврат
entity_id | int64 | id товара в заказе или id доставки
entity_type | string | товар в заказе или доставка
mb_amount | int64 | сумма выплаты в копейках из таблиц маркет биллинг
mb_partner_id | int64 | id партнера из таблиц маркет биллинг
mb_paysys_type_cc | string | тип платежной системы из таблиц маркет биллинг
mb_pod_transaction_date | string | дата, за которую собран драфт, из таблиц маркет биллинг
mb_product | string | тип продукта для выплат из таблиц маркет биллинг
order_id | int64 | id заказа
service_id | int64 | id сервиса в Балансе

В выгрузке результата поля, начинающиеся на префикс _ch__ относятся к таблицам Чекаутера; на префикс _mb__ относятся к таблицам Маркет Биллинга. Все остальные - это общие поля. По ним идет join между выборками для сравнения. Так что оставлено только одно поле.

Как читать результат? Чтобы найти записи, которые есть только в Чекаутере, то надо сделать выборку с условием `mb_amount is null`. Чтобы найти записи, которые есть и в Чекаутере и в Маркет Биллинге, надо сделать выборку с обратным условием `mb_amount is not null`. Чтобы найти записи, с отличающимися суммами - с условием `mb_amount is not null and mb_amount <> ch_cmount`.

{% endcut %}

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/checkouter_payout_right_market_billing_payout](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/checkouter_payout_right_market_billing_payout)) - результат обратной сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
ch_amount | double | сумма выплаты в копейках из таблиц чекаутера
ch_partner_id | int64 | id партнера из таблиц чекаутера
ch_payment_goal | int64 | тип платежа из таблиц чекаутера
ch_paysys_type_cc | string | тип платежной системы из таблиц чекаутера
ch_status_updated_at | string | дата/время последнего изменения статуса из таблиц чекаутера
checkouter_id | int64 | id платежа или рефанда из чекаутера
checkouter_type | string | платеж или возврат
entity_id | int64 | id товара в заказе или id доставки
entity_type | string | товар в заказе или доставка
mb_amount | int64 | сумма выплаты в копейках из таблиц маркет биллинг
mb_partner_id | int64 | id партнера из таблиц маркет биллинг
mb_paysys_type_cc | string | тип платежной системы из таблиц маркет биллинг
mb_pod_transaction_date | string | дата, за которую собран драфт, из таблиц маркет биллинг
mb_product | string | тип продукта для выплат из таблиц маркет биллинг
order_id | int64 | id заказа
service_id | int64 | id сервиса в Балансе

В выгрузке результата поля, начинающиеся на префикс _ch__ относятся к таблицам Чекаутера; на префикс _mb__ относятся к таблицам Маркет Биллинга. Все остальные - это общие поля. По ним идет join между выборками для сравнения. Так что оставлено только одно поле.

Как читать результат? Чтобы найти записи, которые есть только в Маркет Биллинге, то надо сделать выборку с условием `ch_amount is null`. Чтобы найти записи, которые есть и в Чекаутере и в Маркет Биллинге, надо сделать выборку с обратным условием `ch_amount is not null`. Чтобы найти записи, с отличающимися суммами - с условием `ch_amount is not null and mb_amount <> ch_cmount`.

{% endcut %}

### Прямая сверка

Получаем заказы для сверки из помесячных таблиц-выгрузок. Стоит отметить такой момент: может быть ситуация, когда заказ был сильно в прошлом периоде, а refund по такому заказу случился в интересующем нас периоде. Для учета этого кейса смотрим на заказы на год назад (см. **Примечание** ниже).

Получаем заказы в статусе DELIVERED в нужном периоде из таблиц-выгрузок.

Выбираем данные по выплатам из Чекаутера по фильтрам:
- флаг mbi_control_enabled = true
- payment заказа в статусе CLEARED/refund заказа в статусе SUCCESS
- payment_goal в списке (ORDER_PREPAY, SUBSIDY, ORDER_POSTPAY, TINKOFF_CREDIT, VIRTUAL_BNPL, TINKOFF_CESSION)
- заказ перешел в статус (был в статусе) DELIVERED в нужном периоде
- supplier_id **not in** 1p (465852, 431782, 2652811)

При этом данные выбираются отдельно по payment-ам и refund-ам. Кроме того отдельно и по item и по delivery. Это связано с нетривиальным определением supplier_id для delivery в случае 1p/3p поставщиков.

{% note info "Особенности возвратов" %}

- если возврат перешел в статус SUCCESS, то это еще не означает, что он должен быть выплачен _(т.е. удержан. Но для простоты будем говорить выплачен)_

_Возврат выплачивается только после того, как будет выплачен платеж, к которому он относится. С точки зрения Чекаутера платеж всегда есть раньше возврата. Но с точки зрения Маркет Биллинга сама выплата платежа не происходит в момент его перехода в статус CLEAR. Она происходит в момент перехода заказа в статус DELIVERED._

_Получается, что нам надо выбирать такие возвраты, которые уже в статусе SUCCESS и заказы которых перешли в статус DELIVERED, чтобы быть уверенными, что выплата по нему должна быть. Чтобы ее можно было сравнить с тем, что есть в Маркет Биллинге._

- возврат может быть, теоретически, сколь угодно позже перехода заказа в статус DELIVERED

_С точки зрения законодательства есть предельный срок возврата товара, но с точки зрения бизнеса, а именно саппорта, который может сделать возврат в ручном режиме, такого срока нет. Сверку все же надо чем-то ограничить, поэтому был выбран период 1 год назад для таких случаев._

{% endnote %}

К этим данным джойним данные из Маркет Биллинга, в независимости от периода и других фильтров (может быть такое, что выплата должна была быть в одном месяце, а случилась в другом).

{% note info %}

- в записи с entity_type = delivery в поле entity_id прорастает order_id, а на delivery_id

{% endnote %}

### Обратная сверка

Выбираем данные из Маркет Биллинга:
- payment_order_draft.transaction_date в нужном периоде
- org_id = 64554

К этим данным джойним данные из Чекаутера. При этом при выборке данных из Чекаутера действуют _похожие_ фильтры, что и для прямой сверки, а именно:
- флаг mbi_control_enabled = true
- payment заказа в статусе CLEARED/refund заказа в статусе SUCCESS
- payment_goal в списке (ORDER_PREPAY, SUBSIDY, ORDER_POSTPAY, TINKOFF_CREDIT, VIRTUAL_BNPL, TINKOFF_CESSION)
- ~~заказ перешел в статус (был в статусе) DELIVERED в нужном периоде~~
- supplier_id **not in** 1p (465852, 431782, 2652811)

Отличие только в отсутствии проверки перехода заказа в статус DELIVERED.

{% endcut %}

## Драфты Маркет Биллинга <-> Команды на выплату Маркет Биллинга

{% cut "" %}

В этой сверке хотим сравнить драфты команд на выплату со стороны Маркет Биллинга и команды на выплату со стороны Маркет Биллинга.

Текущий вариант сверки-импорта в Чекере:

Название |                                        Описание                                        |                                                       Ссылка                                                       | Расписание
:---: |:--------------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------:| :---:
Payment_Order_Draft_Payment_Order_dashboard | Ежедневная сверка выплат за все время Драфтов команд на выплату с Командами на выплату | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=521&schedulerTypeForCardView=IMPORT) | 0 0 6 * * ? *

Обработка результатов в виде YQL-запроса - [Payment_Order_Draft_Payment_Order_dashboard_Result](https://yql.yandex-team.ru/Operations/YoNNEbq3k_ZYD3qKYARTW66jUYEtVvzX93Rs4v8TQhg=)

### Откуда читаем:

- [//home/market/production/billing/dictionaries/payment_order_draft/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/payment_order_draft/latest) - драфты команд на выплату
- [//home/market/production/billing/dictionaries/payout_group_payment_order/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/payout_group_payment_order/latest) - связь групп выплат с командами на выплату
- [//home/market/production/billing/dictionaries/payment_order/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/payment_order/latest) - команды на выплату

### Куда пишем:

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/payment_order_draft_left_payment_order](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/payment_order_draft_left_payment_order) - результат прямой сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
amount | int64 | сумма в копейках
client_id | int64 | id клиента в Балансе
contract_id | int64 | id контракта в Балансе
currency | string | валюта
max_transaction_date | string | max(дата, за которую собран драфт)
paysys_type_cc | string | тип платёжной системы
product | string | тип продукта
service_id | int64 | id сервиса в Балансе

{% endcut %}

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/payment_order_draft_right_payment_order](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/payment_order_draft_right_payment_order) - результат обратной сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
amount | int64 | сумма в копейках
client_id | int64 | id клиента в Балансе
contract_id | int64 | id контракта в Балансе
currency | string | валюта
is_problem_row | boolean | флаг, является ли строка _проблемной_
org_id | int64 | Операционная единица, через которую осуществляется работа
payment_order_id | int64 | id команды на выплату
paysys_type_cc | string | тип платёжной системы
product | string | тип продукта
service_id | int64 | id сервиса в Балансе
trantime | string | время события

{% endcut %}

### Прямая сверка

Чтобы понять, что конкретный драфт не попал в команду, сверка не нужна. В выгрузке драфтов уже есть поле-флаг, которое это показывает.
Сверка же нужна для объяснения, почему какого-то драфта нет в команде. При этом сами драфты не перекладываются один в один в команды. Они сначала группируются по нескольким полям. Если мы хотим драфты сравнить с командами, то нужно сделать точно такую жу группировку тех драфтов, которые не попали в команду в настоящий момент, и сравнивать уже именно их.

#### Как формируется выгрузка

Выбираем драфты команд на выплату:
- org_id = 64554
- дата драфта до начала текущего месяца

{% note info "Почему такой фильтр по дате" %}

Драфты собираются в команду в зависимости от расписания. Самое общее расписание - раз в месяц, поэтому сверять нужно именно то, что могло теоретически попасть в команду.

{% endnote %}

К этим данным делаем join команд на выплату через таблицу связи групп выплат к командам на выплату и оставляем только те записи, где нет команд на выплату. Оставшиеся записи группируем в разрезе client_id, contract_id, service_id, product, paysys_type_cc, currency, org_id (драфты схлопываются в команды именно по этим полям).

{% note info "Почему нет ограничения на дату снизу" %}

- необработанные драфты (не попавшие в команду на выплату) пытаются обработаться в каждую попытку формирования команд на выплату. И так будет до тех пор, пока драфт не обработается.

{% endnote %}

#### Что показывает выгрузка

Выгрузка показывает, какие должны были быть команды на выплату, но их нет по одной из причин:
- отрицательная или нулевая сумма драфтов - команда на выплату формируется только если сумма драфтов строго больше 0
- отсутствие активных контрактов у клиента
- payout приехал "задним" числом - обработали позже, чем должны были. Например, просыпали и перезабрали

### Обратная сверка

Выбираем команды на выплату:
- org_id = 64554
- payment_order.trantime в нужном периоде

К этим данным делаем join драфтов команд через таблицу связи групп выплат в командам на выплату и делаем union записей, у которых нет драфтов - в итоговой выгрузке is_problem_row = true, и записи, у которых есть драфты - is_problem_row = false. Это нудно для возможности посчитать общую сумму команд на выплату за период.

{% endcut %}

## Команды на выплату Маркет Биллинга <-> Команды на выплату OEBS

{% cut "" %}

В этой сверке хотим сравнить команды на выплату со стороны Маркет Биллинга и команды на выплаты со стороны OEBS.

Текущий вариант сверки-импорта в Чекере

Название |                                                                                     Описание                                                                                     |                                                       Ссылка                                                       | Расписание
:---: |:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------:| :---:
Payment_Order_Oebs_dashboard | Ежедневная сверка выплат за все время Команд на выплату с OEBS | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=520&schedulerTypeForCardView=IMPORT) | 0 0 6 * * ? *

Обработка результатов в виде YQL-запроса - [Payment_Order_Oebs_dashboard_Result](https://yql.yandex-team.ru/Operations/YoNRJq5OD-gvU6zBhHAQ8MnSuN5_RlQoqJTCSv48EYE=)

### Откуда читаем:

- [//home/market/production/billing/dictionaries/payment_order/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/billing/dictionaries/payment_order/latest) - команды на выплату
- [//home/bi/stable/dwh/outbox/external/oebs_oracle/XXYA/XXAP_AGENT_REWARD_DATA/MARKET/XXAP_AGENT_REWARD_DATA](https://yt.yandex-team.ru/hahn/navigation?path=//home/bi/stable/dwh/outbox/external/oebs_oracle/XXYA/XXAP_AGENT_REWARD_DATA/MARKET/XXAP_AGENT_REWARD_DATA)
- [//home/bi/stable/dwh/outbox/external/oebs_oracle/OKE/OKE_K_HEADERS/MARKET/OKE_K_HEADERS](https://yt.yandex-team.ru/hahn/navigation?path=//home/bi/stable/dwh/outbox/external/oebs_oracle/OKE/OKE_K_HEADERS/MARKET/OKE_K_HEADERS)

### Куда пишем:

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/market_billing_payment_order_left_oebs](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/market_billing_payment_order_left_oebs) - результат прямой сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
ard_agent_type_code | string | agent_type_code из таблиц oebs
ard_amount | double | сумма команды на выплату в копейках из таблиц oebs
ard_contract_id | int64 | id контракта в Балансе из таблиц oebs
ard_creation_date | string | creation_date из таблиц oebs
ard_k_alias | string | номер договра в балансе из таблиц oebs
ard_k_header_id | int64 | k_header_id из таблиц oebs
ard_org_id | int64 | Операционная единица, через которую осуществляется работа из таблиц oebs
ard_payment_order_id | int64 | распарсенный id команды на выплату из service_order_id из таблиц oebs
ard_paysys_type_id | int64 | paysys_type_id из таблиц oebs
ard_service_order_id | string | service_order_id из таблиц oebs
ard_transaction_type | string | transaction_type из таблиц oebs
po_amount | int64 | сумма команды на выплату в копейках из таблиц маркет биллинга
po_client_id | int64 | id клиента в Балансе из таблиц маркет биллинга
po_contract_id | int64 | id контракта в Балансе из таблиц маркет биллинга
po_org_id | int64 | Операционная единица, через которую осуществляется работа из таблиц маркет биллинга
po_payment_order_id | int64 | id команды на выплату из таблиц маркет биллинга
po_service_id | int64 | id сервиса в Балансе (609/610) из таблиц маркет биллинга
po_transaction_type | string | Платеж или рефанд  из таблиц маркет биллинга
po_trantime | string | Время события из таблиц маркет биллинга

Поля, начинающиеся на префикс _ard__ относятся к таблицам OEBS; на префикс _po__ относятся к таблицам Маркет Биллинга. Т.к. это прямая сверка Market Billing Left Join OEBS, то поля из таблиц oebs могут быть null. Это значит, что нет данных в OEBS

{% endcut %}

- [//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/market_billing_payment_order_right_oebs](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/mbi/mbi_checker/payment_control/payout/dashboard/market_billing_payment_order_right_oebs) - результат обратной сверки

{% cut "Описание полей выгрузки" %}

Название | Тип | Описание
:--- | :---: | :---
ard_agent_type_code | string | agent_type_code из таблиц oebs
ard_amount | double | сумма команды на выплату в копейках из таблиц oebs
ard_contract_id | int64 | id контракта в Балансе из таблиц oebs
ard_creation_date | string | creation_date из таблиц oebs
ard_k_alias | string | номер договра в балансе из таблиц oebs
ard_k_header_id | int64 | k_header_id из таблиц oebs
ard_org_id | int64 | Операционная единица, через которую осуществляется работа из таблиц oebs
ard_payment_order_id | int64 | распарсенный id команды на выплату из service_order_id из таблиц oebs
ard_paysys_type_id | int64 | paysys_type_id из таблиц oebs
ard_service_order_id | string | service_order_id из таблиц oebs
ard_transaction_type | string | transaction_type из таблиц oebs
po_amount | int64 | сумма команды на выплату в копейках из таблиц маркет биллинга
po_client_id | int64 | id клиента в Балансе из таблиц маркет биллинга
po_contract_id | int64 | id контракта в Балансе из таблиц маркет биллинга
po_org_id | int64 | Операционная единица, через которую осуществляется работа из таблиц маркет биллинга
po_payment_order_id | int64 | id команды на выплату из таблиц маркет биллинга
po_service_id | int64 | id сервиса в Балансе (609/610) из таблиц маркет биллинга
po_transaction_type | string | Платеж или рефанд  из таблиц маркет биллинга
po_trantime | string | Время события из таблиц маркет биллинга

Поля, начинающиеся на префикс _ard__ относятся к таблицам OEBS; на префикс _po__ относятся к таблицам Маркет Биллинга. Т.к. это обратная сверка Market Billing Right Join OEBS, то поля из таблиц market billing могут быть null. Это значит, что нет данных в Market Billing.

{% endcut %}

### Прямая сверка

К командам на выплату с фильтрами:
- payment_order в нужном периоде
- org_id = 64554
- client_id <> market_client_id 1p (39989801)

через service_transaction_id джойним данные из OEBS (в ard поле SERVICE_ORDER_ID).

### Обратная сверка

К данным из OEBS с фильтрами:
- ard.CREATION_DATE в нужном периоде
- org_id = 64554
- ard.AGENT_TYPE_CODE in ('MARKETPAYSBLUE_PAY', 'MARKETPLACEBLUE')
- SERVICE_ORDER_ID like 'payment-order-%'

через SERVICE_ORDER_ID джойним транзакционной лог доходного сервиса (поле service_transaction_id) с фильтрацией записей для 1p магазина (client_id <> 39989801).

{% endcut %}

## Результаты

{% cut "" %}

### Сверки в Чекере

Вся деятельность выше родилась из потребности на ежемесячной основе проводить сверку выплат. Чтобы по итогу создавался тикет (или тикеты), куда будут призываться люди, которые будут анализировать результаты сверок.
Получились следующие сверки в Чекере:

Название | Описание                                                   |                                                      Ссылка                                                       | Расписание
:--- |:-----------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------:| :---:
Checkouter_Payout_monthly | Ежемесячная сверка выплат Чекаутера с Маркет Биллингом | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=533&schedulerTypeForCardView=CHECK) | 0 0 8 3 * ? *
Payout_Checkouter_monthly | Ежемесячная сверка выплат Маркет Биллинга c Чекаутером | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=534&schedulerTypeForCardView=CHECK) | 0 0 8 3 * ? *
Payment_Order_Draft_Payment_Order_monthly | Ежемесячная сверка Драфтов команд на выплату с Командами на выплату | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=510&schedulerTypeForCardView=CHECK) | 0 0 8 3 * ? *
Payment_Order_Oebs_monthly | Ежемесячная сверка Команд на выплату с OEBS | [link](https://billing-admin.market.yandex.ru/checkers?schedulerIdForCardView=509&schedulerTypeForCardView=CHECK) | 0 0 8 3 * ? *

Сверки запускаются 3 числа в 8 утра за предыдущий месяц. По итогу получается тикет, в который призываются люди для анализа расхождений.

### Дашборд

Выгрузки с результатами сверок, конечно, хорошо, но не очень наглядно. Поэтому появился дашборд в DataLens с подробными результатами. Дашброд строится на основе сверок-импортов в Чекере выше.

Ссылка на дашборд в DataLens с результатами сверки - [CPOD_dashboard](https://datalens.yandex-team.ru/ya3ybcnnqflsq-cpod-dashboard?tab=WOg)

#### Описание дашборда

Название представляет собой ~~попытку~~ акронима:
- **C**heckouter
- **P**ayout
- **O**EBS
- **D**raft

Сам дашборд разбит на 5 вкладок:
- Общая сводка
- Чекаутер LEFT JOIN Маркет Биллинг Draft
- Маркет Биллинг Draft LEFT JOIN Чекаутер
- Маркет Биллинг Draft JOIN Маркет Биллинг Payment Order
- Маркет Биллинг JOIN OEBS

{% list tabs %}

- Общая сводка

  На вкладке собрана общая информация со всех остальных вкладок. Важно отметить, что это не исчерпывающая информация. То есть, если на этой вкладке будет расхождение 0 между какими-то системами, это не будет означать, что расхождений совсем нет. Надо перейти на интересующую вкладку и посмотреть результат сверки там.

  На этой вкладке можно увидеть:
  - Общая сумма payout в Чекаутере _- данные из Чекаутера из прямой сверки_
  - Общая сумма payout недоехавших до МБ _- данные из Чекаутера, отсутствующие в Маркет Биллинге, из прямой сверки_
  - Общая сумма проблемных payout между МБ и Чекаутером _- данные из Маркет Биллинга, отсутствующие в Чекаутере, из обратной сверки_
  - Общая сумма команд на выплату в Маркет Биллинге _- данные Команд на выплату Маркет Биллинга из обратной сверки с Драфтами Маркет Биллинга_
  - Общая сумма несформированных команд на выплату _- данные Драфтов Маркет Биллинга из прямой сверки с Командами на выплату Маркет Биллинга_
  - Общая сумма payout в OEBS _- данные из OEBS из обратной сверки с Маркет Биллингом_
  - Общая сумма payout недоехавших до OEBS _- данные из Маркет Биллинга, отсутствующие в OEBS, из прямой сверки_

  Также на вкладке присутствуют фильтры для выборки диапазона периода сверки и максимальные и минимальные даты записей в сверках. По умолчанию они не заполнены, т.е. период, который отображается при пустых фильтрах, является максимальным периодом сверки.

  Как интерпретировать информацию, на какие числа в первую очередь обращать внимание?
  - суммы, выделенные зеленым цветом: _общая сумма в Чекаутере, сумма команд на выплату в Маркет Биллинге и общая сумма в OEBS_, **не** стоит сравнивать между собой. Они скорее приведены для масштаба
  - в первую очередь стоит смотреть на суммы, выделенные красным цветом. В идеале они должны равняться 0

- Чекаутер LEFT JOIN МБ Draft

  На вкладке представлены подробные результаты **прямой сверки** выплат между Чекаутером и Драфтами Маркет Биллинга. Помимо периода сверки по payment-ам(_min(payment_transaction_date) и max(payment_transaction_date)_), периода сверки по refund-ам(_min(refund_transation_date) и max(refund_transation_date)_), данные представлены в виде таблиц
  - Нет данных в Маркет Биллинге. Группировка по типу и сервису _- сгруппированные данные из Чекаутера, отсутствующие в Маркет Биллинге. В таблице представлена как сумма в рублях, так и количество записей сверки_
  - Отличающиеся суммы. Группировка по типу и сервису _- сгруппированные пересекающиеся выплаты из Чекаутера и Маркет Биллинга, у которых отличаются суммы_
  - Общие данные. Группировка по типу и сервису _- сгруппированные общие выплаты из Чекаутера и Маркет Биллинга_
  - Нет данных в Маркет Биллинге. Группировка по партнеру _- сгруппированные данные по партнеру из Чекаутера, отсутствующие в Маркет Биллинге. В таблице приведена сумма в рублях и количество отсутствующих записей_
  - Нет данных в Маркет Биллинге _- все данные по всем выплатам Чекаутера, отсутствующим в Маркет Биллинге, из прямой сверки_
  - Разные суммы _- все данные по всем пересекающимся выплатам из Чекаутера и Маркет Биллинга, у которых отличаются суммы_

  графиков
  - Нет данных в Маркет Биллинге. Суммы по status_updated _- суммы выплат Чекатера, отсутствующих в Маркет Биллинге, из прямой сверки, сгруппированной по дате обновления статуса payment-а/refund-а_
  - Нет данных в Маркет Биллинге. Суммы по delivery_date _- суммы выплат Чекатера, отсутствующих в Маркет Биллинге, из прямой сверки, сгруппированной по дате перехода заказа в статус DELIVERED_

  фильтров
  - payment_transaction_date _- фильтр по дате перехода в статус DELIVERED payment-ов в Чекаутере_
  - refund_transaction_date _- фильтр по дате перехода в статус DELIVERED refund-ов в Чекаутере_
  - partner_id _- фильтр по id партнера_
  - order_id _- фильтр по id заказа_
  - entity_id _- фильтр по id товара/id доставки_
  - entity_type _- фильтр по item/delivery_
  - checkouter_type _- фильтр по payment/refund_
  - checkouter_id _- фильтр по id payment-а/refund-а_
  - service_id _- фильтр по id сервиса в Балансе_
  - payment_goal _- фильтр по типу платежа из Чекаутера_
  - paysys_type_cc _- фильтр по типу платежной системы из Чекаутера_

- МБ Draft LEFT JOIN Чекаутер

  На вкладке представлены подробные результаты **обратной сверки** выплат между Чекаутером и Драфтами Маркет Биллинга. Помимо периода сверки по payment-ам(_min(payment_transaction_date) и max(payment_transaction_date)_), периода сверки по refund-ам(_min(refund_transation_date) и max(refund_transation_date)_), данные представлены в виде таблиц
  - Нет данных в Чекаутере. Группировка по типу и сервису _- сгруппированные данные из Маркет Биллинга, отсутствующие в Чекаутере. В таблице представлена как сумма в рублях, так и количество записей сверки_
  - Отличающиеся суммы. Группировка по типу и сервису _- сгруппированные пересекающиеся выплаты из Чекаутера и Маркет Биллинга, у которых отличаются суммы_
  - Общие данные. Группировка по типу и сервису _- сгруппированные общие выплаты из Чекаутера и Маркет Биллинга_
  - Нет данных в Чекаутере. Группировка по партнеру _- сгруппированные данные по партнеру из Маркет Биллинга, отсутствующие в Чекаутере. В таблице приведена сумма в рублях и количество отсутствующих записей_
  - Нет данных в Чекаутере _- все данные по всем выплатам Маркет Биллинга, отсутствующим в Чекаутере, из прямой сверки_
  - Разные суммы _- все данные по всем пересекающимся выплатам из Чекаутера и Маркет Биллинга, у которых отличаются суммы_

  графиков
  - Нет данных в Чекаутере. Суммы по transaction_date _- суммы выплат Маркет Биллинга, отсутствующих в Чекаутере, из обратной сверки, сгруппированной по времени сбора в драфт выплат_
  - Общие данные. Суммы по transaction_date _- суммы пересекающихся выплат Маркет Биллинга и Чекаутера, из обратной сверки, сгруппированной по времени сбора в драфт выплат_

  фильтров
  - transaction_date _- фильтр по дате сбора в драфт выплат в Маркет Биллинге_
  - partner_id _- фильтр по id партнера_
  - order_id _- фильтр по id заказа_
  - entity_id _- фильтр по id товара/id доставки_
  - entity_type _- фильтр по item/delivery_
  - checkouter_id _- фильтр по id payment-а/refund-а_
  - checkouter_type _- фильтр по payment/refund_
  - paysys_type_cc _- фильтр по типу платежной системы выплаты Маркет Биллинга_
  - service_id _- фильтр по id сервиса в Балансе_
  - product _- фильтр по продукту выплаты Маркет Баллинга_

- МБ Draft JOIN МБ Payment Order

  На вкладке представлены подробные результаты как **прямой** так и **обратной** сверок выплат между Драфтами Маркет Биллинга и Командами на выплату Маркет Биллинга.

  Результаты прямой сверки представлены в виде периода сверки (_min(transaction_date) и max(transaction_date)_), общей суммы несформированных команд на выплату, общей суммы команд на выплату в Маркет Биллинге, а также таблиц
  - Команды на выплату. Нет данных. Потенциальные команды на выплату _- сгруппированные записи Драфтов Маркет Биллинга, которые потенциально могут стать командой на выплату (сумма > 0) из прямой сверки_
  - Команды на выплату. Нет данных. Группировка по client_id, contract_id _- сгруппированные данные записей Драфтов маркет Биллинга, которые могут стать командой на выплату (сумма > 0) по клиенту и контракту из прямой сверки_
  - Команды на выплату. Нет данных. Все записи _- все сгруппированные записи Драфтов Маркет Биллинга, которые не стали командой на выплату из прямой сверки_
  - Драфты команд на выплату. Нет данных _- все записи Команд на выплату, для которых нет Драфтов из обратной сверки_

  графиков
  - Команды на выплату. Нет данных. Потенциальные команды на выплату _- сгруппированные записи Драфтов Маркет Биллинга, которые потенциально могут стать командой на выплату (сумма > 0) из прямой сверки по дате последнего драфта_
  - Команды на выплату по trantime _- суммы сформированных Команд на выплату по дате события команды на выплату из обратной сверки_

  фильтров
  - trantime для суммы команд на выплату _- время события команды на выплату_
  - transaction_date _- максимальная дата сбора выплат в драфт_
  - client_id _- фильтр по id клиента_
  - contract_id _- фильтр по id контракта_
  - paysys_type_cc _- фильтр по типу платежной система в Маркет Биллинге_
  - service_id _- фильтр по id сервиса в Балансе_

- МБ JOIN OEBS

  На вкладке представлены подробные результаты как **прямой** так и **обратной** сверок выплат между Командами на выплату Маркет Биллинга и OEBS.

  Результаты сверой представлены в виде периода сверки (_min(oebs_creation_date) и max(oebs_creation_date)_) из обратной сверки, общей суммы payout в OEBS за этот период из обратной сверки, общей суммы payout недоехавших до OEBS из прямой сверки, а также таблиц
  - Маркет Биллинг LEFT JOIN OEBS. Общие данные. Отличающиеся суммы _- все данные по всем пересекающимся выплатам Команд Маркет Биллинга и OEBS, у которых отличаются суммы, из прямой сверки_
  - Маркет Биллинг RIGHT JOIN OEBS. Общие данные. Отличающиеся суммы _- все данные по всем пересекающимся выплатам Команд Маркет Биллинга и OEBS, у которых отличаются суммы, из обратной сверки_
  - Маркет Биллинг RIGHT JOIN OEBS. Нет данных в Маркет Биллинг _- все данные по всем выплатам OEBS, отсутствующими в Командах Маркет Биллинга, из обратной сверки_
  - Маркет Биллинг Tlog JOIN OEBS. Нет данных в OEBS _- все данные по всем выплатам Команд Маркет Биллинга, отсутствующими в OEBS, из прямой сверки_

  графика
  - Общие данные. Суммы в OEBS по creation_date _- суммы выплат из OEBS по дате creation_date из обратной сверки_

  фильтра
  - oebs_creation_date _- фильтр по дате creation_date из OEBS_

{% endlist %}

{% endcut %}
