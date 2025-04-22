# Quick start

**Тестовый стенд:**
https://ow.tst.market.yandex-team.ru

**Продакшен:**
https://ow.market.yandex-team.ru

## Аутентификация

Единое окно поддерживает basic и TVM аутентификацию для АПИ.

### Basic-аутентификация



### TVM-аутентификация

У всех сотрудников (employee) есть атрибут "TVM application" (tvmApplication). Для подключения TVM-аутентификации
необходимо пользователю прописать tvm-id сервиса, который будет использовать в АПИ. Предполагается, что
"TVM application" будет заполняться у роботных пользователей импортированных со стафа.

TVM-id Единого окна
Среда | TVM-id
:--- | :---:
Production | 2000202
Testing | 2000179

Получение tvm-тикета
```shell
# Получаем ключ: -s - сервис источник, -d - сервис назначения
# Может потребоваться abc-роль "TVM ssh пользователь"
tvmknife get_service_ticket sshkey -s 2000611 -d 2000179
```


## Создание объекта

Для создания произвольного объекта предназначен метод АПИ ```api/basic/entity/${fqn}``` (POST) и
```api/tvm2/entity/${fqn}``` (POST),
где fqn - идентификатор метакласса создаваемого объекта. В теле запроса передается ассоциативный список значений
атрибутов создаваемого объекта.

Пример:

```shell
# Basic-authentication
$ curl -i -k -u triggers_platform:**** -H 'Content-Type: application/json' \
    -d '{"@comment": {"metaclass": "comment$internal", "body": "Описание тикета"}, "brand": "beru", "categories": "beruTestBeruCategory", "channel": "mail", "clientEmail": "test@test.ru", "clientPhone": "+79123456789", "order": 2842648, "service": "beruTransferInfo", "title": "Название тикета"}' \
    -X POST 'https://ow.tst.market.yandex-team.ru/api/basic/entity/ticket$beruOutgoing'

# TVM-authentication
$ curl -i -k -H "X-Ya-Service-Ticket: ****" -H 'Content-Type: application/json' \
    -d '{"@comment": {"metaclass": "comment$internal", "body": "Описание тикета"}, "brand": "beru", "categories": "beruTestBeruCategory", "channel": "mail", "clientEmail": "test@test.ru", "clientPhone": "+79123456789", "order": 2842648, "service": "beruTransferInfo", "title": "Название тикета"}' \
    -X POST 'https://ow.tst.market.yandex-team.ru/api/tvm2/entity/ticket$beruOutgoing'

```

Тело запроса:
```json
{
  "@comment": {
    "metaclass": "comment$internal",
    "body": "Описание тикета"
  },
  "brand": "beru",
  "categories": "",
  "channel": "mail",
  "clientEmail": "test@test.ru",
  "clientPhone": "+79123456789",
  "order": 2842648,
  "service": "beruTransferInfo",
  "title": "Название тикета"
}
```

## Изменение объекта

Для изменения объекта прдназначен метод АПИ ```api/external_user/entity/${gid}``` (PATCH) и
```api/tvm2/entity/${gid}``` (PATCH),
где gid - уникальный идентификатор изменяемого объекта. В теле запроса передается ассоциативный список значений
изменяемых атрибутов объекта.

Пример:

```shell
# Basic-authentication
$ curl -i -k -u triggers_platform:**** -H 'Content-Type: application/json' \
    -d '{"title": "Новое название"}' \
    -X PATCH 'https://ow.tst.market.yandex-team.ru/api/basic/entity/ticket@123'

# TVM-authentication
$ curl -i -k -H "X-Ya-Service-Ticket: ****" -H 'Content-Type: application/json' \
    -d '{"title": "Новое название"}' \
    -X PATCH 'https://ow.tst.market.yandex-team.ru/api/tvm2/entity/ticket@123'
```


## Удаление объекта

Для удаления объекта прдназначен метод АПИ ```api/basic/entity/${gid}``` (DELETE) и
```api/tvm2/entity/${gid}``` (DELETE),
где gid - уникальный идентификатор удаляемого объекта.

Пример:

```shell
# Basic-authentication
$ curl -i -k -u triggers_platform:****
    -X DELETE 'https://ow.tst.market.yandex-team.ru/api/basic/entity/ticket@123'

# TVM-authentication
$ curl -i -k -H "X-Ya-Service-Ticket: ****"
    -X DELETE 'https://ow.tst.market.yandex-team.ru/api/tvm2/entity/ticket@123'
```

## Получение объекта по уникальному идентификатору

Для получение объекта по его уникальному иентификатору прдназначен метод АПИ ```api/basic/entity/${gid}``` (GET) и
```api/tvm2/entity/${gid}``` (GET), где gid - уникальный идентификатор объекта.

Пример:

```shell
# Basic-authentication
$ curl -i -k -u triggers_platform:****
    -X GET 'https://ow.tst.market.yandex-team.ru/api/basic/entity/ticket@123'

# TVM-authentication
$ curl -i -k -H "X-Ya-Service-Ticket: ****"
    -X GET 'https://ow.tst.market.yandex-team.ru/api/tvm2/entity/ticket@123'
```

## Выборки объектов

Для получения объектов по его уникальному иентификатору прдназначен метод АПИ ```/api/basic/entity/list``` (POST) и
```/api/tvm2/entity/list``` (POST).

Пример:

```sh
# Basic-authentication
$ curl -i -k -u triggers_platform:****
    -d '{"metaclass": "ticket"}'
    -X POST 'https://ow.tst.market.yandex-team.ru/api/basic/entity/ticket@123'

# TVM-authentication
$ curl -i -k -H "X-Ya-Service-Ticket: ****"
    -d '{"metaclass": "ticket"}'
    -X POST 'https://ow.tst.market.yandex-team.ru/api/tvm2/entity/ticket@123'
```

Тело запроса:
```json
{
  "metaclass": "ticket",
  "attributes": [
    "status",
    "priority",
    "title"
  ],
  "filters": [
    {
      "type": "eq",
      "attribute": "archived",
      "value": [false]
    }
  ],
  "order": [
    {
      "attribute": "startStatusTime",
      "direction": "DESC"
    }
  ],
  "offset":  0,
  "limit": 100
}
```
