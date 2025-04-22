### /service/push

Отправить пуш-уведомление на клиент таксометра

### Пример запроса

`curl -v -H "Content-Type: application/json" -X POST -d '{"data": null, "code": 840, "driver_id": "b71a6b2071d4494b95dc83336c8a1179", "park_db_id": "7ad36bc7560449998acbe2c57a75c293"}' 'http://driver-protocol.taxi.tst.yandex.net/service/push'`

### Параметры

- `data` - данные пуша (валидный json)
- `code` - код пуша
- `driver_id` - uuid водителя
- `park_db_id` - идентификатор парка

Обязательное поле только `code`

### Пример ответа

400 - невалидный запрос (не удалось извлечь параметры, кто-то из них пустой и т.д.)
200 - Пуш-уведомление было сложено в редис асинхронно.
