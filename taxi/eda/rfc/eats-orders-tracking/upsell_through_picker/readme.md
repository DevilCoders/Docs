# Бэкенд (eats-orders-tracking)
## Получение статусов заказов
Добавить новую очередь eats_orders_tracking_picker_orders, в которую будут ставиться задачи из procaas пикерки. 
Пикерка работает только с заказами типа retail (наша сборка), потому все сообщения о статусах будут приходить исключительно для заказов с этим типом.

Схема stq:
```
name: eats_orders_tracking_picker_orders
arguments:
  - name: event_type
    schema:
        $ref: "#/definitions/ProcessingEventType"
    required: true
  - name: order_nr
    schema:
        type: string
    required: true
  - name: order_status
    schema:
        $ref: "#/definitions/OrderState"
    required: true
  - name: place_id
    schema:
        type: string
    required: true
  - name: customer_id
    schema:
        type: string
    required: false
  - name: picker_id
    schema:
        type: string
    required: false
  - name: customer_picker_phone_forwarding
    schema:
        $ref: "#/definitions/ExpiringPhone"
    required: false
  - name: created_at
    schema:
        type: string
        format: date-time
    required: true

definitions:
    ProcessingEventType:
        type: string
        enum:
          - STATUS_CHANGE
          - ITEM_ADD
          - ITEM_REPLACE
          - ITEM_SOFT_DELETE
          - ITEM_PICKED
          - PICKER_PHONE_FORWARDING_READY

    OrderState:
        type: string
        description: Статус заказа
        enum:
          - new
          - waiting_dispatch
          - dispatching
          - dispatch_failed
          - assigned
          - picking
          - waiting_confirmation
          - confirmed
          - picked_up
          - receipt_processing
          - receipt_rejected
          - paid
          - packing
          - handing
          - cancelled
          - complete

    ExpiringPhone:
        type: object
        additionalProperties: false
        required:
          - phone
          - expires_at
        properties:
            phone:
                type: string
            expires_at:
                type: string
                format: date-time
```

| event_type | Описание |
| ---------- | -------- |
| STATUS_CHANGE | заказ изменил свой статус, нужно сохранить новый статус заказа из поля "order_status" |
| PICKER_PHONE_FORWARDING_READY | был сгенерирован номер телефона сборщика, нужно сохранить номер из поля "customer_picker_phone_forwarging". |

Остальные типы ивентов игнорируются

### Добавить таблицу picker_orders c полями:
- order_nr TEXT NOT NULL
- payload JSONB NOT NULL, -- пэйлоад с кэшированными данными по заказу
- updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()

payload будет иметь поля:
- picker_id: std::optional<::std::string>
- status: std::string
- status_history: PickerOrderHistory

PickerOrderHistory будет иметь поля:
- std::optional<::std::chrono::system_clock::time_point> new_at
- std::optional<::std::chrono::system_clock::time_point> assigned_at
- std::optional<::std::chrono::system_clock::time_point> picking_at
- std::optional<::std::chrono::system_clock::time_point> picked_up_at
- std::optional<::std::chrono::system_clock::time_point> paid_at

### Добавить таблицу picker_phones с полями:
- picker_id TEXT NOT NULL
- phone TEXT
- phone_ttl TEXT
- updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()

Обе таблицы должны очищаться в периодике очистки

### В очереди eats_orders_tracking_picker_orders нужно обновлять данные в таблицах.
В случае event_type == STATUS_CHANGE в таблице picker_orders обновлять payload:
- status = event.order_status
- picker_id = event.picker_id
- status_history: created_at в соответвующее статусу поле. Например(event.status=="new" => new_at = event.created_at, event_status="dispatching" => ничего обновлять не нужно)

В случае event_type == PICKER_PHONE_FORWARDING_READY в таблице picker_phones поля 
- phone = event.customer_picker_phone_forwarging
- phone_ttl = event.customer_picker_phone_forwarging_ttl


