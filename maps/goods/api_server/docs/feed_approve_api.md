# API обеления фидов

Информацию про авторизацию и коды ошибок см. в [основной доке по API](https://a.yandex-team.ru/arc/trunk/arcadia/maps/goods/api_server/docs/api.md).

**Поддерживаемые фиды**
 - `YANDEX_AUTO_RU` &mdash; Авто.ру
 - `YANDEX_EDA` &mdash; Яндекс.Еда
 - `YANDEX_WEBMASTER` &mdash; Яндекс.Вебмастер
 - `YDO` &mdash; Яндекс.Услуги
 - `TYCOON` &mdash; личный кабинет Яндекс.Бизнес, не используется в большинстве ручек (см. описание)

## POST /goods/1.x/company/{company-permalink}/feeds/settings

**Запрос**:
```json
{
    // опциональное поле, если указано disable_feeds=true
    // можно указывать значение TYCOON
    "selected_feed": "YDO",

    // опциональное поле, если указан selected_feed
    // (по умолчанию false)
    "disable_feeds": false
}
```

**Ответ**:
```json
{
    // см. описание поля settings в ручке GET /goods/1.x/company/{company-permalink}/feeds
    "used_feed": "TYCOON", // например, если в YDO сейчас нет товаров, иначе совпадает с selected_feed
    "selected_feed": "YDO", // отсутствует, если disable_feeds=true
    "disable_feeds": false
}
```

## GET /goods/1.x/company/{company-permalink}/feeds

**Ответ**:
```json
{
    "settings": {
        // текущий реально используемый фид
        // может отличаться от выбранного пользователем (selected_feed), если в выбранном нет товаров
        // если в выбранном есть товары, то совпадает с selected_feed
        // отсутствует, если disable_feeds=true
        "used_feed": "YANDEX_EDA",
        "used_feed_name": "Яндекс.Еда",
        "disable_feeds": false,
        // выбранный пользователем фид
        // опциональное поле: может отсутствовать, если настройки не заданы
        "selected_feed": "YDO",
        "selected_feed_name": "Яндекс.Услуги"
    },
    // список всех существующих фидов
    "feeds": [
        {
            "id": "TYCOON",
            "name": "Яндекс.Бизнес",
            "items_count": 0
        },
        {
            "id": "YANDEX_AUTO_RU",
            "name": "Яндекс.Авто",
            "items_count": 0
        },
        {
            "id": "YANDEX_EDA",
            "name": "Яндекс.Еда",
            "items_count": 130,
            // опциональное поле, присутствует если запрос был с параметром count_items_with_photos=true
            "items_with_photos_count": 96,
            // опциональное поле, присутствует если есть/была информация из источника
            "last_update_time": "1970-01-01T00:00:00.000Z",
            // опциональное поле, есть не для всех источников
            "feed_cabinet_url": "https://vendor.eda.yandex/places/12345"
        },
        {
            "id": "YANDEX_WEBMASTER",
            "name": "Яндекс.Вебмастер",
            "items_count": 10000,
            "items_with_photos_count": 0,
            "last_update_time": "1970-01-01T00:00:00.000Z"
        },
        {
            "id": "YDO",
            "name": "Яндекс.Услуги",
            "items_count": 0,
            "items_with_photos_count": 0,
            "last_update_time": "1970-01-01T00:00:00.000Z"
        }
    ]
}
```

