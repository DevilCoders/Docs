## Разделение скидочного и плюсового кэшбэка

### Issue
У нас есть два вида кэшбэка - за счет сервиса (далее *скидочный*) и за счет пользователя (далее *пользовательский*).

Мы хотим передавать их в `/update/cashback` как две разные сущности.

### Как это работает сейчас

- в `universal_cashback_processing` мы вычисляем кэшбэк:
получаем отдельно скидочный кэшбэк (из `url` в 
[конфиге](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/CASHBACK_SERVICES)),
пользовательский кэшбэк (из инвойса от `transactions` в том же 
[конфиге](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/CASHBACK_SERVICES)),
и 
[складываем](https://github.yandex-team.ru/taxi/backend-py3/blob/develop/services/cashback/cashback/modules/cashback_services/module.py#L75)
 их, оперируя дальше одной суммой.

**дальнейший путь суммы кэшбэка**
1) передаем в `/v2/internal/cashback/register` в поле `cashback_sum`

2) создаем/обновляем заказ в `order_clears`, пишем полную сумму кэшбэка за заказ в `order_clears.cashback_sum`

3) если сумма кэшбэка обновилась, создаем событие в `events`, пишем полную сумму кэшбэка за заказ в `events.value`

4) в `cashback_charge_processing`:

- выбираем последнее событие из `events`

- получаем из инвойса `cashback.rewarded` - начисленный кэшбэк

- сравниваем уже начисленное с тем, что записано в `events.value`, если необходимо - отправляем новую сумму в `/update/cashback`


### Note
- Здесь мы рассматриваем только схему пополнения через `transactions`
- Сейчас у нас есть кэшбэк только в такси, и только пользовательский, этот факт можно использовать для плавного перехода. 

### Что предлагается изменить

1. В `/v2/internal/cashback/register` добавляем в request поле `cashback_by_source`:
```
"cashback_by_source": [
    {"value": "100.0000", "source": "user"}, 
  ]
``` 

кладем значения в `events.value` и `events.source`, соответственно, по отдельному ивенту на каждый источник.

2. `cashback.order_clears` - таблицу можно пока не детализировать, для функциональности 
(определить, изменилась ли сумма кэшбэка по сравнению с предыдущей версией) общей суммы достаточно. 
При желании, можно сделать это позже (тогда стоит не забыть про репликацию в YT). 

3. `cashback.events` - через нее мы передаем информацию в `cashback_charge_processing`, необходимо обновить.
Добавляем поле `source TEXT NOT NULL DEFAULT 'user'`. 
Таблица не реплицируется.

4. В `cashback_charge_processing` достаем из `events` ивенты по данному заказу 
(берем последние по каждому из источников) и формируем запрос в `/update/cashback` 
с разбиением по каждому виду кэшбэка.
Выпиливаем использование `v2/charge`.

5. В `universal_cashback_processing` передаем в `/v2/internal/cashback/register` разные типы кэшбэка как элементы массива `cashback_by_source`.



### Задачи (делать в таком порядке)
Добавить новое поле в `cashback.events`

Добавить новое поле в ответ ручки `/internal/events`

Доработки в `cashback_charge_processing`

Доработки в ручке `/v2/internal/cashback/register`

Доработки в `universal_cashback_processing`
