#### /service/chat/add

Ручка для добавления сообщения в чат. POST запрос.

## Параметры

### Параметры в query string
- `db` - идентификатор парка

### Параметры в теле запроса
- `channel` - канал, в который добавляется сообщение
- `driver` - идентификатор водителя, для отправки пушей
- `msg` - тело добавляемого сообщения

Также в теле есть запросы, имеющие отношение к сессии пользователя

- `user_id` - id пользователя
- `yandex` - состоит ли пользователь в Яндексе, строка или bool (True, 'True' и т.д.)
- `user_login` - логин пользователя если yandex = true
- `user_name` - имя пользователя если yandex = false

## Пример запроса

`curl X POST -d '{"msg": "Это тестовое сообщение", "user_login": "olegvp",
"yandex": "True", "user_id": "qwerty123456", "channel": "PRIVATE", "driver": "1111"}'
"driver-protocol.taxi.dev.yandex.net/service/chat/add?db=9b5eb7d445db4aa4a7adae41582de1b9" -v`

## Коды ответа

200 - сообщение было успешно добавлено

400 - невалидный запрос или для данного парка выключен чат

404 - не получен канал (при отсутствии канала не найден парк)

500 - запрос на добавление в редис неудачный или не найдена страна при валидном парке

## Пример добавленного сообщения

    {
      "company": "тт",
      "date": "2017-12-09T20:50:20.973162Z",
      "db": "9b5eb7d445db4aa4a7adae41582de1b9",
      "guid": "c75a5123130c4d88b1a2585b310cd547",
      "msg": "Это тестовое сообщение",
      "name": "olegvp",
      "user": "qwerty123456",
      "user_type": 2
    }

## Пример добавленного пуша

    {
      "Action": 100,
      "Data": {
        "Id": "c75a5123130c4d88b1a2585b310cd547",
        "Message": "Это тестовое сообщение",
        "Name": "olegvp"
      },
      "Db": "9b5eb7d445db4aa4a7adae41582de1b9",
      "Driver": "1111"
    }
