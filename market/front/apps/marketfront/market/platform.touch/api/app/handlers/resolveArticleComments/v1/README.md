# Резолвер resolveArticleComments

## Описание

Резолвер, который возвращает комментарии на статью с авторами.
Обязательный параметр:

| Parameter | Type | Description | Default | Value |
| ----------- | -------- | ----------------------- | ----- | ----- |
| `articleId` | number | Ид статьи | - | - |
| `parentId` | number | Ид родительского комментария, либо не задан | - | - |
| `limit` | number | Количество комментариев, от 1 до 100. Необязательный параметр. | 100 | - |
| `splitLevel` | number | Уровень, начиная с которого комментарии приходят плоским списком. Необязательный параметр. | 1 | - |
| `borderId` | number | Ид комментария, начиная с которого выдать очередную партию комментариев, либо не задан. | - | - |

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/api/app/handlers/resolveArticleComments/v1/index.js#L35)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/commentary/commentary.json)
- [Описание сущности `комментарий` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/commentary/index.js)
