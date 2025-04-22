# Ресурс /vendors/[vendorId]/manager

## GET /vendors/[vendorId]/manager

Получение менеджера привязанного к вендору

### Примечания
  - Присланный менеджер может быть уволенным (`active=false`)!
  Такое может случится, если менеджер был уволен уже будучи привязанным к вендору.
  Бизнес-подход тут таков, что другие менеджеры просто разбирают клиентов ещё до увольнения текущего,
  но т.к. технически это возможно, то нужно учесть кейс, в котором пришедший с бекенда менеджер может быть неактивным.
  - Менеджера у вендора может не быть. В этом случае элемент `item` в [SimpleResponse] будет отсутствовать. 

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[StaffUser](/_entities/staff/StaffUser.md)] >

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)

## PUT /vendors/[vendorId]/manager

Привязка менеджера к вендору

### Параметры
  - **uid** `<UID>`
  - **manager** `<Number|String>` - UID или яндексовый логин менеджера

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[StaffUser](/_entities/staff/StaffUser.md)] >

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
 
#### Яндексовый пользователь не распознан
  - statusCode: `400`
  - code: `NOT_A_USER`
  - message: `Failed to found a yandex user by uid or login: ${manager}`
  
#### Присланный пользователь не имеет роль менеджера
  - statusCode: `400`
  - code: `NOT_A_MANAGER`
  - message: `Specified user is not a vendor manager!`
  
#### Присланный пользователь не является активным сотрудником Яндекса
  - statusCode: `400`
  - code: `NOT_A_STAFF`
  - message: `This user is not a yandex employee: ${login}`
  
## DELETE /vendors/[vendorId]/manager

Удаление менеджера у вендора

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
<[SimpleResponse](/_entities/responses/SimpleResponse.md) [Result] >

`<Result>`:
  - **removed** `<Boolean>` - маркер того удален ли менеджер

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
