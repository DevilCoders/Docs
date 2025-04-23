* `_id`
    * Уникальный идентификатор записи в базе, должен иметь парный `Targeting._id`
    * `string`
    * default отсутствует
* `brand_id`
    * Установить на устройстве новое значение `brand_id`. Пустое значение на устройство не передаётся.
    * `string`
    * default `""`
        ```json
        "brand_id" : "olympic2018",
        ```
* `clids`
    * Новые значения клидов, которые будут отправлены на устройство. Старые клиды тоже будут отправлены, зависит от `delete_old_clids`.
    * `array[{name, value}]`
    * default `[]`
        ```json
        "clids" : [
            {
                "name" : "clid1",
                "value" : "5723832"
            },
            {
                "name" : "clid4",
                "value" : "5723833"
            }
        ],
        ```
* `delete_old_clids`
    * Удаляет старые клиды на устройстве
    * `boolean`
    * default `false`
        ```json
        "delete_old_clids" : false,
        ```
* `priority`
    * Больше значение - больше приоритет у кастомизации
    * `int`
    * default `0`
        ```json
        "priority" : 1,
        ```
* `switch_search_widget_to_yandex`
    * Отправляет на устройство флаг, чтобы появился диалог `"Заменить поиск на домашнем экране на Яндекс?"`, крайне редкий кейс в базе, скорее всего, уже не используется
    * `boolean`
    * default `false`
        ```json
        "switch_search_widget_to_yandex" : false,
        ```
* `title`
    * Используется в админке, на устройство не передаётся
    * `string`
    * default отсутствует
        ```json
        "title" : "browser MOBSERVER-1471",
        ```
