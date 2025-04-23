# Резолвер resolveAnswers

## Описание

Возвращает все ответы на вопрос с авторами и пагинатором.
Обязательный параметр:
- _questionId_ - айдишник вопроса;
Необязательные параметры:
- _pageNum_ - номер страницы, для пейджера;
- _pageSize_ - количество элементов на странице, для пейджера;

**WARNING**: пагинатор приходит в result, а не в коллекциях.

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveAnswers/v1/index.js#L20)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/answer/answer.json)
- [Описание сущности `комментарий` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/answer/v1/index.js)
