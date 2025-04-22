# Сущность "ModelQuestion"

Объект вопроса на товар 

### Поля
  - **id** `<Number>` - идентификатор вопроса
  - **model** `<Object>` - данные о товаре
    - **id** `<Number>` - идентификатор товара на Маркете
    - title `<String>` - заголовок товара
    - image [`<ModelImage>`](/_entities/model-editor/ModelImage.md) - картинка товара
  - **created** [`<DateTime>`](/_entities/DateTime) - время создания вопроса
  - **text** `<String>` - текст вопроса
  - **votes** `<Object>` - оценка вопроса
    - **likeCount** `<Number>` - количество лайков
    - **dislikeCount** `<Number>` - количество дизлайков
    - **userVote** `<Number>` - голос пользователя по текущему вопросу
  - user [`<User>`](/_entities/User) - автор вопроса
  - **answersCount** `<Number>` - количество ответов
  - **answers**`<Array[`[ModelQuestionAnswer](/_entities/questions/ModelQuestionAnswer.md)`]>` - список ответов на этот вопрос
