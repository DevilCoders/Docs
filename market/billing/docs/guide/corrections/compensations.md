# Проведение компенсаций

## Общее описание

Задача: хотят выплаты по претензиям проводить через биллинг.

Раньше это делали через поддержку баланса. Для поддержки в биллинге сделали механизм компенсаций.

Тикет: [FINPROJECTS-22](https://st.yandex-team.ru/FINPROJECTS-22)

## Техническое описание

Таблица Компенсаций по претензиям [`market_billing.claims_compensation`](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/claims_compensation.sql?rev=r9214736#L7).

| Колонка| Значение                                              |
| --- |-------------------------------------------------------|
| id | Идентификатор компенсации                             |
| partner_id | Идентификатор поставщика                              |
| trantime | Время события, к которому привязан момент компенсации |
| type | Тип компенсаций                                       |
| amount | Сумма, в копейках или центах, в валюте договора       |
| note | Комментарий                                           |
| login | Логин того, кто делал компенсацию                     |
| exported_to_tlog | Сохранено ли значение в транзакционный лог            |

#### Типы компенсации

- Претензия [CLAIM](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/compensation/CompensationType.kt?rev=r9244914#L13)
- Утеря или порча отправления/заказа [LOST](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/compensation/CompensationType.kt?rev=r9244914#L18)

Из таблицы [`market_billing.claims_compensation`](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/claims_compensation.sql?rev=r9214736#L7) строки перекладываются в тлог доходных сервисов
([`payments_payouts_transaction_log`](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/payments_payouts_transaction_log.sql?rev=r8821404#L4)),
где данные обогащаются `client_id`, `paysys_type_id`, `service_transaction_id`, `contrat_id`. При этом:
 - `paysys_type_id`
   - для `type` == `claim` - [YANDEX](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/payment/PaysysTypeCc.kt?rev=r9244914#L126)
   - для `type` == `lost` - [YANDEX_LOST](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/payment/PaysysTypeCc.kt?rev=r9244914#L131)
 - `service_transaction_id`
   - имеет вид `compensation-:id`

## Примеры проведения компенсаций

Первый тикет с компенсациями: [MARKETBILLING-3040](https://st.yandex-team.ru/MARKETBILLING-3040)

В тикете приложен файл с разбивкой Номер договора (external_id) - Сумма (amount).

* Вариант 1: Добавить в office макрос, принимающий тикет, тип компенсаций и логин и возвращающий в ячейках K10-K12 данные для миграции, добавить GETINSERTS в любую строчку
```vbnet
Function GETINSERTS(ticket As String, tp as String, login as String)
    Dim rowd As Integer
    Dim result, cell, insert, shop_id As String
    Dim amount As Double
   insertStr = "insert into market_billing.claims_compensation (partner_id, trantime, type, amount, note, login) values ("
    sheet = ThisComponent.Sheets(1)
    result = ""
    	For row = 1 to 10000
        	shop_id_cell = sheet.getCellByPosition(0, row)
			amount = (CDbl(sheet.getCellByPosition(1, row).value) * 100)
			if(shop_id_cell.value = "0") then
				GETINSERTS = ""
				sheet.getCellByPosition(10,10).String = result
				sheet.getCellByPosition(10,8).String =  "--liquibase formatted sql"
				sheet.getCellByPosition(10,9).String = "--changeset " & login & ":" & ticket & "-" & tp & "-compensations"
				Exit Function
			else
			result = result & insertStr	& shop_id_cell.value & ", '" & Format(Now, "YYYY-MM-DD") & "', '" & tp & "', " & amount & ", '" & ticket & "', '" & login & "'); "
			end if
		Next row
End Function

```

* Вариант 2: Средствами текстового редактора поиск строки/замена, можно сформировать строки вида shop_id-amount. Далее, sql запросом (с конкретным примером):
```sql
with data_from_excel as (
    select unnest(array [
        '583050-2542718'
        ]) str
),
     parse_data as (
         select split_part(str, '-', 1) shop_id, replace(split_part(str, '-', 2), ',', '.')::decimal * 100 amount
         from data_from_excel
     ),
     common_data as (
         select ', date ''2022-05-30'', ''claim'', '         as date_type,
                ', ''MARKETBILLING-4251'', ''phillippko'');' as note_login,
                pd.shop_id                                   as shop_id,
                pd.amount::int                               as amount
         from parse_data as pd),
     result as (
         select 'insert into market_billing.claims_compensation (partner_id, trantime, type, amount, note, login)
                     values (' || shop_id || date_type || amount || note_login
         from common_data
     )
select * from result;

```
можно сформировать insert-ы. Остается открыть пр, дождаться шипа и прокатить (не забываем про регламент [{#T}](../../regulations/corrections.md)).
