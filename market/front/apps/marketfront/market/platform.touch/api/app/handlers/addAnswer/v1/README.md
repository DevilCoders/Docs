# Резолвер addAnswer

## Описание

Резолвер, который создает пользовательский ответ на вопрос. Необходима авторизация.
Возращает созданный ответ.
Обязательные параметры:
- _questionId_ - айдишник вопрос, на который отвечаем;
- _text_ - текст ответа;
Необязательный параметр:
- _answerSource_ - место, где ответили. По умолчанию будет main. Необходимо для формирования поля источник у ответа, по умолчанию будет выглядеть примерно так: _market;app;main;_

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addAnswer/v1/index.js#L25)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/questionAnswer/questionAnswer.json)
- [Описание сущности `ответ` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/answer/v1/index.js)
