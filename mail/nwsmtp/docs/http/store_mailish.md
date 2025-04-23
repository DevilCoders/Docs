# /mail/store_mailish

Ручка для сохранения писем мейлиш пользователям

## Headers
`X-Request-Id` идентификатор запроса.

`Content-Type: multipart/mixed` нужен обязательно для multipart запроса.

## Query args

**Обязательные:**

`uid` id пользователя, кому складывается письмо

`fid` id папки в базе, куда складывается письмо

`external_imap_id` внешний imap_id

## Body
**Multipart запрос**. Тело запроса состоит из двух частей (именно в таком порядке): 
1. json
2. тело письма как есть

### Json:

Секция `options`:

`enable_push` (bool) Отсылать пуш. По-умолчанию `false`

Секция `mail_info`:

`received_date` (int) Дата получения письма

`labels` Словарь меток, которые надо проставить на письмо: `lids` ([string]), `symbol` ([string]) - параметр поддерживает такие метки, как: seen_label, deleted_label, recent_label, answered_label и т. д.

Секция `user_info`:

`email` (string) Адрес пользователя, кому складывается письмо (нужно для похода в СО)

### Пример json части запроса:
```
{
    "options": {
        "enable_push": false
    },
    "mail_info": {
        "received_date": 1573795913,
        "labels": {
            "lids": ["1"],
            "symbol": ["seen_label"], 
        }
    },
    "user_info": {
        "email": "foo@yandex.ru"
    }
}
```

## Ответы:
- `200 Ok`

```{"mid": "123", "imap_id": "456"}```

- `400 Bad request`

```{"code": "bad_request", "message": "bad message"}```

- `413 Entity too large`

При превышении ограничения размера тела запроса в ~41MB.
Отлуп дает веб свервер, поэтому формат ответа дефолтный, внутренние обработчики не вызываются.

- `409 Conflict`

```{"code": "store_error", "message": "Permanent store error"}```

```{"code": "duplicate_found", "message": "duplicate found"}```

- `500 Internal server error`

```{"code": "internal_server_error", "message": "Internal error"}```

```{"code": "store_error", "message": "Temporary store error"}```

## Особенности:
1. Если не существует папки с `fid=<fid>`, то операция фейлится.
2. Дубликаты проверяются по кортежу (`uid`, `fid`, `external_imap_id`). 
3. Нет полноценной проверки на спам, в спамообороне получаем только типы и доменную метку.
4. Не работают фильтры и черно-белые списки.
5. Не работает децикляция по заголовкам
6. Нет проверки на вирусы
7. Ручка только для Большой Почты.
