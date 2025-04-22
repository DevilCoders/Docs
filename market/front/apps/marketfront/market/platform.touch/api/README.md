Front API
===

### Описание

Frontend/Front API. Набор endpoint'ов (handler'ов),
которые предоставляют доступ мобильным приложениям к резолверам белого тача

[Архитектура](https://wiki.yandex-team.ru/Market/frontend/apiary/frontend-api/)

### Старт

Для сборки выполни:
* `npm run make:all:api`

Для запуска выполни:
* `npm run start:api`

Для автоматической пересборки:
* `npm run webpack:api:watch`

Доступ на разработческом стенде: `https://<username>.api.market.logrus01ed.yandex.ru` (api!)

Очистка проекта:
* `npm run clean`

### Обязательные ревьюеры

Для ПРов в директорию `/api` необходим хотя бы один `/ok` от [обязательных ревьюреов](https://github.yandex-team.ru/market/marketfront/blob/master/market/.devexp.json#L27

### Структура

Ручки FAPI определены в мандреле (`@yandex-market/mandrel/routes.js.flow`). Сейчас их две:

1. `/doc/v<version>` - WIP. Будет отдавать документацию по указанной версии fapi.
2. `/api/v<version>` - POST-ручка для доступа к handler'ам указанной версии.
  - В качестве параметров передаётся
    - `name` - список имен handler'ов через запятую
  - В качестве заголовков необходимо передать
    - `X-Region-id` - форсировано проставит регион пользователя, которое приложение знает лучше `nodules`
    - `api-platform: ANDROID` / `api-platform: IOS`
    - `Content-Type: application/json`
    - `X-User-Authorization: OAuth <OAuth Token>` - если ручке требуется авторизация
  - В теле запроса обязательно надо указать
    - Массив объектов параметров каждого из указанных в параметре `name` handler'ов

Контроллер FAPI лежит в мандреле: `@yandex-market/mandrel/pages/FrontApiPage`;

Handler'ы определены в `api/app/handlers`.

Интеграционные тесты лежат в `api/app/__integration__` и запустить их можно командой
* `npm run integration`

### Нейминг хендлеров

`resolve` - получение данных, соответвует методу `GET` или `Read` в `CRUD`

`add` - создание новых данных, соответвует методу `POST` или `Create` в `CRUD`

`remove` - удаление данных, соответвует методу `DELETE` или `Delete` в `CRUD`

`save` - замена/обновление данных, соответвует методам `PUT` или `PATCH` или `Update` в `CRUD`

#### Примеры
```
resolveOfferById
addWishlistItem
removeArticleVote
saveWishlistTag
```

### Пример запроса
#### json
```bash
curl -X POST \
  'https://fenruga.api.market.logrus01ed.yandex.ru/api/v1?name=resolveProductRatings' \
  -H 'Content-Type: application/json' \
  -H 'X-User-Authorization: GUEST' \
  -H 'api-platform: ANDROID' \
  -H 'cache-control: no-cache' \
  -d '{
    "params": [{
      "productId" : "11158556,13941547,13941553"
    }]
  }'
```

#### multipart
```bash
curl -X POST \
  'https://fenruga.api.market.logrus01ed.yandex.ru/api/v1?name=resolveProductRatings' \
  -H 'Content-Type: multipart/form-data' \
  -H 'X-User-Authorization: GUEST' \
  -H 'api-platform: ANDROID' \
  -H 'cache-control: no-cache' \
  -F 'params={"qwe":123,"asd":456}' \
  -F 'filename=@self/project/src/some/path/to/file'
```

Особенности работы с мультипарт-запросами:
- Можно передавать только одно имя хэндлера
- Файлы доступны из хэндлеров через `params.files.<filename>`
- Другие параметры, необходимые для запроса, можно передаться как form-data с именем `params` со значением в формате JSON (см. пример)

### Авторизация

У каждого хендлера есть список разрешенных способов авторизации. Надо указывать все допустимые.
Клиент, мобильное приложение, не знает о необходимом способое авторизации для хендлера, поэтому передает текущий способ авторизации пользователя.
Если он залогинен, то OAUTH, если нет, то GUEST.
Допустим, есть хендлер, который отдает даннные в любом случае, то он должен и на GUEST реагировать, и на OAUTH. В списке типов авторизации: `['OAUTH', 'GUEST']`.
А если требуется авторизванный текущий юзер, например, для создания контента, то на GUEST он должен ругнуться. В списке типов авторизации: `['OAUTH']`.

#### GUEST

Подходит для любых запросов, не требующих авторизации для текущего пользователя.

#### OAuth

Для авторизованного текущего пользователя. Для методов, которые могут работать анонимно, все равно надо указывать этот способ авторизации.
Мандрель по токену достанет юзера из паспорта и положит в контекст запроса.

_Откуда взять токен?_ Из мобильного приложения. Нужно авторизоваться под логином, привязанном к стаффу, тогда появится раздел Debug.

https://jing.yandex-team.ru/files/naygeborin/uhura_2019-08-05T07%3A25%3A26.jpg

https://jing.yandex-team.ru/files/naygeborin/uhura_2019-08-05T07%3A25%3A34.jpg

#### Интеграционное тестирование

1. Для тестов с авторизацией запусти кадавр на логрусе

2. Запусти api, обращенный к твоему кадавру на логрусе
* `make all_api && KADAVR_HOST=localhost KADAVR_PORT=<port> make server_api`

3. Можно запускать тесты локально из папки `platform.touch`
* `KADAVR=1 KADAVR_HOST=logrus01ed.market.yandex.net KADAVR_PORT=<port> FAPI_URL=https://<username>.api.market.logrus01ed.yandex.ru FAPI_AUTH_TOKEN="OAuth <token>" npm run integration`

Чтобы обновить снепшоты, убери параметр `--ci` в скрипте `ci:jest:api` в package.json, который лежит папке `platform.touch`
