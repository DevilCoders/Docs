# Ресурс /vendors/[vendorId]/recommended/categories/blacklist

## GET /vendors/[vendorId]/recommended/categories/blacklist

Получение списка категорий, заблокированных вендором

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[CategoryBlacklist](/_entities/categories/CategoryBlacklist.md)] >

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)

## PUT /vendors/[vendorId]/recommended/categories/blacklist

Установка нового списка заблокированных категорий для вендора

### Параметры
  - **uid** `<UID>`

### Данные
[CategoryBlacklist](/_entities/categories/CategoryBlacklist.md)

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[CategoryBlacklist](/_entities/categories/CategoryBlacklist.md)] >

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
 
#### Категория не распознана
  - statusCode: `404`
  - code: `ENTITY_NOT_FOUND`
  - message: `No categories found with ID: ${illegalIds}`
  
#### Категория не принадлежит вендору
  - statusCode: `400`
  - code: `NOT_VENDOR_SUBCATEGORY`
  - message: `Category ${categoryId} ('${categoryPath}') is not a subcategory for vendor ${vendorId}`
