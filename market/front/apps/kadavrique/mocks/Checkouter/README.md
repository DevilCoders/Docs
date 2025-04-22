# Checkouter

Данные в стейте:

```
{
    "Checkouter.collections": {
        order: {
            [ORDER_ID]: {
                items: [ORDER_ITEM_ID],
                delivery: ORDER_DELIVERY_ID,
                buyer: ORDER_BUYER_ID,
                changeRequests: [ORDER_EDIT_REQUEST_ID],
            },
        },
        item: {
            [ORDER_ITEM_ID]: OrderItem,
        },
        delivery: {
            [ORDER_DELIVERY_ID]: OrderDelivery,
        },
        buyer: {
            [ORDER_BUYER_ID]: OrderBuyer,
        },
        orderEditPossibilities: {
            [ORDER_ID]: [{
                availability: "DISABLED" | "ENABLED",
                type: OrderChangeType,
                method: OrderChangeMethod,
            }]
        },
        orderEditOptions: {
            [ORDER_ID]: {
                deliveryOptions: EditDeliveryOption[]
            }
        },
        orderEditRequest: {
            [ORDER_EDIT_REQUEST_ID]: {
                id: 1,
                orderId: 1,
                type: '',
                status: '',
                createdAt: '',
                message: '',
                authorRole: '',
                payload: {},
            }
        },
        payment: {
            [ORDER_ID]: {
                id: 2,
                fake: false,
                status: 'INIT',
                currency: 'RUR',
                totalAmount: 10007,
                creationDate: '30-03-2020 14:42:33',
                statusExpiryDate: '30-03-2020 15:02:33',
                paymentURLActionType: 'I_FRAME',
            }
        },
        removalPermissions: OrderItemsRemovalPermissionResponse,
        ordersChanges: OrderChangesViewModel
    }
}
```
`OrderDelivery` в природе не имеет идентификатора, делаем его исключительно для связки данных.

Никакие поля не являются обязательными, если нужен совершенно случайный заказ, то достаточно положить пустой объект в коллекцию order.



## Ручки, возвращающие заказы

