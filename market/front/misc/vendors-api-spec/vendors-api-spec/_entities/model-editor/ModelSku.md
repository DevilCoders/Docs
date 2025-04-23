# Сущность "ModelSku"

SKU вендорской модели на Маркете

### Поля:
  - id `<Number>` - идентификатор SKU
  - name `<String>` - имя SKU (если не задать, будет сгенерировано из значений переданных параметров)
  - requestId `<Number>` - идентификатор заявки, к которой относится SKU (обязательно при создании/редактировании SKU)
  - modelId `<Number>` - идентификатор модели, к которой относится SKU (обязательно при создании/редактировании SKU, если не задан requestId)
  - categoryId `<Number>` - идентификатор категории, к которой относится модель (обязательно при создании/редактировании SKU)
  - **parameters** `<Array[`[`ModelParameter`](/_entities/model-editor/ModelParameter.md)`]>` - параметры SKU 
  - vendorColor [`<ModelColor>`](/_entities/model-editor/ModelColor.md) - вендорский цвет модели