# API интеграции с CRM для отправки промо-кампаний

## Авторизация

Запросы к API нужно делать с ключами, которые создаются для аккаунта.
Ключ нужно передавать в HTTP Basic auth в качестве имени пользователя, пароль при этом пустой.


## Рендеринг превью шаблонов

Для использования шаблонов рассылятора сторонними системами можно использовать вызов API,
который произведет рендеринг переданного шаблона с параметрами с использованием расширений
шаблонов Рассылятора

    POST /api/0/<account-slug>/render

Пример вызова:

    curl -X POST \
        -u 3579418885b9514a437570d420e46926: \
        -H 'content-type: application/json' \
        -d '{"template": "<template here>", "params":{"arg1": "val1", "arg2": "val2"}}' \
        'https://test.sender.yandex-team.ru/api/0/autoru/render'

Параметры:

* `template` - Jinja2 шаблон для рендеринга
* `params` - опциональные парамерты рендеринга. Параметры передаются в виде объекта json, в шаблоне
они доступны по именам полей объекта
* `strict` - опциональный флаг (`false` по-умолчанию). Этот флаг задает строгий режим рендеринга,
когда отсутствующие в контексте рендеринга переменные шаблона не подменяются
строками-пустышками - если из-за отсутствия какой-либо переменной в контексте возникнет ошибка, то она будет возвращена

Пример ответа:


    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "result":"<rendered template here>"
    }

Пример ответа (400), если возникла ошибка рендеринга:

    {
        "result": {
            "status": "ERROR",
            "error": {
                "detail": "Template improper use of UNDEFINED:\"'var' is undefined\""
            }
        }
    }


## Рендеринг превью письма

Для отображения шаблонов рассылятора в сторонних системах можно использовать вызов API,
который произведет рендеринг отправленного письма с параметрами. При этом рендеринг производится
с защитой от подсчета переходов по реальным ссылкам и влияния на подсчет открытий.

    POST /api/0/<account-slug>/render/campaign/<campaign_id>/letter/<letter_id>

Пример вызова:

    curl -X POST \
        -u 3579418885b9514a437570d420e46926: \
        -H 'content-type: application/json' \
        -d '{"params":{"arg1": "val1", "arg2": "val2"}}' \
        'https://test.sender.yandex-team.ru/api/0/autoru/render/campaign/1/letter/1'

Параметры:

* `params` - опциональные парамерты рендеринга. Параметры передаются в виде объекта json, в шаблоне
они доступны по именам полей объекта
* `strict` - опциональный флаг (`false` по-умолчанию). Этот флаг задает строгий режим рендеринга,
когда отсутствующие в контексте рендеринга переменные шаблона не подменяются
строками-пустышками - если из-за отсутствия какой-либо переменной в контексте возникнет ошибка, то она будет возвращена

Пример ответа:


    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "result": "<rendered template here>",
        "subject": "<rendered subject>",
        "from_name": "<letter.from_name>",
        "from_email": "<letter.from_email>"
    }

Пример ответа (400), если возникла ошибка рендеринга:

    {
        "result": {
            "status": "ERROR",
            "error": {
                "detail": "Template improper use of UNDEFINED:\"'var' is undefined\""
            }
        }
    }


## Автоматизация отправки промо-кампаний

### Создать промо кампанию и, если нужно, сразу же запланировать
```
POST /api/0/<account-slug>/automation/promoletter
```

Ручка позволяет настроить и запланировать промо-кампанию за один вызов, либо создать промо-кампанию, но не планировать ее сразу, а оставить для возможности редактирования/тестирования - запланировать кампанию можно будет позднее при помощи другой ручки

**ВНИМАНИЕ** Если в запросе указаны одновременно список рассылки и время желаемой отправки, то кампания будет создана и запланирована в отправку, если нужно только создать кампанию, но не нужно ее планировать сейчас, чтобы иметь возможность ее отредактировать, то можно явно указать поле `schedule_now: false` в теле запроса.

Список расылки можно задать двумя способами:
- таблица в YT
- передать список получателей в самом запросе


