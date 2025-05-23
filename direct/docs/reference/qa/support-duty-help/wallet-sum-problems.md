# Проблемы с остатком на счете

## Примеры проблем:

- изменилась сумма остатка, хотя никаких операций с кошельком (пополнения, клики) не было
- на кампании осталась какая-то сумма, хочется выкрутить её "в ноль"
- после каких-то операций (пополнения, клики) сумма остатка не та, которая ожидалась


## Немного теории:

### В базе
Остаток денежных средств на кампании - это разность между зачисленными на нее средствами (sum) и 
потраченными средствами (sum_spent). Оба значения [хранятся](https://jing.yandex-team.ru/files/sudar/10-03-22__18-13-29.png) 
в базе в таблице **campaigns**.

{% note warning %}

Оба значения хранятся с НДС, поэтому при перерасчетах на отображаемое значение в интерфейсе нужно это учитывать.

{% endnote %}

- Для клиентов без Общего счета остаток на каждой кампании равен разности между sum и sum_spent для этой кампании с учетом НДС. <br>
- Для Общего счета остаток равен разности между sum кампании-кошелька и всех sum_spent всех крутившихся кампаний с учетом НДС. <br>
То есть чтобы корректо рассчитать остаток средств на кошельке, нужно сначала просуммировать расходы на всех кампаниях.

### Получение значений

Сам Директ эти значения у себя не изменяет, только получает:
- sum получаем из Баланса методом *BalanceClient.NotifyOrder2*
- sum_spent получаем из БК методом *activeorders.ActiveOrdersImportJob*
- посмотреть CostCur, сколько откручено по данным БК. [Запрос](https://nda.ya.ru/t/tuUEZhS84rD8a4)

### Посмотреть изменения

Текущее значение этих полей можно посмотреть запросом в базу. Историю изменений можно посмотреть в logviewer в разделе *binlog_rows_fields_v2*
- [пример для sum](https://jing.yandex-team.ru/files/sudar/10-03-22__18-44-43.png)
- [пример для sum_spent](https://jing.yandex-team.ru/files/sudar/10-03-22__18-45-18.png)

### Возможные пути решения проблем:

- если денег на заказе стало больше, чем ожидалось, то проверить изменения sum_spent. С какой-то регулярностью БК "возвращает"
некорректные открутки и сумма на счету становится больше от этого. Можно заметить в logviewer, что в какой-то момент sum_spent
становится *меньше*.
- у нас присутсвует какая-то сумма, а Баланс утверждает, что у них всё откручено. Скорее всего, нужен тикет в Баланс (PAYSUP), 
чтобы они у себя проверили корректную цифру по откруткам. Как правило, в таких случаях сумма откруток у них и CostCur в БК
различаются. Необходимо, чтобы Баланс синхронизировал эту сумму с БК у себя. Директ в данном случае оперирует данными, 
которые получает из этих сервисов.
