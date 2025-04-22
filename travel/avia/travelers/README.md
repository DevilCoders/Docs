# Записная книжка путешественника

## rest-api

- unstable: https://travelers.unstable.avia.yandex.net
- testing: https://travelers.testing.avia.yandex.net
- production: https://avia-travelers.common.yandex.net

TVM:
- unstable, testing: 2001628 (avia-traveler-testing)
- production: 2001630 (avia-traveler-production)

Обязательные заголовки:
- `X-Ya-Service-Ticket`
- `X-Ya-User-Ticket`

### Путешественник

#### Структура

```json
{
    "agree": {
        "type": "boolean"
    },
    "phone": {
        "type": "string"
    },
    "phone_additional": {
        "type": "string"
    },
    "email": {
        "type": "string"
    },
    "created_at": {
        "type": "string"
    },
    "updated_at": {
        "type": "string"
    }
}
```

#### Методы

Создание/редактирование данных:

```
POST /v1/travelers/<uid>
{
  "email": "user@yandex-team.ru",
  "phone": "+71117654321",
  "phone_additional": null,
  "agree": true
}

```

Получение данных:

```GET /v1/travelers/<uid>?fields=passengers,documents,bonus-cards```

### Пассажиры

#### Структура

```json
{
    "id": {
        "type": "string"
    },
    "title": {
        "type": "string"
    },
    "gender": {
        "type": "string"
    },
    "birth_date": {
        "type": "string"
    },
    "itn": {
        "type": "string"
    },
    "phone": {
        "type": "string"
    },
    "phone_additional": {
        "type": "string"
    },
    "email": {
        "type": "string"
    },
    "attributes": {
        "type": "array",
        "items": [
            {
                "type": "string"
            }
        ],
        "uniqueItems": true
    },
    "created_at": {
        "type": "string"
    },
    "updated_at": {
        "type": "string"
    }
}
```

#### Методы

Создание:

```
POST /v1/travelers/<uid>/passengers
{
  "title": "Коллега",
  "gender": "male",
  "birth_date": "1921-12-28",
  "phone": null,
  "phone_additional": null,
  "email": null,
  "itn": null,
  "train_notifications_enabled": false
}
```

Редактирование:

```
PUT /v1/travelers/<uid>/passengers/<passenger_id>
{
  "title": "Коллега",
  "gender": "male",
  "birth_date": "1921-12-28",
  "phone": null,
  "phone_additional": null,
  "email": null,
  "itn": null,
  "train_notifications_enabled": false
}
```

Получение всех пассажиров путешественника:

```
GET /v1/travelers/<uid>/passengers
```

Получение конкретного пассажира:

```
GET /v1/travelers/<uid>/passengers/<passenger_id>
```

Удаление пассажира:

```
DELETE /v1/travelers/<uid>/passengers/<passenger_id>
```

### Документы

#### Структура

```json
{
    "id": {
        "type": "string"
    },
    "passenger_id": {
        "type": "string"
    },
    "type": {
        "type": "string"
    },
    "title": {
        "type": "string"
    },
    "number": {
        "type": "string"
    },
    "first_name": {
        "type": "string"
    },
    "middle_name": {
        "type": "string"
    },
    "last_name": {
        "type": "string"
    },
    "first_name_en": {
        "type": "string"
    },
    "middle_name_en": {
        "type": "string"
    },
    "last_name_en": {
        "type": "string"
    },
    "issue_date": {
        "type": "string"
    },
    "expiration_date": {
        "type": "string"
    },
    "citizenship": {
        "type": "string"
    },
    "created_at": {
        "type": "string"
    },
    "updated_at": {
        "type": "string"
    }
}
```

#### Методы

Создание:

```
POST /v1/travelers/<uid>/passengers/<passenger_id>/documents
{
  "title": "Мой паспорт РФ",
  "type": "ru_national_passport",
  "first_name": "Иван",
  "middle_name": "Иванович",
  "last_name": "Иванов"
}
```

Редактирование:

```
PUT /v1/travelers/<uid>/passengers/<passenger_id>/documents/<document_id>
{
  "title": "Мой паспорт РФ",
  "type": "ru_national_passport",
  "first_name": "Иван",
  "middle_name": "Иванович",
  "last_name": "Иванов"
}
```

Получение списка всех документов пассажира:

```
GET /v1/travelers/<uid>/passengers/<passenger_id>/documents
```

Получение конкретного документа:

```
GET /v1/travelers/<uid>/passengers/<passenger_id>/documents/<document_id>
```

Удаление документа документа:

```
DELETE /v1/travelers/<uid>/passengers/<passenger_id>/documents/<document_id>
```

### Типы документов

#### Методы

Получение списка типов документов

```
GET /v1/document_types
```

Ответ:

```json
{
  "ru_seaman_passport": {
    "unused": [
      "expiration_date",
      "citizenship",
      "first_name_en",
      "middle_name_en",
      "last_name_en"
    ],
    "required": [
      "number",
      "issue_date",
      "first_name",
      "last_name"
    ],
    "re_validations": {
      "first_name": "^[а-яА-Я ']+$",
      "last_name": "^[а-яА-Я ']+$",
      "middle_name": "^[а-яА-Я ']+$",
      "number": "[а-яА-Я]{2}\\d{7}"
    }
  },
  ...
}

```

### Карты лояльности

#### Структура

