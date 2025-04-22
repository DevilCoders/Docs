# Методы

Словесное описание методов сервиса. OpenAPI схема: [openapi.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/openapi.json)

## POST /v1/tasks

Метод создает заявку. Принимает на вход JSON-объект (схема: [OriginalTask.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/original-task.json)) с информацией о заявке.
Фидбек от пользователей приходит в такую же ручку в [userapi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/userapi/), в userapi фидбек приходит с юзер-тикетом. В feedback-api в ручку приходит только фидбек, который отправляет НК

## POST /v1/tasks/batch

Метод создает набор заявок. Принимает на вход массив JSON-объектов `OrigianalTask`. [Описание полей](format.md), [список типов фидбека](types.md). Фидбек от пользователей приходит в такую же ручку в [userapi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/userapi/), в userapi фидбек приходит с юзер-тикетом. В feedback-api в ручку приходит только фидбек, который отправляет НК

## GET /v1/tasks/$

Получение заявки фидбека по id. [Схема ответа](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/task.json). Для доступа нужен юзер-тикет из внутреннего паспорта и роль на чтение в idm

## GET /v1/tasks

Получение  списка заявок фидбекас заданными фильтрами. [Схема ответа](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/tasks.json). Для доступа нужен юзер-тикет из внутреннего паспорта и роль на чтение в idm

## PUT /v1/tasks/$

Изменение состояния заявки фидбека. Запросы приходят только из НК. [Схема запроса](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions.json?rev=r8916897#L18)

## GET /v1/feedback/meta

Получение всех возможных значений для [полей фидбека](format.md). Используется в [админке](https://feedback-admin.c.maps.yandex-team.ru) для отображения актуальных фильтров.
