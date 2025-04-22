# Ресурс /vendors/[vendorId]/modelEdit/requests/[requestId]

## GET /vendors/[vendorId]/modelEdit/requests/[requestId]

Получение заявки на создание/изменение модели.

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
        - **requestId** `<Integer>` - идентификатор заявки в КВ
        - **model** [`Model`](/_entities/model-editor/Model.md) - исходные данные заявки
        - **status** [`ModelEditRequestStatus`](/_entities/model-editor/ModelEditRequestStatus.md) - текущий статус заявки
        - **creationDate** [`<DateTime>`](/_entities/DateTime.md) - дата создания заявки
        - **modificationDate** [`<DateTime>`](/_entities/DateTime.md) - дата последнего изменения заявки
        - сomment `<String>` - текст последнего комментария от вендора
        - operatorComment `<String>` - текст последнего комментария от оператора
        - autogenerationTms `<Boolean>` - `true`, если заявка обработана по новому пайплайну в МБО
        - draft `<Boolean>` - признак того, что заявка является черновиком
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

## PUT /vendors/[vendorId]/modelEdit/requests/[requestId]

Изменение заявки на создание/изменение модели по идентификатору заявки

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Данные
  - **model** [`Model`](/_entities/model-editor/Model.md) - исходные данные для заявки
  - сomment `<String>` - текст комментария от вендора
  - draft `<Boolean>` - признак того, что изменяемая заявка является черновиком
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **model** [`Model`](/_entities/model-editor/Model.md) - исходные данные для заявки
      - сomment `<String>` - текст комментария от вендора
  - errors `<Error[]>`
  
### Примечания
- В случае редактирования модели, поле model.modelId должно быть заполнено.
- Для черновика заявки не проводится валидация модели. 

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

## DELETE /vendors/[vendorId]/modelEdit/requests/[requestId]

Удаление заявки на создание/изменение модели по идентификатору заявки

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Model>`(/_entities/model-editor/Model.md) - данные для заявки с незаполненным requestId
  - errors `<Error[]>`
  
### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
