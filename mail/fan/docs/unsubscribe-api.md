# API для управления списком отписки

## Авторизация

Запросы к API нужно делать с ключами, которые создаются для аккаунта.
Ключ нужно передавать в HTTP Basic auth в качестве имени пользователя, пароль при этом пустой.


## Получить информацию об отписках получателя в аккаунте

Получить список возможных списков отписки и группы отписки для данного аккаунта, и статус получателя в них.

    GET /api/0/<account-slug>/unsubscribe/info?email=<email>

Пример вызова:

    curl -X GET \
        -u 3579418885b9514a437570d420e46926: \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/info?email=<email>'

Параметры:

* email - email подписчика

Пример ответа:

* group – Информация по отписке от группы, в которую входит аккаунт
* lists - Информация по спискам отписки

Параметры ответа:

    {
      "params": {
        "email": "test@test.ru"
      },
      "result": {
        "group": {
          "unsubscribed": true,
          "slug": "47ESZE62-P94",
          "id": "1",
          "name": "\u042f\u043d\u0434\u0435\u043a\u0441"
        },
        "lists": [
          {
            "list": {
              "account": "baz",
              "description": null,
              "id": "2",
              "name": {"ru":"9PCO6JV3KJDSQHSL", "en": "asdasdsd"},
              "slug": "uh4xaxzzkj6qkt7q"
            },
            "unsubscribed": true
          },
          {
            "list": {
              "account": "baz",
              "description": {"ru":"9PCO6JV3KJDSQHSL"},
              "id": "3",
              "name": {"ru":"9PCO6JV3KJDSQHSL"},
              "slug": "vo01lt4atbvoy2bo"
            },
            "unsubscribed": false
          }
        ]
      }}

## Добавить в список отписки

    PUT /api/0/<account-slug>/unsubscribe/list/<unsubscribe-list-slug>?email=<email>

Пример вызова:

    curl -X PUT \
        -u 3579418885b9514a437570d420e46926: \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/list/CRPTD612-XHN1?email=<email>'


Параметры:

* email - email подписчика

Пример ответа:

    {
      "params": {
        "email": "test@test.ru"
      },
      "result": {
        "status": "ok"
      }
    }

## Удалить из списка отписки

    DELETE /api/0/<account-slug>/unsubscribe/list/<unsubscribe-list-slug>?email=<email>

Пример вызова:

    curl -X PUT \
        -u 3579418885b9514a437570d420e46926: \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/list/CRPTD612-XHN1?email=<email>'


Параметры:

* email - email подписчика

Пример ответа:

    {
      "params": {
        "email": "test@test.ru"
      },
      "result": {
        "status": "ok"
      }
    }

## Получить содержимое списка отписки

    GET /api/0/<account-slug>/unsubscribe/list/<unsubscribe-list-slug>/content?after=<YYYY-MM-DDThh:mm[:ss[.uuuuuu]][+HH:MM|-HH:MM|Z]>&offset=<n>&limit=<n>


Пример вызова:

    curl -X GET \
        -u 3579418885b9514a437570d420e46926: \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/list/CRPTD612-XHN1/content?after=2016-01-01T00:00:00&offset=1&limit=1'


Параметры:

* after - возвращать отписки после указанной даты (*необязательный параметр*)
* offset - пропустить указанное количество записей (*необязательный параметр, по умолчанию 0*)
* limit - вернуть не больше указанного количества записей (*необязательный параметр, по умолчанию 1000*)


Пример ответа:

    {
        "count": 11,
        "previous": "https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/list/CRPTD612-XHN1/content?after=2016-01-01T00%3A00%3A00&limit=1",
        "params": {
            "after": "2016-01-01T00:00:00+03:00",
            "limit": 1,
            "offset": 1
        },
        "result": [
            {
                "email": "test_1@example.com"
            }
        ],
        "next": "https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/list/CRPTD612-XHN1/content?after=2016-01-01T00%3A00%3A00&limit=1&offset=2"
    }

# Глобальная отписка (отписка от группы аккаунтов)

Аккаунт может находиться в одной группе отписок. Например:

#### Яндекс:
* Почта
* Диск
* Музыка
...

#### Авто.Ру:
* Авто.Ру


Аккаунты попадают в группы по следующему принципу: если проект находится под брендом Яндекса, то аккаунт этого проекта
будет в группе Яндекса, если у проекта свой бренд, то для него делаем отдельную группу.

Если пользователь отписывается от группы, то он больше не получает рассылку от всех аккаунтов этой группы.

## Получить информацию о глобальной отписке

    GET /api/0/<account-slug>/unsubscribe/global?email=<email>

Пример вызова:

    curl -X GET \
        -u 3579418885b9514a437570d420e46926: \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/global?email=<email>'


Параметры:

* email - email подписчика

Пример ответа:

    {
      "params": {
        "email": "test@test.ru"
      },
      "result": {
        "unsubscribed": true,
        "slug": "test",
        "id": "1",
        "name": "Test"
      }
    }


## Добавить в глобальный список группы

    PUT /api/0/<account-slug>/unsubscribe/global?email=<email>

Пример вызова:

    curl -X PUT \
        -u 3579418885b9514a437570d420e46926: \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/global?email=<email>'


Параметры:

* email - email подписчика

Пример ответа:

    {
      "params": {
        "email": "test@test.ru"
      },
      "result": {
        "status": "ok"
      }
    }

## Удалить из глобального списка группы

    DELETE /api/0/<account-slug>/unsubscribe/global?email=<email>

Пример вызова:

    curl -X DELETE \
        -u 3579418885b9514a437570d420e46926: \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/global?email=<email>'


Параметры:

* email - email подписчика

Пример ответа:

    {
      "params": {
        "email": "test@test.ru"
      },
      "result": {
        "status": "ok"
      }
    }


## Получить содержимое глобального списка группы

    GET /api/0/<account-slug>/unsubscribe/global/content?after=<YYYY-MM-DDThh:mm[:ss[.uuuuuu]][+HH:MM|-HH:MM|Z]>&offset=<n>&limit=<n>


Пример вызова:

    curl -X GET \
        -u 3579418885b9514a437570d420e46926: \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/global/content?after=2016-01-01T00:00:00&offset=1&limit=1'


Параметры:

* after - возвращать отписки после указанной даты (*необязательный параметр*)
* offset - пропустить указанное количество записей (*необязательный параметр, по умолчанию 0*)
* limit - вернуть не больше указанного количества записей (*необязательный параметр, по умолчанию 1000*)


Пример ответа:

    {
        "count": 11,
        "previous": "https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/global/content?after=2016-01-01T00%3A00%3A00&limit=1",
        "params": {
            "after": "2016-01-01T00:00:00+03:00",
            "limit": 1,
            "offset": 1
        },
        "result": [
            {
                "email": "test_1@example.com"
            }
        ],
        "next": "https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/global/content?after=2016-01-01T00%3A00%3A00&limit=1&offset=2"
    }


## Проверить наличие email'а в списке отписок

    GET /api/0/<account-slug>/unsubscribe/list/<list_slug>/email/<>email

Пример вызова:

    curl -X GET \
        -u 9d11bae2478644838214865818873387: \
        'https://test.sender.yandex-team.ru/api/0/dev/unsubscribe/list/8QJFEBT3-8OR1/email/test@test.ru'

Пример ответа:

    HTTP_200 {"result":{"email":"test@test.ru"}}
    HTTP_404 {"detail":"Email is not in unsublist."}