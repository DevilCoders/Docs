# Ветка комментариев

## Описание

Родителем каждой ветки комментариев является отдельная сущность: отзыв, статья в журнале, автосравнение, ответ на вопрос.

Каждая ветка обладается своим набором параметром, влияющим на отображение и доступные действия с комментриями. На одной странице может быть несколько видов сущностей обладающими своими комментариями.
* id - уникальный идентификатор, по которому можно определить сущность
* canAnswer - может ли текущий пользователь добавлять ответы
* entity - answer, versus, article, review (grade)
* canLike - может ли текущий пользователь оставлять лайки
* canDislike - может ли текущий пользователь оставлять дислайки
* canComplain - может ли текущий пользователь жаловаться на комментарии
* splitLevel - начиная с какого уровня комментарии должны приходить плоским списком
* canDelete - может ли текущий пользователь удалять комментарии

На страницах, где отображаются комментарии разных сущностей, для каждой ветки набор действий может отличаться. Так на странице отзывов на магазин оставлять комментарии можно только в ветке, родителем которой явлеятся комментарий текущего пользователя.
На странице моих отзывов можно жаловаться только на комментарии к продуктам, так как нет админки для обработки жалоб на комментарии на магазин
