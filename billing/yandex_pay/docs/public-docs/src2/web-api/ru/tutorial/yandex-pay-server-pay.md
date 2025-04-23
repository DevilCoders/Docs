# Добавление кнопки с оплатой на стороне {{ product }}

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
   paymentData.version = 3;
   ```
1. Укажите код валюты и код страны, в которой будете работать и принимать платежи.
   ```js
   paymentData.countryCode = YaPay.CountryCode.Ru;
   paymentData.currencyCode = YaPay.CurrencyCode.Rub;
   ```
1. Укажите данные продавца:
   - `merchantId` — идентификатор, который продавец получает при регистрации в {{ product }}.
   ```js
   paymentData.merchantId = 'bbb9c171-2fab-45e6-b1f8-6212980aa9bb'
   ```
   Для тестового окружения можно использовать идентификатор тестового магазина: ` bbb9c171-2fab-45e6-b1f8-6212980aa9bb `.

1.  Идентификатор заказа (` id `) формирует продавец, ` id ` должен быть уникальным для каждого заказа.
   ```js
   paymentData.orderId = 'test-order-id'
   ```

1. Добавьте информацию о корзине покупателя.
   При необходимости можно указать количество товара в корзине через свойство `quantity`.
    ```js
    paymentData.cart = {
      items: [
        {
          productId: '1',
          total: '150.00'
        },
        {
          productId: '2',
          total: '250.00',
          quantity: { count: 3 }
        }
      ]
    };
    ```

1. (Опционально) Укажите дополнительные данные заказа.
   Можно указать произвольные данные — `metadata`. При этом `metadata` не может быть длиннее 128 символов после применения `encodeURIComponent`.
    ```js
    paymentData.metadata = 'order-metadata';
    ```


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
// Создать экземпляр кнопки и смонтировать DOM.
const container = document.querySelector('#button_container');
const button = payment.mountButton(container, {
    type: YaPay.ButtonType.Pay,
    theme: YaPay.ButtonTheme.Black,
    width: YaPay.ButtonWidth.Auto,
});
```

### Шаг 5. Подпишитесь на события платежной формы {#step5}

```js
// Подписаться на событие success.
payment.on(YaPay.PaymentEventType.Success, function onPaymentSuccess(event) {
    // Заказ успешно оформлен
    alert([
        `OrderId — ${event.orderId}`,
        `Metadata — ${event.metadata}`,
    ].join('\n'));
});
```

### Шаг 6. Обработайте исключения {#step6}

```js
// Подписаться на событие error.
payment.on(YaPay.PaymentEventType.Error, function onPaymentError(event) {
  // Вывести информацию о недоступности оплаты в данный момент
  // и предложить пользователю другой способ оплаты.
});

// Подписаться на событие abort.
// Это когда пользователь закрыл форму {{ product }}.
payment.on(YaPay.PaymentEventType.Abort, function onPaymentAbort(event) {
  // Предложить пользователю другой способ оплаты.
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
    version: 3,
    countryCode: YaPay.CountryCode.Ru,
    currencyCode: YaPay.CurrencyCode.Rub,
    merchantId: 'bbb9c171-2fab-45e6-b1f8-6212980aa9bb',
    orderId: 'test-order-id',
    cart: {
      items: [
        {
          productId: '1',
          total: '300.00',
          quantity: { count: 2 }
        }
      ]
    },
    metadata: 'order-metadata'
  };

  // Создать платеж.
  YaPay.createPayment(paymentData)
    .then(function (payment) {
      // Создать экземпляр кнопки и смонтировать в DOM.
      const container = document.querySelector('#button_container');
      const button = payment.mountButton(container, {
        type: YaPay.ButtonType.Pay,
        theme: YaPay.ButtonTheme.Black,
        width: YaPay.ButtonWidth.Auto,
      });

      // Подписаться на событие error.
      payment.on(YaPay.PaymentEventType.Error, function onPaymentError(event) {
        // Вывести информацию о недоступности оплаты в данный момент
        // и предложить пользователю другой способ оплаты.
      });

      // Подписаться на событие abort.
      // Это когда пользователь закрыл форму {{ product }}.
      payment.on(YaPay.PaymentEventType.Abort, function onPaymentAbort(event) {
        // Предложить пользователю другой способ оплаты.
      });

      // Подписаться на событие success.
      payment.on(YaPay.PaymentEventType.Success, function onPaymentSuccess(event) {
        // Заказ успешно оформлен
        alert([
            `OrderId — ${event.orderId}`,
            `Metadata — ${event.metadata}`,
        ].join('\n'));
      });
    })
    .catch(function (err) {
      // Платеж не создан.
    });
}
```

## Интеграция {{ product }} Checkout на сервере {#integration-server}

Для интеграции на сервере воспользуйтесь [данной инструкцией](https://ya.ru).

См. также:
- [Подключение формы {{ product }} Checkout](yandex-pay-checkout.md)
- [Подключение кнопки c оплатой на стороне {{ product }}](yandex-pay-server-pay.md)
- [Работа {{ product }} через редиректы](pay-via-query.md)
- [Частые ошибки в подключении](common-mistakes.md)
- [Тестирование](testing-integration.md)
