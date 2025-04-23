# Резолвер addProductQuestion

## Описание

Резолвер, который создает вопрос на товар. Необходима авторизация.
Возращает созданный вопрос.
Обязательные параметры:
- _productId_ - айдишник товара;
- _text_ - текст вопроса;
Необязательные параметры:
- _questionSource_ - место, где задали вопрос. По умолчанию будет main. Необходимо для формирования поля источник у вопроса, по умолчанию будет выглядеть примерно так: _market;app;main;_
- _fetchUserData_ - запрашивать ли информацию о юзере, создавшим вопрос, по умолчанию `true`;
- _clid_ - id места показа ссылки на внешних ресурсах

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addProductQuestion/v1/index.js#L25)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/question/question.json)
- [Описание сущности `вопрос` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/question/index.js)
