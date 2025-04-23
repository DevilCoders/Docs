# Описание формата пушей
Пример пуша для пушного: https://paste.yandex-team.ru/1085862/text

## Xiva payload

Отсюда берутся поля для переупаковки

```js
{
    "title": "ГАЗ 21 «Волга», 1969",  // [M] - Заголовок уведомления
    "body": "2 000 000 ₽ / 1 000 км посмотреть объявление", // [M] - Текст уведомления
    "action": "notification_center", // [M] - Индикатор пуша центра уведомлений, тип для определения происхождения пуша (подписки - "deeplink", ЦУ - "notification_center")
    "image_url": "//avatars.mds.yandex.net/get-autoru-vos/2106781/0424288c1373bbe35d317afb069eb842/1440x720", // [O] - картинка для отображения в пуше
    "android_channel": { // [M] - идентификатор канала пуш-уведомлений для андроид
        "id":"personal_recommendations",
        "name":"Персональные рекомендации"
    }, 
    "topic": "personal_recommendations", // [M] - Тематика пуша
    "notification_id": 12345, // [M] -  идентификатор уведомления, по которому пуш можно схлопнуть, если уведомление уже прочитано в колокольчике
    "ios_action": { // [O] - действие при нажатии на пуш-уведомление
        "url": "ios_main_url" // Открыть диплинк по заданному url
    },
    "android_action": { // [O] - действие при нажатии на пуш-уведомление
        "url": "android_main_url" // Открыть диплинк по заданному url
    },
    "ios_actions": [{ // [O] - Отказались от реализации на iOS до запроса со стороны продукта. Действия для кнопок. Не больше 3-х кнопок.
            "text": "Open", // Текст на кнопке
            "action": {
                "url": "ios_specific_url" // Открыть диплинк по заданному url
            }
        },
        {
            "text": "Go to",
            "action": {
                "url": "ios_specific_url"
            }
        }
    ],
    "android_actions": [{ // [O] - действия для кнопок. Не больше 3-х кнопок
            "text": "Open", // текст на кнопке
            "action": {
                "url": "android_specific_url"
            }
        },
        {
            "text": "Go to", // текст на кнопке
            "action": {
                "url": "android_specific_url"
            }
        }
    ]
}
// [M] - Mandatory
// [O] - Optional
```

## iOS
```js
{
    "apns": {
        "aps": {
            "alert": {
                "title": "ГАЗ 21 «Волга», 1969",
                "body": "2 000 000 ₽ / 1 000 км посмотреть объявление"
            },
            "badge": 1,
            "sound": "default",
            "category": "ios_category_id", // определяет шаблон отображения, будет задано отправителем (более мелкое деление, чем топик) 
            "mutable-content": 1,
            "thread-id": "" // используется для группировки сообщений ({topic}_{object_type}_{object_id}?)
        },
        "collapse-id": "12345", // несколько уведомлений с одним идентификатором будут показаны как одно (системный заголовок apns-collapse-id)
        "repack_payload": [
            "action",
            "image_url",
            "topic", // нужно ли, если есть category?
            "notification_id", 
            "ios_action", 
            "ios_actions"
        ]
    }
}
```

## Android
```js
{
    "gcm": {
        "repack_payload": [
            "title",
            "body",
            "action",
            "android_channel", 
            "notification_id", 
            "image_url",
            "android_action",
            "android_actions"
        ]
    }
}
```
