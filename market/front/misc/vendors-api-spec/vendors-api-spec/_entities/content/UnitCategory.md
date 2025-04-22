# Сущность категории (в иерархическом представлении)

### Поля:
  - **id** `<Number>` - id категории
  - **name** `<String>` - имя категории 
  - categoryExtendedInfo `<`[UnitCategoryInfo](UnitCategoryInfo.md)`>` - дополнительная информация о категории
  - children [`<Array[UnitCategory]`>](UnitCategory.md) - дочерние категории

### Примечания
  - categoryInfo возвращается при передаче параметра zoom=full в ручку GET /vendors/[vendorId]/content/categories
