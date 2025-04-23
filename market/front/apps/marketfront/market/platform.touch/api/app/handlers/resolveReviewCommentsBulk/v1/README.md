# Резолвер resolveReviewCommentsBulk

## Описание

Резолвер, который возвращает все комментарии на отзывы с авторами.
Обязательный параметр:
- _reviewIds_ - массив айдишников отзывов;

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveReviewCommentsBulk/v1/index.js#L20)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/commentary/commentary.json)
- [Описание сущности `комментарий` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/commentary/index.js)
