# YaPay.createPayment — конструктор платежа

YaPay.createPayment — конструктор платежа.



### **Конструктор** {#constructor}
Функция-конструктор. На основе переданных параметров асинхронно создает объект платежа и возвращает его в promise.resolve.
Если платеж создать не удалось, возвращает ошибку в promise.reject.



```
{Promise} createPayment(paymentData)
```

**Параметры:**
| **Название** | **Тип** | **Описание** | **По умолчанию** |
| --- | --- | --- | --- |
| `paymentData` | [PaymentData](yapay.md#paymentdata) | Настройки платежа. | — |
