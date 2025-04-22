# Изменить данные черновика заказа

Запрос позволяет редактировать информацию о кост-центрах клиента в [черновике заказа](order-create.md).

## Синтаксис запроса

```
PUT https://business.taxi.yandex.ru/api/1.0/client/{идентификатор клиента}/order/{идентификатор заказа}/change
```

{% include [order-create-headers-p](../_includes/concepts/order-create/id-order-create/headers-p.md) %}


#### Authorization
OAuth-токен. Процесс получения токена описан в разделе [Начало работы](quickstart.md).

Данные о заказе передаются в теле запроса в формате JSON:

Поле | Описание | Формат
----- | ----- | -----
`cost_center` | [Название центра затрат](cost-center-create-old.md) клиента. Поле игнорируется при наличии в запросе поля `cost_center_values`. | Строка
`cost_center_values` | Новые поля [центров затрат](cost-center-settings-list.md). | Массив
`cost_center_values.[N].id` | id поля [центров затрат](cost-center-settings-list.md). | Строка
`cost_center_values.[N].title` | Название поля [центров затрат](cost-center-settings-list.md). | Строка
`cost_center_values.[N].value` | Значение поля [центров затрат](cost-center-settings-list.md) для данного заказа. | Строка


## Описание полей ответа

В случае успеха вернется пустой ответ с кодом 200.

## Пример запроса

```
PUT https://business.taxi.yandex.ru/api/1.0/client/a2...d09/order/a3...b386/change
...
Authorization: <OAuth-токен>

    { "cost_center": "some cost center",
      "cost_center_values": [
        {
            "id": "cost_center",
            "title": "Цель поездки",
            "value": "производственная необходимость"
        },
        {
            "id": "0123456789abcdef0123456789abcde1",
            "title": "Цель поездки",
            "value": "особая цель"
        }
      ]
 }
```

## Возможные коды ответа

{% include [cost-center-create-possible-answers-code](../_includes/concepts/cost-center-create/id-cost-center-create/possible-answers-code.md) %}


- `200` — запрос выполнен успешно.
- `400` — в запросе был передан неизвестный параметр или параметр с недопустимым значением.
- `401` — был передан неверный [OAuth-токен](quickstart.md).
- `403` — у клиента не хватает прав на выполнение данного запроса.
- `404` — запрашиваемая запись не найдена.
- `406 GENERAL` - ошибка при проверке возможности сделать заказ, точная причина указана в теле ответа в поле `message`.

