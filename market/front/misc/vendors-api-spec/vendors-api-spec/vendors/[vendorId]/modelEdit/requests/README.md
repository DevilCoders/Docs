# Ресурс /vendors/[vendorId]/modelEdit/requests

## POST /vendors/[vendorId]/modelEdit/requests

Создание заявки на создание/изменение модели

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  
### Данные
  - **model** [`Model`](/_entities/model-editor/Model.md) - исходные данные для заявки
  - comment `<String>` - текст комментария от вендора
  - draft `<Boolean>` - признак того, что создаётся черновик заявки
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **requestId** `<Integer>` - идентификатор заявки в КВ
  - errors `<Error[]>`
  
### Примечания
- В случае изменения модели, поле model.modelId должно быть заполнено.
- Для черновика заявки не проводится валидация модели. 

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## GET /vendors/[vendorId]/modelEdit/requests

Получение списка заявок на создание/изменение модели. Список отсортирован (сначала свежие заявки).

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - requestId `<Integer>` - идентификатор заявки в КВ
  - modelId `<Integer>` - идентификатор модели (при заполнении, заявки отображаются целиком)
  - active `<Boolean>` - показывать только открытые заявки
  - text `<String>` - поиск по вхождению текста в заголовок заявки
  - [Параметры пагинации](/_entities/Pager.md#Параметры)
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **items** `<Array[Object]>`
        - **requestId** `<Integer>` - идентификатор заявки в КВ
        - **model** [`Model`](/_entities/model-editor/Model.md) - исходные данные заявки (если не заполнен modelId, отдаются только modelId, title, category, brandId и images)
        - **status** [`ModelEditRequestStatus`](/_entities/model-editor/ModelEditRequestStatus.md) - текущий статус заявки
        - **creationDate** [`<DateTime>`](/_entities/DateTime.md) - дата создания заявки
        - **modificationDate** [`<DateTime>`](/_entities/DateTime.md) - дата последнего изменения заявки
        - сomment `<String>` - текст последнего комментария от вендора (если он есть и если заполнен modelId)
        - operatorComment `<String>` - текст последнего комментария от оператора (если он есть и если заполнен modelId)
        - autogenerationTms `<Boolean>` - `true`, если заявка обработана по новому пайплайну в МБО
  - errors `<Error[]>`

### Примечания
- Если черновик заявки не изменялся в течение последних 30 дней, он не попадает в список. 

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)