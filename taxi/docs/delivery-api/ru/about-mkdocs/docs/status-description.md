# Описание статусов

|Статус | Описание |
|:--- |:--- |
|DRAFT| Создан черновик заявки|
|VALIDATING| Заявка обрабатывается|
|VALIDATING_ERROR| Ошибка подтверждения заявки, пересоздайте заказ|
|CREATED| Заказ создан|
|DELIVERY_PROCESSING_STARTED| Заказ создаётся в сортировочном центре|
|DELIVERY_PROCESSING_STARTED| Заказ создан в сортировочном центре|
|DELIVERY_PROCESSING_STARTED| Заказ подтверждён в сортировочном центре|
|DELIVERY_TRACK_RECEIVED| Заказ создан в системе службы доставки|
|SENDER_WAIT_FULFILLMENT| Ожидается поступление на склад|
|DELIVERY_LOADED| Заказ подтверждён|
|DELIVERY_AT_START| Заказ поступил в сортировочный центр|
|DELIVERY_TRANSPORTATION| Доставляется в город получателя|
|DELIVERY_ARRIVED |Заказ поступил в город получателя|
|DELIVERY_TRANSPORTATION_RECIPIENT| Посылка доставляется клиенту|
|DELIVERY_STORAGE_PERIOD_EXTENDED| Срок хранения заказа в службе доставки увеличен|
|DELIVERY_STORAGE_PERIOD_EXPIRED| Срок хранения заказа в службе доставки истек|
|DELIVERY_UPDATED| Доставка перенесена отправителем|
|DELIVERY_UPDATED_BY_RECIPIENT| Доставка перенесена по просьбе клиента|
|DELIVERY_UPDATED_BY_DELIVERY| Доставка перенесена службой доставки|
|DELIVERY_ARRIVED_PICKUP_POINT| В пункте самовывоза|
|DELIVERY_TRANSMITTED_TO_RECIPIENT| Заказ передан клиенту|
|DELIVERY_DELIVERED| Доставлен|
|DELIVERY_ATTEMPT_FAILED| Неудачная попытка вручения|
|DELIVERY_CAN_NOT_BE_COMPLETED| Заказ не может быть доставлен|
|RETURN_PREPARING| Готовится к возврату|
|SORTING_CENTER_AT_START| На складе сортировочного центра|
|SORTING_CENTER_PREPARED|Готов к отправке в службу доставки|
|SORTING_CENTER_RETURN_PREPARING| Готовится к возврату|
|SORTING_CENTER_RETURN_RFF_ARRIVED_FULFILLMENT| Возвращен на сортировочный центр|
|SORTING_CENTER_RETURN_ARRIVED| Возврат на складе сортировочного центра|
|SORTING_CENTER_RETURN_PREPARING_SENDER| Готов для передачи магазину|
|SORTING_CENTER_RETURN_TRANSFERRED| Возврат передан на доставку в магазин|
|SORTING_CENTER_RETURN_RETURNED*|Возвращен в магазин|
|SORTING_CENTER_CANCELED| Отменен сортировочным центром|
|SORTING_CENTER_ERROR| Ошибка создания заказа в сортировочном центре|
|CANCELLED*| Заказ отменен|

\* Конечный статус
