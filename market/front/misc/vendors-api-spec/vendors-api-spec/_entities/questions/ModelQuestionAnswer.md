# Сущность "ModelQuestionAnswer"

Объект ответа к вопросу на товар

### Поля
  - **id** `<Number>` - идентификатор ответа
  - **text** `<String>` - текст ответа
  - **updateTime** [`<DateTime>`](/_entities/DateTime) - время последнего изменения ответа
  - **canEdit** `<Boolean>` - признак возможности редактирования/удаления ответа
  - **postedByVendor** `<Boolean>` - признак того что ответ оставлен вендором
  - **votes** `<Object>` - оценка ответа
    - **likeCount** `<Number>` - количество лайков
    - **dislikeCount** `<Number>` - количество дизлайков
    - **userVote** `<Number>` - голос пользователя по текущему ответу
  - user [`<User>`](/_entities/User) - автор ответа
  - **comments** `<Array[`[ModelQuestionComment](/_entities/questions/ModelQuestionComment.md)`]>` - список комментариев на ответ
