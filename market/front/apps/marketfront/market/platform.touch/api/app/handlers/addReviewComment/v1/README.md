# Резолвер addReviewComment

## Описание

Резолвер, который создает комментарий на отзыв. Необходима авторизация.
Можно отвечать на другие комментарии, таким образом создавать "дерево" комментариев. Комментарий, на который ответ, определяется параметром parentId.
Возращает созданный комментарий с автором.
Обязательные параметры:
- _reviewId_ - айдишник отзыва;
- _text_ - текст комментария;
Необязательные параметры:
- _parentId_ - айдишник комментария, на который "ответ";

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addReviewComment/v1/index.js#L24)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/commentary/commentary.json)
- [Описание сущности `комментарий` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/commentary/index.js)