##### Параметры
###### Обязательные параметры
- `title` - название кампании
- `subject` - тема письма
- `from_addr` - email и отображаемое имя отправителя в форме объекта: `{"name": "Alice", "email": "alice@example.com"}`
- `letter_body` - содержание письма в виде текста с HTML разметкой
- `unsubscribe_list` - slug списка отписки, который нужно связать с рассылкой - на ящики из этого списка НЕ будут отправлены письма, а кликнувшие по Рассыляторской ссылке отписки из письма пользователи попадут в этот список

###### Опциональные параметры
- `segment` - правило (шаблон) по которому необходимо создать схему расчета списка рассылки, должен содержать JSON вида
    ```json
    {
      "template": "<template>",
      "params": {}
    }
    ````
    где `<template>` - это вид шаблона, а `params` содержит параметры для соответствующего шаблона.<br>
    Доступно два типа шаблонов:
    - `ytlist` - схема расчета на основе таблицы YT. Поле `path` в `params` содержит полный путь к таблице на кластере Hahn, например:
        ```json
        {
          "template": "ytlist",
          "params": {
            "path": "//path/to/my/table/at/hahn"
          }
        }
        ```
    - `singleuselist` - схема расчета на основе данных в самом запросе. Поле `recipients` в `params` содержит непустой список получаталей, например:
        ```json
        {
          "template": "singleuselist",
          "params": {
            "recipients": [
              {
                "email": "alice@example.com"
              },
              {
                "email": "david@example.com",
                "params": {
                  "var": "val"
                }
              }
            ]
          }
        }
        ```
      Каждый получатель - это объект с обязательным полем `email`. Опциональное поле `params` содержит переменные для рендеринга шаблона письма.

- `schedule_time` - дата и время отравки. Если задано, то кампания немедленно будет отправлена на планирование
- `schedule_now` - необязательный флаг, __предотвращающий старое поведение ручки__ - если явно указать `schedule_now = False`, то наличие в запросе поля `segment` и `schedule_time` НЕ запустит планирование кампании
- `reply_to` - email для ответов
- `tags` - список тегов кампании
- `utm` - параметры UTM разметки для ссылок внутри письма - они применяются к ссылкам внутри тегов `{% wrap %}...{% endwrap %}`
- `allowed_stat_domains` - домены, на которые разрешен редирект при учете статистики. Если ссылка на домен не была явно использована в тегах `{% wrap %}...{% endwrap %}` на момент загрузки, то необходимо указать
домен в этом параметре


Пример вызова:
```bash
curl -X POST \
-u 3579418885b9514a437570d420e46926: \
-H 'content-type: application/json' \
-d '{
"title": "Название кампании",
"subject": "Тема письма",
"from_addr": {
    "name": "Имя отправителя",
    "email": "test@example.com"
},
"reply_to": "reply@to.me",
"tags": ["tag1", "tag2"],
"utm":{
    "source": "utm_source",
    "medium": "utm_medium",
    "campaign": "utm_campaign",
    "content": "utm_content"
},
"letter_body": "Your letter here",
"allowed_stat_domains": ["unused.in.template.domain.com"],
"segment":{
    "template":"ytlist",
    "params":{
        "path": "//path/to/my/table/at/hahn"
    }
},
"unsubscribe_list": "CRPTD612-XHN1",
"schedule_time": "2018-01-01T00:00:01"
}' \
http://test.sender.yandex-team.ru/api/0/fan/automation/promoletter
```

Пример ответа:
```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "result":{
        "id": 1,
        "slug": "GUG2RFM2-MV51",
        "campaign_is_scheduled": true
    }
}
```

### Обновить данные кампании

`PATCH /api/0/<account-slug>/automation/promoletter/<campaign-slug>`

Позволяет обновить параметры промо кампании, созданной в ручке `POST /automation/promo`, если кампания находится в редактируемом состоянии и не была запланирована.

Параметры доутспные для обновление такие же как в ручке `POST /automation/promo`, но здесь они опциональные - параметры, указанные в запросе, будет использованы для обновления данных камапании. В отличие от ручки создание кампании, в этой ручке не происходит планирования кампании ни при каких условиях - это обычная ручка обновления данных.

Формат ответа такой же как в ручке просмотра кампании, например:
```json
{
   "result" : {
      "state" : "draft",
      "single_use_maillist" : false,
      "description" : "",
      "lists" : [],
      "type" : "simple",
      "sending_state_modified_at" : null,
      "submitted_by" : null,
      "ignore_unsubscribe" : false,
      "clone_of" : null,
      "account" : "Yandex.Mail",
      "event_hooks" : [],
      "ab_winner_code" : null,
      "scheduled_for" : "2019-12-31T21:00:00Z",
      "project" : null,
      "modified_at" : "2020-02-17T09:48:16.870Z",
      "sending_control" : null,
      "submitted_at" : null,
      "id" : "140",
      "scheduling_status" : null,
      "unsubscribe_redirect" : null,
      "tags" : [],
      "slug" : "CJY7E2J3-KC2",
      "moderation_state" : null,
      "deleted" : false,
      "sending_state" : null,
      "title" : "New title",
      "created_by" : "_robot",
      "created_at" : "2020-02-13T08:16:15.943Z",
      "valid_until" : null,
      "letters" : [
         {
            "code" : "A",
            "created_at" : "2020-02-13T08:16:15.956Z",
            "id" : "157"
         }
      ],
      "magic_list_id" : null
   }
}
```

#### Примеры запросов
##### Изменить название кампании и шаблон письма
```bash
curl -X PATCH \
    -u abc: \
    -H "content-type:application/json" \
    -d '{"title": "New title", "letter_body": "New letter body"}' \
    'http://localhost:8000/api/0/Yandex.Mail/automation/promoletter/CJY7E2J3-KC2'
