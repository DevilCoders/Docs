# Ресурс /clients/[ID]

## GET /clients/[ID]

Получает информацию о клиенте Баланса с таким ID

### Примечания
  - Этот метод доступен только менеджерам

### Параметры
  - **uid** `<UID>` - сейчас необязательный параметр из-за [бага](https://st.yandex-team.ru/VNDMARKET-53)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **users** `<Array[Object]>` - список пользователей, связанных с этим клиентом в балансе
        - **login** `<String>` - логин пользователя
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого клиента](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### Запрос не-менеджером
  - statusCode: `403`
  - code: `ROLE_NOT_ALLOWED`
  - message: `Only MANAGER role is allowed to access this method`
