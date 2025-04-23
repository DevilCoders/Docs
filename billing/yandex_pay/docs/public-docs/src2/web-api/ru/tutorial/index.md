# Добавление кнопки {{ product }}

Добавьте кнопку {{ product }} на страницу оплаты вашего сайта.


## Требования к подключению {#prepare}

Для установки кнопки {{ product }} должны быть выполнены следующие требования:
- Ваш сайт работает по протоколу HTTPS.
- На вашем сайте не должен обрезаться параметр `__YP__` из URL ([подробнее](pay-via-query.md)).
- Политики [CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) на вашем сайте разрешают использовать:
   ```
   script-src: https://pay.yandex.ru
   frame-src: https://pay.yandex.ru
   img-src: https://pay.yandex.ru
   connect-src: https://pay.yandex.ru
   ```

## Подключение {{ product }} {#connect-yandex-pay}

### Шаг 1. Подключите SDK {#step1}

Установите HTML-код на всех страницах, где будет размещена кнопка {{ product }}, перед закрывающим тегом ` </body> `.
В качестве значения в атрибут ` onload ` передайте название метода, который будет отвечать за инициализацию и обработку платежей.

```html
<script src="https://pay.yandex.ru/sdk/v1/pay.js" onload="onYaPayLoad()" async></script>
```


### Шаг 2. Сформируйте данные платежа {#step2}
Используйте объект ` paymentData `.

1. Укажите окружение для работы. Для разработки используйте тестовое окружение ` SANDBOX `.
   ```js
   paymentData.env = YaPay.PaymentEnv.Sandbox;
   ```
1. Выберите версию {{ product }} API.
   ```js
   paymentData.version = 2;
   ```
1. Укажите код валюты и код страны, в которой будете работать и принимать платежи.
   ```js
   paymentData.countryCode = YaPay.CountryCode.Ru;
   paymentData.currencyCode = YaPay.CurrencyCode.Rub;
   ```
1. Укажите данные продавца:
   - ` id ` — идентификатор, который продавец получает при регистрации в {{ product }}.
   - ` name ` — имя продавца.
   ```js
   paymentData.merchant = {
     id: 'bbb9c171-2fab-45e6-b1f8-6212980aa9bb',
     name: 'test-merchant-name',
     url: 'https://test-merchant-url.ru'
   };
   ```
   Для тестового окружения можно использовать идентификатор тестового магазина: ` bbb9c171-2fab-45e6-b1f8-6212980aa9bb `.

1. Добавьте информацию о товарах и сумме платежа. Идентификатор заказа (` id `) формирует продавец, ` id ` должен быть уникальным для каждого заказа.
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
1. Добавьте доступные методы оплаты.
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
         YaPay.AllowedCardNetwork.Maestro,
         YaPay.AllowedCardNetwork.VisaElectron
       ]
     }
   ];
   ```
   В примере указаны значения для тестового окружения.
   Список всех разрешенных платежных систем можно найти в [справочнике](../method-reference/index.md).


### Шаг 3. Создайте новый экземпляр платежа и запустите проверку {#step3}

```js
window.YaPay.createPayment(paymentData)
  .then(function (payment) {
    // Платеж готов к оплате.
    // Можно показать кнопку {{ product }}.
  })
  .catch(function (err) {
    // Не получилось создать платеж.
  });
```

### Шаг 4. Создайте кнопку {{ product }} {#step4}

```js
// Создать экземпляр кнопки.
const container = document.querySelector('#button_container');
const button = payment.createButton({
  type: YaPay.ButtonType.Pay,
  theme: YaPay.ButtonTheme.Black,
  width: YaPay.ButtonWidth.Auto,
});

// Смонтировать кнопку в DOM.
button.mount(container);

// Подписаться на событие click.
button.on(YaPay.ButtonEventType.Click, function onPaymentButtonClick() {
  // Запустить оплату после клика на кнопку.
  payment.checkout();
});
```

### Шаг 5. Подпишитесь на события платежной формы {#step5}

```js
// Подписаться на событие process.
payment.on(YaPay.PaymentEventType.Process, function onPaymentProcess(event) {
  // Получить платежный токен.
  alert('Payment token — ' + event.token);
  // Закрыть форму Yandex.Pay.
  payment.complete(YaPay.CompleteReason.Success);
});
```



### Шаг 6. Обработайте исключения {#step6}

```js
// Подписаться на событие error.
payment.on(YaPay.PaymentEventType.Error, function onPaymentError(event) {
  // Вывести информацию о недоступности оплаты в данный момент
  // и предложить пользователю другой способ оплаты.

  // Закрыть форму Yandex.Pay
  payment.complete(YaPay.CompleteReason.Error);
});

// Подписаться на событие abort.
// Это когда пользователь закрыл форму Yandex.Pay.
payment.on(YaPay.PaymentEventType.Abort, function onPaymentError(event) {
  // Предложить пользователю другой способ оплаты.
});
```

### Шаг 7. (Опционально) Запросите email плательщика {#step7}

Если вам нужен email плательщика для отправки чека, то его можно запросить с платежной формы Yandex.Pay.

```js
paymentData.requiredFields = {
  billingContact: { email: true }
};