```

##### Изменить список рассылки у кампании
```bash
curl -X PATCH \
    -u abc: \
    -H "content-type:application/json" \
    -d '{"segment": {"template": "singleuselist", "params": {"recipients": [{"email": "deavid@example.com"}]}}}' \
    'http://localhost:8000/api/0/Yandex.Mail/automation/promoletter/CJY7E2J3-KC2'
```

Чтобы сбросить/удалить utm или segment можно указать `null` в качестве значения, чтобы удалить теги можно указать пустой список в качестве значения.

### Отправить тестовые письма для кампани

`POST /api/0/<account-slug>/automation/promoletter/<campaign-slug>/test`

Отправит тестовые письма на указанные адреса

Параметры
 - `recipients` - непустой список получаталей тестовых писем вида
    ```json
    [
      {
        "email": "alice@example.com"
      },
      {
        "email": "david@example.com",
        "params": {
          "var": "val"
        }
      }
    ]
    ```
    Каждый получатель - это объект с обязательным полем email. Опциональное поле params содержит переменные для рендеринга шаблона письма.

Пример запроса:
```
curl -v -X POST \
    -u abc: \
    -H "content-type:application/json" \
    -d '{"recipients": [{"email": "alice@example.com", "params": {"var": "val"}}]}' \
    'http://localhost:8000/api/0/Yandex.Mail/automation/promoletter/CJY7E2J3-KC2/test'
```

Если все ок, вернет пустой ответ с кодом 200.


### Запланировать промо-кампанию

`POST /api/0/<account-slug>/automation/promoletter/<campaign-slug>/schedule`

Перевести кампанию в состояние отправки и запланировать.

Параметры:
- `schedule_time` - желаемое время отправки кампании. Специальное значение `now` запланирует рассылку на ближайшее время. Этот параметр не обязателен, если в ручке создания или обновления кампании время отправки уже было установлено. Если параметр указан, то именно его значение будет использовано для планирования, независимо от значения, установленного на кампании ранее.

Формат ответа: идентификаторы кампании и время, использованное для планирования кампании, например
```json
{"result":{"schedule_time":"2020-01-01T00:00:00Z","id":140,"slug":"CJY7E2J3-KC2"}}
```

#### Примеры запросов

##### Запланировать кампанию, если у нее уже установлена дата отправки
```bash
curl -v -X POST \
    -u ce3ee6e2bdf3484f9b02b080694af289: \
    -H "content-type:application/json" \
    'http://localhost:8000/api/0/Yandex.Mail/automation/promoletter/CJY7E2J3-KC2/schedule'
