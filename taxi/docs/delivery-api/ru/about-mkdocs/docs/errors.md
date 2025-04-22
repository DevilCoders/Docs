# Справочник ошибок

|Код ошибки | Текст ошибки | Описание ошибки |
|:--- |:--- |:--- |
|401|Not authorized request|Убедитесь, что передали верный токен|
|404|Delivery interval in the past|Интервал доставки указан в прошлом|
|404|Delivery interval is too narrow|Указан узкий интервал. Интервалы принимаются в GMT+0 в формате UNIX/UTC|
|404|Item's articles must be unique. Bad article: ...|Указаны одинаковые артикулы|
|404|Cannot deliver|Не удаётся создать заявку. Неправильно передан интервал, доставка в регион невозможна, не заведены отгрузки|
|404|Dimensions should not exceed|Превышение габаритов|
|404|Inconsistency billing details|Ошибка стоимости товаров. Проверьте, что `assessed_unit_price` ≥ `unit_price`|
|400|Incorrect station platform ID|Проверьте правильность передачи ID станции|
|400|Incorrect JSON content. Please check the formatting|Сверьтесь с нашими примерами интеграции|
|400|There is place with no items|Есть место, в котором не заданы товары|
|400|There are items with no place|Есть товары, у которых нет места|
|400|Cannot parse ... info|Ошибка при чтении JSON. Проверьте данные или обратитесь в поддержку|
|400|There already was request with such code within this employer|Проверьте данные. Ключ `operator_request_id` должен быть уникальным для каждого заказа|
