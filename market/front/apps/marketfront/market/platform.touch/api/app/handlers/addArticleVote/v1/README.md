# Резолвер addArticleVote

## Описание

Резолвер, который позволяет оставить лайк/дизлайк журнальной статье. Необходима авторизация.
В случае успеха отвечает пустым массивом.
Обязательные параметры:
- _articleId_ - айдишник статьи;
- _vote_ - голос юзера, значения: 1 (лайк) и -1 (дизлайк);

Ссылочки:

- [pers-qa's Swagger](http://pers-qa.tst.vs.market.yandex.net/swagger-ui.html@self/platform/vote-controller/createArticleVoteUsingPOST)
- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addArticleVote/v1/index.js#L20)
