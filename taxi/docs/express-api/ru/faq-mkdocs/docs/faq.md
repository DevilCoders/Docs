# Частые вопросы

## Работа с заявкой {#claim}

### Общие вопросы {#claim-general}

#### 1. Почему некоторые запросы делаются к v2, а некоторые к v1? {#claim-general-v}

Для некоторых операций существует две версии API: `v1` и `v2`. Более актуальной является версия `v2`. Поэтому, если у метода есть аналог в `v2`, мы рекомендуем использовать версию `v2`.

Устаревшие поля и методы, не рекомендуемые к использованию, зафиксированы отметкой `[DEPRECATED]`.

### Создание заявки {#claim-create}

#### 2. Что такое request_id? Почему метод может возвращать информацию о ранее созданной заявке? {#claim-create-request_id}

Параметр `request_id` — это уникальный идентификатор заявки, так называемый признак идемпотентности, по значению которого заявку можно отличить от других заявок.

У каждой новой заявки должен быть свой, отличный от предыдущих, параметр `request_id`. При использовании старого значения `request_id`, вне зависимости от тела запроса, метод вернет информацию о старом заказе. Использовать прежнее значение `request_id` следует только для повторной попытки создания конкретной заявки в случае ошибок сервера с кодами `5xx`.

В записи значения `request_id` допускаются буквы, цифры, другие символы. Чтобы гарантировать уникальность значений, рекомендуем использовать формат `uuid` и его производные.

#### 3. Как выбрать тариф и тип автомобиля? {#claim-create-client_requirements}

Если вы передали в запросе вес и габариты грузов, система автоматически подберет подходящее авто.

Также вы можете выбрать тариф и опции самостоятельно. Для этого передайте в параметре `client_requirements` соответствующие значения:

* **Тариф** (`taxi_class`):
  * "Курьер" — `courier`;
  * "Экспресс" — `express`;
  * "Грузовой" — `cargo`. В случае `cargo` необходимо дополнительно указать **Размер кузова** (`cargo_type`):
     * "Маленький кузов" — `van`;
     * "Средний кузов" — `lcv_m`;
     * "Большой кузов" — `lcv_l`.
* **Количество грузчиков** (`cargo_loaders`): 1 или 2 (тип `integer`).
* **Дополнительные опции** (`cargo_options`):
  * "Термосумка" — `thermobag`;
  * "Только курьер на авто" — `auto_courier`.

Если система определит, что товары которые необходимо доставить, не удовлетворяют критериям выбранного ТС (например, слишком габаритный груз, или превышена грузоподъемность), помимо статуса `ready_for_approval` в ответе будет предупреждение с кодом `not_fit_in_car`.

**Вес отправления:**

* "Курьер" (`courier`): до 10 кг;
* "Экспресс" (`express`): до 20 кг;
* "Грузовой" (`cargo`):
  * "Маленький кузов": до 300 кг;
  * "Средний кузов": до 700 кг;
  * "Большой кузов": до 1400 кг.

**Габариты отправления (формат ДxШxВ):**

* "Курьер" (`courier`): до 0,80 м × 0,50 м × 0,50 м;
* "Экспресс" (`express`): до 1,00 м × 0,60 м × 0,50 м;
* "Грузовой" (`cargo`):
  * "Маленький кузов": до 1,70 м × 0,96 м × 0,90 м;
  * "Средний кузов": до 2,60 м × 1,30 м × 1,50 м;
  * "Большой кузов": до 3,80 м × 1,80 м × 1,80 м.

#### 4. Как сделать отложенный заказ — заказ к определенному времени? {#claim-create-due}

По умолчанию вызов курьера при создании заявки происходит на ближайшее время (поле `due` не передается). Если вам необходимо создать отложенный заказ, то в поле `due` передайте желаемые дату и время прибытия курьера на точку А (откуда забрать отправление).

#### 5. Обязательно ли передавать значения цены товара и валюты, в которой указана цена? {#claim-create-cost}

Поля цены товара `items[].cost_value` и валюты `items[].cost_currency` обязательны для заполнения, без их указания создание заявки невозможно. Если цена неизвестна, можно передать `"cost_value": "0"` , `"cost_currency": "RUB"`.

#### 6. Обязательно ли передавать габариты и вес товара? {#claim-create-size}

Если используется автоопределение ТС (поле `taxi_class` не задано), передача габаритов и веса товара обязательна.

Если поле `taxi_class` задано, можно не передавать габариты и вес товара. Однако рекомендуется и в этом случае описать габариты и вес товара с учетом ограничений полей `items[].size` и `items[].weight`, чтобы исключить ошибки в выборе средства транспортировки.

