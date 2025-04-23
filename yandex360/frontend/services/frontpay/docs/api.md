# Внешний API

Для запросов через внешний API необходимо получить токен для сервиса Яндекс.Оплата в кабинете разработчика:

- [Прод](https://developer.tech.yandex.ru/)
- [Тест](https://developer-test.paysys.yandex.ru)

## POST /v1/order

> Создаёт новый заказ.

<details>
<summary>Формат тела запроса</summary>

```json
{
  "caption": "string",
  "description": "string",
  "max_amount": 0,
  "autoclear": true,
  "items": [
    {
      "nds": "string",
      "amount": 0,
      "name": "string",
      "price": 0,
      "currency": "RUB"
    }
  ],
  "kind": "string"
}
```

</details>

<details>
<summary>Формат ответа</summary>

Статус `200`

```json
{
  "data": {
    "verified": true,
    "user_email": "string",
    "active": true,
    "max_amount": 0,
    "trust_resp_code": "string",
    "service_merchant_id": 0,
    "updated": "2019-11-06T16:02:31.693Z",
    "created": "2019-11-06T16:02:31.693Z",
    "price": 0,
    "closed": "2019-11-06T16:02:31.693Z",
    "pay_status": "string",
    "original_order_id": 0,
    "refund_status": "string",
    "order_id": 0,
    "order_url": "string",
    "kind": "string",
    "currency": "RUB",
    "paymethod_id": "string",
    "payment_url": "string",
    "email": {
      "to_email": "user@example.com",
      "reply_email": "user@example.com"
    },
    "revision": 0,
    "payment_hash": "string",
    "uid": 0,
    "user_description": "string",
    "items": [
      {
        "nds": "string",
        "amount": 0,
        "name": "string",
        "product_id": 0,
        "price": 0,
        "currency": "RUB"
      }
    ],
    "caption": "string",
    "description": "string",
    "issued_amount": 0,
    "held_at": "2019-11-06T16:02:31.693Z",
    "order_hash": "string",
    "customer_uid": 0,
    "autoclear": true
  },
  "code": "string",
  "status": "string"
}
```

</details>

## POST /v1/order/{id}/deactivate

> Деактивирует заказ.

Обязательные параметры:
- `id` — идентификатор заказа

<details>
<summary>Формат ответа</summary>

Статус `200`

</details>

## GET /v1/order/{id}

> Возвращает заказ по `id`.

Обязательные параметры:
- `id` — идентификатор заказа

<details>
<summary>Формат ответа</summary>

Статус `200`

```json
{
  "data": {
    "verified": true,
    "user_email": "string",
    "active": true,
    "max_amount": 0,
    "trust_resp_code": "string",
    "service_merchant_id": 0,
    "updated": "2019-11-06T16:16:28.762Z",
    "created": "2019-11-06T16:16:28.762Z",
    "price": 0,
    "closed": "2019-11-06T16:16:28.762Z",
    "pay_status": "string",
    "original_order_id": 0,
    "refund_status": "string",
    "order_id": 0,
    "order_url": "string",
    "kind": "string",
    "currency": "RUB",
    "paymethod_id": "string",
    "payment_url": "string",
    "email": {
      "to_email": "user@example.com",
      "reply_email": "user@example.com"
    },
    "revision": 0,
    "payment_hash": "string",
    "uid": 0,
    "user_description": "string",
    "items": [
      {
        "nds": "string",
        "amount": 0,
        "name": "string",
        "product_id": 0,
        "price": 0,
        "currency": "RUB"
      }
    ],
    "caption": "string",
    "description": "string",
    "issued_amount": 0,
    "held_at": "2019-11-06T16:16:28.762Z",
    "order_hash": "string",
    "customer_uid": 0,
    "autoclear": true
  },
  "code": "string",
  "status": "string"
}
```

</details>
