# Ресурс /vendors/[vendorId]/[productKey]/balance/clientLogins


## GET /vendors/[vendorId]/[productKey]/balance/clientLogins

Получение пользователей, связанных с клиентом в балансе 

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Идентификаторы
  - **vendorId** `<ID>` - вендорский ID
  - **productKey** `<ProductKey>` - перечислимый тип для ключей списка платных услуг, описанный [тут](/_entities/ProductKey.md)

### Ответ
  - **clientLogins** `<Array[String]>` - набор связанных логинов 

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет активной кампании для типа продукта productKey](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение productKey](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## PUT /vendors/[vendorId]/[productKey]/balance/clientLogins

Связывание пользователей с клиентом в балансе 

### Примечания
  - В ручку передается набор пользовательских логинов. Отсутствующие в наборе, но присутствующие в балансе - отвязываются. 
    Присутствующие в наборе, но отсутствующие в балансе - привязываются. Остальные игнорируются.

### Параметры
  - **uid** `<UID>` - менеджерский UID
  
### Идентификаторы
  - **vendorId** `<ID>` - вендорский ID
  - **productKey** `<ProductKey>` - перечислимый тип для ключей списка платных услуг, описанный [тут](/_entities/ProductKey.md)
  
### Данные
  - **`<Array[String]>`** - массив с пользовательскими логинами, которые следует связать с клиентом, не может быть пустым
  
### Пример запроса
```
PUT /vendors/42/recommended/balance/clientLogins?uid=12345
[
	"beko-market",
	"beko-vendor",
	"beko-vendor",
	"bla-bla"
]
```

### Ответ
  - **currentClientLogins** `<Array[String]>` - набор текущих связанных логинов 
  - **failedToBindClientLogins** `<Array[String]>` - набор логинов, которые не удалось связать 
  - **failedToUnbindClientLogins** `<Array[String]>` - набор логинов, которые не удалось отвязать 

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет активной кампании для типа продукта productKey](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение productKey](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Некорректное значение пользовательского логина (blackbox не распознал его)](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Массив с пользовательскими логинами не может быть пустым](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

