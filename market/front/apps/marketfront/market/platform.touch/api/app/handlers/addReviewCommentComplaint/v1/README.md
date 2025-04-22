# Резолвер addReviewCommentComplaint

## Описание

Резолвер, который создает жалобу на комментарий к отзыву на товар.
Обязательные параметры:
- _reviewId_ - айдишник отзыва;
- _commentId_ - айдишник комментария;
- _reasonId_ - айдишник причины жалобы, возможные значеня:
  - 1 - Другое
  - 2 - Спам или реклама
  - 3 - Оскорбтельное высказывание
Необязательные параметры:
- _text_ - сообщение жалобы;

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addReviewCommentComplaint/v1/index.js#L23)
