# Резолвер addPostByInterest

## Описание

Резолвер загружает в persQa пост, привязанный к интересу.
Для авторизованного пользователя

В ответе приходит пост.

## Параметры

| Parameter | Type | Description | Default |
|---------------|----------|------------------|------------------|
| `interestId` | number | Айди интереса (обязательно) | - |
| `title` | string |  Заголовок поста (обязательно) | - |
| `text` | string |  Текст поста, максимум 80 символов (обязательно) | - |
| `photos` | array |  Фотографии к посту | [] |
| `productIds` | array | Массив айди товаров, к которым может относиться пост | [] |

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addPostByInterest/v1/index.js)
- [Описание сущности `post` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/post/index.js)
