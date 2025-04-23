# Ресурс /oauth

## GET /oauth/contentApi/link

Запрос ссылки для получения oauth-токена для текущего пользователя

### Параметры
  - **uid** `<UID>` пользователя от которого идет запрос

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **link** [`<HtmlLink>`] - ссылка для получения oauth-токена
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)

[`<HtmlLink>`]: /_entities/HtmlLink.md
