## Учет лимита овердрафта в фикспрайсных заказах для лояльных пользователей

### Продуктовое описание
Иногда у старых лояльных пользователей возникают проблемы с оплатой.
У них меняется группа антифрода и при последующих заказах деньги
начинают списываться в соответствии с порогами антифрода, на что
пользователи обижаются. Чтобы такого не происходило, нужно для поездок
по фиксу перед списанием антифрода проверять размер доступного
пользователю овердрафта: если овердрафт покрывает стоимость заказа,
то деньги за такую поездку нужно списывать по окончании самой поездки

### Техническая информация
Поскольку фича затрагивает функционал оплаты поездки, то правки предполагается
вносить в stq update_transactions. 

Про овердрафт узнаем у сервиса долгов debts в ручке `/v1/overdraft/limit`,
где идем в сервис антифрода (что в backend-cpp).

Как сейчас происходит списания по порогам антифрода:
1) При смене статуса на `transporting` в `status_handling` [ставится в очередь](https://github.yandex-team.ru/taxi/backend/blob/a79ee48cd391a1aa53e0dea8cf247bf9f02b89d7/taxi/internal/order_kit/plg/status_handling.py#L593) stq-шка антифрода
2) Внутри [antifraud_start_proc](https://github.yandex-team.ru/taxi/backend/blob/9b014b7b71705cf38a5fc2541b2716a0e30a7b39/taxi/internal/order_kit/invoice_handler.py#L2278) вызывается [_antifraud_try_hold](https://github.yandex-team.ru/taxi/backend/blob/9b014b7b71705cf38a5fc2541b2716a0e30a7b39/taxi/internal/order_kit/invoice_handler.py#L2376)
3) Внутри `_antifraud_try_hold` вызывается [antifraud.update_ride_sum](https://github.yandex-team.ru/taxi/backend/blob/a6f61b63ae0bccca38194cdb618c595aa7fa9a8c/taxi/internal/order_kit/antifraud.py#L217)
4) В `update_ride_sum` в зависимости от настроек, группы пользователя и [конфига ANTIFRAUD_COMMON](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/ANTIFRAUD_COMMON?name=antifraud) вычисляются дельты платежей и новая сумма выставляется в поле заказа `payment_tech.sum_to_pay.ride`
5) Если есть новая сумма — [вызывается update_transactions](https://github.yandex-team.ru/taxi/backend/blob/9b014b7b71705cf38a5fc2541b2716a0e30a7b39/taxi/internal/order_kit/invoice_handler.py#L2430)
6) В update_transactions начинаются списания

### Что можно сделать
Внутри `_antifraud_try_hold`, если понимаем, что нужно вызывать `antifraud.update_ride_sum`,
проверяем, что это фиксовый заказ и что стоимость заказа (в сумме с возможными долгами) меньше доступного лимита
овердрафта — в таком случае прекращаем процедуры антифрода вызовом [antifraud.finish_procedure](https://github.yandex-team.ru/taxi/backend/blob/a6f61b63ae0bccca38194cdb618c595aa7fa9a8c/taxi/internal/order_kit/antifraud.py#L361).

Также, вместо поэтапного списания теперь списываем всю сумму сразу.

### Раскатка
Раскатываться на всех планируется через exp3, попроцентно.

### Нагрузка
Судя по графикам `/3.0/ordercommit` в пике дополнительная нагрузка на сервис долгов
вырастет на 100 рпс, но по факту ниже, т.к. не все заказы по фиксу и не во всех заказах
нужно будет дергать ручку `/v1/overdraft/limit`. На [yasm-графиках debts](https://yasm.yandex-team.ru/panel/robot-taxi-clown.nanny_taxi_debts_stable)
видно, что сервис имеет солидный запас по ресурсам.

Сервис antifraud так же имеет достаточный запас по [ресурсам](https://grafana.yandex-team.ru/d/UKDwcdkWz/taxi_conductor_taxi_antifraud?orgId=1&refresh=30s)
