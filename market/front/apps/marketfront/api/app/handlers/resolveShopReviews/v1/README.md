# Резолвер resolveShopReviews

## Описание

Резолвер, возвращает отзывы на магазин дополненные информацией об авторах.
Умеет сортировать и фильтровать выдачу отзывов. Обязательный параметр - `shopId` или `businessId`.
### Доступные параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `shopId` | number | Айди магазина | - | - |
| `businessId` | number | Айди бизнеса | - | - |
| `pageNum` | number | Номер страницы | 0 | - |
| `pageSize` | number | Количество отзывов на странице | 10 | - |
| `sortBy` | строка | Поле для сортировке | date | date,grade,relevance,rank |
| `sortType` | строка | Направление сортировки | asc | asc, desc |
| `gradeValues` | массив | Фильтрация по оценкам | - | 1,2,3,4,5 |
| `withClone` | boolean | Клоны магазинов? | false | true, false |
| `firstReviewId` | number | Ид отзыва, который должен быть на первом месте | - | - |
| `addUserVote` | boolean | Нужно ли получать голоса на отзывы | true | true, false |

_Сущность user была переименована в publicUser._


- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/review/helperTypes.js#L11-L38)
- [Описание сущности `отзыв` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/review/index.js)

