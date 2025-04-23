# API для редактирования списка рассылки


## Авторизация

Запросы к API нужно делать с ключами, которые создаются для аккаунта.
Ключ нужно передавать в HTTP Basic auth в качестве имени пользователя, пароль при этом пустой.


## Добавить получателя в список

    PUT /api/0/<account-slug>/maillist/<maillist-slug>/subscription

Пример вызова:

    curl -X PUT \
        -u 3579418885b9514a437570d420e46926: \
        -d params='{"name":"Test Test","var1":"value1"}' \
        -d email="test@test.ru" \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/maillist/SBPYSTY1-ALV/subscription'

Параметры:

* email - email подписчика
* params - дополнительные параметры подписчика в формате JSON

Пример ответа:

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "params": {
            "email":"test@test.ru",
            "params":"{\"var1\": \"value1\"}"
        },
        "result": {
            "status":"OK"
        }
    }


## Double Opt-In

Для того, чтобы вы могли подписывать по схеме double opt-in, необходимо:

* Создать транзакционное письмо, которое будет отправлятся для подтверждения.
* Указать в шаблоне ссылку на подтверждение подписки. В это письмо будет автоматически подставлен url подтверждения подписки (`{{ subscribe_link }}`).
* В настройках Аккаунта, либо конкретного списка, выбрать данное письмо.

При вызове метода API: подписчик добавляется в список, как неактивный подписчик, и, если он еще не был подписан, отправляется транзакционное письмо.

    POST /api/0/<account-slug>/maillist/<maillist-slug>/subscription/request

Пример:

    curl -X POST \
        -u 3579418885b9514a437570d420e46926: \
        -d to_email="test@test.ru" \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/maillist/SBPYSTY1-ALV/subscription/request'

Параметры:

* to_email - email подписчика
* params - дополнительные параметры подписчика в формате JSON (например name)
* args - json с переменными, которые будут подставлены в тело письма
* async - отправить письмо сразу (синхронно, без очереди) или положить в очередь
* countdown - для асинхронной отправки - отправить рассылку не сразу, а через countdown секунд. можно задавать в виде целого числа или в виде "12h13m11s"
* expires - для асинхронной отправки - не отправлять через expires секунд. через какое время уже не нужно отправлять письмо. формат параметра такой же, как countdown.


Пример ответа:

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "params": {
            "email":"test@test.ru",
            "params":"{\"var1\": \"value1\"}"
        },
        "result": {
            "status":"OK"
        }
    }


## Удаление из списка

    DELETE /api/0/<account-slug>/maillist/<maillist-slug>/subscription

Пример вызова:

    curl -X DELETE \
        -u 3579418885b9514a437570d420e46926: \
        -d email="test@test.ru" \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/maillist/SBPYSTY1-ALV/subscription'

Параметры:

* email - email подписчика

Пример ответа:

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "params": {
            "email":"test@test.ru"
        },
        "result": {
            "status":"OK",
            "disabled":1,
            "already_disabled":0
        }
    }


## Добавить список получателей

Ассинхронная ручка добавления большого количества подписчиков в список.
**Количество элементов списка ограниченно, за один запрос можно добавить 1000 элеметов.**

    PUT /api/0/<account-slug>/maillist/<maillist-slug>/subscription/bulk

Пример вызова:

    curl -X PUT \
        -u 3579418885b9514a437570d420e46926: \
        -H "Content-Type: application/json" -d {"items":[{"email":"b@as.ru"}, {"email":"ba@as.ru"}]} \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/maillist/SBPYSTY1-ALV/subscription/bulk'

Параметры:

* items - JSON со списком получателей:
    * email - email подписчика
    * params - дополнительные параметры подписчика в формате JSON
* rev - номер версии списка, к которой добавить подписчиков (по умолчанию генерируется новая версия)
* disable_others - отписывать подписчиков предыдущих версий (по умолчанию не отписываем)

Пример ответа:

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "result": {
            "status":"OK",
            "task_id": "d56c72dd-ff71-4aba-8363-160e5de8c3b3",
            "rev": 123923123123
        }
    }


## Удалить список получателей

Ассинхронная ручка удаления из списка большого количества подписчиков.
**Количество элементов списка ограниченно, за один запрос можно добавить 1000 элеметов.**

    DELETE /api/0/<account-slug>/maillist/<maillist-slug>/subscription/bulk

Пример вызова:

    curl -X DELETE \
        -u 3579418885b9514a437570d420e46926: \
        -H "Content-Type: application/json" -d '[{"email":"b@as.ru"}, {"email":"ba@as.ru"}]' \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/maillist/SBPYSTY1-ALV/subscription/bulk'

Параметры:

* items - JSON со списком получателей:
    * email - email подписчика

Пример ответа:

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "result": {
            "status":"OK",
            "task_id": "d56c72dd-ff71-4aba-8363-160e5de8c3b3"
        }
    }

## Получить содержимое списка получателей

    GET /api/0/<account-slug>/maillist/<maillist-slug>/content?after=<YYYY-MM-DDThh:mm[:ss[.uuuuuu]][+HH:MM|-HH:MM|Z]>&offset=<n>&limit=<n>


Пример вызова:

    curl -X GET \
        -u 3579418885b9514a437570d420e46926: \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/maillist/SBPYSTY1-ALV/content?after=2016-01-01T00:00:00&offset=1&limit=1'


Параметры:

* after - возвращать отписки после указанной даты (*необязательный параметр*)
* offset - пропустить указанное количество записей (*необязательный параметр, по умолчанию 0*)
* limit - вернуть не больше указанного количества записей (*необязательный параметр, по умолчанию 1000*)


Пример ответа:

    {
        "count": 11,
        "previous": "https://test.sender.yandex-team.ru/api/0/Yandex.Mail/maillist/SBPYSTY1-ALV/content?after=2016-01-01T00%3A00%3A00&limit=1",
        "params": {
            "after": "2016-01-01T00:00:00+03:00",
            "limit": 1,
            "offset": 1
        },
        "result": [
            "_created_at": "2017-03-27T14:25:56.014Z",
            "_modified_at": "2017-03-27T14:28:27.540Z",
            "name": "test_1",
            "_enabled": true,
            "_status": "",
            "email": "test_1@example.com"
        ],
        "next": "https://test.sender.yandex-team.ru/api/0/Yandex.Mail/unsubscribe/list/CRPTD612-XHN1/content?after=2016-01-01T00%3A00%3A00&limit=1&offset=2"
    }

## Получить элемент списка получателей по email, если список существует и email в него входит

Другими словами - проверить, что email принадлежит списку получателей.
Формат результата запроса соответствует формату одного элемента из точки "содержимое списка получателей".
Если email не принадлежит списку получателей, или указанного списка нет - будет ошибка 404.

    GET /api/0/<account-slug>/maillist/<maillist-slug>/email/<email>

Пример вызова:

    curl -X GET \
        -u 3579418885b9514a437570d420e46926: \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/maillist/SBPYSTY1-ALV/email/guido@eggs.ni'

Пример положительного ответа:

    {
        "result": {
            "_created_at": "2017-03-27T14:25:56.014Z",
            "_modified_at": "2017-03-27T14:28:27.540Z",
            "name": "Guido",
            "_enabled": true,
            "_status": "",
            "email": "guido@eggs.ni"
        }
    }

Ответ (404), если email нет в списке

    {
        "result": {
            "status": "ERROR",
            "error": {"detail": "Email is not in maillist."}
        }
    }

Ответ (400), если email невалидный:

    {
        "result": {
            "status": "ERROR",
            "error": {"detail": "Wrong email format"}
        }
    }
