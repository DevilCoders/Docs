# Резолвер resolveQuestionsByProductId

## Описание

Резолвер, способный вернуть вопросы на продукт вместе с пользователями, которые их оставили.
А также с информацией о первом/лучшем ответе и его авторе.
Обязательный параметр:
- _productId_ - айдишник товара;
Необязательные параметры:
- _pageNum_ - номер страницы, для пейджера;
- _pageSize_ - количество элементов на странице, для пейджера;
- _clid_ - id места показа ссылки на внешних ресурсах

_Сущность user была переименована в publicUser. Для обеспечения обратной совместимости отправляются 2 коллекции - в старом и новом формате. В новом коде предпочтительно использовать новое имя сущности и коллекции, т.е publicUser. По возможности в старом коде также желательно выполнить миграцию._

Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveQuestionsByProductId/v1/index.js#L20)
- [Микроформат сущности](https://github.yandex-team.ru/market/microformats/blob/master/question/question.json)
- [Описание сущности `вопрос` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/entities/question/index.js)
