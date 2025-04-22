## Booking Yang

Сервис ручных бронирований заказов с подтверждением броней через Янг.

#### Testing
api: http://booking-yang.tst.geosmb.maps.yandex.net
tvm: 2018982

#### Production
api: http://booking-yang.geosmb.maps.yandex.net
tvm: 2018588

* [ABC](https://abc.yandex-team.ru/services/maps-adv-bookings-yang/)
* Yav [testing](https://yav.yandex-team.ru/secret/sec-01e1kz0mx7dh942q6h30qgrgbk) [production](https://yav.yandex-team.ru/secret/sec-01e2g7g5j1ghe5akp4ddpc1pc4)
* [CD](https://a.yandex-team.ru/ci/maps-adv-bookings-yang/releases/timeline?dir=maps_adv%2Fgeosmb%2Fbooking_yang%2Fserver&id=stable-release)
* [Sandbox resources](https://sandbox.yandex-team.ru/resources?type=GEOSMB_BOOKING_YANG)
* [Deploy](https://deploy.yandex-team.ru/projects/geosmb-booking-yang)
* Awacs [testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.tst.geosmb.slb.maps.yandex.net/show/) [production](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/communal.geosmb.slb.maps.yandex.net/show/)
* YC [PostgreSQL](https://yc.yandex-team.ru/folders/foo6djppbp2m3dmisslg)
* Solomon [админка](https://solomon.yandex-team.ru/admin/projects/geosmb)

## API

Полные протоколы в директории `./proto/`

#### Cоздать заявку на бронирование с переданными параметрами

`POST /v1/orders/`

Input: `OrderInput`

Output: `OrderOutput`

Specific Errors:
- `404 ORG_NOT_FOUND`
- `404 ORG_WITHOUT_PHONE`
- `409 INSUFFICIENT_TIME_TO_CONFIRM` - возникает, когда между временем, когда мы можем позвонить в организацию, и временем желаемого бронирования менее 45 минут.

#### Получить список заявок на бронирование запрошенного клиента

`POST /v1/list_client_orders/`

Input: `ListClientOrdersInput`

Output: `ClientOrders`

#### Получить список актуальных на переданный момент заказов

`POST /v1/fetch_actual_orders/`

Input: `ActualOrdersInput`

Output: `ActualOrdersOutput`


## Выгрузки на YT

Таблицы лежат тут:

- Prod: `//home/geoadv/geosmb/booking_yang/prod/`
- Testing: `//home/geoadv/geosmb/booking_yang/testing/`

#### created_orders

Созданные заявки на бронирование

| **column name**  | **description**  | 
|---|---|
|  order_id  |id заявки на бронирование|
|  created_at  |время, когда заявка поступила в BookingYang (UTC)|
|  processing_time  |время, когда заявка поступит на обработку в Янг (UTC). Если `NULL`, значит мы рассчитали, что между временем бронирования и временем, когда сможем отправить заявку, меньше 45 минут, и отклонили заявку сразу без отправки в Янг|

#### orders_processed_by_yang

Заявки на бронирование, отправленные в Янг. Заявки, находящиеся сейчас на обработке в Янге, не учитываются.

| **column name**  | **description**  | 
|---|---|
|  order_id  |id заявки на бронирование|
|  yang_suite_id  |id задачи в Янге|
|  yang_task_created_at  |время, когда удалось создать задачу в Янге по версии Янга (UTC)|
|  task_created_at  |время, когда удалось создать задачу в Янге (UTC). По сути время, в которое мы смогли получить данные по созданной задаче.|
|  task_result_got_at  |время, когда получили результат обработки заявки из Янга (UTC)|

#### orders_notified_to_users

Обработанные в Янге заявки на бронирование. Не включает в себя заявки, отлонённые сразу и не поступившие в Янг.

| **column name**  | **description**  | 
|---|---|
|  order_id  |id заявки на бронирование|
|  yang_suite_id  |id задачи в Янге|
|  booking_verdict  |результат обработки заявки. Вердикт соответствует названию смс-шаблона, который мы отправили пользователю|
|  sms_sent_at  |время отправки смс пользователю (UTC)|
