# Изменения в toll-roads для фичи "Платные Дороги" (Toll Roads)

Проект описан [здесь](https://st.yandex-team.ru/PARTNERSPROJECT-575)

Задача: научиться определять, была ли предложена пассажиру платная дорога, была ли выбрана платная дорога в качестве маршрута,
кто будет оплачивать проезд по платной дороге: водитель или пассажир.

## Изменения в запросе к toll_roads_order_save

В запрос к STQ-таске на сохранение заказа с платной дорогой добавится поле `auto_payment` и будет сохраняться в БД.

## Изменения в ответе /tolls/v1/order/retrieve 

В ответе ручки будем возвращать поля `auto_payment` и необязательное поле `price`, цену за платную дорогу. Если платит пассажир, вернем None.

Также добавится новая ручка `/tolls/v1/order/price`, в которую будет передаваться цена, введенная водителем за платную дорогу. Будем сохранять пару order_id - price в отдельную табличку, если order_id в сервисе toll_roads еще отсутствует - напишем об этом в лог, но завершению заказа и сохранению цены не помешаем.

### Изменения схемы ручек 

`/tolls/v1/order/retrieve`

```yaml
paths:
  /toll-roads/v1/order/price:
    post:
      summary: Сохранить цену платной дороги
      operationId: orderPriceSave
      parameters:
        - in: body
          name: body
          required: true
          schema:
            $ref: '#/definitions/OrderPriceSaveRequest'
      responses:
        200:
          description: OK. Цена успешно сохранена
        400:
          description: Некорректный запрос
        500:
          description: Внутренняя ошибка сервиса

definitions:
  OrderPriceSaveRequest:
    type: object
    properties:
      order_id:
        type: string
        description: id заказа, который построен по платному маршруту
      price:
        type: string
        description: Цена платной дороги
    required:
      - offer_id
    additionalProperties: false

  RetrieveResponse:
    properties:
      ...
      toll_roads:
        type: object
        description: информация о платных участках на построенном маршруте
        properties:
          auto_payment:
            type: boolean
            description: плата за проезд по платной дороге списывается с клиента автоматически
          price:
            type: string
            description: стоимость платной дороги

```
