# YaPay.Payment

YaPay.Payment — объект. Содержит методы, позволяющие инициировать платеж.



### **Методы** {#methods}
| **Название** | **Возвращает** | **Описание** |
| --- | --- | --- |
| createButton(options) | Button | Создает объект Button. |
| update(updateData) | undefined | Обновляет объект платежа. |
| checkout() | undefined | Запускает процесс оплаты. |
| destroy() | undefined | Удаляет объект и все слушатели. |
| on (type, listener) | function | Добавляет слушатель на различные события при проведении платежа. |
| complete(reason) | undefined | Завершает работу платежной формы. |




### **Описание методов** {#methods-description}



### **createButton** {#method-create-button}
На основе переданных параметров создает объект кнопки и возвращает его.



```
{Button} create(options)
```

**Параметры:**
| **Название** | **Тип** | **Описание** | **По умолчанию** |
| --- | --- | --- | --- |
| `options` | [ButtonOptions](yapay.md#button-options) | Настройки кнопки. | — |




#### **update** {#method-update}
Обновляет данные платежа.



```
{void} update(updateData)
```

**Параметры:**
| **Название** | **Тип** | **Описание** | **По умолчанию** |
| --- | --- | --- | --- |
| `updateData` | [UpdatePaymentData](yapay.md#update-payment-data) | Настройки платежа. | — |





#### **checkout** {#method-checkout}
Запускает процесс оплаты.



```
{void} checkout()
```




#### **destroy** {#method-destroy}
Удаляет объект и все слушатели.



```
{void} destroy()
```




#### **on** {#method-on}
Добавляет слушатель на различные события при проведении платежа. Возвращает функцию, при вызове которой обработчик будет удален.



```
{function} on(type, listener)
```

**Параметры:**

#|
|| **Название** | **Тип** | **Описание** | **По умолчанию** ||
|| `type` | [PaymentEventType](yapay.md#enums) | Событие оплаты:
* ` PaymentEventType.Ready ` — форма оплаты загружена.
* ` PaymentEventType.Abort ` — оплата отменена. Пример: пользователь закрыл форму.
* ` PaymentEventType.Error ` — ошибка в процессе оплаты.
* ` PaymentEventType.Process ` — процесс оплаты запущен. Вместе с событием вернется платежный токен. | — ||
|| `listener` | Listener<Event> | Callback, вызываемый при возникновении события. | — ||
|#





#### **complete** {#method-complete}
Завершает работу с формой.
Должен вызываться, когда платежный токен был получен и обработан.



```
{void} complete(reason)
```


**Параметры:**

#|
|| **Название** | **Тип** | **Описание** | **По умолчанию** ||
|| `reason` | [CompleteReason](yapay.md#enums) | Событие завершения:
* ` CompleteReason.Success ` — оплата успешно произведена.
* ` CompleteReason.Error ` — произошла ошибка. Пример: ошибка в случае проведения платежа через банк-эквайер.
* ` CompleteReason.AuthRedirect ` — требуется дополнительная авторизация на стороне банка-эквайера.
* ` CompleteReason.Close ` — форма оплаты закрыта.  | — ||
|#

