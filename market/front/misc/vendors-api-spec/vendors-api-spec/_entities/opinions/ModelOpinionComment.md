# Сущность "ModelOpinionComment"

Объект комментария к отзыву на модель

### Поля
  - **id** `<Number>` - идентификатор комментария
  - **text** `<String>` - текст комментария
  - **updateTime** [`<DateTime>`](/entries/DateTime) - время последнего изменения комментария
  - **canEdit** `<Boolean>` - признак возможности редактирования/удаления комментария
  - user [`<User>`](/entries/User) - автор комментария
  - comments `<Array[`[ModelOpinionComment](/_entities/opinions/ModelOpinionComment.md)`]>` - дерево ответов на комментарий
