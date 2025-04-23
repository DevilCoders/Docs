# Резолвер resolveQuestionById

## Описание

Резолвер, который возвращает вопрос с автором по айдишнику.
Обязательный параметр:
- _questionId_ - айдишник вопроса;
Необязательные параметры:
- _fetchSubscriptions_ - получать ли информацию о подписках, по умолчанию - `false`;

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveQuestionById/v2/index.js#L20)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/question/question.json)
- [Описание сущности `вопрос` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/question/index.js)
