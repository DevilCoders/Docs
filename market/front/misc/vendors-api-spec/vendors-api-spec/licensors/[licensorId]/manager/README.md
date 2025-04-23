# Ресурс /licensors/[licensorId]/manager

## GET /licensors/[licensorId]/manager

Получение карточки менеджера, назначенного лицензиару

### Примечания
  - Получение карточки менеджера доступно для менеджера, "читающего" менеджера, суппорта и всех ролей лицензиара (на текущий момент админ и управленец контентом)

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[StaffUser](/_entities/staff/StaffUser.md)] >

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)

## PUT /licensors/[licensorId]/manager

Назначение менеджера карточке лицензиара

### Примечания
  - Назначение менеджера карточке лицензиара доступно только менеджеру

### Параметры
  - **uid** `<UID>`
  - **manager** `<Number|String>` - UID или яндексовый логин менеджера

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[StaffUser](/_entities/staff/StaffUser.md)] >

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого лицензиара](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
 
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
  
## DELETE /licensors/[licensorId]/manager

Удаление менеджера у карточки лицензиара (передача карточки в саппорт)

### Примечания
- Удаление менеджера у карточки менеджера (передача карточки в саппорт) доступно только менеджеру

### Параметры
- **uid** `<UID>`

### Ответ
  <[SimpleResponse](/_entities/responses/SimpleResponse.md) [[StaffUser](/_entities/staff/StaffUser.md)] >
  
### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого лицензиара](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)