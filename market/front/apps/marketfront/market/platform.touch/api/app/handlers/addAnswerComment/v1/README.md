# Резолвер addAnswerComment

## Описание

Резолвер, который создает комментарий на ответ. Необходима авторизация.
Возращает созданный комментарий.
Обязательные параметры:
- _answerId_ - айдишник ответа;
- _text_ - текст комментария;
Необязательные параметры:
- _fetchUserData_ - запрашивать ли информацию о юзере, оставившим комментарий, по умолчанию `true`;

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addAnswerComment/v1/index.js#L24)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/commentary/commentary.json)
- [Описание сущности `комментарий` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/commentary/index.js)
