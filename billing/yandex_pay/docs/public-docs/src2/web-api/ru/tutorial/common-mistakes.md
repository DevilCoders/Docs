# Частые ошибки

Ошибки при работе с {{ product }} Web SDK могут быть связаны с поведением браузеров или с внутренней логикой {{ product }}.

Ниже приведены примеры ошибок, которых следует избегать, и рекомендации по их исправлению.


## Блокировка окна {{ product }} {#popup-block}

Некоторые браузеры могут блокировать показ окна с формой {{ product }}, если между нажатием кнопки {{ product }} и созданием окна был любой асинхронный вызов. Это поведение пока характерно для браузеров Safari и Firefox.

![](../_images/Vector.svg) **Рекомендуется**
```js
button.on(YaPay.ButtonEventType.Click, function () {
  payment.checkout();
  <any-async-action>.then(() => {
    // ...
  });
});
```
![](../_images/Vector-1.svg) **Не рекомендуется**
```js
button.on(YaPay.ButtonEventType.Click, function () {
  // Любое асинхронное действие между кликом и показом блокирует показ всплывающего окна.
  <any-async-action>.then(() => {
    payment.checkout();
  });
});
```


## Работа с событиями {{ product }} {#redirect-flow}

После создания платежа нужно сразу подписываться на события платежа.
Это важно при работе {{ product }} через [редиректы](pay-via-query.md).

![](../_images/Vector.svg) **Рекомендуется**

```js
YaPay.createPayment(paymentData).then(function (payment) {
  /* ... cинхронные действия ... */
  payment.on(YaPay.PaymentEventType.Process, function(event) { /*...*/ });
  payment.on(YaPay.PaymentEventType.Error, function(event) { /*...*/ });
  payment.on(YaPay.PaymentEventType.Abort, function(event) { /*...*/ });
});
```
![](../_images/Vector-1.svg) **Не рекомендуется**
```js
YaPay.createPayment(paymentData).then(function (payment) {
  var button = payment.createButton();

  button.on(YaPay.ButtonEventType.Click, function () {
    // Подписаться на события после клика.
    payment.on(YaPay.PaymentEventType.Process, function(event) { /*...*/ });
    payment.on(YaPay.PaymentEventType.Error, function(event) { /*...*/ });
    payment.on(YaPay.PaymentEventType.Abort, function(event) { /*...*/ });

    payment.checkout();
  });
});
```
или
```js
YaPay.createPayment(paymentData).then(function (payment) {
  <any-async-action>.then(() => {
    // Подписаться на события после асинхронного действия.
    payment.on(YaPay.PaymentEventType.Process, function(event) { /*...*/ });
    payment.on(YaPay.PaymentEventType.Error, function(event) { /*...*/ });
    payment.on(YaPay.PaymentEventType.Abort, function(event) { /*...*/ });
  });
});
```


## Проверка платежа {#check-payment}

Если вам нужно проверить доступность оплаты {{ product }} без совершения платежа, используйте метод ` YaPay.readyToPayCheck `.

Например, вы хотите показать в интерфейсе вкладку с оплатой {{ product }}, если оплата доступна.


![](../_images/Vector.svg) **Рекомендуется**

```js
YaPay.readyToPayCheck(checkParams).then(function (isReady) {
  if (isReady) {
    // {{ product }} доступен, показать вкладку.
  }
});
```
![](../_images/Vector-1.svg) **Не рекомендуется**
```js
YaPay.createPayment(paymentData).then(function (payment) {
 // {{ product }} доступен, показать вкладку.
});
```



См. также:

- [Подключение кнопки {{ product }}](./index.md)
- [Подключение кнопки с оплатой на стороне {{ product }}](yandex-pay-server-pay.md)
- [Подключение формы {{ product }} Checkout](yandex-pay-checkout.md)
- [Работа {{ product }} через редиректы](pay-via-query.md)
- [Тестирование](testing-integration.md)
