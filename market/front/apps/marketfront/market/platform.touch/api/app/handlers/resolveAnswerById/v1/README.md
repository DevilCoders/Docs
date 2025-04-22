# Резолвер resolveAnswerById

## Описание

Возвращает ответ по айдишнику на вопрос с автором.
Обязательный параметр:
- _answerId_ - айдишник ответа;

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveAnswers/v1/index.js#L20)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/answer/answer.json)
- [Описание сущности `комментарий` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/answer/v1/index.js)
