# Включение и выключение факторинга 

Включение и отключение производится telnet командой *change-contract-factor* в billing-tms, которая редактирует содержимое таблицы market_billing.client_factor в PG.

## Команда отключения в billing-tms
*change-contract-factor set --factor=market*

## Команда включения в billing-tms
Включаем для конкретных частот (bi-weekly остаётся не по факторингу):

*change-contract-factor set --factor=raiffeisen --frequency=weekly*

*change-contract-factor set --factor=raiffeisen --frequency=daily*

## Проверка
Результат работы команды можно проверить по содержимому таблицы market_billing.client_factor в PG.

При выключенном факторинге:

|income_contract_id|frequency|factor|
|----------|:-------------:|------:|
| NULL| bi-weekly |market|
| NULL| daily |market|
| NULL| weekly |market|


При включенном факторинге:

|income_contract_id|frequency|factor|
|----------|:-------------:|------:|
| NULL| bi-weekly |market|
| NULL| daily |raiffeisen|
| NULL| weekly |raiffeisen|
