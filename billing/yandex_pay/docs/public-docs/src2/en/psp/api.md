# API for payment gateway

The Yandex Pay API is used for cross-server data transfers from the payment gateway to the Yandex Pay service.

## Authentication {#auth}

For authentication, pass the JWS token from the request with detached content according to [RFC7515 Appendix F](https://tools.ietf.org/html/rfc7515#appendix-F) in the `Authorization` header:

```text
Authorization: Bearer <JWS-token>
```

The JWS token is signed with an authentication key that's [created](integration.md#genkey-auth) during integration.

## JWS token for the request {#gen-token}

### Create a signature message {#msg-to-sign}

Message template:

```text
message = upper(method) + '&' + resource_path + '&' + url_query + '&' + request_body
```

Message components:

* `upper(method)`: A HTTP method.
* `resource_path`: A path to the resource.
* `url_query`: Request parameters with URL encoding, for example, `bar=baz&foo=quux`.
* `request_body`: A request body.

For example, for the request:

```text
POST /api/psp/v1/example?bar=baz&foo=quux
Content-Type: application/json; encoding=utf-8
Content-Length: 2
...
{"foo": "bar"}
```

The message (`message`) according to the template is as follows:

```text
POST&/api/psp/v1/example&bar=baz&foo=quux&{"foo": "bar"}
```

### Request signature {#sign-msg}

Using the private authentication key (auth key), the payment gateway creates a JWS token and signs [message](#msg-to-sign) using the `ECDSA` algorithm with a `P-256` curve and a `SHA-256` hash function.
The following data is transmitted in the `protected` header:

* `kid` of the key.
* The `ES256` algorithm.
* `iat`: the token creation timestamp in seconds since the beginning of the UNIX epoch.

Sample request in Python:

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

Sample JWT token:

```text
eyJhbGciOiJFUzI1NiIsImlhdCI6MTYwOTMyODc1Niwia2lkIjoiMS1nYXRld2F5SWQifQ..2zm8VExAPQr9nBHb5JCWdChOoqfquv6Jm0Ky6eESaJXz
Pu9s9RrsRh2-tJNGdYPdt21ifJ_is-ZL-rp_vCrFSA
```

## Sending notifications about payment status changes {#payment-notification}

### Request URI {#payment-notification-uri}

Production:

```text
POST https://pay.yandex.ru/api/psp/v1/payment_notification
```

Testing:

```text
POST https://sandbox.pay.yandex.ru/api/psp/v1/payment_notification
```

### Request format {#payment-notification-params}

| Parameter | Type | Description |
| -------------- | ------------------ | ------- |
| `messageId` | string | The message ID from the decrypted PaymentToken. |
| `paymentId` | string  | The unique identifier of the payment in PSP's system. |
| `recurring` | boolean | Flag indicating that the payment was performed by previously stored PaymentToken. |
| `status` | string enum | <p> Payment status: </p> <ul><li>`SUCCESS`: The payment is completed successfully. Authorized for single-stage or post-authorized for two-stage payment.</li> <li>`FAIL`: Payment error. The reason for the error is indicated in the `reasonCode` and `reason` boxes.</li><li>`REVERSE`: The payment is canceled (the funds are unblocked).</li><li>`REFUND`: A full or partial refund.</li><li>`CHARGEBACK`: A refund after a protest from the issuing bank.</li><li>`HOLD`: The funds are blocked for a two-stage payment.</li></ul> <p>The status list can be expanded.</p> |
| `eventTime` | string | The time of the current event with a millisecond precision or higher. The `RFC 3339` format: `YYYY-MM-DDThh:mm:ss.sssTZD` |
| `amount` | integer | The amount of the current event in minimum currency units. For example, the minimum unit for the ruble is a kopeck. |
| `currency` | string | The ISO 4217 currency code. For example, the code for the ruble is `RUB`. |
| `rrn` | string | RRN (Reference Retrieval Number) ID of the bank transaction. This parameter is required for the `SUCCESS` and `HOLD` statuses. For other statuses, it's optional. |
| `approvalCode` | string | The payment ApprovalCode. This parameter is required for the `SUCCESS` and `HOLD` statuses. For other statuses, it's optional. |
| `eci` | string | The transaction ECI (Electronic Commerce Indicator). This parameter is required for the `SUCCESS` and `HOLD` statuses. For other statuses, it's optional. |
| `reasonCode` | string | The error code. The parameter is required only for the `FAIL` status. |
| `reason` | string | A text description of the error. The parameter is required only for the `FAIL` status. For example, the description of the `ISSUER_DECLINED` code may contain the reason for the rejection, like insufficient funds. |

### Error codes {#payment-notification-codes}

The error code list can be expanded.

| Code | <div align="center">Reason type</div> | Description |
| ------------------------------------------------ | --------------------------------------- | ----------------------------------------------------------------------------- |
| `YANDEX_PAY_TOKEN_AMOUNT_MISMATCH` | <div align="center">Yandex Pay</div> | The payment amount doesn't match the amount in `transactionDetails` in `PaymentToken`. |
| `YANDEX_PAY_TOKEN_INVALID` | <div align="center">Yandex Pay</div> | Invalid token. |
| `YANDEX_PAY_TOKEN_EXPIRED` | <div align="center">Yandex Pay</div> | The `PaymentToken` has expired. |
| `3DS_ERROR` | <div align="center">Common</div> | 3DS error. |
| `ISSUER_DECLINED` | <div align="center">Common</div> | The payment was rejected by the issuing bank. |
| `REJECTED` | <div align="center">Common</div> | Other reasons for payment cancelation. |

### Request examples {#payment-notification-body-example}

#### Blocking funds {#payment-notification-hold}

An example of blocking 100 rubles:

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

#### Unblocking funds {#payment-notification-reverse}

An example of unblocking 100 rubles:

```text
{
    "messageId": "8f4ac9e4-...",
    "status": "REVERSE",
    "amount: 10000,
    "currency": "RUB",
    "eventTime": "2020-12-18T22:33:11.456+03:00"
}
```

#### Debiting funds {#payment-notification-success}

An example of debiting 50 rubles using a Visa card:

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

The charged amount may be less than the blocked amount.

#### Payment error {#payment-notification-fail}

An example of a payment of USD 50 with an error:

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

#### Refund {#payment-notification-refund}

An example of a refund of 1 ruble:

```text
{
    "messageId": "8f4ac9e4-...",
    "status": "REFUND",
    "amount": 100,
    "currency": "RUB",
    "eventTime": "2020-12-18T22:33:11.456+03:00"
}
```

The number of refunds can be more than one. The refund can be partial (the refund amount is less than the charged amount).

#### An HTTP request with headers {#payment-notification-http-request}

An example of a request with headers:

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

The message is signed during the creation of the JWT token:

```text
POST&/api/psp/v1/payment_notification&&{"messageId": "123", "status": "REFUND", "eventTime": "2020-12-18T22:33:11+03:00", "amount": 100, "currency": "RUB"}
```

### Response format {#payment-notification-response-format}

| Parameter | Description |
| --------- | ------- |
| `status` | <p> Response status: </p> <ul><li>`success`: The request was processed successfully.</li> <li>`fail`: Processing error.</li></ul> |
| `code` | A numeric HTTP response code. |
| `data` | A document with a response or an error. |

The `data` format with an error:

| Parameter | Description |
| --------- | -------- |
| `message` | The error code. |
| `params` | The document that's specific to the error code. |

### Response examples {#payment-notification-response-examples}

If the request is successful, a response with code 200 and an empty document will be returned. For example:

```text
{
  "status": "success",
  "code": 200,
  "data": {
  }
}
```

Otherwise, a response with an error code is returned. For example:

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

### Guarantees of message delivery {#retries}

The payment gateway must repeat the request with the notification until a successful response (code 2xx) from Yandex Pay is received. The repeat policy must be exponential or alternative. Repeats must occur within a day.
