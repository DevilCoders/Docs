# Ресурс /categories

## GET /categories

Поиск категорий по параметрам

### Примечания
  - Используется в саджесте выбора категорий для создания карточки

### Параметры
  - **uid** `<UID>` - сейчас необязательный параметр из-за [бага](https://st.yandex-team.ru/VNDMARKET-53)
  - name `<String>` - строка для поиска по имени
  - vendorId `<Integer>` - идентификатор для поиска категорий вендора
  (категории в ответе отсортированы по популярности)
  - type `GROUP|LEAF` - тип категории, узловая или листовая. По умолчанию - все. 
  - outputType `Array[`[`CategoryOutputType`](/_entities/CategoryOutputType.md)`]` - фильтр по типу выдачи категории (может быть задано несколько значений)
  - grouped `<Boolean>` - фильтрация по тому, является ли категория групповой 
  - canCreateSku `<Boolean>` - фильтрация по тому, возможно ли в категории создавать SKU
  - [Параметры пагинации](/_entities/Pager.md#Параметры)

### Ответ

  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **categories** `<Array[Object]>`
        - **id** `<Integer>` - id категории
        - **path** `Array[String]` - "путь" категории (не более 4-х последних элементов). Последний элемент - имя самой категории.
        - **name** `<String>` - элементы коллекции "path" склеенные по `/`
        - outputType `<`[CategoryOutputType](/_entities/CategoryOutputType.md)`>` - тип выдачи категории
        - grouped `<Boolean>` - групповая категория или нет
        - canCreateSku `<Boolean>` - можно ли создавать SKU в категории
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)

### Доработки
  - Добавить параметр **brandId** для получения информации об уже использованных категориях для этого бренда
    - В категорию добавить поле campaignId
      - campaignId `<Integer>`
        - *если категория для этого бренда занята – id карточки, где она находится*
    - Нужно сделать в ближайшее время
