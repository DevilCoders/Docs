# Ресурс /vendors/{vendorId}/categories

## GET /vendors/{vendorId}/categories/top

Получение топовой по кликам листовой категории вендора

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  [`<SimpleResponse>`](/_entities/responses/SimpleResponse.md)
  - **item**
    - **topCategory** [`<Category>`](/_entities/Category.md) - топовая категория бренда

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)

#### У вендора не найдено ни одной листовой категории
Такое может быть, только если у вендора нет категорий вообще
  - statusCode: `404`
  - code: `VENDOR_HAS_NO_CATEGORY`
  - message: `No leaf category was found for vendor: ${vendorId}`

### Пример запроса
```
GET /vendors/42/categories/top?uid=12345
"item": {
    "topCategory": {
        "id": 91016,
        "path": [
            "Все товары",
            "Компьютерная техника",
            "Компьютеры",
            "Промышленные компьютеры"
        ],
        "name": "Все товары/Компьютерная техника/Компьютеры/Промышленные компьютеры"
    }
}
```