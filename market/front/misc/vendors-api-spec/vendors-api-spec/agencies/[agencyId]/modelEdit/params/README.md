# Ресурс /agencies/[agencyId]/modelEdit/params

## GET /agencies/[agencyId]/modelEdit/params/byCategory

Получение параметров для категории по hid

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - **categoryId** `<Number>` - идентификатор листовой категории (hid)
  - brandId `<Number>` - идентификатор бренда (для фильтрации линеек)
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
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## GET /agencies/[agencyId]/modelEdit/params/byModel

Получение параметров модели по modelId со значениями из репорта. Работает аналогично [методу для вендора](/vendors/%5BvendorId%5D/modelEdit/params#get-vendorsvendoridmodeleditparamsbymodel).
