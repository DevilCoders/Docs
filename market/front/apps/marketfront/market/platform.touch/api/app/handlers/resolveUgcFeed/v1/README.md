# Резолвер resolveUgcFeed

## Описание

Резолвер, который позволяет получить персонализированную ленту пользовательского контента.
Лента состоит из отзывов, вопросов и статей.
В ответе приходят дополнительные данные: связанные товары, ответы, комментарии, юзеры, магазины и вендоры.
Работает с бэкэндом `dj-recommender`.

## Параметры из body запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `useDj` | boolean | ~~Использовать ли dj-ранжировщик~~ Если передано любое значение, `true` или `false`, то идем в dj. | `undefined` | - |
| `experiment` | string | Эксперимент dj-ранжировщика | `market_app_ugc_feed` | - |
| `articles` | number[] | Массив айдишников рекомендованных статей в рамках сессии | `[]` | - |
| `reviews` | number[] | Массив айдишников рекомендованных отзывов в рамках сессии | `[]` | - |
| `questions` | number[] | Массив айдишников рекомендованных вопросов в рамках сессии | `[]` | - |
| `ugcVideos` | number[] | Массив айдишников рекомендованных видео в рамках сессии | `[]` | - |
| `interests` | number[] | Массив интересов для фильтрации в ленте | все интересы | - |
| `posts` | number[] | Массив айдишников рекомендованных постов в рамках сессии | `[]` | - |
| `pageNum` | number | Номер страницы выдачи, нужно для генерации пейджера | - | - |
| `pageSize` | number | Количество элементов на одной странице выдачи, нужно для генерации пейджера | - | - |

## Параметры из query запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `deviceId` | string | Идентификатор устройства | - | - |
| `idfa` | string | Рекламный идентификатор для iOS | - | - |
| `gaid` | string | Рекламный идентификатор для Android | - | - |
| `uuid` | string | Идентификатор установки приложения | - | - |

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveUgcFeed/v1/index.js#L21)
- [Описание сущности `отзыв` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/review/v1/index.js)
- [Описание сущности `вопрос` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/question/v1/index.js)
- [Описание сущности `статья для ленты` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/feedArticle/index.js)
- [Описание сущности `интерес` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/interest/index.js)
- [Описание сущности `ugc-видео` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/ugcVideo/index.js)
- [Описание сущности `пост` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/post/index.js)