## Фолбек на случай, если не дошли ивенты о смене заказа
Необходимо учесть ситуацию, если вдруг сообщение будет потеряно (плохая выкатка сервиса, неполадки сети).
Добавить эксперимент, который будет определять через сколько времени нужно обновить информацию о заказе, 
если тот находится в одном и том же статусе какое-то время.
Схема эксперимента
```
name: eats_orders_tracking_picker_statuses_timeout
type: experiment
value:
    schema:
        type: array
        items:
            $ref: '#/definitions/TimeoutSettings'
        definitions:
            TimeoutSettings:
                description: Соответствие статуса заказа и времени, через которое заказ нужно обновить
                type: object
                additionalProperties: false
                required:
                  - status
                  - timeout
                properties:
                    status:
                        description: Статус заказа
                        type: string
                        enum:
                          - new
                          - waiting_dispatch
                          - dispatching
                          - dispatch_failed
                          - assigned
                          - picking
                          - waiting_confirmation
                          - confirmed
                          - picked_up
                          - receipt_processing
                          - receipt_rejected
                          - paid
                          - packing
                          - handing
                          - cancelled
                          - complete
                    timeout:
                        description: Время в секундах, через которое нужно обновить заказ
                        type: integer
                        x-taxi-cpp-type: std::chrono::seconds
```
Добавить периодик picker_orders_updater, который проходит по всем заказам в таблице picker_orders
### Логика работы периодика
Получить эксперимент, пройти по всем заказам в бд.
Для каждого заказа: если ```now() - updated_at < timeout```, то необходимо вызвать ручку eats-picker-orders GET /api/v1/order c номером заказа и обновить в бд актуальные данные.
Если текущий статус заказа не указан в эксперименте, то обновлять заказ не нужно.


## Реакция на статусы заказов
Так как изменениям логики будут только для заказов нашей сборки, то в случае flow type заказа shop, ничего не меняется.
Если заказ retail, то в зависимости от статуса:

### Сборщик еще не начал собирать заказ или номер его телефона еще не доступен или уже протух (!picking_at || !phone || (phone && now() >= updated_at + phone_ttl))
Так как требуется время, чтобы сгенерировался номер сборщика, заказ может быть уже в статусе picking, но телефон сборщика еще не будет доступен.
Эту функциональность хорошо бы регулировать отдельным экспериментом.
1. Нужно поменять Title и Description на "Забыли товар? Позвони нам, мы добавим его в корзину"
2. Показать кнопку "Связаться с нами"
3. Показать баннер с подписью "Позвони нам, если забыл что-то купить. Мы все сделаем". При нажатии на баннер ничего не происходит (поле appLink пустое)

### Сборщик собирает заказ и его номер телефона доступен (picking_at && !picked_up && phone && (now() < updated_at + phone_ttl))
Эту функциональность хорошо бы регулировать отдельным экспериментом.
1. Нужно поменять Title и Description на "Забыли самое нужное? Просто позвоните сборщику и попросите добавить товар в заказ"
2. Показать кнопку "Позвонить сборщику"
3. Показать баннер с подписью "Позвони нам, если забыл что-то купить. Мы все сделаем". При нажатии на баннер ничего не происходит (поле appLink пустое)

### Заказ в состоянии "Оплачиваем" (picked_up_at && !payed_at)
1. Нужно поменять Title и Description на "Стоим в очереди на кассу, скоро оплатим"
2. Больше ее показывать кнопку "Позвонить сборщику"
3. Не показывать баннер

### Заказ в любом из последующих состояний (payed_at)
Все по старой логике

### Замена сборщика
Возможна такая ситуация, когда сборщик будет заменен на другого.

При получении сообщения event_type = "STATUS_CHANGE" c другим picker_id никакой дополнительной логики не требуется, 
так как в таблице picker_phone для нового сборщика не будет записи.
Телефон для нового сборщика будет получен в сообщении event_type = PICKER_PHONE_FORWARDING_READY

### Протухание телефона сборщика
Телефон сборщика живет в течение времени, указанного в customer_picker_phone_forwarging_ttl. 
Когда он протухнет, придет новое сообщение с новым телефоном сборщика.

## Кнопка "Позвонить сборщику".
В спеке ручки /eats/v1/eats-orders-tracking/v1/tracking в TrackedOrderButtonContactType добавляется новое значение picker, которое будет использоваться при нажатии на кнопку "Позвонить сборщику"

# Фронт:
Нужно поддержать добавление нового значения в поле payload.contact_type для кнопок
```
TrackedOrderButtonContactType:
    type: string
    enum:
      - courier
      - place
      - picker
```

Баннеры будут некликабельными с пустым полем appLink
