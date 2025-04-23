# Сущность "ModelColor"

Вендорский цвет модели 

### Поля:
  - id `<Integer>` - уникальный идентификатор вендорского цвета
  - **name** `<String>` - название вендорского цвета
  - **categoryId** `<Long>` - категория в рамках которой создан вендорский цвет
  - **baseColors** `<Array[<Integer>]>` - идентификаторы базовых цветов
  - pickers `<Array[`[`ModelImage`](/_entities/model-editor/ModelImage.md)`]>` - картинки-пикеры (тип PICKER)
