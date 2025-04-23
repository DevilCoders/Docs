# API создания промо-кампании

## Авторизация

Запросы к API нужно делать с ключами, которые создаются для аккаунта.
Ключ нужно передавать в HTTP Basic auth в качестве имени пользователя, пароль при этом пустой.

## Создание кампании

С помощью API возможно создать черновик промо-кампании с заданным именем

    POST /api/0/<account-slug>/campaign

Параметры:
    * title - название кампании, отображаемое в интерфейсе (обязательный параметр)

Пример вызова:

    curl -X POST \
      -u 3579418885b9514a437570d420e46926: \
      -H "Content-Type: application/json" -d '{"title": "TestApi"}'\
      'http://test.sender.yandex-team.ru/api/0/Yandex.Mail/campaign/'

Пример ответа:

    {
        "result": {
            "letters": [
                {
                    "created_at": "2017-10-19T10:57:45.389Z",
                    "code": "A",
                    "id": "4947"
                }
            ],
            "clone_of": null,
            "scheduled_for": null,
            "sending_state_modified_at": null,
            "ignore_unsubscribe": false,
            "unsubscribe_redirect": null,
            "id": "3736",
            "submitted_by": null,
            "title": "TestApi",
            "created_by": null,
            "state": "draft",
            "type": "simple",
            "valid_until": null,
            "description": "",
            "deleted": false,
            "ab_winner_code": null,
            "lists": [],
            "sending_state": null,
            "sending_control": null,
            "account": "fan",
            "magic_list_id": null,
            "slug": "0Q41AGL2-SHS1",
            "moderation_state": null,
            "submitted_at": null,
            "created_at": "2017-10-19T10:57:45.335Z",
            "modified_at": "2017-10-19T10:57:45.335Z",
            "project": null,
            "event_hooks": [],
            "single_use_maillist": false
        }
    }

## Информация о кампании

    GET /api/0/<account-slug>/campaign/<campaign-slug>/

Пример вызова

    curl -X GET \
        -u 3579418885b9514a437570d420e46926: \
        'https://test.sender.yandex-team.ru/api/0/Yandex.Mail/campaign/0Q41AGL2-SHS1/'

Пример ответа

    {
        "result": {
            "letters": [
                {
                    "created_at": "2017-10-19T10:57:45.389Z",
                    "code": "A",
                    "id": "4947"
                }
            ],
            "clone_of": null,
            "scheduled_for": null,
            "sending_state_modified_at": null,
            "ignore_unsubscribe": false,
            "unsubscribe_redirect": null,
            "id": "3736",
            "submitted_by": null,
            "title": "TestApi",
            "created_by": null,
            "state": "draft",
            "type": "simple",
            "valid_until": null,
            "description": "",
            "deleted": false,
            "ab_winner_code": null,
            "lists": [],
            "sending_state": null,
            "sending_control": null,
            "account": "fan",
            "magic_list_id": null,
            "slug": "0Q41AGL2-SHS1",
            "moderation_state": null,
            "submitted_at": null,
            "created_at": "2017-10-19T10:57:45.335Z",
            "modified_at": "2017-10-19T10:57:45.335Z",
            "project": null,
            "event_hooks": [],
            "single_use_maillist": false
        }
    }

## Добавление одноразового списка адресатов

С помощью API можно задать спискок адресатов кампании (аналогично одноразовому списку, загружаемому из файла)

    POST /api/0/<account-slug>/campaign/<campaign-slug>/recipients

Принимаются только значения json

Параметры:
    * в теле запроса передается массив обектов json со следующими атрибутами:
        * email - адрес получателя (обязательный параметр)
        * params - json объект с дополнительными параметрами для отправки письма (необязательный параметр)

Пример запроса:

    curl -X POST \
      -u 3579418885b9514a437570d420e46926: \
      -H "Content-Type: application/json" -d '[{"email": "test@example.com", "params": {"name": "drew", "foo": {"test": "bar"}}}]'\
      'http://test.sender.yandex-team.ru/api/0/Yandex.Mail/campaign/0Q41AGL2-SHS1/recipients'

Пример ответа:

    {
        "result": {
            "recipients_count": 1,
            "errors_count": 0
        }
    }