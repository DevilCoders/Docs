# Поисковые подсказки (саджесты)

Поисковые подсказки выполняют 2 цели:

1. Сократить время ввода для пользователя
2. Показать пользователю возможности сервиса

## Методы

-   `suggest` :: `GET /api/hotels_portal/v1/suggest`
-   `logSuggest` :: `POST /api/hotels_portal/v1/log_suggest`

## Описание данных саджеста

API может вовзвращать 3 типа саджеста:

1. Регион (`type == "region"`)
2. Отель (`type == "hotel"`)
3. Поисковый запрос (`type == "search"`)

В поле `request_params` содержатся параметры, с которыми надо выполнить переход или поиск при выборе пользователем саджеста.

-   `type` - тип саджеста
-   `geoId` - идентификатор региона
-   `permalink` или `hotelSlug` - идентификатор отеля
-   `searchText` - поисковый запрос

## Требования к бэкенду

1. Бэкенд отдает список саджестов разного типа в ручке `suggest` с некоторым приоритетом, определяемым на бэкенде, а так же логирует запрос пользователся и предложенные саджесты.
1. Каждая поисковая подсказка содержит уникальный идентификатор, который зависит только от подсказки и формуруется по следующему формату:
    - Для саджеста с типом `region` id формируется как `region-{region-id}-{lang-code}`, где `region-id` - идентификатор региона, `lang-code` - код языка.
    - Для саджеста с типом `hotel` id формируется как `hotel-{permalink}-{lang-code}`, где `permalink` - пермалинк отеля, `lang-code` - код языка.
    - Для саджеста с типом `search` id формируется как `search-{slug}-{lang-code}`, где `slug` транслитерация текста запроса, `lang-code` - код языка.
1. При вызове `logSuggest`, бэкенд логирует переданный id саджеста.
1. Бэкенд умеет поставлять вышеуказанные логи в YT.
1. Бэкенд определяет регион пользователя на основе заголовка `X-Ya-User-Gid`, а в случае его отсутствия на основе IP из `X-Ya-User-Ip`.
1. Бэкенд отдает посковые подсказки, сгруппированные по типу. Общее количество подсказок во всех группах не должно превышать число, переданное в параметре `limit`.

### Логика обработки запроса

1. Если параметр query не пустая строка, в ответе будет саджест по организациям, регионам и посковым подсказкам.
1. Если geoId присутствует, вернет массив с единственным SuggestItem для указанного geoId, или пустой массив для несуществующего geoId.
1. Если permalink или hotelSlug присутствует, вернет массив с единственным SuggestItem для указанной организации, или пустой массив для несуществующего permalink.
1. Если пункты 1-3 не подошли, вернет саджест с популярными направлениями.

## Требования к фронтенду

1. При заходе пользователя на страницу с саджестом, фронтенд генерирует случайный UUID, который является идентификатором саджест-сессии и устанавливает счетчик запросов в 0.
   При каждом запросе к `suggest` и `logSuggest` в запросе передается этот идентификатор и текущее значение счетчика запросов, после чего счетчик запросов инкрементируется.
   Все взаимодействия в рамках одной подгрузки страницы считаются совершенными в одной саджст-сессии.
1. Фронт отображает саджесты в том виде и с той группировкой, которая пришла от бэкенда.
1. После того, как пользователь выбрал саджест, необходимо передать данные о выборе пользователя в запросе к `logSuggest`, для того, чтобы отслеживать выбор пользователей и улучшать качество саджеста.
1. При выборе саджеста с типом "Регион", пользователя перенаправляет на страницу поиска отеля в выбранном регионе. Так же в саджесте может присутствовать поисковый запрос.
1. При выборе саджеста с типом "Отель", пользователя перенаправляет на страницу выбранного отеля.
1. При выборе саджеста с типом "Поисковый запрос", пользователся перенаправляет на страницу поиска с выбранным поисковым запросом.
