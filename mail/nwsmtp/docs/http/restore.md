# /mail/restore

Ручка востановления письма в метабазу по метаданным.


Используется:


## Query args

**Обязательные:**

`uid` id пользователя

`service` имя сервиса-клиента.

`request_id` id запроса

**Пример запроса c аргументами:**

```
/mail/restore?uid=1&service=service&request_id=id
```


## Body

Тело запроса - json с параметрами

Секция `user_info`:

`email` (string) адрес получателя (нужен для СО)

Секция `mail_info`:

`stid` (string) `stid` оригинала письма

`fid` (string) `fid` папки, в которую следует сложить письмо

`tab` (string) имя таба, в который следует сложить письмо

`received_date` (int) дата получения оригинала письма

`lids` ([string]) набор меток (лидов), которые нужно проставить на письмо

`system` ([string]) массив системных меток

`symbol` ([string]) массив символьных меток

**Пример тела запроса:**

```
Content-Type: application/json
MIME-Version: 1.0

{
    "user_info": {
        "email": "email@yandex.ru"
    },
    "mail_info": {
        "stid": "320.mail:271344218.E893786:500447599397365724348105987",
        "fid": "1",
        "tab": "news"
        "received_date": 1573795913,
        "lids": ["lid1", "lid2"],
        "system": ["system"],
        "symbol": ["seen_label"]
    }
}
```


## Ответы:

- `200 Ok`

```{"mid": "123"}```

- `400 Bad request`

- `500 Internal server error`

- `406 Not Acceptable`

Ошибка восстановления письма, возникающая из-за попытки восстановить уже существующее письмо

```{"code": "DuplicateError", "message": "mid письма"}```

Ошибка недоступности, связанных с доставкой, компонент

```{"code": "ServiceUnavaliable", "message": "..."}```

Ошибка восстановления письма, возникающая из-за невалидного fid в теле запроса

```{"code": "InvalidFid", "message": "..."}```

Общие ошибки восстановления письма

```{"code": "RestoreError", "message": "..."}```

Ошибка восстановления письма, возникающая из-за отсутствия письма в сторадже

```{"code": "StorageMailNotFound", "message": "..."}```

Ошибка восстановления письма, возникающая из-за ошибок в nsls

```{"code": "NslsPermanentError", "message": "..."}```