payment.on(YaPay.PaymentEventType.Process, function onPaymentProcess(event) {
  // Получить email плательщика.
  // Будет присутствовать, только если был запрошен в PaymentData.
  alert('Billing email — ' + event.billingContact.email);
});
```

{% note info %}

Воспользуйтесь разделом [Частые ошибки](common-mistakes.md), если у вас возникли сложности с настройкой.

{% endnote %}



### Пример {#example}


```js
function onYaPayLoad() {
  const YaPay = window.YaPay;

  // Сформировать данные платежа.
  const paymentData = {
    env: YaPay.PaymentEnv.Sandbox,
    version: 2,
    countryCode: YaPay.CountryCode.Ru,
    currencyCode: YaPay.CurrencyCode.Rub,
    merchant: {
      id: 'bbb9c171-2fab-45e6-b1f8-6212980aa9bb',
      name: 'test-merchant-name',
      url: 'https://test-merchant-url.ru'
    },
    order: {
      id: 'test-order-id',
      total: { amount: '40.00' },
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
          YaPay.AllowedCardNetwork.Maestro,
          YaPay.AllowedCardNetwork.VisaElectron
        ]
      }
    ],
    // Опционально (если выполнить шаг 7).
    requiredFields: {
      billingContact: { email: true }
    },
  };

  // Создать платеж.
  YaPay.createPayment(paymentData)
    .then(function (payment) {
      // Создать экземпляр кнопки.
      const container = document.querySelector('#button_container');
      const button = payment.createButton({
        type: YaPay.ButtonType.Pay,
        theme: YaPay.ButtonTheme.Black,
        width: YaPay.ButtonWidth.Auto,
      });

      // Опционально (если выполнить шаг 8)
      button = payment.createButton({
        type: YaPay.ButtonType.Checkout,
        theme: YaPay.ButtonTheme.Black,
        width: YaPay.ButtonWidth.Auto,
      });

      // Смонтировать кнопку в DOM.
      button.mount(container);

      // Подписаться на событие click.
      button.on(YaPay.ButtonEventType.Click, function onPaymentButtonClick() {
        // Запустить оплату после клика на кнопку.
        payment.checkout();
      });

      // Подписаться на событие error.
      payment.on(YaPay.PaymentEventType.Error, function onPaymentError(event) {
        // Вывести информацию о недоступности оплаты в данный момент
        // и предложить пользователю другой способ оплаты.

        // Закрыть форму Yandex.Pay.
        payment.complete(YaPay.CompleteReason.Error);
      });

      // Подписаться на событие abort.
      // Это когда пользователь закрыл форму {{ product }}.
      payment.on(YaPay.PaymentEventType.Abort, function onPaymentAbort(event) {
        // Предложить пользователю другой способ оплаты.
      });

      // Подписаться на событие process.
      payment.on(YaPay.PaymentEventType.Process, function onPaymentProcess(event) {
        // Получить платежный токен.
        alert('Payment token — ' + event.token);

        // Опционально (если выполнить шаг 7).
        alert('Billing email — ' + event.billingContact.email);

        // Закрыть форму {{ product }}.
        payment.complete(YaPay.CompleteReason.Success);
      });
    })
    .catch(function (err) {
      // Платеж не создан.
    });
}
```



## Проверка доступности {{ product }} {#ready-to-pay-check}

Если вам нужно проверить, доступен ли {{ product }} для конкретного платежа, это можно сделать



### Проверка merchantId {#ready-to-pay-check-case1}
```js
function onYaPayLoad() {
  const YaPay = window.YaPay;

  const checkParams = {
    merchantId: 'bbb9c171-2fab-45e6-b1f8-6212980aa9bb'
  };

  YaPay.readyToPayCheck(checkParams)
    .then(function (isReady) {
      if (isReady) {
        // {{ product }} доступен для мерчанта bbb9c171...
      } else {
        // Оплата через {{ product }} недоступна
      }
    });
}
```



### Проверка merchantId и paymentMethods {#ready-to-pay-check-case2}
```js
function onYaPayLoad() {
  const YaPay = window.YaPay;

  const checkParams = {
    merchantId: 'bbb9c171-2fab-45e6-b1f8-6212980aa9bb',
    paymentMethods: [
      {
        type: YaPay.PaymentMethodType.Card,
        gateway: 'test-gateway',
        gatewayMerchantId: 'test-gateway-merchant-id',
        allowedAuthMethods: [YaPay.AllowedAuthMethod.PanOnly],
        allowedCardNetworks: [
          YaPay.AllowedCardNetwork.Mir,
        ]
      }
    ]
  };

  YaPay.readyToPayCheck(checkParams)
    .then(function (isReady) {
      if (isReady) {
        // {{ product }} доступен для оплаты картой МИР
      } else {
        // Оплата через {{ product }} недоступна
      }
    });
}
```

См. также:
- [Подключение формы {{ product }} Checkout](yandex-pay-checkout.md)
- [Подключение кнопки с оплатой на стороне {{ product }}](yandex-pay-server-pay.md)
- [Работа {{ product }} через редиректы](pay-via-query.md)
- [Частые ошибки в подключении](common-mistakes.md)
- [Тестирование](testing-integration.md)
