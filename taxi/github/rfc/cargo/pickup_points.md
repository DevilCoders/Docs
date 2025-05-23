## Задача
Интеграция доставки из пунктов выдачи заказов (ПВЗ) в суперапп. 
Такие заказы необходимо подтверждать с помощью электронной подписи (код из СМС), которая исполльзуется для подписания,
акта приема-передачи. В бекенде `cargo-*` эти механизмы уже существуют, поэтому необходимо проинтегрироваться с ними.
### Flow

Максимально упрощенная схема, опущены многие детали вроде СМС-уведомлений и прочего.

1. Пользователь сделал заказ в интернет магазине. В качестве способа доставки выбрал ПВЗ/постамат партнера
2. Когда товар приедет в ПВЗ, в бекенд логистики (конкретно сервис cargo-misc) придет пуш от партнера с информацией о
 заказе и о заказчике. Мы сохраним эти данные в БД.
3. (Далее рассматриваем кейс, когда получатель - уже клиент Яндекс.Такси). Получатель при запуске приложения видит 
информацию о том, что в ПВЗ его ожидает посылка. Выбирает точку Б и нажимает кнопку "Оценить стоимость доставки".
 При оценке стоимости доставки необходимо создать заявку на перевозку груза (в бекенде логистики),
  где точка А - адрес ПВЗ, а точка Б - адрес, который укажет пользователь.
  Если пользователь согласен с ценой, то нажимает Заказать.
4. Бекенд `cargo-*` создает заказ от имени пользователя через int-api. 
5. Отмена заказа ограничена статусами заказа (нельзя отменить ни водителем, ни клиентом после получения посылки).

### Клиентские роуты

[[swagger]](https://github.yandex-team.ru/taxi/uservices/blob/4f467c0606a1d0576e330838aaf500481b26471a/services/cargo-misc/docs/yaml/api/pickup-points.yaml)

Все роуты, которые будут использоваться пользователями, обернуты Passenger Authorizer и лежат в бекенде cargo-misc.

* #### Получить список посылок `/4.0/pickup-points/v1/shipments/list`
1. Находим по phone_id актуальные посылки пользователя в БД
2. Находим в БД по каждой посылке её ПВЗ (график работы, адрес, ...). 
Данные о ПВЗ будут обновляться в БД periodic_task'ой раз в день.
3. Отдаем список посылок пользователю.

* #### Оценить стоимость доставки `/4.0/pickup-points/v1/shipment/estimate`
1. Берем точку А - адрес ПВЗ, точку Б - выбранный клиентом адрес и создаем / обновляем заявку на доставку в бекенде cargo-claims 
    * бекенд cargo ставит STQ таску на оценку заявки
    * STQ таска в зависимости от габаритов груза выбирает таксишный тариф.
    * Затем STQ таска для пользователя создает новый объект в db.users через ручку `/v1/profile` (int-api) с тем же номером и связью по yandex_uid.
     Это позволит переиспользовать [механизм](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/INTEGRATION_API_ENABLED_CROSSDEVICE_FOR_SOURCE),
      который был создан для Алисы
    * В конце STQ таска идет в таксишный integration-api в `v1/orders/estimate` и получает offer, который сохраняется в заявку cargo-claims

2. В это время из cargo-misc поллим заявку в cargo-claims, пока в ней не окажется оффера / статус не станет терминальным. 
3. Сохраняем оффер в БД.
4. Отдаем его пользователю


* #### Заказать доставку `/4.0/pickup-points/v1/shipment/order`
1. Добавляем в заявку door to door информацию (подъезд, этаж, квартиру), затем отмечаем заявку в cargo-claims принятой,
 тем самым соглашаясь с оффером 
    * claims переводит заявку в следующий статус
    * бекенд cargo ставит STQ таску на создание заказа
    * stq-таска идет в int-api (`orderdraft`/`ordercommit`), создавая заказ с `sourceid = cargo`.

2. Поллим заявку из cargo-claims, пока в ней не окажется статуса начала выполнения заявки / статус не станет терминальным. 
3. Отдаем пользователю HTTP code 200.
4. Чтобы заказ подтянулся в приложение, клиент должен будет вызвать ручку /launch.

* #### Способы оплаты `/4.0/pickup-points/v1/paymentmethods`
Проксирует таксишную ручку `paymentmethods`. Потому что когда мы в будущем мы подменим схему на супераппную,
 нам не будут подходить таксишные payment_id. Клиент уже сразу будет ходить в нашу ручку,
  чтобы мы могли делать эту подмену, не затрагивая клиент