```

##### Запланировать кампанию явно указав время отправки
```bash
curl -v -X POST \
    -u ce3ee6e2bdf3484f9b02b080694af289: \
    -H "content-type:application/json" \
    -d '{"schedule_time": "2020-01-01T00:00:00+00:00"}' \
    'http://localhost:8000/api/0/Yandex.Mail/automation/promoletter/CJY7E2J3-KC2/schedule'
```

##### Запланировать кампанию на ближайшее время
```bash
curl -v -X POST \
    -u ce3ee6e2bdf3484f9b02b080694af289: \
    -H "content-type:application/json" \
    -d '{"schedule_time": "now"}' \
    'http://localhost:8000/api/0/Yandex.Mail/automation/promoletter/CJY7E2J3-KC2/schedule'
```

## Автоматизация отправки транзакционных кампаний

Тразнакционная кампания с настроенным письмом и автоматической активацией может быть создана следующим вызовом

    POST /api/0/<account-slug>/automation/newtransact

Пример вызова:

    curl -X POST \
      -u 3579418885b9514a437570d420e46926: \
      -H 'content-type: application/json' \
      -d '{
        "title": "Название кампании",
        "subject": "Тема письма",
        "from_addr": {
            "name": "Имя отправителя",
            "email": "test@example.com"
        },
        "reply_to": "reply@to.me",
        "tags": ["tag1", "tag2"],
        "utm":{
            "source": "utm_source",
            "medium": "utm_medium",
            "campaign": "utm_campaign",
            "content": "utm_content"
        },
        "letter_body": "Your letter here",
        "allowed_stat_domains": ['unused.in.template.domain.com'],
        "unsubscribe_list": "CRPTD612-XHN1"
      }' \
      http://test.sender.yandex-team.ru/api/0/fan/automation/newtransact

Параметры:

* title - название кампании, обязательный параметр
* subject - тема письма, обязательный параметр
* from_addr - email и отображаемое имя отправителя, обязательный параметр
* reply_to - email для ответов, опционально
* tags - список тегов кампании, опционально
* utm - разметка ссылок камании. Если указаны значения, то применяются к ссылкам внутри тегов {%wrap%}...{%endwrap%}
* letter_body - текст HTML тела письма, обязательный параметр
* allowed_stat_domains - домены, на которые разрешен редирект при учете статистики.
Если ссылка на домен не быля явно использована в тегах {%wrap%}...{%endwrap%} на момент загрузки, то необходимо указать
домен в этом параметре
* unsubscribe_list - slug списка отписки, обязательный параметр

Пример ответа:


    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "result":{
            "id": 1,
            "slug": "GUG2RFM2-MV51"
        }
    }


## Создание новой ревизии транзакционной кампании

Для существующей транзакционной кампании можно создать новую версию письма

    POST POST /api/0/<account-slug>/automation/transactrevision/<campaign_slug>

Пример вызова:

    curl -X POST \
      -u 3579418885b9514a437570d420e46926: \
      -H 'content-type: application/json' \
      -d '{
        "subject": "Тема письма",
        "from_addr": {
            "name": "Имя отправителя",
            "email": "test@example.com"
        },
        "reply_to": "reply@to.me",
        "tags": ["tag1", "tag2"],
        "utm":{
            "source": "utm_source",
            "medium": "utm_medium",
            "campaign": "utm_campaign",
            "content": "utm_content"
        },
        "letter_body": "Your letter here",
        "allowed_stat_domains": ['unused.in.template.domain.com'],
      }' \
      http://test.sender.yandex-team.ru/api/0/fan/automation/newtransact

Параметры:

* subject - тема письма, обязательный параметр
* from_addr - email и отображаемое имя отправителя, обязательный параметр
* reply_to - email для ответов, опционально
* tags - список тегов кампании, опционально
* utm - разметка ссылок камании. Если указаны значения, то применяются к ссылкам внутри тегов {%wrap%}...{%endwrap%}
* letter_body - текст HTML тела письма, обязательный параметр
* allowed_stat_domains - домены, на которые разрешен редирект при учете статистики.
Если ссылка на домен не быля явно использована в тегах {%wrap%}...{%endwrap%} на момент загрузки, то необходимо указать
домен в этом параметре

Пример ответа:


    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "result":{
            "code": "B"
        }
    }

