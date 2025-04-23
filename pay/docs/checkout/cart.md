# Работа с корзиной

## Сущность корзины


@startuml
entity "cart" as cart {
  id : uuid
  --
  uid: int
  merchant_id : uuid "FK"
  external_id : text
  currency: text
  items: jsonb "list[item]"
  coupons: jsonb "list[coupon]"
  metadata: jsonb "dict[str,str]"
}
@enduml


## Создание корзины `POST /carts`
```
{
  "merchant_id": "220246e4-cf46-4828-8b30-35a83c196ae3",
  "pay_session_id": "pay_session_id", // idempotency key (кажется, лучше передавать в заголовке)
  "external_id": "123456", // optional
  "currency": "RUB",
  "items": [
    {
      "id": "product-1",
      "quantity": { // optional
        "count": "1.5",
        "label": "kg" // optional
      }
    }
  ],
  "coupons" : [ // optinal
      {"value": "abc"},
      {"value": "efg"}
  ]
  "metadata": { // optional
    "key-1": "value"
  }
}
```


## Обновление корзины `POST /carts/<cart_id>`

Считаем что в корзине нельзя обновить:
* merchant_id
* валюту

```
{
  "external_id": "123456"
  "items": [
    {
      "id": "product-1",
      "quantity": {
        "count": "1.5",
        "label": "kg"
      }
    }
  ],
  "metadata": {
    "key-1": "value"
  }
}
```