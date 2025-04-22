# Проактивный саппорт. Оповещение о проблемных заказах.

## Текущее решение:

Сейчас мы оповещаем обо всех заказах.

## Задача:

Хочется, оповещать о заказе, если мы считаем, что что-то пошло не так. 

## Плавный переход:

Нам нужен плавный переход от старого решения к новому, чтобы убедиться, что все кейсы "что-то пошло не так" описаны верно, а также, что нет такого кейса, который не описан.

Мы договорились, что бот дополнительно начнет писать в чат поддержки специального вида сообщения. Ребята из саппорта будут работать по старой схеме, забирать себе заказы и ручками отслеживать все ли ОК, при этом если что-то идет не так, они будут проверять, что бот прислал сообщение об этом. Также они будут проверять, что если бот что-то прислал, то что-то дейстивтельно идет не так. Таким образом за несколько итераций мы сможем синхронизировать эти оповещения и полностью перейти на новый тип оповещений, перестав посылать старые.

Надо не забывать, что мы хотим оповещать не обо всех "проблемных заказах", а только о заказах, которые входят в нашу выборку: заказы ровера, вип заказы, заказы, сумма которых >= X.

## База eats_misc.notified_orders

Раньше у нас был один вид оповещений, теперь их станет больше. Помимо этого, как уже было сказано ранее, нам надо оповещать только о проблемных заказах. Для этого нам нужно сделать некоторые изменения в базе.

Сейчас в базе *eats_misc.notified_orders* есть два поля - это order_nr и notified_at. Надо добавить новые поля:
 ```
ALTER TABLE eats_misc.notified_orders
    ADD COLUMN notify_type TEXT NOT NULL DEFAULT 'in_process';
    ADD COLUMN order_type TEXT NOT NULL;
    ADD COLUMN subtotal INTEGER NOT NULL;
 ```
 
А также сделать ключем связку (order_nr, notify_type). Таким образом у каждой проблемы будет свое название, и мы сможем смотреть, когда последний раз мы оповещали об этом заказе с такой проблемой. Т.к саппорту также необходима информация о order_type и subtotal мы добавим их в базу. Ранее этого не требовалось, потому что мы оповещали о конкретном заказе сразу и не предполагалось, что далее будет еще одно оповещение по этому заказу, теперь же такое произойти может, например, если возникнет какая-то проблема.

Для каждого кейса проблемы будет конфиг, который будет задавать время хранения записи об опощении заказа с такой проблемой. Таким образом, схема проверки необходимости отправить оповещение останется прежней. Надо будет посмотреть, есть ли в таблице запись с соответсвенным заказом и проблемой, и если есть, то оповещать не надо. Удаляться запись из таблицы будет после того, как с момента notified_at пройдет указанное в конфиге время.

Надо отметить особый статус - 'in_process'. Такой статус мы будем ставить для заказов, которые сейчас обрабатываем. Это означает, что мы отправили сообщение, о создании заказа - то есть оно подходит под выборку: заказы ровера, вип заказы, заказы, сумма которых >= X. Сейчас мы храним запись об отправлении такого сообщения 10 минут, но теперь такая запись значит для нас больше - нам важно понимать, для каких заказов мы хотим отправлять проблемные кейсы, поэтому предлагаю увеличить время хранения таких записей до адекватно-максимального(может чуть больше) времени доставки заказа.


## Заказы лавки

Также одна из подзадач - не оповещать о заказах лавки. Для этого надо смотреть на поле orders.processing_type. Если там будет стоять 'store', значит заказ из лавки. Поэтому такое условие надо внести в запросы, которые сейчас выбирают заказы.

## Определение проблемного заказа
Чтобы определить проблемные заказы, мы будем выбирать все проблемные заказы на данный момент, и мержить со списком заказов, у которых notify_type - 'in_process', то есть мы скйчас обрабатываем заказ.
Надо заметить, что при выборе проблемных заказов, мы продублируем условие с orders.processing_type = 'store', чтобы уменьшить количество проблемных заказов.


