# Получение обновленного комментария к заказу

После того, как оператор поддержки добавит нужные товары в комментарий к заказу, нужно будет, чтобы эта информация обновилась внутри сервиса eats-picker-orders.
Тогда сборщик сможет ее увидеть этот коментарий и добавить указанные товары или созвониться с пользователем.

## Задачи:
1. Добавить новую ручку, которая получала бы обновленный комментарий. 
   Будет сделано в задаче https://st.yandex-team.ru/RETAILDEV-1067
2. Использовать новую ручки пикерки при обновлении комментария в админке (только для заказов нашей сборки). 
   Будет сделано в задаче https://st.yandex-team.ru/EDADEV-44829


# Обновление статусов заказов на трекинге

Через procaas cтавить задачи в stq трекинга при изменении статуса (STATUS_CHANGE) или после генерации номера телефона сборщика (PICKER_PHONE_FORWARDING_READY).

Формат:
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

Поле created_at будет добавлено в задаче https://st.yandex-team.ru/RETAILDEV-1105