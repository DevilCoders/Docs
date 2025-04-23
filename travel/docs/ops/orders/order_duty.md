---
title: Дежурства по заказам
---

## График дежурств

Основной график — [тут](https://abc.yandex-team.ru/services/travelorchetsrator/duty/) (верхний блок)
Его зеркало, необходимое операторам, у которых нет доступа к ABC, поддерживается силами службы операторов [тут](https://wiki.yandex-team.ru/travel/hotels/product/operations/hotel-duty/#kalendardezhurstv)

Дежурный приступает к работе в 10:00 понедельника, информируя предыдущего дежурного сообщением в tg-канале `[Travel] Order Alers`.

{% note warning %}

Активный дежурный должен быть на готов ответить на телефонный звонок круглосуточно, 7 дней в неделю.  

{% endnote %}

## Обязанности дежурного

* Следить за работоспособностью сервиса заказов (orders-app) и api бронирования (orders-related часть в travel-api), реагируя на технические алерты о проблемах в этих компонентах;
* Реагировать на обнаруженные проблемы в заказах, падения заказных Workflow и тп. При невозможности устранить проблему своими силами, эскалировать на разработчиков вертикали или внешних сервисов, ответственных за проблемный заказ;
* Помогать операторам поддержки в решении нетиповых кейсов, требующих ручных правок в базе данных, выполнении специальных команд через CLI по [типовым рецептам](recipes) и тп.
* Модерировать (размечать) тарифные планы отелей на прямой продаже в соответствии с инструкцией.

{% note info}

Модерация тарифных планов — временная обязанность, в будущем ответственность за нее будет передана в контентную службу соответствующей вертикали.

{% endnote %}

## Каналы

### В телеграмме
* [Order Alerts](https://t.me/joinchat/CEnvnEwFRBYKJ7i6PY_J6Q) — алерты о проблемах в production-окружении
* [Order Alerts testing](https://t.me/joinchat/Co-lrkXE3VJCrGbM7C5MWQ) — алерты о проблемах в testing-окружении

### В слаке

* **#orders-notifications** в спейсе yndx-travel.slack.com — канал, в который оркестратор заказов отправялет сообщения об остановленных и упавших workflow

## Очереди в ST

* [TRAVELORDERSUP](https://st.yandex-team.ru/TRAVELORDERSUP) — очередь, где в автоматическом режиме создаются тикеты о проблемных заказах;
* [TRAVELSUP](https://st.yandex-team.ru/TRAVELSUP) — очередь для разбора заявок созданных звонками в коллцентр, через форму обратной связи, и тп.

### Работа с очередью TRAVELORDERSUP

Тикеты в этой очереди заводятся автоматически при обнаружении ошибок и проблем с заказами и проверяются операторами КЦ.
Для некоторых типов ошибок в тикет пишется явная инструкция с действиями для оператора.
В случае, если инструкции нет или в ней явно написано позвонить дежурному, оператор КЦ звонит дежурному. Если дежурный обнаруживает открытый тикет раньше и пишет в него фразу, явно сообщающую, что не надо звонить, оператор звонить не будет. Пример фразы: _"Разбираюсь с проблемой. Звонить не нужно."_
Если в ходе проверки проблемы обнуруживается баг или требуется какая-то доработка, необходимо завести связанный тикет в очереди разработки (TRAVELBACK/TRAVELFRONT и тп) и написать об этом комментарий. Если проблема в заказе вызвана известным багом/недоработкой, стоит  написать комментарий, сославшись на соответствующий тикет.

Если в процессе работы дежурный понимает, что оператору колл-центра необходимо что-то сообщить пользователю, необходимо в комментарии призывать [@avilchenkon](https://staff.yandex-team.ru/avilchenkon) и [@beloviktor](https://staff.yandex-team.ru/beloviktor). Это старшие операторы, они работают весь день и помогут скоординировать дальнейшие действия с операторами.

### Работа с очередью TRAVELSUP

Тикеты в этой очереди заводятся операторами поддержки на основании заявок пользователей.
Если для решения заявки требуется помощь дежурного (внести ручные правки в заказ, вернуть деньги, перегенерировать ваучер и тп), оператор призывает дежурного, который следует [типовым рецептам](recipes) для стандартных действий или вручную выполняет SQL запросы в базе данных для нестандартных.

{% note info}

Если какое-то "нестандартное" действие приходится выполнять из раза в раз, стоит завести тикет на его автоматизацию и добавление в список типовых рецептов.

{% endnote %}


## Дашборды

* Главный дашборд оркестратора — [prod](https://solomon.yandex-team.ru/?project=travel&cluster=orders_app_prod&service=orders_app&dashboard=travel_order_app&l.host=cluster&b=1d&e=), [testing](https://solomon.yandex-team.ru/?project=travel&cluster=orders_app_testing&service=orders_app&dashboard=travel_order_app&l.host=cluster)
* Дашборд запущенных workflow — [prod](https://solomon.yandex-team.ru/?project=travel&cluster=orders_app_prod&service=orders_app&host=!cluster&dashboard=travel_order_app_workflow_processing&b=1d&e=), [testing](https://solomon.yandex-team.ru/?project=travel&cluster=orders_app_testing&service=orders_app&host=!cluster&dashboard=travel_order_app_workflow_processing&b=1d&e=)
* Отельные заказы в API — [prod](https://solomon.yandex-team.ru/?project=travel&host=cluster&cluster=api_prod&service=api&dashboard=hotels-boy-new), [testing](https://solomon.yandex-team.ru/?project=travel&host=cluster&cluster=api_testing&service=api&dashboard=hotels-boy-new)
* ЖД и Авиа заказы в API — [prod](https://solomon.yandex-team.ru/?project=travel&cluster=api_prod&service=api&dashboard=avia-and-train-boy&l.host=cluster), [testing](https://solomon.yandex-team.ru/?project=travel&cluster=api_testing&service=api&dashboard=avia-and-train-boy&l.host=cluster)
* [логи орка - занимаемое место](https://monitoring.yandex-team.ru/projects/kikimr/explorer/queries?q.0.text=alias%28%0Agroup_by_time%281w%2C%20%27sum%27%2C%0Adiff%28%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22ydb_ru%22%2C%20service%3D%22tablets%22%2C%20host%3D%22cluster%22%2C%20slot%3D%22static%22%2C%20database%3D%22%2Fru%2Ftravelorchetsrator%2Fprod%2Forder_logs_prod%22%2C%20type%3D%22DataShard%22%2C%20category%3D%22executor%22%2C%20sensor%3D%22SUM%28DbDataBytes%29%22%7D%29%0A%29%0A%2C%20%22speed%20per%201w%22%29&q.0.axis=r&q.1.text=alias%28%0A%7Bproject%3D%22kikimr%22%2C%20cluster%3D%22ydb_ru%22%2C%20service%3D%22tablets%22%2C%20host%3D%22cluster%22%2C%20slot%3D%22static%22%2C%20database%3D%22%2Fru%2Ftravelorchetsrator%2Fprod%2Forder_logs_prod%22%2C%20type%3D%22DataShard%22%2C%20category%3D%22executor%22%2C%20sensor%3D%22SUM%28DbDataBytes%29%22%7D%0A%2C%20%22total%22%29&refresh=60&range=6mo&normz=off&colors=auto&type=line&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default)

## Анализ ошибок в API

Если в канал `Order Alerts` репортится ошибка вида `api-orders-failed-requests - User request failed with 5xx` (т.е. при обработке какого-то запроса к API случилась пятисотка), то имеет смысл проанализировать причины этой ошибки. Для этого стоит перейти к [sentry](https://travel-sentry.n.yandex-team.ru/travel/api-prod/) и найти там случившуюся ошибку (для этого можно открыть панель фильтров и отфильтровать ошибки по URL метода, в котором случилась ошибка; этот URL видно из алерта в TG). Дежурный может проанализировать stack trace ошибки, понять компонент или вертикаль, в котором произошла ошибка — и завести тикет на соответствующую команду разработки.
Больше информации про sentry можно получить в соответствующем [разделе документации](../tools/sentry).


## Как остановить Workflow

Возникают ситуации когда надо остановить workflow, чтобы перестал происходить polling заказа. В этом случае стоит использовать запрос следующей структуры

```sql
update workflows set state = '2' where id in (
-- your ids go here)
;
```

Стоит учитывать, что для того, чтобы состояние OrderAggregateState поменялось, необходимо произвести его пересчет. То есть для заказов, которые связаны с этим workflow надо вызвать следующий sql.

```sql
insert into order_aggregate_state_changes (id, order_id, created_at)
select nextval('order_aggregate_state_change_id_seq'), o.id, now()
from orders o
where 1 = 0
-- remove 1=0 and write your own condition here
```

## Как перезапустить Refund

В случае ошибок на стороне Trust'a во время проведения возврата, создается тикет вида https://st.yandex-team.ru/TRAVELORDERSUP-3525 в котором разработчику необходимо перезапустить возврат на нашей стороне. Следующий алгоритм действий поможет это сделать:
* Сущность возврата находится в ошибочном состоянии (RS_ERROR = 7). Находим рефанд в базе, проверяем, что он действительно находится в ошибочном состоянии и переводим его в нужное состояние (RS_CREATE = 2)
  ```sql
  select id, workflow_id, state from trust_refunds where invoice_id = (select id from invoices where order_id = '<YOUR_ORDER_ID_HERE>');
  ```
  Запоминаем workflow_id отсюда, он нам понадобится на следующем шаге
  ```sql
  update trust_refunds set state = 2 where state = 7 and invoice_id = (select id from invoices where order_id = '<YOUR_ORDER_ID_HERE>');
  ```
* Необходимо заново обработать событие виде TCreateRefund
  ```sql
  update workflow_events 
  set state = 1
  where id = (
      select id from workflow_events
      where workflow_id = '<YOUR_WORKFLOW_ID_HERE>'
      and class_name = 'ru.yandex.travel.orders.workflow.trust.refund.proto.TCreateRefund'
      );
  ```
