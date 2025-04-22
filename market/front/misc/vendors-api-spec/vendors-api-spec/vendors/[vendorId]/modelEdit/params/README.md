# Ресурс /vendors/[vendorId]/modelEdit/params

## GET /vendors/[vendorId]/modelEdit/params/byCategory

Получение параметров для категории по hid

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - **categoryId** `<Integer>` - идентификатор листовой категории (hid)
  - sku `<Boolean>` - показывать параметры SKU или параметры модели
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **category** [`<Category>`](/_entities/Category.md) - категория, к которой относится модель
      - **editable** `<Boolean>` - признак возможности редактирования моделей в категории
      - **parameters** `<Array[`[`ModelParameter`](/_entities/model-editor/ModelParameter.md)`]>` - параметры модели
      - **canCreateSku** `<Boolean>` - признак возможности создания и редактирования SKU моделей в категории
      - **canDefineColor** `<Boolean>` - признак возможности задания вендорского цвета
      - baseColors `<Array[Object]>` - базовые цвета, доступные для выбора в категории
        - **id** `Long` - идентификатор базового цвета
        - **name** `String` - имя базового цвета
  - errors `<Error[]>`

### Примечания

В ответе не заполняются значения параметров

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## GET /vendors/[vendorId]/modelEdit/params/byModel

Получение параметров модели по modelId со значениями из репорта

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - **modelId** `<Integer>` - идентификатор модели
  - fields `<Array[`[`ModelField`](/_entities/model-editor/ModelField.md)`]>` - список разделов для загрузки. Если передано пустое поле, загружается только базовая информация о модели (заголовок, категория, картинки). Если поле не передано, загружается базовая информация о модели и её параметры.
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **model** [`<Model>`](/_entities/model-editor/Model.md) - модель с параметрами
      - **editable** `<Boolean>` - признак возможности редактирования модели
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)