Габариты указываются в метрах, вес в килограммах.

#### 7. В каком формате передавать телефонный номер? {#claim-create-phone}

Телефонный номер передается в формате "+7XXXXXXXXXX".

#### 8. Обязательна ли передача координат? {#claim-create-coordinates}

Поле является обязательным. Требуется передавать корректные координаты, так как в соответствии с координатами формируется точка маршрута. Важно передавать координаты (поле `route_points[].address.coordinates[]`) в порядке [долгота, широта], иначе возникнет ошибка оценки заявки.

#### 9. Как правильно указать порядок посещения точки? {#claim-create-visit order}

Поле `route_points[].visit_order` задает порядковый номер точки на маршруте. Место, откуда требуется забрать товар, должно иметь номер 1. Следующая точка, куда надо доставить товар, — номер 2, и так далее. Последняя точка (место возврата товара) добавляется автоматически и по умолчанию совпадает с точкой отправления, если не указан иной адрес.

#### 10. Как передать дополнительную информацию водителю? {#claim-create-comment}

Мы рекомендуем передавать текстовый комментарий для водителя, чтобы он мог быстрее найти отправителя и получателя. Информацию для водителя можно передать в общем комментарии к заказу (`comment`) или в комментариях к точкам (`route_points[].address.comment`).

Примеры текста комментария приведены в [документации](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsCreate.html).

#### 11. Как указать код, который нужно сообщить на складе, чтобы курьер смог получить заказ? {#claim-create-warehouse-code}

Код можно передать через комментарий к точке с типом `source` (или `source_point` для v1). Курьер увидит сообщения из комментариев ко всем точкам только после того, как станет исполнителем заказа.

#### 12. Как отправитель узнает, за каким заказом приехал курьер? Как водитель поймет, на какой точке маршрута и какой заказ требуется передать получателю? Где указать внутренний номер заказа? {#claim-create-order}

Каждая точка маршрута имеет свой идентификатор `route_points[].point_id` — произвольно заданное целое число. При заполнении информации о товаре значения полей `items[].pickup_point` (точка забора товара) и `items[].droppof_point` (точка доставки товара) будут соответствовать значениям `route_points[].point_id` точки забора и точки доставки.

Номер заказа можно передать в поле `route_points[].external_order_id` метода создания заявки, а также продублировать в поле `items[].extra_id`. В поле `items[].extra_id` допускается указать иной возможный идентификатор товара.

{% note warning "Внимание." %}

Внутренний номер заказа можно передавать только в блоке полей, относящихся к массиву точки Б (точки доставки товара).

{% endnote %}

Если поле `external_order_id` заполнено, в момент забора заказа водитель увидит номера заказов и сможет назвать их отправителю.

Всю необходимую дополнительную информацию можно передавать в общем комментарии к заказу и дополнительных комментариях к точкам.

#### 13. Как указать специальные требования к заявке? {#claim-create-cargo_options}

В тарифе "Курьер" можно выбрать термосумку и/или курьера на авто. Для этого передайте в параметре `client_requirements.taxi_class` значение `courier`, а в параметре `client_requirements.cargo_options` укажите значение `thermobag` и/или `auto_courier`.

