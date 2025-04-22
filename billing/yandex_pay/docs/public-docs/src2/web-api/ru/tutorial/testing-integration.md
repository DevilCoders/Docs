# Тестирование

Для установки кнопки оплаты {{ product }} вам доступна интеграция в тестовой среде, с помощью которой можно провести сценарий покупки через {{ product }} на вашем сайте.

Чтобы воспользоваться тестовой средой, укажите в объекте ` paymentData ` окружение ` SANDBOX `:

Пример кода:


```
paymentData.env = YaPay.PaymentEnv.Sandbox;;
```

Подробнее см. в разделе [Подключение](./index.md).

В тестовой среде доступны тестовые платежные карты:
- ` Visa ***4242 ` для проверки сценария [платежа по банковской карте](../method-reference/yapay.md#allowed-auth-method) ` AllowedAuthMethod==PanOnly `.
- ` MasterCard ***4444 ` для проверики сценария [платежа по токенизированной карте](../method-reference/yapay.md#allowed-auth-method) ` AllowedAuthMethod==CloudToken `.
