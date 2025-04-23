#### GET /api/v1/user_cards?default_uid=1234
Параметры запроса:
* `default_uid` - число. Передавать, если известен. Для того, чтобы мультиавторизация не ломала нам пользовательский опыт

Ответ:
```
{
  "status": "success",
  "code": 200,
  "data": {
    "cards": [
      {
        "id": "guid",
        "uid": int,
        "last4": str,
        "card_network": "AMEX|DISCOVER|JCB|MASTERCARD|VISA|MIR|UNIONPAY|UZCARD|MAESTRO|VISAELECTRON",
        "card_art": {
            "pictures": { // Поле отсутствует у нетокенизированных карт
                "original": { // Помимо original, в будущем могут появиться новые размеры
                    "uri": str
                }
            }
        },
        "issuer_bank": str // Нормализованное название банка
      }
    ]
  }
}
```


#### POST /api/v1/checkout
Параметры запроса:

query:
* `default_uid` - число. Передавать, если известен. Для того, чтобы мультиавторизация не ломала нам пользовательский опыт

body (application/json):
```
{
  "merchant_origin": "https://best-shop.ru",
  "card_id": guid,
  "challenge_return_path": string,  # optional. Зависит от поля verification_details
  "sheet": {
      "version": 2,
      "order": {
          "id": string,
          "total": {
              "amount": decimal ("322.00"),
              "label": string,  # optional
          },
          "items": array<{  # optional
              "amount": decimal ("42.00"),
              "label": string,
          }>,
      },
      "currency_code": "RUB",
      "country_code": "ru",
      "merchant": {
          "id": guid,
          "name": string,
      },
      "payment_methods": array<{
          "type": "CARD",
          "gateway": string,
          "gateway_merchant_id": string,
          "allowed_auth_methods": array<PAN_ONLY|CLOUD_TOKEN>,
          "allowed_card_networks": array<AMEX|DISCOVER|JCB|MASTERCARD|VISA|MIR|UNIONPAY|UZCARD>,
          "verification_details": bool,  # optional
      }>
  }
}
```

Ответ:
```
{
  "status": "success",
  "code": 200,
  "data": {
    "payment_token": str,
    "payment_method_info": {
        "type": "CARD",
        "card_last4": string,  #optional
        "card_network": "AMEX|DISCOVER|JCB|MASTERCARD|VISA|MIR|UNIONPAY|UZCARD|MAESTRO|VISAELECTRON"  #optional
    }
  }
}
```


```
{
  "status": "fail",
  "code": 400,
  "data": {
    "message": "CARD_NOT_FOUND",
    "params": {}
  }
}
```


```
{
  "status": "fail",
  "code": 403,
  "data": {
    "message": "CHALLENGE_REQUIRED",
    "params": {
      "challenge_url": str
    }
  }
}
```

Список кодов ошибок:
* `MERCHANT_ORIGIN_ERROR` - неопознанный ориджин
* `INSECURE_MERCHANT_ORIGIN` - схема ориджина мерчанта не HTTPS
* `AMOUNT_LIMIT_EXCEEDED` - сумма заказа превышает максимально возможную `params.max_amount`
* `CARD_NOT_FOUND` - карта не найдена, или токен не существует, или токен не активен
* `INVALID_AMOUNT` - decimal'ы вроде `"0.00"` (ноль), `"-10.01"` (отрицательное число), `"10.0001"` (слишком точное число)
* `AMOUNT_MISMATCH` - если указаны items, но сумма по всем `item.amount` не равна `total.amount`
* `INVALID_COUNTRY` - пока поддерживается только `"ru"`
* `INVALID_CURRENCY` - пока поддерживается только `"RUB"`
* `INVALID_VERSION` - поддерживается только `2`
* `MERCHANT_NOT_FOUND` - мерчант не найден
* `GATEWAY_NOT_FOUND` - psp не найден
* `CARD_NETWORK_NOT_SUPPORTED` - карта принадлежит визе (или миру)
* `INSECURE_MERCHANT_ORIGIN` — сайт мерчанта не защищен HTTPS.
* `MERCHANT_ORIGIN_ERROR` — невалидный `merchant_origin`.
* `CHALLENGE_REQUIRED` — необходимо пройти антифрод и подтвердить устройство.
* `CHALLENGE_DENIED` — запрет от антифрода.
* `CHALLENGE_RETURN_PATH_REQUIRED` — запрошена проверка антифрода, но не передан `challenge_return_path`.
* `PSP_ACCOUNT_ERROR` — платежный шлюз заблокирован.
* `MERCHANT_ACCOUNT_ERROR` — мерчант или ориджин заблокированы.


