# Ресурс /licensors/[licensorId]/offer

## POST /licensors/[licensorId]/offer/accept

Принятие оферты лицензиаром

### Примечания
  - Ручка доступна только админу лицензиара

### Параметры
  - **uid** `<UID>` - UID пользователя
  
### Идентификаторы
  - **licensorId** `<ID>` - ID лицензиара
  
### Ответ
  - **status** `<boolean>` - всегда возвращает true либо летят ошибки, описанные ниже

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого лицензиара](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение licensorId: лицензиар уже принял оферту](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

