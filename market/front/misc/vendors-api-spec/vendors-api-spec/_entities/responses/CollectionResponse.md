# Сущность "CollectionResponse[T]"

Объект возвращаемый в большинстве случаев, когда ручка должна логически вернуть список элементов.
Является обёрткой над коллекцией объектов-результатов, позволяющей передать мета-информацию, или ошибки.
Параметризуется типом элементов в коллекции.

### Поля
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **items** `<Array[T]>`
  - errors `<Error[]>`

### Примеры

#### `<CollectionResponse[Category]>`
```
{
  "errors": [],
  "meta": {
    "host": "braavos"
  },
  "result": {
    "item": {
      "pager": {
        "total": 2,
        "pages": 1,
        "page": 1
      },
      "items": [
        {
          "id": 90401,
          "path": [
            "Все товары"
          ],
          "name": "Все товары"
        },
        {
          "id": 43658,
          "path": [
            "Все товары",
            "Электроника"
          ],
          "name": "Все товары/Электроника"
        }
      ]
    }
  }
}
```

#### `<CollectionResponse[Image]>`
```
{
  "errors": [],
  "meta": {
    "host": "braavos"
  },
  "result": {
    "item": {
      "pager": {
        "total": 6,
        "pages": 3,
        "page": 2
      },
      "items": [
        {
          "url": "http://i.imgur.com/dI6dpOW.jpg"
        },
        {
          "url": "http://i.imgur.com/Fl9SVMX.jpg"
        }
      ]
    }
  }
}
```