Подробнее читайте в [документации](https://yandex.ru/dev/logistics/api/ref/estimate/IntegrationV1Tariffs.html).

#### 14. Что такое коды подтверждения, как они работают? {#claim-create-confirmation}

Код подтверждения — электронная цифровая подпись курьера, которая служит свидетельством принятия, передачи или возврата товара.

**Подтверждение на точке А (магазин).** Водитель после приезда на точку устанавливает в своем приложении соответствующий статус (статус API `ready_for_pickup_confirmation`). Затем водитель сообщает, что забрал посылку. В этот момент автоматически генерируется код, который приходит отправителю через SMS, личный кабинет или API. Полученный код необходимо сообщить водителю. Водитель введет код в своем приложении, после чего сможет направиться к получателю.

**Подтверждение на точке Б (у получателя).** Приехав на точку, водитель сообщает об этом в своем приложении (статус API `ready_for_delivery_confirmation`). Затем генерируется код и направляется получателю по SMS. Полученный код требуется сообщить курьеру, который введет его в свое приложение, после чего сможет закрыть заказ.

**Подтверждение в точке возврата (если не удалось передать товар и требуется вернуть его обратно)**. После того как водитель сделает пометку, что он прибыл на точку (статус API  `ready_for_return_confirmation`), сформируется код, который будет направлен клиенту через SMS, личный кабинет или API. Полученный код необходимо сообщить для ввода курьером в свое приложение. После ввода кода водитель сможет отменить заказ как успешно возвращенный.

Необходимость прохождения процедуры подтверждения в конкретной точке маршрута определяется значением поля `route_points[].skip_confirmation`. По умолчанию устанавливается значение `false` — нельзя избежать процедуры подтверждения. Вы можете изменить это значение на `true` — можно не использовать процедуру подтверждения на данной точке.

### Оценка заявки {#claim-estimate}

#### 15. Что такое ценовой оффер? {#claim-estimate-offer}

Ценовой оффер — актуальная стоимость потенциального заказа — формируется при успешном прохождении процедуры оценки заявки. Обратите внимание, что срок жизни ценового оффера порядка 10 минут: с момента установки статуса `ready_for_approval` и до получения статуса `accepted`.

Если заявка не будет подтверждена в течение 10 минут, понадобится отправить заявку на повторную оценку. Сделать это можно, используя метод [Редактирование заявки](https://yandex.ru/dev/logistics/api/ref/claim-edit/IntegrationV2ClaimsEdit.html), или путем создания новой заявки с новым значением параметра `request_id`.

Подтверждение заявки с уже истекшим по прошествии 10 минут оффером приведет к ошибке: ответ сервиса будет `200`, но вскоре заявка перейдет в статус `failed`. Статус заявки можно узнать с помощью методов получения информации о заявке.

#### 16. Что такое version — версия заявки? {#claim-estimate-version}

Заявка может последовательно проходить через несколько версий. Вновь созданная заявка — это версия номер 1. При каждом изменении заявки с использованием метода редактирования номер версии будет увеличиваться на единицу: 2, 3 и так далее.

### Подтверждение заявки {#claim-approve}

#### 17. Как подтвердить созданную заявку? {#claim-approve-approve}

Для подтверждения созданной заявки требуется, чтобы заявка успешно прошла процедуру оценки. Оценка происходит автоматически и занимает несколько секунд, после чего заявка переходит в статус `ready_for_approval`, то есть готова к подтверждению. Уточнить статус заявки можно с помощью методов [Журнал изменений заказа](https://yandex.ru/dev/logistics/api/ref/claim-info/IntegrationV2ClaimsJournal.html) и [Получение информации по заявке](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html).

Подтвердить заявку необходимо в течение 10 минут после получения статуса `ready_for_approval`. Для подтверждения необходимо воспользоваться методом [Подтверждение заявки](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsAccept.html). Поиск исполнителя начнется только после подтверждения заявки.

### Отслеживание заявки {#claim-info}

#### 18. Как происходит информирование о смене статуса заказа? {#claim-info-status}

Информацию о текущем статусе заказа можно получить с помощью методов [Получение информации по заявкам](https://yandex.ru/dev/logistics/api/ref/claim-info/IntegrationV2ClaimsBulkInfo.html) и [Журнал изменения заказов](https://yandex.ru/dev/logistics/api/ref/claim-info/IntegrationV2ClaimsJournal.html).

#### 19. Сколько времени длится поиск курьера? {#claim-info-courier}

Поиск курьера занимает не более 30 минут при создании заказа на ближайшее время.

#### 20. Как получить информацию о водителе? {#claim-info-driver}

Информация о водителе доступна в разделе `performer_info`, возвращаемом методами [Получение информации по заявке](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) и [Получение информации по нескольким заявкам](https://yandex.ru/dev/logistics/api/ref/claim-info/IntegrationV2ClaimsBulkInfo.html).

Для получения телефона водителя можно воспользоваться методом [Получение номера телефона для звонка водителю](https://yandex.ru/dev/logistics/api/ref/performer-info/IntegrationV1DriverVoiceForwarding.html). В целях сохранения персональных данных используются подменные номера. Срок действия номера ограничен сроком жизни заявки, то есть получением конечного статуса. 

### Отмена заявки {#claim-cancel}

#### 21. Как отменить заявку? {#claim-cancel-cancel}

Для отмены заявки:

1. В методе [Получение информации по заявке](https://yandex.ru/dev/logistics/api/ref/basic/IntegrationV2ClaimsInfo.html) в поле `available_cancel_state` следует получить признак возможности отмены: платно или бесплатно.

1. Отменить заявку через метод [Отмена заявки](https://yandex.ru/dev/logistics/api/ref/cancel-and-skip-points/IntegrationV2ClaimsCancel.html). Заявка получит статус `cancelled`, если заказ отменен до приезда водителя на точку А (откуда забрать отправление), или статус `cancelled_with_payment`, если водитель уже отметил, что приехал, но еще не забрал товар.
