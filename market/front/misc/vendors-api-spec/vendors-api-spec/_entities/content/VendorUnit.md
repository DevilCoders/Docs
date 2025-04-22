# Сущность модели, SKU или заявки на товар у вендора

Представляет собой базовую информацию о модели, SKU или заявке на создание товара

### Поля:
  - **id** `<Number>` - идентификатор модели, SKU или заявки
  - **name** `<String>` - название модели, SKU или заявки
  - **entityType** `<Enum>` - тип сущности: "MODEL" (опубликованный товар), "REQUEST" (заявка на создание) или "SKU"
  - categoryPath `<Array[String]>` - краткий "путь" категории (не более 4-х последних элементов)
  - rating `<Number>` - рейтинг товара
  - image [`<Image>`](/_entities/Image.md) - изображение товара
  - opinionsCount `<Number>` - количество отзывов
  - questionsCount `<Number>` - общее количество вопросов
  - notAnsweredQuestionsCount `<Number>` - количество неотвеченных вопросов
  - requestState [`<ModelEditRequestState>`](/_entities/model-editor/ModelEditRequestState.md) - состояние заявки
  - requestCreationDate [`<DateTime>`](/_entities/DateTime.md) - дата создания заявки
  - requestModificationDate [`<DateTime>`](/_entities/DateTime.md) - дата последнего изменения заявки
  - skuList [`<Array[VendorSku]>`](VendorSku.md) - список SKU товара
  - parentId `<Number>` - идентификатор родительской сущности (для SKU - id товара)
  - parentName `<String>` - имя родительской сущности (для SKU - имя товара)

### Примечания
  - Поле `requestState` для `entityType` MODEL сдержит статус, если с товаром есть ассоциированная заявка
  - Поле `requestCreationDate` для `entityType` MODEL сдержит дату создания, если с товаром есть ассоциированная заявка
  - Поле `requestModificationDate` для `entityType` MODEL сдержит дату создания, если с товаром есть ассоциированная заявка
  - Поля `requestState`, `requestCreationDate` и `requestModificationDate` для `entityType` REQUEST обязательны
  - Поля `opinionsCount` и `questionsCount` имеют значение только для `entityType` MODEL
  - Поле `skuList` заполняется только для `entityType` MODEL   
  - Поле `rating` заполняется для `entityType` MODEL и обязательно для него
