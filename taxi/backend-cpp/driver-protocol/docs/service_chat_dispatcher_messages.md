## /service/chat/dispatcher/messages

Ручка для просмотра сообщений в диспетчерской парка. POST запрос.

Возвращаются только недавние сообщения (временной промежуток регулируется конфигом
CHAT_DISPATCHER_MESSAGES_LAST_MINUTES). Сообщения идут в порядке от давних к новым.
Дата в каждом сообщении меняется с учетом временной зоны, соответствующей парку.

## Параметры

### Параметры в query string
- `db` - идентификатор парка

### Параметры в теле запроса
- `md5` - хэш, соответствующий парку. Если совпадает с тем, что в базе, то новых сообщений нет.

## Пример запроса

`curl X POST -d '{"md5": "111"}' "driver-protocol.taxi.tst.yandex.net/service/chat/dispatcher/messages
?db=7ad36bc7560449998acbe2c57a75c293" -v`

## Коды ответа

200 - сообщения успешно получены

400 - невалидный запрос

404 - не найден парк

## Пример ответа

    {
      "items":[
        {
          "company": "Лещ",
          "date": "2017-11-29T18:44:20+0000",
          "db": "7ad36bc7560449998acbe2c57a75c293",
          "guid": "80c58c2ee57c40a8b276fcd6a8d0a53c",
          "icon": "https://storage.mdst.yandex.net/get-taximeter/4267/206897fa266d4427a2f565d0ded71c5e_large.jpg",
          "id": "80c58c2ee57c40a8b276fcd6a8d0a53c",
          "msg": "123\\n7 (917) 526-87-18",
          "name": "[0001] Громов Иван Сергеевич",
          "user": "8f6c9d9736044d3a8a29cd0762a5f392",
          "user_type": 1
        },
        {
          "company": "Лещ",
          "date": "2017-11-29T19:42:38+0000",
          "db": "7ad36bc7560449998acbe2c57a75c293",
          "guid": "2b5c3c6e9d354753b119714ea1b45c10",
          "icon": "https://storage.mdst.yandex.net/get-taximeter/4267/206897fa266d4427a2f565d0ded71c5e_large.jpg",
          "id": "2b5c3c6e9d354753b119714ea1b45c10",
          "msg": "SOS водителю нужна помощь\\n7 (917) 526-87-18",
          "name": "[0001] Громов Иван Сергеевич",
          "tag": "SOS",
          "user": "8f6c9d9736044d3a8a29cd0762a5f392",
          "user_type": 1
        }
      ],
      "md5":"343d541ee461243b2ebe0a4b32613ba5"
    }
