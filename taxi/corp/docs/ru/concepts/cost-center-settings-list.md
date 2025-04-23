# Список настроек кост-центров

{% include [cost-center-edit-about](../_includes/concepts/cost-center-edit/id-cost-center-edit/about.md) %}


## Синтаксис запроса

```
GET https://business.taxi.yandex.ru/api/1.0/client/{идентификатор клиента}/cost_centers 
```

{% include [order-create-headers-p](../_includes/concepts/order-create/id-order-create/headers-p.md) %}


#### Authorization
OAuth-токен. Процесс получения токена описан в разделе [Начало работы](quickstart.md).

## Пример запроса

```
GET https://business.taxi.yandex.ru/api/1.0/client/a2...d09/cost_centers

Authorization: <OAuth-токен>
```

## Пример ответа

```
{
    "items": [
        {
            "id": "1234567890abcdef1234567890abcdef",
            "name": "Основной центр затрат",
            "default": true,
            "field_settings": [
                 {
                   "id": "0123456789abcdef0123456789abcde0",
                   "hidden": false,
                   "title": "Центр затрат",
                   "required": true,
                   "services": ["taxi"],
                   "format": "select",
                   "values": ["командировка", "в центральный офис"]
                 },
                 {
                   "id": "0123456789abcdef0123456789abcde1",
                   "hidden": false,
                   "title": "Цель поездки",
                   "services": ["taxi"],
                   "required": true,
                   "format": "mixed",
                   "values": ["цель 1", "цель 2", "особая цель"]
                 },
                 {
                   "id": "0123456789abcdef0123456789abcde2",
                   "hidden": true,
                   "title": "Номер дела",
                   "services": ["taxi"],
                   "required": true,
                   "format": "text",
                   "values": []
                 }
            ]
        }
    ]
}
```

## Описание полей ответа

Поле | Описание | Формат
----- | ----- | -----
`items` | Список наборов настроек центров затрат. | Массив
`id` | id набора настроек центра затрат. | Строка
`client_id` | id клиента. | Строка
`name` | Название набора настроек центра затрат. | Строка
`default` | Является ли набор настроек основным. | Логическое
`field_settings` | Список настроек для каждого поля центров затрат. | Массив
`field_settings.[N].id` | id поля. | Строка
`field_settings.[N].title` | Название поля. | Строка
`field_settings.[N].required` | Обязательно ли заполнять это поле при заказе. | Логическое
`field_settings.[N].hidden` | Не показывать и не использовать это поле при заказе. Необязательное поле. | Логическое
`field_settings.[N].services` | Идентификаторы сервисов, в которых можно использовать это поле при заказе. На данный момент поддерживается только `taxi`. | Массив
`field_settings.[N].format` | Формат указания центра затрат для сотрудника. Возможные значения: <br/>- `select` — сотрудник выбирает кост-центр из списка.<br/>- `text` — сотрудник самостоятельно указывает кост-центр в текстовом поле.<br/>- `mixed` — сотруднику доступны выбор кост-центра из списка и свободный ввод в текстовом поле. | Объект
`field_settings.[N].values` | Cписок кост-центров, доступных для сотрудника. Формат списка `"кост_центр1","кост_центр2", ...`.<br/>Доступен только при значении формата `mixed` и `select`. | Объект


## Возможные коды ответа

{% include [cost-center-create-possible-answers-code](../_includes/concepts/cost-center-create/id-cost-center-create/possible-answers-code.md) %}


- `200` — запрос выполнен успешно.
- `401` — был передан неверный [OAuth-токен](quickstart.md).
- `403` — у клиента не хватает прав на выполнение данного запроса.

