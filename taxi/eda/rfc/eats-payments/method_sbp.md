# Метод оплаты СБП

## Общее описание

Система быстрых платежей (СБП) — это сервис Банка России, позволяющий физическим лицам совершать мгновенные переводы по номеру мобильного телефона в любой банк — участник СБП, а также производить оплату товаров и услуг в розничных магазинах и сети интернет по QR-коду.

При оплате через СБП нет холдирования (блокировки средств), так как средства списываются и возвращаются моментально. Из-за этого для ритейна нужно сделать списание на 10% большей суммы, чтобы взять дополнительные средства при формировании заказа.

[Тикет](https://st.yandex-team.ru/EDAPRODUCT-1649)

[Описание в Трасте](https://wiki.yandex-team.ru/trust/sbp/)

[Как работает СБП](https://sbp.nspk.ru/business/)

### Шаги пользователя

1. Пользователь открывает чекаут
2. На чекауте отображается новый метод оплаты - СБП
3. Пользователь выбирает его и нажимает "Оплатить"
4. Открывается окно выбора банка
5. Пользователь выбирает банк
6. Происходит открытие приложения банка
7. Пользователь нажимает "Оплатить" в приложении банка
8. Происходит возврат на чекаут
9. На чекауте происходит переход на трекинг заказа

В десктопе после нажатия "Оплатить" на чекауте открывается окно с qr-кодом, который нужно просканировать телефоном, чтобы открыть окно выбора банка.

### Технические шаги

1. Открытие чекатуа, запрос в ручку `/api/v2/cart/go-checkout`
2. В ответе приходят офферы `type: sbp`
3. В списке методов оплаты появляется новый - СБП
4. Создание заказа `/api/v1/orders` с `type: sbp`
5. Запуск трекинга оплаты `/eats/v1/eats-payments/v1/order/tracking`, ожидание статуса `sbp_required`
6. Открытие `PaymentSDK` с токеном и предвыбранным методом оплаты СБП
7. Выбор банка пользователем, переход в приложение банка
8. При открытии приложения Еды обратно, переход на трекинг заказа `/api/v2/orders/tracking` - там будет статус "Ожидание оплаты"

### Неудачный сценарий оплаты

В любом случае переходить на трекинг заказа (как и в случае с 3DS), там будет ссылка на СБП (допустим, если пользователь потерял ее или закрыл банковское приложение), так же, появится кнопка повтора заказа при таймауте оплаты.

## Изменения в ручках

### eda-checkout

[go-checkout](https://github.yandex-team.ru/taxi/schemas/blob/develop/schemas/services/eda-checkout/api/definitions/go-checkout.yaml)

Приходит новый способ оплаты СБП для отображения в списке:

```
PossiblePayment:
    ...
    discriminator:
        ...
        mapping:
            cash: "#/PossiblePaymentBase"
            card: "#/PossiblePaymentCard"
            add_new_card: "#/PossiblePaymentAddNewCard"
            applepay: "#/PossiblePaymentApplepay"
            googlepay: "#/PossiblePaymentGooglepay"
            corp: "#/PossiblePaymentBase"
            personal_wallet: "#/PossiblePaymentBase"
            postpayment: "#/PossiblePaymentBase"
+           sbp: "#/PossiblePaymentBase"

PossiblePaymentBase:
    ...
    properties:
        ...
        type:
            type: string
            description: Тип оплаты
            example: card
            enum:
                - cash
                - card
                - add_new_card
                - applepay
                - googlepay
                - corp
                - personal_wallet
                - postpayment
+               - sbp
```

Так же, в `description` в `PossiblePaymentBase` будет приходить [объяснение того](https://st.yandex-team.ru/EDAWWW-3462#620ccd7cba6fe7060a52a6f8), почему в ритейле спишется большая сумма, чем стоимость заказа (для дополнительных списаний).

[orders](https://github.yandex-team.ru/taxi/schemas/blob/develop/schemas/services/eda-checkout/api/definitions/orders.yaml)

Возможность отправки нового способа при создании заказа:

```
+SBP:
+    type: object
+    additionalProperties: false
+    description: СБП
+    required:
+      - type
+      - costForCustomer
+    properties:
+        type:
+            type: string
+            enum: [sbp]
+        costForCustomer:
+            type: string
+            description: Стоимость для клиента
+            example: "100.00"

PaymentInformation:
    ...
    oneOf:
        - $ref: "#/Cash"
        - $ref: "#/Card"
        - $ref: "#/ApplePay"
        - $ref: "#/GooglePay"
        - $ref: "#/Corporate"
        - $ref: "#/PersonalWallet"
+       - $ref: "#/SBP"
    discriminator:
        ...
        mapping:
            cash: "#/Cash"
            card: "#/Card"
            applepay: "#/ApplePay"
            googlepay: "#/GooglePay"
            corp: "#/Corporate"
            personal_wallet: "#/PersonalWallet"
+           sbp: "#/SBP"
```

Как бэкенд узнает о том, что деньги списались - описание [в схеме](https://wiki.yandex-team.ru/trust/sbp/#sxemavzaimodejjstvijaservisastrastom), на 15 и 16 пункте.

### eats-payments

[tracking](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/uservices/services/eats-payments/docs/yaml/api/order_tracking.yaml)

Приходит новый статус в трекинге, требующий оплатить через СБП:

```
+PaymentPayloadSBP:
+    type: object
+    additionalProperties: false
+    required:
+      - type
+      - url
+      - purchase_token
+    properties:
+        type:
+            type: string
+            enum:
+              - sbp
+        url:
+            type: string
+            description: Адрес страницы с СБП
+        purchase_token:
+            type: string
+            description: purchase_token от траста

PaymentPayload:
    oneOf:
      - $ref: '#/components/schemas/PaymentPayload3ds'
+     - $ref: '#/components/schemas/PaymentPayloadSBP'
    discriminator:
        propertyName: type
        mapping:
            3ds: '#/components/schemas/PaymentPayload3ds'
+           sbp: '#/components/schemas/PaymentPayloadSBP'

TrackedOrderPayment:
    ...
    properties:
        status:
            ...
            enum:
              - pending
              - 3ds_required
+             - sbp_required
              - done
              - error
```

Логика работы аналогична `3ds_required` - нужно дождаться `done` и перейти на трекинг заказа.

## На клиентах

Что нужно добавить:

- Поддержать вывод нового метода оплаты - СБП;
- Поддержать создание заказа с новым методом оплаты;
- Поддержать новый статус трекинга оплаты.

### Трекинг оплаты

![menu_search](./img/clients_sbp.svg)

<!--
%%(plantuml)
@startuml

participant Приложение
participant PaymentTracking
participant "PaymentSDK/WebSDK"
participant Банк

loop status != sbp_required
  Приложение -> PaymentTracking: Опрос статуса оплаты
  Приложение <- PaymentTracking: status
end
Приложение <- PaymentTracking: purchase_token
Приложение -> "PaymentSDK/WebSDK": Начать оплату по СБП
alt Десктопный веб
  "PaymentSDK/WebSDK" -> "PaymentSDK/WebSDK": Пользователь сканирует qr-код
end
"PaymentSDK/WebSDK" -> "PaymentSDK/WebSDK": Открыть окно выбора банка
"PaymentSDK/WebSDK" -> Банк: Открыть приложение банка
"PaymentSDK/WebSDK" <-- Банк
Приложение <-- "PaymentSDK/WebSDK"
loop status != done
  Приложение -> PaymentTracking: Опрос статуса оплаты
  Приложение <- PaymentTracking: status
end
Приложение -> Приложение: Переход на трекинг заказа

@enduml
%%
-->

В вебе нужно открывать прямые ссылки на СБП в новом окне - `qr.nspk.ru`
