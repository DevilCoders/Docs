# Сущность "SimpleResponse[T]"

Объект возвращаемый в большинстве случаев, когда ручка должна логически вернуть 1 элемент.
Является оболочкой над объектом-результатом, позволяющей передать мета-информацию, или ошибки.
Параметризуется типом содержащегося объекта.

### Поля
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<T>`
  - errors `<Error[]>`

### Примеры

#### `<SimpleResponse[Category]>`
```
{
  "errors": [],
  "meta": {
    "host": "braavos"
  },
  "result": {
    "item": {
      "id": 90401,
      "path": [
        "Все товары"
      ],
      "name": "Все товары"
    }
  }
}
```

#### `<SimpleResponse[Image]>`
```
{
  "errors": [],
  "meta": {
    "host": "braavos"
  },
  "result": {
    "item": {
      "url": "http://i.imgur.com/gEf0iaz.jpg"
    }
  }
}
```
