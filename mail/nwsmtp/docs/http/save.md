# /mail/save

Ручка для сохранения писем, которые будут отправлены наружу


Используется:

1. для сохранения черновиков;
2. для отложенной и отменяемой отправки;


## Query args

**Обязательные:**

`uid` id отправителя

`email` email отправителя
    
`service` имя сервиса-клиента. Сервис: "sendbernar"

`request_id` id запроса

`fid` id папки, в которую следует сложить письмо 

**Необязательные:**

`lid` список id меток, которые проставляются на письмо

`system` список системных меток, которые проставляются на письмо

`symbol` список символьных меток, которые проставляются на письмо

`old_mid` id письма, которое по-возможности нужно обновить вместо создания нового письма

`detect_spam` проверка письма на спам. Если выставлен в 0 - проверка на спам не производится

`detect_virus` проверка письма на вирусы. Если выставлен в 0 - проверка на вирусы не производится

`received_date` дата получения письма

**Пример запроса c аргументами:**

```
/mail/save?uid=1&email=test%40yandex.ru&service=sendbernar&request_id=id&fid=1&old_mid=1&lid=lid1&system=SystMetkaSO:label1&symbol=symbol:label2&detect_spam=0&detect_virus=0&received_date=1
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

```{"error": "Success", "mid": "228", "explanation": "Ok"}```

- `400 Bad request`

- `500 Internal server error`

- `406 Not acceptable`

Попытка отправить спамовое письмо

```{"error": "Spam", "mid": "", "explanation": "..."}```

Попытка отправить malicious спамовое письмо

```{"error": "StrongSpam", "mid": "", "explanation": "..."}```

Попытка отправить вирусного письмо

```{"error": "Virus", "mid": "", "explanation": "..."}```

Ошибка попытки отправки письма

```{"error": "SendMessageFailed", "mid": "", "explanation": "..."}```

Ошибка недоступности, связанных с доставкой, компонент

```{"error": "ServiceUnavaliable", "mid": "", "explanation": "..."}```
