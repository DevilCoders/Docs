# Подключение {{ product }} Checkout

Технология {{ product }} Checkout подключает форму оформления заказа для вашего интернет-магазина.

С помощью {{ product }} Checkout вы можете получить сведения о заказе:
- данные покупателя;
- контакт получателя;
- способ доставки;
- адрес доставки.

## Подключение {{ product }} Checkout на сайте {#integration-client}

### Требования к подключению {#requirements}

Для установки кнопки {{ product }} должны быть выполнены следующие требования:
- Ваш сайт работает по протоколу HTTPS.
- На вашем сайте не должен обрезаться параметр `__YP__` из URL ([подробнее](!/../pay-via-query/)).
- Политики [CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) на вашем сайте разрешают использовать:
  ```
  script-src: https://pay.yandex.ru
  frame-src: https://pay.yandex.ru
  img-src: https://pay.yandex.ru
  connect-src: https://pay.yandex.ru
  ```

### Подготовка к подключению {#preparation}

Для подключения {{ product }} Checkout получите `merchant-id`. Для этого [заполните заявку](https://forms.yandex.ru/cloud/624ea6d37039b509a3f25284/).

## Шаг 1. Подключите SDK {#step-1}

Установите HTML-код на всех страницах, где будет размещена кнопка {{ product }}, перед закрывающим тегом `</body>`.
В качестве значения в атрибут `onload` передайте название метода, который будет отвечать за инициализацию и обработку платежей.

```html
<script src="https://pay.yandex.ru/sdk/v1/pay.js" onload="onYaPayLoad()" async></script>
```

## Шаг 2. Сформируйте данные для чекаута {#step-2}

Используйте объект `checkoutData`.

1. Укажите окружение для работы. Для разработки используйте тестовое окружение `SANDBOX`.
    ```js
    checkoutData.env = YaPay.Env.Sandbox;
    ```
2. Укажите версию {{ product }} Checkout API.
    ```js
    checkoutData.version = 3;
    ```
3. Укажите код валюты и код страны, в которой передается корзина.
    ```js
    checkoutData.countryCode = YaPay.CountryCode.Ru;
    checkoutData.currencyCode = YaPay.CurrencyCode.Rub;
    ```
4. Укажите данные продавца:
    - `merchantId` — идентификатор, который продавец получает при регистрации в {{ product }} Checkout.
    ```js
    checkoutData.merchantId = 'bbb9c171-2fab-45e6-b1f8-6212980aa9bb';
    ```
5. Добавьте информацию о корзине покупателя.
   При необходимости можно указать количество товара в корзине через свойство `quantity`.
    ```js
    checkoutData.cart = {
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

6. (Опционально) Укажите дополнительные данные корзины.
   Можно указать произвольные данные — `metadata`. При этом `metadata` не может быть длиннее 128 символов после применения `encodeURIComponent`.
    ```js
    checkoutData.metadata = 'order-metadata';
    ```


## Шаг 3. Создайте новый экземпляр чекаута и запустите проверку {#step-3}

```js
window.YaPay.createCheckout(checkoutData)
  .then(function (checkout) {
    // Чекаут доступен, можно показать кнопку {{ product }}.
  })
  .catch(function (err) {
    // Не получилось создать чекаут-объект.
  });
```

## Шаг 4. Выведите кнопку {{ product }} Checkout {#step-4}

```js
const container = document.querySelector('#button_container');

checkout.mountButton(container, {
  type: YaPay.ButtonType.Checkout,
  theme: YaPay.ButtonTheme.Black,
  width: YaPay.ButtonWidth.Auto,
});
```

## Шаг 5. Подпишитесь на события чекаут формы {#step-5}

```js
// Подписаться на событие success.
checkout.on(YaPay.CheckoutEventType.Success, function onCheckoutSuccess(event) {
  // Заказ успешно оформлен
  alert([
    `OrderId — ${event.orderId}`,
    `Metadata — ${event.metadata}`,
  ].join('\n'));
});

// Подписаться на событие error.
checkout.on(YaPay.CheckoutEventType.Error, function onCheckoutError(event) {
  // Вывести информацию о недоступности оформления заказа в данный момент
  // и предложить пользователю другой способ оформления заказа.
});

// Подписаться на событие abort.
// Пользователь закрыл форму {{ product }}.
checkout.on(YaPay.CheckoutEventType.Abort, function onCheckoutAbort(event) {
  // Предложить пользователю другой способ оформления заказа.
});
```

## Шаг 6. (Опционально) Обновите корзину если она поменялась {#step-6}

При обновлении передайте полную новую корзину (`cart`) и опционально `metadata`.

```js
checkout.update({
  cart: {
    items: [
      {
        productId: '1',
        total: '300.00',
        quantity: { count: 2 }
      }
    ]
  },
  metadata: 'new-order-metadata'
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
  const checkoutData = {
    env: YaPay.Env.Sandbox,
    version: 3,
    currencyCode: YaPay.CurrencyCode.Rub,
    merchantId: 'bbb9c171-2fab-45e6-b1f8-6212980aa9bb',
    cart: {
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
    },
    metadata: 'order-metadata'
  };

  YaPay.createCheckout(checkoutData)
    .then(function (checkout) {
      // Вывести кнопку {{ product }} Checkout.
      const container = document.querySelector('#button_container');

      checkout.mountButton(container, {
        type: YaPay.ButtonType.Checkout,
        theme: YaPay.ButtonTheme.Black,
        width: YaPay.ButtonWidth.Auto,
      });

      // Подписаться на событие success.
      checkout.on(YaPay.CheckoutEventType.Success, function onCheckoutSuccess(event) {
        // Заказ успешно оформлен
        alert([
          `OrderId — ${event.orderId}`,
          `Metadata — ${event.metadata}`,
        ].join('\n'));
      });

      // Подписаться на событие error.
      checkout.on(YaPay.CheckoutEventType.Error, function onCheckoutError(event) {
        // Вывести информацию о недоступности оформления заказа в данный момент
        // и предложить пользователю другой способ оформления заказа.
      });

      // Подписаться на событие abort.
      // Пользователь закрыл форму {{ product }} Checkout.
      checkout.on(YaPay.CheckoutEventType.Abort, function onCheckoutAbort(event) {
        // Предложить пользователю другой способ оформления заказа.
      });
    })
    .catch(function (err) {
      // Чекаут не создан.
    });
}
```

## Интеграция {{ product }} Checkout на сервере {#integration-server}

Для интеграции на сервере воспользуйтесь [данной инструкцией](https://ya.ru).
