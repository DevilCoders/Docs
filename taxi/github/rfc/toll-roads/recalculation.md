# Платные дороги: перерасчет

Задача: Научиться изменять стоимость платной дороги отдельно от стоимости поездки в админке в разделе "[Платежи](https://tariff-editor.taxi.yandex-team.ru/payments)"

### Что нужно

На стороне продукта: поддержать возможность изменения цены в order.payment_tech.sum_to_pay.toll_road и отправлять эти данные в биллинг.
На стороне фронта: поддержать новую форму ввода для изменения стоимости платной дороги по аналогии с формочкой изменения стоимости поездки.

### Как делаем

В сервисе tolls (uservices) добавляем новый хендлер /toll-roads/v1/order/price, который принимает order_id и обновляет в dbtaxi значение поля order.payment_tech.sum_to_pay.toll_road для заданного заказа, после чего планирует STQ задачу update_transactions, где по аналогии с [обновлением стоимости поездки](https://github.yandex-team.ru/taxi/backend/blob/develop/taxi/internal/payment_kit/invoices.py#L681) новая цена отправляется в биллинг.

На стороне админки без кода добавляем конфиг, который позволит проксировать запросы с фронта админки в сервис tolls. (https://wiki.yandex-team.ru/taxi/backend/adminka-bez-koda/#kakpolzovatsja)

### API

```
POST /toll-roads/v1/order/price:
{
    "order_id": "order_id",
    "toll_road_cost": "123.000"
}
```

### API
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
      - order_id
      - price
    additionalProperties: false
```
