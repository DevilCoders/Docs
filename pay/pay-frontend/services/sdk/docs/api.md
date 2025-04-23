# JS API

- [Интерфейс YaPay](../src/typings/index.ts)

## Инструкция подключения кнопки YandexPay на странице мерчанта

### Шаг 0

Для начала установите следующий HTML-код на всех страницах, где будет использоваться платёжные кнопки:
```html
<script src="https://pay.yandex.ru/sdk/v1/pay.js" onload="onYaPayLoad()" async></script>
```
Обратите внимание на аттрибут `onload`. В качестве значения в этот аттрибут необходимо передать название метода, в котором будет произведена инициализация и обработка платежей.

### Шаг 1 — Сформируйте данные платежа

Подробное описание полей можно найти в [интерфейсе](#интерфейс-yapay).

```js
var paymentData = {};
```

- Укажите окружение для работы. Для разработки лучше использовать тестовое окружение — `SANDBOX`:
  ```js
  paymentData.env = YaPay.PaymentEnv.Sandbox;
  ```
- Выберите версию YaPay Api:
  ```js
  paymentData.version = 2;
  ```
- Задайте код страны в которой будете работать и код валюты в которой будете принимать платежи:
  ```js
  paymentData.countryCode = YaPay.CountryCode.Ru;
  paymentData.currencyCode = YaPay.CurrencyCode.Rub;
  ```
- Укажите данные продавца:
  ```js
  paymentData.merchant = {
    id: 'test-merchant-id',
    name: 'test-merchant-name'
  };
  ```
  Значение `id` выдаётся при регистрации в Yandex Pay. В `name` укажите имя продавца.
  В примере указаны значения для тестового окружения.
- Сформируйте данные о товарах и сумме платежа:
  ```js
  paymentData.order = {
    id: 'test-order-id',
    total: {
      amount: '40.00',
    },
    items: [
      { label: 'Item A', amount: '15.00' },
      { label: 'Item B', amount: '25.00' }
    ]
  };
  ```
  Значение `id` формирует продавец, оно должно быть уникальным для каждого заказа.
- Выберите доступные методы оплаты:
  ```js
  paymentData.paymentMethods = [
    {
      type: YaPay.PaymentMethodType.Card,
      gateway: 'test-gateway',
      gatewayMerchantId: 'test-gateway-merchant-id',
      allowedAuthMethods: [YaPay.AllowedAuthMethod.PanOnly],
      allowedCardNetworks: [
        YaPay.AllowedCardNetwork.Visa,
        YaPay.AllowedCardNetwork.Mastercard,
        YaPay.AllowedCardNetwork.Mir,
        YaPay.AllowedCardNetwork.Uzcard
      ]
    }
  ];
  ```
  В примере указаны значения для тестового окружения.

- Если после оплаты необходимо вернуть пользовательский email для отправки чека:
  ```js
  // Запрашиваемые доп. данные
  paymentData.requiredFields: {
    billingContact: {
      email: true
    }
  }
  ```
### Шаг 2 — Создайте новый экземпляр платежа и запустите подготовку

```js
var payment = window.YaPay.Payment.create(paymentData);

// Запустить проверку данных.
payment.prepare().then(function onPaymentPrepared() {
  // Платёж готов к оплате.
  // Можно показать кнопку YaPay.
});
```

### Шаг 3 — Создайте кнопку

```js
// Создать экземпляр кнопки.
var container = document.querySelector('#button_container');
var button = YaPay.Button.create({
  type: YaPay.ButtonType.Simple,
  theme: YaPay.ButtonTheme.Black,
  width: YaPay.ButtonWidth.Auto,
});

// Смонтировать кнопку в dom.
button.mount(container);

// Подписаться на событие click.
button.on(YaPay.ButtonEventType.Click, function onPaymentButtonClick() {
  // Запустить оплату после клика на кнопку.
  payment.checkout();
});
```

### Шаг 4 — Опишите обработку событий от платёжной формы

```js
// Подписаться на событие process.
paymeny.on(YaPay.PaymentEventType.Process, function onPaymentProcess(event) {
  // Получить платёжный токен.
  alert('Payment token — ' + event.token);
  // Получить Email плательщика.
  alert('Email — ' + event.billingContact.email);
});
```

### Полный код примера

```js
function onYaPayLoad() {
  const YaPay = window.YaPay;

  // Сформировать данные платежа.
  var paymentData = {
    env: YaPay.PaymentEnv.Sandbox,
    version: 1,
    countryCode: YaPay.CountryCode.Ru,
    currencyCode: YaPay.CurrencyCode.Rub,
    merchant: {
      id: 'test-merchant-id',
      name: 'test-merchant-name'
    },
    order: {
      id: 'test-order-id',
      total: { amount: '20.00' },
      items: [
        { label: 'Item A', amount: '15.00' },
        { label: 'Item B', amount: '25.00' }
      ]
    },
    paymentMethods: [
      {
        type: YaPay.PaymentMethodType.Card,
        gateway: 'test-gateway',
        gatewayMerchantId: 'test-gateway-merchant-id',
        allowedAuthMethods: [YaPay.AllowedAuthMethod.PanOnly],
        allowedCardNetworks: [
          YaPay.AllowedCardNetwork.Visa,
          YaPay.AllowedCardNetwork.Mastercard,
          YaPay.AllowedCardNetwork.Mir,
          YaPay.AllowedCardNetwork.Uzcard
        ]
      }
    ],
    // Запрашиваемые доп. данные
    requiredFields: {
      billingContact: {
        email: true
      }
    }
  };

  // Создать экземпляр платежа.
  YaPay.createPayment(paymentData).then(function onPaymentPrepared(payment) {
    // Создать экземпляр кнопки.
    var container = document.querySelector('#button_container');
    var button = payment.createButton({
      type: YaPay.ButtonType.Simple,
      theme: YaPay.ButtonTheme.Black,
      width: YaPay.ButtonWidth.Auto,
    });

    // Смонтировать кнопку в dom.
    button.mount(container);

    // Подписаться на событие click.
    button.on(YaPay.ButtonEventType.Click, function onPaymentButtonClick() {
      // Запустить оплату после клика на кнопку.
      payment.checkout();
    });
  });

  // Подписаться на событие process.
  payment.on(YaPay.PaymentEventType.Process, function onPaymentProcess(event) {
    // Получить платёжный токен.
    alert('Payment token — ' + event.token);
    // Получить Email плательщика.
    alert('Email — ' + event.billingContact.email);
  });
}
```