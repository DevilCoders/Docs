# Модели и спецификации системы бронирований Яндекс.Путешествий

### Терминология
* *Спецификация* -- в стандартном смысле TLA+; набор предикатов, описывающих допустимую эволицию системы в форме `Init /\ [][Next]_vars /\ Liveness`.
* *Модель* -- частичная спецификация в открытой форме; обычно содержит набор предикатов-действий, используемых в спецификации более высокого уровня, включающую в себя модель.

## Оглавление
* *ExpediaBookingModel* -- модель бронирования отеля в Expedia.
* *ExpediaServiceModel* -- модель событийного автомата, обслуживающего услугу по размещению, реализованную через Expedia.
* *ExpediaServiceSpec* -- тестовый сценарий взаимодействия с автоматом ExpediaServiceModel.
* *TrustPaymentModel* -- модель платежа в Trust.
* *TrustInvoiceModel* -- модель событийного автомата, обслуживающего платеж через Trust.
* *TrustInvoiceSpec* -- тестовый сценарий взаимодействия с автоматом TrustInvoiceModel.
* *HotelOrderModel* -- модель отельного заказа.
* *HotelOrderSpec* -- тестовый сценарий взаимодействия с отельным заказом.

## Оформление
Отступы по умолчанию в два пробела. Линии в ~80 символов. В остальном следует следовать внутреннему чувству красоты.