## Кейсы "что-то пошло не так":
Во всех запросах мы дополнительно накладываем условие, что дата создания заказа > Now() - ACTIVE_ORDERS_INTERVAL, где ACTIVE_ORDERS_INTERVAL задается конфигом. Это необходимо, потому что в базе присутствуют
заказы в нефинишных статусах за очень старые даты.([Пример1](https://admin.eda.yandex-team.ru/orders/200816-147756/edit), [Пример2](https://admin.eda.yandex-team.ru/orders/200926-451646/edit)). Я предполагаю,
что хорошим значением для этого конфига будет - 3 дня. С таким значением мы не будем отсекать заказы "на позже", потому что их можно сделать максимум на день-два вперед, но при этом все старые невалидные заказы отпадут.

Теперь взглянем на сами запросы.
### Заказ не подтверждается рестораном более X секунд(place_unconfirmed_order)
Это единственный кейс, где нам надо будет сделать два запроса - один для asap заказов, второй - для отложенных.


ASAP закакы. Запрос и его EXPLAIN:
```
SELECT
    order_nr
FROM orders
WHERE
    status = 1
    AND call_center_confirmed_at < Now() - INTERVAL 5 MINUTE
    AND is_asap = 1
    AND created_at > Now() - INTERVAL 3 DAY
    AND processing_type != 'store';
 ```
|id|select_type|table|partitions|type|possible_keys|key|key_len|ref|rows|filtered|Extra|
|--|-----------|-----|----------|----|-------------|---|-------|---|----|--------|-----|
|1|SIMPLE|orders||ref|idx_created_at,idx_status_courier_delivered|idx_status_courier_delivered|2|const|442|0.18|Using where|


Отложенные заказы. Запрос и его EXPLAIN:
```
SELECT
	order_nr
FROM orders
WHERE
    status = 1
    AND remind_at < Now() - INTERVAL 5 MINUTE
    AND is_asap = 0
    AND created_at > Now() - INTERVAL 3 DAY
    AND processing_type != 'store';
```
|id|select_type|table|partitions|type|possible_keys|key|key_len|ref|rows|filtered|Extra|
|--|-----------|-----|----------|----|-------------|---|-------|---|----|--------|-----|
|1|SIMPLE|orders||ref|idx_created_at,idx_status_courier_delivered|idx_status_courier_delivered|2|const|441|0.18|Using where|




### Курьер найден, но не принимает заказ более X секунд(not_adopted_by_courier)

Запрос и его EXPLAIN:
```
SELECT
    order_nr
FROM orders
WHERE
    courier_assigned_at < Now() - INTERVAL 5 MINUTE
    AND adopted_by_courier = 0
    AND processing_type != 'store'
    AND created_at > Now() - INTERVAL 3 DAY
    AND status in (1, 2, 3);
```
|id|select_type|table|partitions|type|possible_keys|key|key_len|ref|rows|filtered|Extra|
|--|-----------|-----|----------|----|-------------|---|-------|---|----|--------|-----|
|1|SIMPLE|orders||range|idx_created_at,idx_status_courier_delivered,idx__orders__courier_assigned_at|idx_status_courier_delivered|2||537|0.25|Using index condition; Using where|



### Не назначен такси курьер (Поиск X секунд)(no_taxi_for_order)

Как только мы начинаем искать такси, в таблице logistics_taxi_dispatch_requests создается запись.

Запрос и его EXPLAIN:
```
SELECT
    logistics_taxi_dispatch_requests.order_nr
FROM orders
JOIN logistics_taxi_dispatch_requests
ON logistics_taxi_dispatch_requests.order_nr = orders.order_nr
WHERE
    orders.courier_assigned_at IS NULL
    AND logistics_taxi_dispatch_requests.created_at < Now() - INTERVAL 20 MINUTE
    AND orders.processing_type != 'store'
    AND orders.created_at > Now() - INTERVAL 3 DAY
    AND orders.status in (1, 2, 3);
```
|id|select_type|table|partitions|type|possible_keys|key|key_len|ref|rows|filtered|Extra|
|--|-----------|-----|----------|----|-------------|---|-------|---|----|--------|-----|
|1|SIMPLE|orders||range|order_nr_idx,idx_created_at,idx_status_courier_delivered,idx__orders__courier_assigned_at|idx_status_courier_delivered|2||538|4.06|Using index condition; Using where|
|1|SIMPLE|logistics_taxi_dispatch_requests||eq_ref|PRIMARY,idx__logistics_taxi_dispatch_requests__created_at|PRIMARY|767|bigfood_staging.orders.order_nr|1|100.0|Using where|




### Прошло более X секунд, после статуса "Плановое время прибытия курьера в ресторан" (курьер не прибыл) (courier_not_arrived_to_place)

Запрос и его EXPLAIN:
```
SELECT 
    orders.order_nr
FROM orders
JOIN order_delivery_info ON order_delivery_info.order_id = orders.id
WHERE
    order_delivery_info.actual_arrived_to_place IS NULL
    AND order_delivery_info.planned_arrived_to_place < Now() - INTERVAL 5 MINUTE 
    AND orders.processing_type != 'store'
    AND orders.created_at > Now() - INTERVAL 3 DAY
    AND orders.status in (1, 2, 3);
```
|id|select_type|table|partitions|type|possible_keys|key|key_len|ref|rows|filtered|Extra|
|--|-----------|-----|----------|----|-------------|---|-------|---|----|--------|-----|
|1|SIMPLE|orders||range|PRIMARY,idx_created_at,idx_status_courier_delivered|idx_status_courier_delivered|2||537|5.52|Using index condition; Using where|
|1|SIMPLE|order_delivery_info||ref|IDX_136B180D8D9F6D38|IDX_136B180D8D9F6D38|4|bigfood_staging.orders.id|1|4.92|Using where|




### Прошло более X секунд после статуса "Курьер забрал заказ" (курьер не забрал заказ). (order_not_taken)


Запрос и его EXPLAIN:
```
SELECT
    orders.order_nr
FROM orders
JOIN order_delivery_info ON order_delivery_info.order_id = orders.id
WHERE
    order_delivery_info.actual_order_taken IS NULL
    AND order_delivery_info.planned_order_taken < Now() - INTERVAL 5 MINUTE 
    AND orders.processing_type != 'store'
    AND orders.created_at > Now() - INTERVAL 3 DAY
    AND orders.status in (1, 2, 3);
```

|id|select_type|table|partitions|type|possible_keys|key|key_len|ref|rows|filtered|Extra|
|--|-----------|-----|----------|----|-------------|---|-------|---|----|--------|-----|
|1|SIMPLE|orders||range|PRIMARY,idx_created_at,idx_status_courier_delivered|idx_created_at|5||471|4.49|Using index condition; Using where|
|1|SIMPLE|order_delivery_info||ref|IDX_136B180D8D9F6D38|IDX_136B180D8D9F6D38|4|bigfood_staging.orders.id|1|5.0|Using where|



### Прошло более X секунд после планового времени прибытия к клиенту, (курьер еще не прибыл) (courier_not_arrived_to_customer)

Запрос и его EXPLAIN:
```
SELECT
    orders.order_nr
FROM orders
JOIN order_delivery_info AS odi ON odi.order_id = orders.id
WHERE
    odi.actual_arrived_to_customer IS NULL
    AND odi.planned_arrived_to_customer < Now() - INTERVAL 10 MINUTE
    AND orders.processing_type != 'store'
    AND orders.created_at > Now() - INTERVAL 3 DAY
    AND orders.status in (1, 2, 3, 9);
```

|id|select_type|table|partitions|type|possible_keys|key|key_len|ref|rows|filtered|Extra|
|--|-----------|-----|----------|----|-------------|---|-------|---|----|--------|-----|
|1|SIMPLE|orders||range|PRIMARY,idx_created_at,idx_status_courier_delivered|idx_status_courier_delivered|2||558|5.48|Using index condition; Using where|
|1|SIMPLE|odi||ref|IDX_136B180D8D9F6D38|IDX_136B180D8D9F6D38|4|bigfood_staging.orders.id|1|4.92|Using where|


### Прошло X секунд с момент статуса «Прибыл к клиенту» (not_finished_order)
Запрос и его EXPLAIN:
```
SELECT
    orders.order_nr
FROM orders
WHERE
    status = 6
    AND arrived_to_customer_at < Now() - INTERVAL 5 MINUTE 
    AND orders.created_at > Now() - INTERVAL 3 DAY
    AND processing_type != 'store';
```
|id|select_type|table|partitions|type|possible_keys|key|key_len|ref|rows|filtered|Extra|
|--|-----------|-----|----------|----|-------------|---|-------|---|----|--------|-----|
|1|SIMPLE|orders||ref|idx_created_at,idx_status_courier_delivered|idx_status_courier_delivered|2|const|22|1.83|Using where|



### Прошло X секунд после планового времени доставки заказ МП (заказ недоставлен) (not_finished_marketplace_order)
Чтобы вычислить плановое время доставки для заказов маркетплейсов - надо к полю place_confirmed_at из таблички orders добавить pre_delivery_time. Чтобы условие выполнилось, надо проверить, что не прошло X секунд после этого времени.


Запрос и его EXPLAIN:
```
SELECT
    order_nr
FROM orders
WHERE
    place_confirmed_at + INTERVAL time_to_delivery_max MINUTE < Now() - INTERVAL 10 MINUTE
    AND type = 'marketplace'
    AND status not in (4,5,7)
    AND orders.created_at > Now() - INTERVAL 3 DAY
    AND orders.processing_type != 'store';
```

|id|select_type|table|partitions|type|possible_keys|key|key_len|ref|rows|filtered|Extra|
|--|-----------|-----|----------|----|-------------|---|-------|---|----|--------|-----|
|1|SIMPLE|orders||range|idx_created_at,idx_status_courier_delivered|idx_created_at|5||577|2.77|Using index condition; Using where|



## Полный переход
Если мы сможем сбалансированно снизить цену для заказов типа 'big_order' до нуля, то есть по сути, обращать внимание на все заказы, то, мы сможем полносью перейти на механизм оповещения только проблемных заказов. То есть в таком случае, мы сможем отказаться от хранения заказов, которые сейчас "в обработке", и выполнять только запросы, которые ищут проблемные заказы. Единственное, что надо будет добавить в эти запросы, это вывод поля orders.phone_number. Это необходимо, потому что при оповещении о всех проблемных заказах, саппорта все равно важно видеть является этот заказ вип или нет.

К сожалению, такой переход слишком маловероятен, потому что ресурс саппорта ограничен, и придется либо жертвовать в качестве поддержки(увеличивать интервалы, когда какая-то проблема является нормой), либо жертвовать количеством заказов, которые мы обрабатываем.
