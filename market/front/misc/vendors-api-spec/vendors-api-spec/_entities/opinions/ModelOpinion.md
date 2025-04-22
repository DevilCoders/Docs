# Сущность "ModelOpinion"

Объект отзыва на модель 

### Поля
  - **id** `<Number>` - идентификатор отзыва
  - **model** `<Object>` - данные о модели
    - **id** `<Number>` - идентификатор модели на Маркете
    - title `<String>` - заголовок модели
    - image [`<ModelImage>`](/_entities/model-editor/ModelImage.md) - картинка модели
  - **created** [`<DateTime>`](/entries/DateTime) - время создания отзыва
  - **review** `<Object>` - текст отзыва
    - **comment** `<String>` - содержимое раздела "Комментарий"
    - **pro** `<String>` - содержимое раздела "Достоинства"
    - **contra** `<String>` - содержимое раздела "Недостатки"
  - **recommend** `<Boolean>` - признак рекоммендации модели пользователем
  - **cpa** `<Boolean>` - признак проверенного покупателя
  - **votes** `<Object>` -  оценка отзыва
    - **agree** `<Number>` - количество оценок "отзыв полезен"
    - **reject** `<Number>` - количество оценок "отзыв не полезен"
    - **total** `<Number>` - всего оценок
  - user [`<User>`](/entries/User) - автор отзыва
  - **region** `<Number>` - регион автора отзыва
  - **averageGrade** `<Number>` - средняя оценка модели
  - photos `<Array[`[Image](/_entities/Image.md)`]>` - фотографии, прикреплённые к отзыву (в поле `url` лежит не полный url, а `groupId/imageName`)
  - **usage** `<Number>` - время использования (0 - меньше месяца, 1 - несколько месяцев, 2 - больше года)
  - comments `<Array[`[ModelOpinionComment](/_entities/opinions/ModelOpinionComment.md)`]>` - дерево комментариев к отзыву
  - **canReply** `<Boolean>` - может ли вендор отвечать на комментарии к этому отзыву
  - **anonymous** `<Boolean>` - признак был ли сделан отзыв анонимно
