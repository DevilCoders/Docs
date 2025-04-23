# Контроллеры

## Назначение

Контроллеры отвечают за принятие и обработку запросов от браузера. В их задачи входит:

-   определение типа запроса - GET/POST/PUT/DELETE/etc (декоратор `@requestMethod('GET')`)
-   логирование запроса от браузера (декоратор `@logAction`)
-   чтение данных из объекта `req` (req.query, req.data)
-   вызов и передача параметров в нужный метод сервиса
-   валидация параметров
-   обработка ответа

**❗IMPORTANT❗**: В контроллерах не должно быть бизнес логики, за это отвечает слой сервисов `server/services/`

## Общие подходы

-   для определения типа запроса используется декоратор `@requestMethod('GET')`
-   для обработки ответа используются общие утилиты `handleResponse`, `handleError`

Каждому методу контроллера соотвествует 1 метод сервиса (см. про api архитектуру в [browser-http-client](../../docs/browser-http-client.md))

## Структура и нейминг

В каждой директории папки /controllers/ находится:

-   файл `index.ts`, в котором:
    -   реализуется общая для всех контроллеров обвязка `makeProxyInvoker` (необходимая для DI);
    -   определяется соответствие методов контроллеров внешнему роутингу запроса;
-   один или набор классов, которые имплементируют обработку запросов.

В примере ниже метод `getValue` контроллера `Controller` будет вызываться при запросе `<prefix>/firstPathFragment/secondPathFragment/`

```ts
import makeProxyInvoker from 'server/utilities/makeProxyInvoker';

import {Controller} from './Controller';

const controllerInstanse = makeProxyInvoker(Controller);

export default {
    firstPathFragment: {
        secondPathFragment: controller.getValue,
    },
};
```
