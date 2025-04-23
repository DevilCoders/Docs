# Резолвер removeUgcVideoVote

## Описание

Резолвер, который позволяет добавить или заменить лайк/дизлайк на видео.
В случае успеха отвечает объектом с полями result (пустой массив) и collections (пустой объект).

| Parameter | Type | Description | Default | Value |
| ----------- | -------- | ----------------------- | ----- | ----- |
| `videoId` | UgcVideoId | Ид отзыва | - | - |
| `vote` | number | -1 dislike, 1 like | - | -1, 1 |

Ссылочки:

- [persQA's Swagger](http://pers-qa.tst.vs.market.yandex.net/swagger-ui.html@self/platform/vote-controller/createVideoVoteUsingPOST)
- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/api/app/handlers/addUgcVideoVote/v1/index.js#L20)
