# API для платежного шлюза

Yandex Pay API используется для межсерверной передачи данных от платежного шлюза к сервису Yandex Pay.

## Аутентификация {#auth}

Для аутентификации передайте JWS-токен от передаваемого запроса с detached-контентом согласно [RFC7515 Appendix F](https://tools.ietf.org/html/rfc7515#appendix-F) в заголовке `Authorization`:

```text
Authorization: Bearer <JWS-token>
```

JWS-токен подписывается ключом аутентификации, который [создается](integration.md#genkey-auth) в процессе интеграции.

## JWS-токен для запроса {#gen-token}

### Создание сообщения для подписи {#msg-to-sign}

Шаблон сообщения:

```text
message = upper(method) + '&' + resource_path + '&' + url_query + '&' + request_body
```

Компоненты сообщения:

* `upper(method)` — HTTP-метод.
* `resource_path` — путь к ресурсу.
* `url_query` — параметры запроса c URL-кодированием, например `bar=baz&foo=quux`.
* `request_body` — тело запроса.

Например, для запроса:

```text
POST /api/psp/v1/example?bar=baz&foo=quux
Content-Type: application/json; encoding=utf-8
Content-Length: 2
...
{"foo": "bar"}
```

Cообщение (`message`) согласно шаблону будет следующим:

```text
POST&/api/psp/v1/example&bar=baz&foo=quux&{"foo": "bar"}
```

### Подпись запроса {#sign-msg}

С помощью приватного ключа аутентификации (auth key) платежный шлюз создает JWS-токен и подписывает [message](#msg-to-sign), используя алгоритм `ECDSA` с кривой `P-256` и хеш-функцией `SHA-256`.
В заголовке `protected` передаются:

* `kid` ключа;
* алгоритм `ES256`;
* `iat` — timestamp в секундах с начала эпохи UNIX создания токена.

Пример запроса на Python:

```python
from time import time
from jwcrypto import jwk, jws

with open("key.pem", "rb") as pemfile:
    key = jwk.JWK.from_pem(pemfile.read())

iat = int(time())
kid = '1-gatewayId'
message = b'POST&/api/psp/v1/example&bar=baz&foo=quux&{}'

token = jws.JWS(message)
token.add_signature(key, protected={
    'kid': kid,
    'alg': 'ES256',
    'iat': iat,
})
token.detach_payload()
sign = token.serialize(compact=True)
print(sign)
```

Пример JWT-токена:

```text
eyJhbGciOiJFUzI1NiIsImlhdCI6MTYwOTMyODc1Niwia2lkIjoiMS1nYXRld2F5SWQifQ..2zm8VExAPQr9nBHb5JCWdChOoqfquv6Jm0Ky6eESaJXz
Pu9s9RrsRh2-tJNGdYPdt21ifJ_is-ZL-rp_vCrFSA
```

## Отправка уведомлений об изменении статуса платежа {#payment-notification}

### URI запроса {#payment-notification-uri}

Продакшн:

```text
POST https://pay.yandex.ru/api/psp/v1/payment_notification
```

Тестинг:

```text
POST https://sandbox.pay.yandex.ru/api/psp/v1/payment_notification
```

### Формат запроса {#payment-notification-params}

| Параметр      | Тип               | Описание|
| --------------|------------------ | ------- |
| `messageId`   | string            | Идентификатор сообщения из расшифрованного PaymentToken. |
| `paymentId`   | string            | Идентификатор платежа на стороне шлюза.                                        |
| `recurring`   | boolean           | Флаг, означающий, что платеж был выполнен по ранее сохраненному PaymentToken.  |
| `status`      | string enum       | <p> Статус платежа: </p> <ul><li>`SUCCESS` — платеж успешно проведен. Авторизован для одностадийной или пост-авторизован для двухстадийной оплаты.</li> <li>`FAIL` — ошибка платежа. В полях `reasonCode` и `reason` указывается причина ошибки.</li><li>`REVERSE` — платеж отменен (средства разблокированы).</li><li>`REFUND` — возврат средств полный или частичный.</li><li>`CHARGEBACK` — возврат средств после опротестования по инициативе банка-эмитента.</li><li>`HOLD` — блокировка средств для двухстадийного платежа.</li></ul> <p>Список статусов может быть расширен.</p>|
| `eventTime`   | string            | Время текущего события с точностью до миллисекунд или выше. Формат `RFC 3339`: `YYYY-MM-DDThh:mm:ss.sssTZD` |
| `amount`      | integer           | Сумма текущего события в минимальных единицах валюты. Например, для рубля в копейках.|
| `currency`    | string            | Код валюты по ISO 4217. Например, для рубля код `RUB`. |
| `rrn`         | string            | RRN (Reference Retrieval Number) идентификатор банковской транзакции. Параметр обязателен для статусов `SUCCESS` и `HOLD`, опциональный для остальных статусов. |
| `approvalCode`| string            | ApprovalCode оплаты. Параметр обязателен для статусов `SUCCESS` и `HOLD`, опциональный для остальных статусов. |
| `eci`         | string            | ECI (Electronic Commerce Indicator) транзакции. Параметр обязателен для статусов `SUCCESS` и `HOLD`, опциональный для остальных статусов. |
| `reasonCode`  | string            | Код ошибки. Параметр обязательный только для статуса `FAIL`. |
| `reason`      | string            | Текстовое описание ошибки. Параметр обязательный только для статуса `FAIL`. Например, для кода `ISSUER_DECLINED` в описании может быть написана причина отклонения — недостаточно средств. |

### Коды ошибок {#payment-notification-codes}

Список кодов ошибок может быть расширен.

| Код                                              | <div align="center">Тип причины</div>  |    Описание                                                                                           |
| ------------------------------------------------ | ---------------------------------------| ----------------------------------------------------------------------------- |
| `YANDEX_PAY_TOKEN_AMOUNT_MISMATCH`               | <div align="center">Yandex Pay</div>   | Сумма платежа не совпадает с amount из `transactionDetails` в `PaymentToken`. |
| `YANDEX_PAY_TOKEN_INVALID`                       | <div align="center">Yandex Pay</div>   | Недействительный токен.                                                       |
| `YANDEX_PAY_TOKEN_EXPIRED`                       | <div align="center">Yandex Pay</div>   | Истекло время жизни `PaymentToken`.                                           |
| `3DS_ERROR`                                      | <div align="center">Общие</div>        | Ошибка 3DS.                                                                   |
| `ISSUER_DECLINED`                                | <div align="center">Общие</div>        | Платеж отклонен банком-эмитентом.                                             |
| `REJECTED`                                       | <div align="center">Общие</div>        | Иные причины отмены платежа.                                                  |

### Примеры запросов {#payment-notification-body-example}

#### Блокировка средств {#payment-notification-hold}

Пример блокировки средств на 100 рублей:

```text
{
    "messageId": "8f4ac9e4-...",
    "status": "HOLD",
    "amount: 10000,
    "currency": "RUB",
    "eventTime": "2020-12-18T22:33:11.456+03:00",
    "rrn": "255240195632",
    "approvalCode": "917220",
    "eci": "05"
}
```

#### Разблокировка средств {#payment-notification-reverse}

Пример разблокировки средств на 100 рублей:

```text
{
    "messageId": "8f4ac9e4-...",
    "status": "REVERSE",
    "amount: 10000,
    "currency": "RUB",
    "eventTime": "2020-12-18T22:33:11.456+03:00"
}
```

#### Списание средств {#payment-notification-success}

Пример списания средств на 50 рублей по карте Visa:

```text
{
    "messageId": "8f4ac9e4-...",
    "status": "SUCCESS",
    "amount: 5000,
    "currency": "RUB",
    "eventTime": "2020-12-18T22:33:11.456+03:00",
    "rrn": "255240195632",
    "approvalCode": "917220",
    "eci": "05"
}
```

Сумма списания может быть меньше суммы блокировки.

#### Ошибка платежа {#payment-notification-fail}

Пример платежа на 50 USD, завершенного с ошибкой:

```text
{
    "messageId": "8f4ac9e4-...",
    "amount: 5000,
    "currency": "USD",
    "status": "FAIL",
    "eventTime": "2020-12-18T22:33:11.456+03:00",
    "reasonCode": "ISSUER_DECLINED",
    "reason": "processing error: ..."
}
```

#### Возврат средств {#payment-notification-refund}

Пример с возвратом средств на 1 рубль:

```text
{
    "messageId": "8f4ac9e4-...",
    "status": "REFUND",
    "amount": 100,
    "currency": "RUB",
    "eventTime": "2020-12-18T22:33:11.456+03:00"
}
```

Количество возвратов может быть больше одного. Возврат может быть частичным (сумма возврата меньше, суммы списания).

#### HTTP-запрос с заголовками {#payment-notification-http-request}

Пример запроса с заголовками:

```text
> POST /api/psp/v1/payment_notification HTTP/1.1
> Host: sandbox.pay.yandex.ru
> Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJFUzI1NiIsImlhdCI6MTYyNDYzMz
M0Mywia2lkIjoiMS1OSENsdUJBZE5qSWcifQ..VpKjWGP0ADShKcLOeInN4Eoo7pD1a1H1sJhLeXc6rVvcmkooiL7zpgnvNLT1ZAJdciW9I8i3x-xaRirCSnkS1Q
> Content-Type: application/json
> Content-Length: 116
>
> {"messageId": "123", "status": "REFUND", "eventTime": "2020-01-01T00:00:00+00:00", "amount": 100, "currency": "RUB"}
```

При создании JWT-токена подписывается сообщение:

```text
POST&/api/psp/v1/payment_notification&&{"messageId": "123", "status": "REFUND", "eventTime": "2020-12-18T22:33:11+03:00", "amount": 100, "currency": "RUB"}
```

### Формат ответа {#payment-notification-response-format}

| Параметр  | Описание|
| --------- | ------- |
| `status`  | <p> Статус ответа: </p> <ul><li>`success` — запрос обработан успешно.</li> <li>`fail` — ошибка при обработке запроса.</li></ul>|
| `code`    | Числовой HTTP-код ответа. |
| `data`    | Документ с ответом или ошибкой. |

Формат `data` c ошибкой:

| Параметр  | Описание |
| --------- | -------- |
| `message` | Код ошибки.|
| `params`  | Документ специфичный для кода ошибки.|

### Примеры ответов {#payment-notification-response-examples}

В случае успеха, вернется ответ с кодом 200 и пустым документом. Например:

```text
{
  "status": "success",
  "code": 200,
  "data": {
  }
}
```

В противном случае вернется ответ с кодом ошибки. Например:

```text
{
  "data": {
    "params": {
      "description": "Authorization header is malformed"
      },
    "message": "ACCESS_DENIED"
  },
  "code": 403,
  "status": "fail"
}
```

### Гарантии доставки сообщений {#retries}

Платежный шлюз должен повторять запрос с отправкой нотификации до успешного ответа (код 2xx) от Yandex Pay. Политика повторов должна быть экспоненциальной или альтернативной. Повторы должны происходить в течение суток.
