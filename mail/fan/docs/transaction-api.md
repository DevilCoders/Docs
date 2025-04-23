# API для отправки транзакционного письма

## Авторизация

Запросы к API нужно делать с ключами, которые создаются для аккаунта.
Ключ нужно передавать в HTTP Basic auth в качестве имени пользователя, пароль при этом пустой.

Так же возможнен вариант авторизации по средствав TVM2.0, для этого необходимо дополниельно внести tvm-id клиена в таблицу 'Tvm services'.

## Обычная отправка

После создания транзакционной рассылки появляется подсказка [например тут](https://test.sender.yandex-team.ru/autoru/campaign/775/overview)

```
POST /api/0/<account-slug>/transactional/<campaign-slug>/send
```

Исторически ручка корректно работала только с параметрами, передваемыми как данные формы. Сейчас можно отправлять параметры в теле запроса двумя способами: как данные формы (`Content-Type: application/x-www-form-urlencoded`) или как обычный JSON (`Content-Type: application/json`). Параметр `to_email` может быть указан в адресной строке как `?to_email=alice@example.com`. Если данные отправляются как данные формы, то для "сложных" полей значения нужно указывать в виде JSON строки, а также не забыть перевести все параметры запроса в percent encoding: https://developer.mozilla.org/en-US/docs/Glossary/percent-encoding.

Указать получателя можно тремя способами, их приоритет соответсвует хронологическому появлению соответствующего способа:
1. параметр `to_email` - самый приоритетный - этот параметр можно указать в теле запроса или как параметр URL - позволяет указать одного получателя. См. также пункт "Отправка на uid".
2. параметр `to_yandex_puid` - позволяет указать одного получателя через его UID - мы сходим за дефолтным адресом в блэкбокс синхронно, а если не получится вернем ошибку
3. параметры `to`, `cc`, `bcc` - позволяют задать нескольких получаталей одного письма. `cc` и `bcc` опциональные. Параметр `to` задаем непосредственных получаталей письма, которые будут указаны в заголовке `To` письма, параметр `cc` задает получаталей копии письма, которые будут указаны в заголовке `Cc` и `bcc` задает получателей скрытой копии письма, которые не будут указаны в заголовках письма, но которые также получат само письмо. Списки `to`, `cc`, `bcc` вместе формируют всех получаталей письма (будут указаны командой `RCPT TO: {email}` во время сессии с SMTP-сервером).
    Все три параметра это массивы объектов с обязательным ключем `email` и опциональным ключем `name`. Например, в теле JSON запроса можно написать:<br>
    ```json
    {
     "to": [
         {"email": "alice@example.com", "name": "Alice"},
         {"email": "bob@example.com", "name": "Bob"}
       ]
     }
   ```

 Остальные параметры:
 * `args` - переменные, которые будут подставлены в тело письма - объект с ключами или соответствующая ему JSON-строчка. **Если args был послан как строчка (что неизбежно, если посылать x-www-form-urlencoded), то в ответе ручки args тоже будет строчкой - это вынужденная мера для легаси клиентов. Если посылать args как объект в application/json запросе, то в ответе тоже будет объект**
 * `host` - тестинг https://test.sender.yandex-team.ru, продакшен https://sender.yandex-team.ru
 * `async` - `true` или `false`, по-умолчанию `true` - рекомендуется отправлять письма асинхронно, указывая `async=true`, в этом случае будет создана задача на отправку письма в бэкенд доставки. Как только задача будет создана и положена в очередь задач, клиенту вернется 200 ОК. Задача отправки будет выполнена в ближайшее возможное время, пропорциональное отношению загруженности очереди к скорости ее разгребания воркерами. Синхронный режим __НЕ__ рекомендуется.
 * `countdown` - для асинхронной отправки - отправить рассылку не сразу, а через countdown секунд. можно задавать в виде целого числа или в виде "12h13m11s"
 * `expires` - для асинхронной отправки - не отправлять через expires секунд. через какое время уже не нужно отправлять письмо. формат параметра такой же, как countdown.
 * `ignore_empty_email` - если ```true```, то при пустом значении ```to_email``` ручка вернёт HTTP 202. Без этого параметра вернёт HTTP 400.
 * `attachments` - прикрепить файлы к письму. Массив объектов вида:<br>
    ```json
    [{"filename": "a.jpg", "mime_type": "image/jpeg", "data": "<base64-encoded data>"}]
   ```
   где ключ `data` содержит base64 encoded бинарные данные файла.
 * `headers` - дополнительные заголовки письма - объект со строковыми значениями, чтобы задать заголовок письма "header: value" нужно указать<br>
    ```json
    {"header":  "value"}
    ```
   Можно указать свой `Reply-To`.
 * `from_email, from_name` - заменить адрес отправителя, прописанный в шаблоне, на эти значения (это нужно в редких кейсах; обычно лучше использовать адрес, прописанный в шаблоне Рассылятора). Может приводить к ошибкам, т.к. будет проведена валидация доступности используемого домена для Вашего аккаунта, а так же проверка на эксклюзивные права использования email-адреса (есть список адресов e.g. passport@yandex(-team)?.ru, отправка от имени которых ограничена).
 * `has_ugc` - True|False, флаг буде использован в СО при проверки письма. Флаг не проставляется автоматически, поэтому его всегда необходимо передавать. Значение true обозначет, что письмо бедт содержать ugc, который мы не контролируем и потенциально может быть опасным.

HTTP-заголовки:
* `X-Sender-Real-User-IP` - ip инициатора отправки письма. Необходимо проставлять этот заголовок всегда, когда инициатором отправки письма является пользователь. Например, пользователь заполняет форму на Вашем сайте и нажимает кнопку "отправить как email". В таком случае требуется передать ip адрес пользователя и дополнительно передавать флаг `has_ugc:true`
* `X-Sender-I-Am-Sender` - `true|false`, флаг обозначающей, что инициатором отправки является сам сервис. Например, отправка письма с восстановлением пароля.

 `X-Sender-I-Am-Sender` и `X-Sender-Real-User-IP` являются взаимоисключающими заголовками. В дальнейшем их использование станет обязательным. 

### Примеры
####Отправляем параметры как JSON
```bash
curl -X POST -u ce3ee6e2bdf3484f9b02b080694af289: -H "content-type: application/json" -d @transact_data.json 'https://test.sender.yandex-team.ru/api/0/autoru/transactional/STIYWPX1-LUX/send'
```

где transact_json:
```json
{
  "from_name": "Bob",
  "from_email": "bob@example.com",
  "cc": [
    {
      "email": "mary@example.com",
      "name": "Mary"
    },
    {
      "email": "john@example.com",
      "name": "John"
    }
  ],
  "bcc": [
    {
      "email": "tom@example.com",
      "name": "Tom"
    },
    {
      "email": "jan@example.com",
      "name": "Jan"
    }
  ],
  "to": [
    {
      "email": "alice@example.com",
      "name": "Alice"
    },
    {
      "email": "bob@example.com",
      "name": "Bob"
    }
  ],
  "attachments": [
    {
      "data": "",
      "mime_type": "application/text",
      "filename": "a.txt"
    }
  ],
  "args": {
    "var": "val"
  },
  "headers": {
    "one": "1",
    "two": "2",
    "three": "3"
  },
  "async": true
}
```

Пример ответа
```json
{
   "params" : {
      "source" : {
         "cc" : [
            {
               "name" : "Mary",
               "email" : "mary@example.com"
            },
            {
               "email" : "john@example.com",
               "name" : "John"
            }
         ],
         "to" : [
            {
               "name" : "Alice",
               "email" : "alice@example.com"
            },
            {
               "name" : "Bob",
               "email" : "bob@example.com"
            }
         ],
         "args" : {
            "var" : "val"
         },
         "attachments" : [
            {
               "filename" : "a.txt",
               "mime_type" : "application/text",
               "data" : "<binary data>"
            }
         ],
         "bcc" : [
            {
               "email" : "tom@example.com",
               "name" : "Tom"
            },
            {
               "name" : "Jan",
               "email" : "jan@example.com"
            }
         ],
         "headers" : {
            "three" : "3",
            "two" : "2",
            "one" : "1"
         }
      },
      "control" : {
         "for_testing" : false,
         "async" : true,
         "expires" : 86400,
         "countdown" : null
      }
   },
   "result" : {
      "message_id" : "<20200427085314.395111.98f6a1887b0c4a52ab068ba909d9efcd@bc2393cb47a9>",
      "status" : "OK",
      "task_id" : "91b279e0-e1c8-46ac-8c69-d91ea3235da2"
   }
}
```

#### Отправляем параметры как данные формы
```bash
curl -X POST \
    -u 3579418885b9514a437570d420e46926: \
    -d args='{"var1":"value1"}' \
    -d async=true \
    -d attachments='[{"filename": "a.jpg", "mime_type": "image/jpeg", "data": "<base64-encoded data>"}]' \
    -d from_name='Ivan' \
    -d from_email='devnull@yandex.ru' \
    -d to_email=alice@example.com \
    'https://test.sender.yandex-team.ru/api/0/autoru/transactional/STIYWPX1-LUX/send'
```

Пример ответа:

```
HTTP/1.1 200 OK
Content-Type: application/json
```

**Ответ содержит приведенные к JSON данные (кроме args)**
```json
{
   "params" : {
      "control" : {
         "expires" : 86400,
         "for_testing" : false,
         "async" : true,
         "countdown" : null
      },
      "source" : {
         "to" : [],
         "args" : "{\"var1\" : \"value1\"}",
         "attachments" : [
            {
               "mime_type" : "image/jpeg",
               "data" : "<binary data>",
               "filename" : "a.jpg"
            }
         ],
         "bcc" : [],
         "to_email" : "alice@example.com",
         "cc" : []
      }
   },
   "result" : {
      "status" : "OK",
      "task_id" : "2258a15b-6209-44f9-841b-53ac1f47fa52",
      "message_id" : "<20200507080804.478082.fecae2b1367a4afc8115047f75a7f405@api-10.production.ysendercloud>"
   }
}

```

Возникла ошибка:
    
    HTTP/1.1 500 Internal Server Error
    Content-Type: application/json
    
    {
      "params": {
        "control": {
          "async": false,
          "countdown": null,
          "expires": 86400,
          "for_testing": false
        },
        "source": {
          "to_email": "s@lavr.me",
          "header": [],
          "ignore_empty_email": false
        }
      },
      "result": {
        "status": "ERROR",
        "message": "TemplateRuntimeError: unsupported operand type(s) for -: 'Undefined' and 'Undefined'"
      }
    }


## Отправка на uid

Вместо email-адреса ```to_email``` в ручки можно передавать яндексовый uid в параметре ```to_yandex_puid```.
В этом случае Рассылятор синхронно сходит в Паспорт (blackbox), возьмёт дефолтный email пользователя.

Если блэкбокс недоступен, то ручка вернёт код 500.

Если email в паспорте не указан, то письмо не будет отправлено, а ручка вернёт код ответа 400 или 202 в зависимости от наличия параметра ```ignore_empty_email```.

Если передать в ручку оба параметра ```to_email``` и  ```to_yandex_puid```, то для отправки будет использован адрес ```to_email```.

## TVM-авторизация

```bash
curl -X POST \
    -H 'X-Ya-Service-Ticket:3:serv:CBAQ__________9_IggIwMQHEMqJeg:ATgOsZmfQ40FiQg3fioPkzi09P_THDulqgbhNhVQx-8t4ED4r0q2aF8Cm6UZbWkTUtCW0S9l5I6ShWoMkoU9INXpdyyg1621x44X-nDJiSTsEqlNJNAQ5viQg48Rt8qbjv4j5qEDPXmDxybamzjqEFnkw2Ps4djGh3HakgmGu1w' \
    -d args='{"var1":"value1"}' \
    -d async=true \
    -d to_email='user@yandex-team.ru' \
    'http://localhost:8000/api/0/dev/transactional/4T3EDKO3-IH7/send'
```

Возможные ошибки
 - `HTTP_401_UNAUTHORIZED {"detail":"TVM source 123456 does not exists"}` - это обозначает, что аккаунт не привязан к используемум tvm-id. Исправить это можно в админке через "Tvm services".
 - `HTTP_401_UNAUTHORIZED {"detail":"TVM source 123456 has more then one linked account, put chosenone to X-Sender-Prefer-Account header"` - Такое бывает, если к одному tvm-id привязано несколько сервисов. В таком случае, нельзя однозначно определить какой использвоать. На такой случай есть заголовок `X-Sender-Prefer-Account`, в который нужно проставить slug нужного сервиса.


## Проврека статуса отправки
Можно попросить администратора включить асинхронную проверку статуса отправленного сообщения.
После вызова метода `send` в течение некоторо времени (выставляется для каждого аккаунта отдельно) будет доступна ручка
```
POST /api/0/<account-slug>/transactional/<campaign-slug>/status?message_id=$VALUE
```

### Пример запроса
Отправляем письмо:
```
curl -X POST
     -u 8304aacb34cb40b0aa8ea591b5096984:
     -d args='{"var1":"value1"}'
     -d async=true
     -d to_email='email@yandex-team.ru'
     'http://fan:8000/api/0/dev/transactional/0WTUX7Q3-RB21/send'
```
В ответ приходит:
```{
    "params" : {
        "control" : {
            "async" : true,
            "countdown" : null,
            "expires" : 86400,
            "for_testing" : false
        },
        "source" : {
            "to_email" : "vkoakrev@yandex-team.ru",
            "args" : "{\"var1\":\"value1\"}"}},"result":{"status":"OK","message_id":"<20200819200830.826528.82d3ac43c67f40449ac5dbfb6da0d3f0@3f9714fb21f6>","task_id":"793964fc-cc76-4bcd-a739-eeb415a653b8"
}
```
Нас интересует параметр `message_id`, будем использвоать его в запросе:
```
curl -X GET
     -u 8304aacb34cb40b0aa8ea591b5096984:
     'http://fan:8000/api/0/dev/transactional/0WTUX7Q3-RB21/status?message_id=<20200819200830.826528.82d3ac43c67f40449ac5dbfb6da0d3f0@3f9714fb21f6>'
```
Ответ:
```
{
    "msg" : "SMTPSenderRefused: Invalid sender sndr.bnc.test@yandex.ru",
    "code" : 550,
    "message_id" : "<20200819200819.670208.52e313c5f1b4437ea0de509fcd9a563c@3f9714fb21f6>",
    "retry" : false
}
```

### Расшифровка ответа
* `msg` - текстовое описание статуса
* `code` - smtp статус код
    * `200-299` - OK
    * `500` - Internal error
    * `404` - запись с таким идентификатором отсутствует (скорее всего истех срок хранения)  
    * `104` - письмо находится в обработке
* `retry` - флаг, который сообщает, будет ли рассылятор пытаться отправить письмо еще раз. Такое возможно, например, при сетевой ошибке