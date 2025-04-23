# /mail/send_system_mail

Ручка для отправки системных писем


## Query args

**Обязательные:**

`uid` id отправителя

`from` email отправителя
    
`service` имя сервиса-клиента. Сервис: "sendbernar"

`to` список получателей

`request_id` id запроса

**Необязательные:**

`lid` список id меток, которые проставятся на письмо

`label` список меток, которые проставятся на письмо

**Пример запроса c аргументами:**

```
/mail/send_system_mail?uid=1&from=test%40yandex.ru&service=sendbernar&request_id=id&to=first@email.com&to=second@email.com&lid=lid1&label=label1
```


## Body

Тело запроса - тело письма как есть

**Пример тела письма:**

```
Content-Type: message/rfc822
MIME-Version: 1.0

Subject: Hello

Test
```

## Ответы

- `200 Ok`

```{"error": "Success", "explanation": "Ok"}```

- `400 Bad request`

- `500 Internal server error`

- `406 Not acceptable`

Ошибка связанная c временным баном и плохой кармой пользователей 

```{"error": "BadKarmaBanTime", "explanation": "..."}```

Ошибка попытки отправки письма

```{"error": "SendMessageFailed", "explanation": "..."}```

Ошибка недоступности, связанных с доставкой, компонент

```{"error": "ServiceUnavaliable", "explanation": "..."}```

Превышение лимита на количество получателей

```{"error": "ToManyRecipients", "explanation": "..."}```
