# REST API

Сервис поддерживает работу с БД через простое REST-подобное API.
API позволяет извлекать и удалять документы из БД. Изменение и создание на момент написания этого текста не реализовано )

Запросы формируются по шаблону:
`{HttpMethod} {rootUrl}/api/{EntityType}?{filters}`

Возвращают json.

**`{rootUrl}`** - корневой url апдейтера.
Локально это http://localhost:3000 .
В продакшене: https://serpdocs.si.yandex-team.ru/updater

**`{HttpMethod}`** - тип http запроса:
* `GET` - достать данные
* `DELETE` - удалить данные

**`{EntityType}`** - имя коллекции в БД (модели mongoose):
* `pr`
* `constructives`
* `rawlogs`
* `types`
* `docs`
* `errors`
* `logs`

_Пример:_ получить все пулл-реквесты:
`GET` https://serpdocs.si.yandex-team.ru/updater/api/pr

**`{filters}`** - критерии поиска документов.
Ключи - названия полей модели, значения - допустимые значения свойства.
В качестве значений можно задавать:
* точное значение

    _Пример:_ получить пулл-реквест 15539:
    `GET` https://serpdocs.si.yandex-team.ru/updater/api/pr?pullRequest=15539

    _Пример:_ получить тип `App` для дева (`pullRequest=docs`):
    `GET` https://serpdocs.si.yandex-team.ru/updater/api/types?name=App&pullRequest=docs

* регулярное выражение в формате `/regexp/[options]`

    _Пример:_ получить все логи действий с тегами
    `GET` https://serpdocs.si.yandex-team.ru/updater/api/logs?action=/тег/i

* дата в формате 'YYYY.MM.DD' (ISO 8601) или 'YYYY.MM.DD-YYYY.MM.DD'

    _Пример:_ получить логи за 5 апреля 2018
    `GET` https://serpdocs.si.yandex-team.ru/updater/api/logs?timestamp=2018.04.05
    _Пример:_ получить логи с 5 по 20 апреля 2018
    `GET` https://serpdocs.si.yandex-team.ru/updater/api/logs?timestamp=2018.04.05-2018.04.20

Метод **`DELETE /api/pr`** особенный: он чистит данные для пулл-реквестов. Принимает параметры в теле запроса.

_Пример:_ удалить данные для пулл-реквестов 14500 и 14501
```
DELETE /updater/api/pr HTTP/1.1
Host: serpdocs.si.yandex-team.ru
Content-Type: application/json

{"prNumber": [14500, 14501]}
```

### Узнать больше
Код api-методов можно посмотреть в [контроллере](api.js)
Особенности маршрутизации в [роутере](../routes/api.js)
