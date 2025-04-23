## /driver/channels

Ручка для просмотра каналов, в которых водитель может отправлять сообщения. GET запрос.

## Параметры

- `db` - идентификатор парка
- `session` - водительская сессия для проверки авторизации

## Пример запроса

`curl X GET "driver-protocol.taxi.tst.yandex.net/driver/channels?db=7ad36bc7560449998acbe2c57a75c293&
session=27b87ff254be497ab9ff4d5597e5f097" -v`

## Коды ответа

200 - каналы успешно получены

401 - авторизация не удалась, невалидные парк или сессия

## Пример ответа

    [
      {
        "id": "Index.РОССИЯ",
        "name": "General chat"
      },
      {
        "id": "Sos",
        "name": "SOS"
      },
      {
        "id": "Support",
        "name": "Technical"
      },
      {
        "id": "7ad36bc7560449998acbe2c57a75c293",
        "name": "My taxi company"
      },
      {
        "id": "City.Москва",
        "name": "Москва"
      }
    ]
