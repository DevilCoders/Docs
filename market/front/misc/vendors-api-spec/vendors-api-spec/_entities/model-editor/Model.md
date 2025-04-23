# Сущность "Model"

Вендорская модель на Маркете

### Поля:
  - modelId `<Integer>` - идентификатор модели
  - **title** `<String>` - заголовок модели 
  - **category** [`<Category>`](/_entities/Category.md) - категория, к которой относится модель
  - **brandId** `<Integer>` - идентификатор бренда (вендора в МБО) 
  - brandName `<String>` - имя бренда (вендора в МБО). Только для чтения.
  - parameters `<Array[`[`ModelParameter`](/_entities/model-editor/ModelParameter.md)`]>` - параметры модели  (кроме SKU-параметров)
  - vendorColor [`<ModelColor>`](/_entities/model-editor/ModelColor.md) - вендорский цвет модели
  - sku `<Array[`[`ModelSku`](/_entities/model-editor/ModelSku.md)`]>` - SKU модели
  - aliases `<Array[String]>` - альтернативные названия модели 
  - images `<Array[`[`ModelImage`](/_entities/model-editor/ModelImage.md)`]>` - картинки модели
  - ~~description~~ `<String>` - _(deprecated)_ описание модели 
  - url `<String>` - страница с описанием модели 
  - ~~barcode~~ `<String>` - _(deprecated)_ баркод модели 
  - barcodes `Array[<String>]` - баркоды модели
  - ~~vendorCode~~ `<String>` - _(deprecated)_ номер модели в международной классификации 
  - vendorCodes `Array[<String>]` - номера модели в международной классификации 

### Примечания

Поле `fileId` в структуре картинки модели заполяется в случае, когда была загружена новая картинка. 