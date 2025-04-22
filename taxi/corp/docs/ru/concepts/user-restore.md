# Восстановление пользователя

Запрос позволяет восстановить удаленного пользователя клиента.

## Синтаксис запроса

```
PUT https://business.taxi.yandex.ru/api/1.0/client/{идентификатор клиента}/user/{идентификатор пользователя}/restore
```

{% include [order-create-headers-p](../_includes/concepts/order-create/id-order-create/headers-p.md) %}


#### Authorization
OAuth-токен. Процесс получения токена описан в разделе [Начало работы](quickstart.md).

Данные о пользователе передаются в теле запроса в формате JSON:

Поле | Описание | Формат
----- | ----- | -----
`email` | Адрес электронной почты пользователя. | Строка
`fullname` | Полное имя пользователя. | Строка
`department_id` | Идентификационный номер подразделения. | Строка
`nickname` | Краткое имя пользователя. | Строка
`role` | Блок с информацией о роли пользователя. Роль можно указать следующими способами: <br/>- При помощи [идентификатора уже существующей роли](role-create.md#role-id-desc).<br/>- При помощи описания новой роли пользователя. Поля с описанием роли аналогичны полям запроса [Создание новой роли](role-create.md) (кроме поля [name](role-create.md#name-desc)). | Объект
`role_id` | Идентификационный номер роли пользователя. | Строка
`classes` | Список доступных пользователю тарифов. Данное поле следует передавать если не был передан параметр `role_id` в блоке `role`. | Масиив
`limit` | Ограничения на сумму, которую пользователь может потратить на поездки за календарный месяц. | Строка
`phone` | Телефонный номер пользователя. | Строка
`is_active` | Признак активности пользователя. Неактивный пользователь не имеет возможности самостоятельного заказа и на его имя нельзя заказать поездку. | Логическое
`cost_center` | Название [кост-центра клиента](cost-center-create.md). | Строка


## Описание полей ответа

В случае успешного запроса, будет возвращен пустой ответ с кодом 200.

## Примеры запросов

Запрос с указанием существующей роли:

```
PUT https://business.taxi.yandex.ru/api/1.0/client/a2...d09/user/3caa3587675b49deb62e3286b753b05e
...
Authorization: <OAuth-токен>
        
    {
        "email": "example-mail@example-company.ru",
        "fullname": "Иванов Илья",
        "department_id": "233e725b0511459da7b38cb24f2d8fd7",
        "nickname": "ИИлья",
        "role": {
            "role_id": "620d2b39bb154e3ebe5debc8341b3471"
        },
        "phone": "+75551234567",
        "is_active": false,
        "cost_center": "some cost center"
    }
      
```

Запрос с указанием новой роли:

```
POST https://business.taxi.yandex.ru/api/1.0/client/a2...d09/user/
...
Authorization: <OAuth-токен>

    {
        "email": "example-mail@example-company.ru",
        "fullname": "Иванов Илья",
        "department_id": "233e725b0511459da7b38cb24f2d8fd7", 
        "nickname": "ИИлья",
        "role": {
            "limit": 10000,
            "classes": ["econom"],
            "restrictions": [
                {
                    "days": ["mo", "we", "sa"],
                    "start_time": "00:00:00",
                    "end_time": "23:59:00",
                    "type": "weekly_date"
                }
            ],
            "geo_restrictions": [
                {
                    "source": "geo_restriction_id1", 
                    "destination": "geo_restriction_id2";
                },
                {
                    "source": "geo_restriction_id3";
                }
            ]
        },
        "phone": "+75551234567",
        "is_active": false,
        "cost_center": "some cost center"
    }

```

## Возможные коды ответа

Ответ на данный запрос может содержать следующие стандартные HTTP-коды:

- `200` — запрос выполнен успешно.
- `401` — был передан неверный [OAuth-токен](quickstart.md).
- `403` — у клиента не хватает прав на выполнение данного запроса.
- `404` — запрашиваемая запись не найдена.

