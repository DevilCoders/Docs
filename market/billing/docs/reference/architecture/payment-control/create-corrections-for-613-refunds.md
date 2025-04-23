# Создание корректировок возвратов по 613 сервису

## Описание корректировок
Возвраты по 613 сервису — это возвраты по постоплатным или кредитным платежам. Необходимость проводить корректировки возникает в том случае, если возврат был проведён дважды: один раз в рамках Управления выплатами и второй раз в Балансе в рамках старой логики. При этом у возврата, созданного в рамках УВ, неправильное значение поля `paysys_type_cc`. Поэтому для того, чтобы вернуть партнёру излишне удержанные деньги и привести в норму отчётность, для каждого такого возврата мы создаём две корректировки:
1. Корректировка начисления (запись в таблице PG `market_billing.accrual_correction`). Эта корректировка позволяет убрать из отчётности возврат с неправильным `paysys_type`.
2. Корректировка выплаты (запись в таблице PG `market_billing.payout_correction`). Эта корректировка компенсирует лишнее удержание денег с партнёра.

## Общий алгоритм проведения корректировок
1. Запускаем в YT запрос для расчёта данных корректировок ([запрос тут](https://yql.yandex-team.ru/Operations/YkQ8OQVK8B0VjR4OaoJNK_j92t72H8Nay8bljX6-HOg=)). Если корректировка проводится по заранее известным заказам, то этот пункт можно пропустить.
2. Создаём тикет на расчёт корректировок, сохраняем в него запрос, количество корректировок, общую сумму и разбивку суммы по `paysys_type_cc` ([пример тикета](https://st.yandex-team.ru/MARKETBILLING-3302)).
3. Создаём тикет на согласование корректировок, прикапываем туда данные из предыдущего пункта, призываем согласующих ([пример тикета](https://st.yandex-team.ru/MARKETBILLING-3303)). В зависимости от суммы корректировок возможны два варианта согласующих. Подробнее в [регламенте](https://docs.yandex-team.ru/market-billing/regulations/corrections).
4. Создаём ПР с сохранением во временной таблице БД данных корректировок ([пример ПР'а](https://a.yandex-team.ru/review/2427009)).
5. Запускаем в YT запрос с валидацией рассчитанных данных корректировок ([запрос тут](https://yql.yandex-team.ru/Operations/YkWMn5fFt4slUYAumS2-Tk3hh4NA1SbEFfTucpcUvHY=)).
6. В случае выплаты корректировок вне расписания создаём ПР'ы на добавление и удаление 2 числа во все расписания выплат ([пример ПР'а на добавление](https://a.yandex-team.ru/review/2340987) и [пример ПР'а на удаление](https://a.yandex-team.ru/review/2344528)).
7. Создаём ПР с переливкой данных корректировок из временной таблицы в таблицы `accrual_correction` и `payout_correction`, исключая корректировки, которые не прошли валидацию ([пример ПР'а](https://a.yandex-team.ru/review/2427519)).
8. Выкладываем корректировки в прод по одному из планов (см. ниже), в зависимости от того, должны ли корректировки выплатиться по расписанию или вне его ([пример тикета с выплатой по расписанию](https://st.yandex-team.ru/MARKETBILLING-3027), [пример тикета с выплатой вне расписания](https://st.yandex-team.ru/MARKETBILLING-2718)).

Далее более подробно рассмотрены некоторые из шагов.

## Расчёт данных для корректировок
При расчёте новых корректировок необходимо отфильтровать ранее проведённые корректировки. Для этого в YQL-запросе надо сохранить в файл список проведённых корректировок, получить которые можно запросом:
```sql
select
    ac.partner_id,
    ac.checkouter_id,
    ac.transaction_type,
    ac.order_id,
    ac.entity_id,
    ac.entity_type,
    ac.paysys_type_cc,
    ac.amount / 100.0 amount_rub,
    date(ac.trantime) correction_date
from market_billing.accrual_correction ac
where ac.st_ticket in (
    'MARKETBILLING-1850', 'MARKETBILLING-1851', 'MARKETBILLING-1852', 'MARKETBILLING-2058', -- итерация 1
    'MARKETBILLING-2120',                                                                   -- итерация 2
    'MARKETBILLING-2242',                                                                   -- итерация 3
    'MARKETBILLING-2243',                                                                   -- итерация 4
    'MARKETBILLING-2509',                                                                   -- итерация 5
    'MARKETBILLING-2717',                                                                   -- итерация 6
    'MARKETBILLING-2872',                                                                   -- итерация 7
    'MARKETBILLING-2929', 'MARKETBILLING-3026', 'MARKETBILLING-3064',                       -- итерация 8
    'MARKETBILLING-3254',                                                                   -- итерация 9
    'MARKETBILLING-3312'                                                                    -- итерация 10
)
order by ac.partner_id, ac.order_id, ac.entity_id;
```

## Валидация корректировок
Для валидации необходимо в YQL-запросе сохранить в файл рассчитанные данные корректировок.

## Создание корректировок из временной таблицы
Для `accrual_correction` поле `transaction_type` должно быть равно `'refund'`, `checkouter_id` — `id` возврата, `amount` — отрицательной сумме возврата.

Для `payout_correction` поле `transaction_type` должно быть равно `'payment'`, `checkouter_id` — `id` платежа, по которому проведён возврат, `amount` — положительной сумме возврата.

Для поля `trantime` в качестве даты указывается первое число месяца, в котором проводятся корректировки. Время значения не имеет, но по устоявшейся традиции принято указывать 15:00. Таким образом для корректировок, проводимых в апреле 2022 года, значение поля `trantime` будет `2022-04-01 15:00:00`.

Остальные поля корректировок (`order_id`, `entity_id`, `entity_type`, `product`, `currency`, `org_id`) совпадают с полями в возврате из таблицы PG `market_billing.accrual`.

## Выкладывание корректировок в прод
Есть два плана в зависимости от того, должны ли выплаты произойти в рамках расписания выплат для каждого из партнёров или вне его.

### План для выкладывания в рамках расписания выплат
1. Дожидаемся согласования в тикете на согласование корректировок *(п. 2 в алгоритме)*.
2. Ждём валидации корректировок с ARD *(п. 5 в алгоритме)*.
3. В чате службы просим всех не выкатывать релизы `market-billing-tms` и `market-billing-db`.
4. Оповещаем дежурного, что будем отключать джобы для УВ и возможно загорание мониторингов.
5. Выключаем сбор тлогов `payments_payouts_transaction_log` и `expenses_payouts_transaction_log`.
*Для этого надо установить переменную `market.billing.tms.payouts.tlog.collect` в `false`, выполнив на любой продовой машине `merket-billing-tms` в `tms`-консоли команду `env set market.billing.tms.payouts.tlog.collect false`.*
6. Выключаем работу джоб, которые собирают черновики команд на выплату (`paymentOrderDraftExecutor`) и сами команды (`paymentOrderFromDraftExecutor`) *(устанавливаем в `false` переменную `mbi.billing.payment.order.draft.enabled`)*.
7. Мёрджим и катим в прод ПР с корректировками *(из п. 7 алгоритма)*.
8. Проверяем запросами данные, которые создала миграция.
9. Включаем работу джоб, которые собирают черновики команд на выплату (`paymentOrderDraftExecutor`) и сами команды (`paymentOrderFromDraftExecutor`) *(устанавливаем в `true` переменную `mbi.billing.payment.order.draft.enabled`)*.
10. Включаем сбор тлогов `payments_payouts_transaction_log` и `expenses_payouts_transaction_log` *(устанавливаем в `true` переменную `mbi.billing.payment.order.draft.enabled`)*.
11. Оповещаем всех в чате службы, что работы закончены.
12. На следующий день утром смотрим, что корректировки доехали до тлога.
13. Через день запускаем запрос валидации корректировок, чтобы убедиться, что суммы по скорректированным заказам в ARD и Чекаутере совпадают.

### План для выкладывания вне расписания выплат
1. Дожидаемся согласования в тикете на согласование корректировок *(п. 2 в алгоритме)*.
2. Ждём валидации корректировок с ARD *(п. 5 в алгоритме)*.
3. В чате службы просим всех не выкатывать релизы `market-billing-tms` и `market-billing-db`.
4. Оповещаем дежурного, что будем отключать джобы для УВ и возможно загорание мониторингов.
5. Выключаем сбор тлогов `payments_payouts_transaction_log` и `expenses_payouts_transaction_log`.
   *Для этого надо установить переменную `market.billing.tms.payouts.tlog.collect` в `false`, выполнив на любой продовой машине `merket-billing-tms` в `tms`-консоли команду `env set market.billing.tms.payouts.tlog.collect false`.*
6. Выключаем работу джоб, которые собирают черновики команд на выплату (`paymentOrderDraftExecutor`) и сами команды (`paymentOrderFromDraftExecutor`) *(устанавливаем в `false` переменную `mbi.billing.payment.order.draft.enabled`)*.
7. Мёрджим и катим в прод ПР с добавлением в расписание выплат 2 числа *(из п. 6 алгоритма)*.
8. Мёрджим и катим в прод ПР с корректировками *(из п. 7 алгоритма)*.
9. Проверяем запросами данные, которые создала миграция.
10. Включаем работу джоб, которые собирают черновики команд на выплату (`paymentOrderDraftExecutor`) и сами команды (`paymentOrderFromDraftExecutor`) *(устанавливаем в `true` переменную `mbi.billing.payment.order.draft.enabled`)*.
11. Запускаем джобу сбора черновиков *(командой `tms-run paymentOrderDraftExecutor` в `tms`-консоли `market-billing-tms`)*.
12. Ждём, когда созданные `payout_correction` соберутся в черновики. *Проверить можно запросом:*
```sql
select
    count(pc.entity_id) as total_corrections_count,
    count(pc.payout_group_id) as drafted_corrections_count
from market_billing.payout_correction pc
where pc.st_ticket = 'MARKETBILLING-3312'; -- здесь указываем тикет для создаваемых корректировок
```
13. Запрещаем джобе `paymentOrderFromDraftExecutor` обрабатывать дни подряд *(устанавливаем в `true` переменную `market.billing.payment-order-from-draft-executor.stop-after-day-processed`)*.
14. Записываем предыдущую дату в джобе `paymentOrderFromDraftExecutor` *(получить её можно `tms`-командой `env get market.billing.payment-order-from-draft-executor.date-to-collect`)*.
15. Выставляем дату обработки в джобе `paymentOrderFromDraftExecutor` в первый день месяца *(устанавливаем переменную `market.billing.payment-order-from-draft-executor.date-to-collect`)*.
16. Запускаем джобу `paymentOrderFromDraftExecutor` *(командой `tms-run paymentOrderFromDraftExecutor` в `tms-`консоли `market-billing-tms`)*.
17. Ждём, пока отработает джоба *(в кварц-логе значение поля `job_status` равно `OK` для последнего запуска джобы `paymentOrderFromDraftExecutor`)*.
18. Проверяем, что для `payout_correction` создались команды на выплату.

   *Сделать это можно запросом:*
```sql
select
    count(pc.entity_id) as total_corrections_count,
    count(pgpo.payment_order_id) as collected_corrections_count
from market_billing.payout_correction pc
    left join market_billing.payout_group_payment_order pgpo on pgpo.payout_group_id = pc.payout_group_id
where pc.st_ticket = 'MARKETBILLING-3312'; -- здесь указываем тикет для создаваемых корректировок
```
19. Включаем сбор тлогов `payments_payouts_transaction_log` и `expenses_payouts_transaction_log` *(устанавливаем в `true` переменную `mbi.billing.payment.order.draft.enabled`)*.
20. Запускаем сбор в тлог *(командой `tms-run payoutsPaymentsTransactionLogCollectionExecutor` в `tms-`консоли `market-billing-tms`)*.
21. Ждём, пока соберётся тлог *(в кварц-логе значение поля `job_status` равно `OK` для последнего запуска джобы `payoutsPaymentsTransactionLogCollectionExecutor`)*.
22. Запускаем экспорт тлог в YT *(командой `tms-run paymentsPayoutsTransactionLogYtExportExecutor` в `tms-`консоли `market-billing-tms`)*.
23. Смотрим на записи в YT, селектим суммы.
24. Выставляем дату обработки в джобе `paymentOrderFromDraftExecutor` в дату, которая была до наших изменений *(устанавливаем переменную `market.billing.payment-order-from-draft-executor.date-to-collect`)*.
25. Разрешаем джобе `paymentOrderFromDraftExecutor` обрабатывать дни подряд *(устанавливаем в `false` переменную `market.billing.payment-order-from-draft-executor.stop-after-day-processed`)*.
26. Включаем ещё раз джобы, которые собирают черновики и команды на выплату (потому что джоба `paymentOrderFromDraftExecutor` при однократной работе сбросила переменную в `false`).
27. Оповещаем всех в чате службы, что работы закончены.
28. Мёрджим и катим в прод ПР с удалением из расписания выплат 2 числа *(из п. 6 алгоритма)*.
29. Через день запускаем запрос валидации корректировок, чтобы убедиться, что суммы по скорректированным заказам в ARD и Чекаутере совпадают.
