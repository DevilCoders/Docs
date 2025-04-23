# Резолвер resolvePostByIdsBulk

## Описание

Возвращает коллекцию постов по айдишникам

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `postIds` | array | Айди постов | - |

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolvePostByIdsBulk/v1/index.js)
- [Описание сущности `post` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/post/index.js)