```json
{
    "id": {
        "type": "string"
    },
    "passenger_id": {
        "type": "string"
    },
    "type": {
        "type": "string"
    },
    "title": {
        "type": "string"
    },
    "number": {
        "type": "string"
    },
    "created_at": {
        "type": "string"
    },
    "updated_at": {
        "type": "string"
    }
}
```

#### Методы

Создание:

```
POST /v1/travelers/<uid>/passengers/<passenger_id>/bonus-cards
{
  "title": "card_title",
  "type": "card_type",
  "number": "card_number"
}
```

Редактирование:

```
PUT /v1/travelers/<uid>/passengers/<passenger_id>/bonus-cards/<bonus_card_id>
{
  "title": "Card title",
  "type": "Card type",
  "number": "Card number"
}
```

Получение списка всех карт лояльности пассажира:

```
GET /v1/travelers/<uid>/passengers/<passenger_id>/bonus-cards
```

Получение конкретной карты лояльности:

```
GET /v1/travelers/<uid>/passengers/<passenger_id>/bonus-cards/<bonus_card_id>
```

Удаление карты лояльности:

```
DELETE /v1/travelers/<uid>/passengers/<passenger_id>/bonus-cards/<bonus_card_id>
```

### Объединение пассажиров
Удаляет всех пассажиров с идентификаторами из списка `passengers`,
переносит все их документы и бонусные карты пассажиру с идентификатором `passenger_id` и
обновляет у него поля, переданные в запросе.
#### Формат запроса
```
POST /v1/travelers/<uid>/passengers/<passenger_id>/combine
{
  "passengers": [<id1>, <id2>, ...],
  "title": "Коллега",
  "gender": "male",
  "birth_date": "1921-12-28",
  "phone": null,
  "phone_additional": null,
  "email": null
}
```
#### Формат ответа
```json
{
  "id": "...",
  "title": "Коллега",
  "gender": "male",
  "birth_date": "1921-12-28",
  "phone": null,
  "phone_additional": null,
  "email": null
}
```

## Разразботка

```
$ ./tools/create-env.sh
$ cp ./tools/samples/environments.sh ./tools/.
$ vi ./tools/environment.sh
$ ./tools/run-dev.sh
```

### Запуск тестов

```
bash tools/run-tests.sh
```

### Отправка запросов

1. Прописать в `environment.sh` переменные `AVIA_TRAVELERS_TVM_SERVICE_ID` и `AVIA_TRAVELERS_TVM_SECRET`.
1. Зарегистрироваться в тестовом паспорте: https://passport-test.yandex.ru.
1. После авторизации в тестовом паспорте запомнить значение куки `Session_id`.

Пример скрипта создания путешественника:

```python
import requests
from lxml import etree

from travel.library.python.tvm_ticket_provider import provider_fabric

sessionid = '...'
userip = '...'
host = 'passport-test.yandex.ru'

tvm_provider = provider_fabric.create(
    source_id=2000573,  # Тестовый фронт
    secret='...',  # Секрет тестового фронта
    destinations=[2001628],
    renew=True,
)
travelers_service_ticket = tvm_provider.get_ticket(2001628)

passport_tvm_provider = provider_fabric.create(
    source_id=2000573,  # Тестовый фронт
    secret='...',  # Секрет тестового фронта
    destinations=[224],  # Тестовый паспорт
    renew=True,
)

response = requests.get(
    'http://pass-test.yandex.ru/blackbox',
    headers={
        'X-Ya-Service-Ticket': passport_tvm_provider.get_ticket(224),
    },
    params={
        'method': 'sessionid',
        'sessionid': sessionid,
        'userip': userip,
        'host': host,
        'get_user_ticket': 'yes',
    },
)

response.raise_for_status()
xml = etree.fromstring(response.content)
error = xml.find('error')

if error.text != 'OK':
    raise RuntimeError(error.text)

uid = xml.find('uid').text
user_ticket = xml.find('user_ticket').text

response = requests.post(
    'http://avia-travelers.LOGIN.avia.dev.yandex.net/travelers/{uid}'.format(uid=uid),
    headers={
        'X-Ya-User-Ticket': user_ticket,
        'X-Ya-Service-Ticket': travelers_service_ticket,
    },
    json={
        'agree': True,
        'phone': '...',
        'phone_additional': None,
        'email': '...@yandex-team.ru',
    },
)
response.raise_for_status()
```

#### Отправка запросов из консоли

Для отправки запросов из консоли необходимы:
- tvm-секрет от avia-frontend (можно получить у разработчика)
- Кука "Session_id" пользователя (можно посмотреть в куках после авторизации на https://travel-test.yandex.ru)
- ip пользователя (Нужен ipv6 адрес со страницы https://yandex.ru/internet/)

```
$ /app/test_request -h
```

Примеры запросов:

Получение путешественника:

```
$ /app/test_request --avia_frontend_tvm_secret "..." --userip "2a02:6b8:0:2807:a116:e970:4315:5031" --sessionid "..." | json_pp
```

Получение пассажиров:

```
$ /app/test_request --avia_frontend_tvm_secret "..." --userip "2a02:6b8:0:2807:a116:e970:4315:5031" --sessionid "..." --api_path "/travelers/{uid}/passengers" | json_pp
```

Создание пассажира:

```
$ /app/test_request --avia_frontend_tvm_secret "..." --userip "2a02:6b8:0:2807:a116:e970:4315:5031" --sessionid "..." --api_path "/travelers/{uid}/passengers" --method POST --data '{"birth_date":"1900-01-01","gender":"male","title":"test"}'
```