#### POST /api/v1/validate
Параметры запроса:
query:
* `default_uid` - число. Передавать, если известен. Для того, чтобы мультиавторизация не ломала нам пользовательский опыт

body (application/json)
* `merchant_origin` - ориджин мерчанта согласно: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Origin#syntax
```
{
  "merchant_origin": "https://best-shop.ru",
  "sheet": PaymentSheet
}
```

Ответ:
```
{
  "status": "success",
  "code": 200,
  "data": {}
}
```

```
{
  "status": "fail",
  "code": 400,
  "data": {
    "message": "MERCHANT_ORIGIN_ERROR",
    "params": {}
  }
}
```

Список кодов ошибок:
* `MERCHANT_ORIGIN_ERROR` - неопознанный ориджин
* `INSECURE_MERCHANT_ORIGIN` - схема ориджина мерчанта не HTTPS
* `AMOUNT_LIMIT_EXCEEDED` - сумма заказа превышает максимально возможную `params.max_amount`
* `INVALID_AMOUNT` - decimal'ы вроде `"0.00"` (ноль), `"-10.01"` (отрицательное число), `"10.0001"` (слишком точное число)
* `AMOUNT_MISMATCH` - если указаны items, но сумма по всем `item.amount` не равна `total.amount`
* `INVALID_COUNTRY` - пока поддерживается только `"ru"`
* `INVALID_CURRENCY` - пока поддерживается только `"RUB"`
* `INVALID_VERSION` - поддерживается только `2`
* `MERCHANT_NOT_FOUND` - мерчант не найден
* `GATEWAY_NOT_FOUND` - psp не найден
* `PSP_ACCOUNT_ERROR` — платежный шлюз заблокирован.
* `MERCHANT_ACCOUNT_ERROR` — мерчант или ориджин заблокированы.

#### POST /api/v1/user_cards/{card_id}/set_default (draft)
Параметры запроса:

path:
* `card_id` - guid

query:
* `default_uid` - число. Передавать, если известен. Для того, чтобы мультиавторизация не ломала нам пользовательский опыт

Ответ:
```
{
  "status": "success",
  "code": 200,
  "data": {}
}
```

```
{
  "status": "fail",
  "code": 400,
  "data": {
    "message": "CARD_NOT_FOUND",
    "params": {}
  }
}
```


#### POST /api/v1/is_ready_to_pay
Параметры запроса:

query:
* `default_uid` - число. Передавать, если известен. Для того, чтобы мультиавторизация не ломала нам пользовательский опыт

Тело запроса:
```
{
  "merchant_origin": "https://best-shop.ru",
  "merchant_id": "guid",

  "existing_payment_method_required": true|false,
  "payment_methods": array<{
      "type": "CARD",
      "gateway": string,
      "gateway_merchant_id": string,
      "allowed_auth_methods": array<PAN_ONLY|CLOUD_TOKEN>,
      "allowed_card_networks": array<AMEX|DISCOVER|JCB|MASTERCARD|VISA|MIR|UNIONPAY|UZCARD>,
  }>
}
```

Ответ:
```
{
  "status": "success",
  "code": 200,
  "data": {
    "is_ready_to_pay": true|false
  }
}
```

```
{
  "status": "fail",
  "code": 400,
  "data": {
    "message": "MERCHANT_NOT_FOUND",
    "params": {}
  }
}
```

Коды ошибок:

* `MERCHANT_NOT_FOUND` — мерчант не найден.
* `MERCHANT_ORIGIN_ERROR` — невалидный `merchant_origin`.
* `INSECURE_MERCHANT_ORIGIN` — сайт мерчанта не защищен HTTPS.
* `MERCHANT_ACCOUNT_ERROR` — мерчант или ориджин заблокированы.
