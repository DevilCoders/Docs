[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/monomarket&vcs=github&repoFilter=lib/lib/stout)](https://oko.yandex-team.ru/github/market/monomarket?repoFilter=lib/lib/stout) [![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-market/stout)](https://oko.yandex-team.ru/pkg/@yandex-market/stout)

[![Build Status](https://jenkins.yandex-team.ru/buildStatus/icon?job=market-frontend-stout-unit-tests)](https://jenkins.yandex-team.ru/view/Market-Frontend/job/market-frontend-stout-unit-tests/)

Stout
======

**Stout** - высокоуровневый объектно-ориентированый фреймворк для создания web-приложений на платформе [NodeJS](https://nodejs.org).

- [Hello, world!](#hello-world)
- [Архитектура](#Архитектура)
  - [Схема зависимостей компонент](#Схема-зависимостей-компонент)
  - [Обработка запроса](#Обработка-запроса)

### Hello, world!

**Файловая структура приложения:**
```
/
 - start.js - стартовый скрипт приложения
 - pages - директория страниц
 | - Index.js - контроллер страницы
```
 
**Файл `pages/Index.js`:**
```javascript
var stout = require('stout');

// Базовый контроллер, на основе которого будет создана страница
var Page = stout.getPage();

// Контроллер страницы
function Index() {
  // Обработка запроса, формирование ответа
  this.write('Hello, world!');
}

// Инициализация контроллера и экспорт
module.exports = Page.create(Index);
```

**Файл `start.js`:**
```javascript
var stout = require('stout');

stout
  .on(stout.EVENT_UNCAUGHT_EXCEPTION, function (error) {
      error.log();
  })
  // Загрузка страниц
  .loadPages('pages')
  
  // Создание роутера
  .createRouter([{
    name: 'Index', // Уникальное имя роута
    pattern: '/', // URL страницы
    data: {
      method: 'GET',
      pageName: 'Index', // Имя страницы
      pageData: { // Данные страницы
        timeout: 20000 // Таймаут для страницы. Значение по умолчанию 10000
      }
    }
  }])
  
  // Создание и запуск сервера
  .createServer({
    port: 1337
  });
```

**Запуск приложения из корня проекта:**
```
> node start.js
```

### Архитектура

Инициализация и доступ к компонентам фреймворка осуществляется через единую точку входа - объект [stout](docs/api/stout.md).
Бизнес-логика приложения строится в императивном стиле с помощью высокоуровневых объектов [Page](docs/api/Page.md).
Объект `Page` представляет собой очередь задач, которая выполняется на каждый запрос пользователя.
В качестве задачи могут выступать объекты [Response](https://github.com/B-Vladi/Response), [виджеты](docs/api/Widget.md), функции, [middleware-ы](docs/api/Page.md), а так же любые другие пользовательские объекты.

**Компоненты `Stout`:**

 * [stout](docs/api/stout.md) - входная точка, предоставляющая API к остальным компонентам фреймворка
 * [HTTPServer](docs/api/HTTPServer.md) (+ [Request](docs/api/Request.md)) - обработка входящих http-запросов клиента
 * [Router](docs/api/Router.md) - обертка над [Susanin](https://github.com/nodules/susanin)
 * [Page](docs/api/Page.md) - контроллер запроса
 * [Widget](docs/api/Widget.md) - самостоятельная, повторно используемая часть логики, не зависящая от места вызова

**Внешние компоненты:**

 * [Response](https://github.com/B-Vladi/Response) - реализация состояний, очередь
 * [EventEmitter](https://github.com/B-Vladi/EventEmitter) - расширенная реализация событийной модели, совместимая с нативным объектом [EventEmitter](https://nodejs.org/api/events.html#events_class_events_eventemitter)
 * [Susanin](https://github.com/nodules/susanin) - кросс-платформенная система роутинга
 * [HTTPStatus](https://github.com/B-Vladi/HTTPStatus) - список HTTP кодов и их описаний


#### Схема зависимостей компонент
![components](docs/images/components.png)

#### Обработка запроса
![session](docs/images/session.png)

**Описание:**
  1. NodeJS принимает запрос пользователя,
  2. и передает его [серверу](docs/api/stout.md#server).
  3. Сервер создает экземпляр объекта [request](docs/api/Request.md),
  4. и генерирует событие "[request](docs/api/HTTPServer.md#EVENT_REQUEST)", которое обрабатывает [stout](docs/api/stout.md).
  5. На основе данных запроса, [роутер](docs/api/stout.md#router) осуществляет поиск страницы,
  6. и возвращает её имя.
  7. Stout [создает экземпляр страницы](docs/api/Base.md#make) и запускает последовательное выполнение конструкторов из цепочки наследования.
  8. Во время выполнения конструкторов, в очередь страницы добавляются задачи,
  9. например, [виджеты](docs/api/Widget.md).
  10. После выполнения всех конструкторов,
  11. очередь запускается на выполнение, последовательно обходя все добавленные задачи.
  12. В это время виджеты выполняют основную работу
  13. используя API приложения,
  14. которое возвращает данные и выполняет другие полезые функции.
  15. Результаты вычислений обрабатываются и агрегируются в виджетах.
  16. По результатам работы виджет принимает одно из состояний: `resolve` (успешно) или `reject` (ошибка).
  17. По окончании работы всех задач страница выполняет пост-обработку полученных данных от задач и
  18. принимает одно из состояний: `resolve` или `reject`.
  19. Stout реагирует на изменение состояния страницы и закрывает соединение, передавая в тело ответа результат работы страницы.
  20. Сервер закрывает соединение, и
  21. возвращает ответ пользователю.
