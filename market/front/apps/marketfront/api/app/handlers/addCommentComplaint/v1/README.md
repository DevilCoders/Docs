# Резолвер addCommentComplaint

## Описание

Универсальный метод, который создает жалобу на любой комментарий (кроме комментариев на отзыв, это в перспективе тоже будет).

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `commentId`* | number | Айди комментария | - | - |
| `entity`* | string | Идентификатор сущности, к которой оставлен комментарий | - | [`'articleComment'`, `'answerComment'`, `'postComment'`, `'versusComment'`, `'productReviewComment'`, `'shopReviewComment'`] |
| `reasonId`* | number |  Идентификатор причины жалобы | - | [`1` (Другое), `2` (Спам или реклама), `3` (Оскорбительный контент)] |
| `text` | string| Текст жалобы (Обязательно для причины `1`) | `''` | - |

\* - обязательный параметр

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/addCommentComplaint/v1/index.js)
