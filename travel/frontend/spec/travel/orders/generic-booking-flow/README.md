# Generic booking flow

## Методы

-   `estimateDiscount` :: `POST /api/generic_booking_flow/v1/estimate_discount`
-   `createOrder` :: `POST /api/generic_booking_flow/v1/create_order`
-   `addService` :: `POST /api/generic_booking_flow/v1/add_service`
-   `getOrder` :: `GET /api/generic_booking_flow/v1/get_order`
-   `getOrderState` :: `GET /api/generic_booking_flow/v1/get_order_state`
-   `startPayment` :: `POST /api/generic_booking_flow/v1/start_payment`
-   `cancelOrder` :: `POST /api/generic_booking_flow/v1/cancel_order`
-   `calculateRefundAmount` :: `POST /api/generic_booking_flow/v1/calculate_refund_amount`
-   `startRefund` :: `POST /api/generic_booking_flow/v1/start_refund`
-   `downloadBlank` :: `GET /api/generic_booking_flow/v1/download_blank`

## Асинхронность операций

Непосредственный результат возвращаю только методы `estimateDiscount`, `getOrder` и `getOrderState`.
Остальные методы запускают асинхронный процесс модификации заказа,
результаты которого можно отслеживать периодическим перезапросом (polling-ом) состояния заказа.
У заказа есть промежуточные (in progress) состояния, когда он обрабатывается и
в результате выполнения операции должен перейти в другое состояние, и устойчивые (stable), когда все текущие операции
выполнены и с заказом можно проводить новые операции.

## Процесс бронирования

1. `/api/generic_booking_flow/v1/estimate_discount` - Метод для расчёта скидки при наличии промокодов.
   На вход подаются данные, аналогичные запросу create_order.
   Исключением является отсутствие необходимости передавать заполенную информацию о пассажирах/гостях.
2. `/api/generic_booking_flow/v1/create_order` - После заполнения всех необходимых для бронирования данных
   вызывается метод create_order. Метод создаёт новый заказ и начинает резервирование услуг у партнёров.
   В результате polling-а состояния заказа (см. `get_order_state`) клиент должен дождаться наступления
   одного из событий:
    - `RESERVED` - все услуги зарезервированы, можно переходить к оплате; тут возможен сброс промокода
      (старый статус `RESERVED_WITH_RESTRICTIONS`), детали нужно смотреть в данных заказа;
    - `CANCELLED` - зарезервировать услуги не удалось, заказ отменён и не может быть оплачен;
      детали об ошибках можно найти в соответствующих услугах.
3. `/api/generic_booking_flow/v1/get_order_state` - Возвращает текущее состояние заказа и версию этого состояния,
   которая меняется только при переходах из состояния в состояние.
4. `/api/generic_booking_flow/v1/get_order` - Возвращает полную информацию о заказе. Всю детализацию по ошибкам
   резервирования, применения промокодов, оплаты и подтверждения заказа нужно получать отсюда.
5. `/api/generic_booking_flow/v1/add_service` - Добавляет услугу к заказу в статусе `RESERVED`.
   Начинается фоновое бронирование, нужно дождаться новый переход заказа в состояние `RESERVED`.
6. `/api/generic_booking_flow/v1/start_payment` - Начинает оплату для заказа в статусе `RESERVED` или
   `PAYMENT_FAILED`. Операция асинхронная, нужно начинать polling и ждать перехода в `WAITING_PAYMENT`
   (был сгенерирован счёт на оплату и ссылка на форму доступна в заказе).
7. После отображения пользователю ссылки на страницу оплаты и её закрытия снова переходим в polling
   для получения одного из следующих исходов:
    - `CONFIRMED` - заказ успешно оплачен и подтверждён; можно идти на Happy Page;
    - `PAYMENT_FAILED` - оплата не удалась, детали в информации о заказе;
      можно предложить пользователю повторную попытку оплаты;
    - `CANCELLED` - оплата не удалать и повторные попытки не доступны.
8. `/api/generic_booking_flow/v1/cancel_order` - При неуспешной оплате и переходе заказа в статус `PAYMENT_FAILED`,
   если пользователь отказывается от повторной оплаты, то отменяем заказ, чтобы снять все активные брони у партнёров
   (кнопка "Отмена"). Операция асинхронная, но необходимости ждать результата нет.
9. `/api/generic_booking_flow/v1/calculate_refund_amount` - Расчитывает сумму к возврату. Принимает на вход коллекцию объектов `IRefundPartCtx`, которые можно найти в технической секции про возврат, как на уровне заказа, так на уровне позиции/услуги, и частей услуги (e.g. билет)
10. `/api/generic_booking_flow/v1/start_refund` - Производит возврат, по токену, полученному при расчете суммы к возврату
11. `/api/generic_booking_flow/v1/download_blank` - Скачивает бланк заказа/билета/возврата по токену

[Диаграмма переходов состояний бронирования](https://wiki.yandex-team.ru/travel/hotels/projects/multiusluzhnyjj-zakaz-i-edinyjj-api/frontend-flow/)

## Booking flow как конечный автомат

Для упрощения управления процессом бронирования и избавления от лишнего состояния на клиенте можно реализовать
однозначный набор обработчиков заказа для каждого из возможных состояний:

-   `NEW` - Заказ в обработке, ждём перехода в другое состояние.
    Заказ только что создан и должен перейти в стадию бронирования.
-   `IN_PROGRESS` - Заказ в обработке, ждём перехода в другое состояние.
-   `RESERVED` - Все услуги зарезервированны. Нужно начать оплату с помощью вызова `start_payment`. (см. описание API)
-   `WAITING_PAYMENT` - Счёт на оплату сформирован, нужно направить пользователя по ссылке из заказа `payment.paymentUrl`.
-   `PAYMENT_FAILED` - Предыдущая попытка оплаты не удалась. Возможна или повторная попытка (`start_payment`)
    или отмена заказа (`cancel_order`, см. описание API). Запрашивается выбор пользователя.
-   `CONFIRMED` - Заказ успешно оформлен. Показываем Happy Page.
-   `CANCELLED` - Заказ отменён. Никаких действий по нему больше не совершить.
-   `REFUNDED` - Все услуги из заказа отменены, а деньги возвращены с учётом правил отмены. Никаких действий не доступно.

Все неописанные состояния стоит по умолчанию рассматривать как in progress
и ждать перехода в одно из описанных выше состояний.

## Повторные запросы при сетевых ошибках

-   по умолчанию считаем, что все 5хх-е ошибки можно и нужно retry-ить, но не менять при этом данные запроса
    (deduplication id для create_order)
-   запросы с кодами ответа 4хх повторно отправлять смысла нет

## Регист названий полей

Для передачи данных с названиями полей в camelCase в запросе должен быть передан заголовок `X-Ya-UseCamelCase: true`
