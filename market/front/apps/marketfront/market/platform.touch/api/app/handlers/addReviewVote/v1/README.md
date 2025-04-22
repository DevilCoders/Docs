# Резолвер addReviewVote

## Описание

Резолвер ставит лайк/дизлайк отзыву на продукт. Необходима авторизация.
В случае успеха отвечает пустым массивом.

## Входные параметры

    {
        reviewId: идентификатор отзыва,
        vote: тип оценки, 1 — лайк, -1 — дизлайк,
    }

Оба параметра обязательны.

## Ссылочки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/resolvers/review/index.js#L102-L105)
