# Резолвер addQuestionSubscription

## Описание

Резолвер, который позволяет подписаться на новые ответы на вопрос.
Если подписка уже существует, то отвечает существующей подпиской.
Необходима авторизация. Подписка происходит на дефолтный email текущего юзера.

Обязательный параметр:
- _questionId_ - айдишник вопроса;

Необязательный параметр:
- _place_ - место где юзер запросил подписку, по умолачнию `question_page`;

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addQuestionSubscription/v1/index.js#L20)
- [Описание сущности `подписка` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/subscription/index.js)
