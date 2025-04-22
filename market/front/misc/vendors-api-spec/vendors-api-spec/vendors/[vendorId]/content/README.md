# Ресурс /vendors/[vendorId]/content
## GET /vendors/[vendorId]/content/models

Получение общей информации о товарах и заявках на товары у вендора

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - entityType `<Enum>` - тип ответа: "MODEL"|"REQUEST"|"SKU" (по умолчанию - "MODEL" + "REQUEST")
  - modelName `<String>` - фильтр по названию товара
  - categoryId `<Number>` - фильтр по id категории 
  - requestState [`<Array[ModelEditRequestState]`>](/_entities/model-editor/ModelEditRequestState.md) - фильтр по состоянию заявки
  - orderBy `<Enum>` - поле сортировки: "POPULARITY"|"PRICE"|"DATE"|"QUALITY"|"OPINIONS". По-умолчанию: "POPULARITY"
  - orderDirection `<Enum>` - направление сортировки: "ASC"|"DESC". По-умолчанию: "DESC"
  - page `<Number>` - номер страницы
  - pageSize `<Number>` - количество элементов на странице (по-умолчанию - 30)

### Примечания
 - Сортировка для SKU не применима
 - Вне зависимости от сортировки заявки на модели располагаются после товаров
 - Возможные комбинации сортировки: POPULARITY+DESC, PRICE+ASC, PRICE+DESC, DATE+DESC, QUALITY+DESC, OPINIONS+DESC

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **items** `<Array[`[VendorUnit](/_entities/content/VendorUnit.md)`]>` - список товаров/заявок/sku
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

## GET /vendors/[vendorId]/content/models/count

Получение количества моделей и SKU вендора

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации 

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **totalCount** `<Number>` - суммарное количество моделей и SKU вендора
  - errors `<Error[]>`
  
### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

## GET /vendors/[vendorId]/content/requests/count

Получение количества заявок на редактирование моделей по статусам

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации 
  - modelName `<String>` - фильтр по названию товара
  - categoryId `<Number>` - фильтр по id категории 

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **completedRequestsCount** `<Number>` - количество заявок в статусе "завершено"
      - **rejectedRequestsCount** `<Number>` - количество заявок в статусе "отклонено"
      - **waitingRequestsCount** `<Number>` - количество заявок в статусе "ожидание" (обработка)
      - **editingRequestsCount** `<Number>` - количество заявок в статусе "редактирование"
  - errors `<Error[]>`
  
### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

## GET /vendors/[vendorId]/content/categories

Получение древовидной структуры категорий вендора

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации 
  - zoom `<Enum>` - "micro"|"full". Детализация информации по категории (см. [UnitCategoryInfo]). По-умолчанию "micro"
  - categoryName `<String>` - фильтр по имени категории
  - page `<Number>` - номер страницы
  - pageSize `<Number>` - размер страницы

### Примечания
 - Размер страницы в ответе может превышать pageSize, так как корневые категории попадают в неё полностью
 - При применении фильра по категории в выдачу так же попадают все дочерные и родительские категории вендора
  
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **items** `<Array[`[UnitCategory](/_entities/content/UnitCategory.md)`]>` - категории вендора
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

## GET /vendors/[vendorId]/content/categories/[categoryId]

Получение информации о категории вендора по её идентификатору (hyper_id)

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации 
  - zoom `<Enum>` - "micro"|"full". Детализация информации по категории (см. [UnitCategoryInfo]). По-умолчанию "micro"
  
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** [`<UnitCategory>`](/_entities/content/UnitCategory.md) - информация о категории
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