При отдаче данные обогащаются по [схеме](https://github.yandex-team.ru/market/kadavrique/blob/master/mocks/Checkouter/schema.js).

Эта схема минимально необходимая для отображения заказа на фронте, по мере необходимости ее нужно дополнять.

Учитывается правильность формирования итоговых сумм: на основании стоимости и количества товарных позиций и стоимости доставки.

### `/orders/by-uid/<uid>`

Отдается весь список заказов из `Checkouter.collections.order` с пагинацией.
Поддерживаемые параметры:
* page - номер страны
* pageSize - количество заказов на одной странице

Заказы отсортированы по id. Если важен порядок, то id для всех заказов должны быть заранее определены.

**Принятые допущения:**
* пока не предусмотрены ошибочные ответы
* пока не предусмотрена работа с пользователем

### `/orders/by-uid/<uid>/recent`

"Быстрая" ручка заказов. Под капотом использует обычную ручку (см. `/orders/by-uid/<uid>`)
Поддерживаемые параметры:
* partials - дополнительные данные, которая ручка должна вернуть

см. https://wiki.yandex-team.ru/market/marketplace/Dev/checkouter/get/orders/by-uid/uid/recent/

### `/orders/<orderId>`

Находит заказ с переданным id в `Checkouter.collections.order`

**Принятые допущения:**
* пока не предусмотрены ошибочные ответы

### `/cart`

Возращает минимальный объект необходимый для актуализации корзины, по мере необходимости дополняем.
Учитывает в саммари и опциях доставки примененные бонусы.
При наличии данных в коллекциях `cart` и `cartItem`, собирает ответ из них, в противном случае - использует
данные из запроса.

**Принятые допущения:**
* пока актуализация сама задает одну опцию доставки с заданной ценой
* пока учитываем ограничения только у бонусов типа FIXED
* пока примерный расчет скидки для бонусов типа PERCENT
* пока не рассчитывается скидка на конкретный товар если их несколько
* пока не учитывается подходит ли бонус на конкретный товар, только на всю корзину

### `/checkout`

Оформление заказа. При наличии данных в коллекциях `order` и `item` собирает ответ из них, в противном случае - генерирует ответ
на основе данных из запроса.

В объекте `Checkouter.options` в стейте можно указать параметр `isCheckoutSuccessful`.
Если он равен `true`, будет симулирован упешный чекаут, если `false` - неуспешный.
Во втором случае ордеры попадут в `orderFailures`.

При успешном чекауте складывает ордеры в нормализованном виде в коллекции.

### `/orders/cancellation-substatuses`

Отдается список причин отмены заказа.
Для каждого статуса заказа берется сгенерированный массив причин отмены.
Причина отмены имеет код, соотвествующий коду в чекаутере и рандомно сгенерированный текст.


### `/orders/<orderId>/cancellation-request`

Отменяет заказ по переданному id, если он есть в `Checkouter.collections.order`.
* Если это фарма-заказ (`fulfillment === false`), то отменяет заказ сразу
* Если не фарма-заказ, создает запрос на отмену заказа (код причины отмены берется из параметра substatus тела запроса)
* Если заказ не найден в стейте, возвращает объект с ошибкой


### `/actualize`

Актуализация товара.
Ручка возвращает рандомно сгенерированный ответ основываясь на теле `POST` запроса.
Ответ можно кастомизировать под себя, если установить в ключ стейта `Сheckouter.actualize` нужные поля, основываясь на схеме.
Например, чтобы сбросить стоки досточно установить `Checkouter.actualize.count = 0`;

**Принятые допущения:**
* пока не предусмотрены ошибочные ответы

### `/orders/by-bind-key/<bindKey>`

Информация о заказе, который хотим присоединить.
* Ищет в коллекции orderBind заказ по bindKey
* Если в заказе указано поле bindIfo.error - отадет ошибку с указанным кодом
* Если error нет - отдает сам заказ

### `/get-orders`

POST-ручка с расширенным набором параметров для получения списка заказов.

[swagger](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/order-controller/getOrdersUsingPOST)
### `/get-orders-for-pi`

Облегчённая версия предыдущей ручки.

[swagger](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/order-controller/getOrdersForPIUsingPOST)
[MARKETCHECKOUT-26125](https://st.yandex-team.ru/MARKETCHECKOUT-26125)

### `/move-orders`

Присоединение заказов
* Ищет в коллекции orderBind заказы по orderIds
* Возвращает список статусов привязки, основываясь на поле bindInfo заказа
* Доступные поля bindInfo
  * status - SUCCESS, FAIL, ORDER_NOT_FOUND (можно указать любую строку, но на фронте нужны такие)
  * bonuses
    * если не указан, не веренется информация о привязке бонусов (coinBindingResult)
    * если указано, нужно указать totalCount и succesfullBindCount

### `/orders/<orderId>/delivery/parcels/<parcelId>/boxes`

Заменяет список коробок переданными коробками.

### `/orders/<orderId>/status`

Изменение статуса заказа.

### `/orders/<orderId>/change-requests/<changeRequestId>`

http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/order-edit-controller/updateChangeRequestStatusUsingPATCH

### `/orders/payment`

Инициализирует оплату заказов и возвращает информацию для траста (purchaseToken, paymentUrl и т.п.).
[Swagger](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/payment-controller/doPayUsingPOST_1)

* Если заказа, присутствующего в теле запроса, нет в коллеции order, возвращает ошибку с кодом `ORDER_NOT_FOUND`.
* Если один из заказов, присутствующих в теле запроса, находится не в статусе `UNPAID`,
    возвращает ошибку с кодом `order_invalid`.
* В остальных случаях возвращает содержимое коллекции `Checkouter.collections.payment` из стейта.

### `/orders/<orderId>/items/<itemId>/instances`
Сохранение кодов маркировки товаров. Возвращает обновленные данные о товаре с кодами (поле instances).
[Swagger](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/order-items-controller/putOrderItemInstancesUsingPUT)

###  `/orders/<orderId>/payment`
Является ли заказ архивным. Возвращает `paymentId` и `fake` для песочных заказов.
[Swagger](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/payment-controller/getPaymentForOrderUsingGET)

### `/payments/<paymentId>/notify`
Эмуляция оплаты, после которой меняется статус заказа с "UNPAID" на "PENDING" или "PROCESSING"
[Swagger](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/payment-controller/notifyPaymentUsingPOST)

### `orders/<orderId>/events`
Получение историю событий для заказа и идентификатором orderId
[Swagger](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/order-history-events-controller/getOrderHistoryEventsUsingGET)

### `orders/<orderId>/items/removal-permissions`
Получение информации по возможности изменения состава заказа для FBS
[Swagger](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/order-items-controller/getOrderItemsRemovalPermissionsUsingGET)

### `/orders/changes`
Получение изменений в нескольких заказах
[Swagger](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/order-controller/bulkGetOrderChangesUsingGET)

### `/orders/<orderId>/delivery/parcels/<parcelId>/track`
Создание трек-кода для заказа
[Swagger](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/track-controller/addDeliveryTrackUsingPOST)

### `/orders/<orderId>/delivery/parcels/<parcelId>/tracks/update`
Обновление трек-кода для заказа
[Swagger](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/track-controller/updateDeliveryTracksUsingPUT)
