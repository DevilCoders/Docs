# Ресурс /brands

## GET /brands

Получение списка всех брендов (например, для саджеста в заявке)

### Примечания
  - Используется в саджесте выбора бренда для создания карточки

### Параметры
  - uid `<UID>`
  - name `<String>` - строка для поиска по имени бренда
  - [Параметры пагинации](/_entities/Pager.md#Параметры)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **brands** [`<Array[Brand]>`](/_entities/Brand.md)
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/brands-api-spec#Стандартные-ошибки)
