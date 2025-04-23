# Rules of integration interaction for payment gateway

In the [payment process](https://yandex.ru/dev/yandex-pay/doc/index.html), the seller passes the Yandex Pay payment token to the payment gateway (PSP). The document defines the rules for payment token processing and the gateway's interaction with Yandex Pay.

The [PaymentToken cryptography](payment_token.md) section describes how the payment token is authenticated and decrypted.

The [API for payment gateway](api.md) section describes sending payment notifications from the payment gateway to the Yandex Pay API.

The [Integration](integration.md) section defines the procedure for generating, exchanging, and updating cryptographic keys between the gateway and Yandex Pay.
