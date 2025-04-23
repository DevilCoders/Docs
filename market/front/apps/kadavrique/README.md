Кадаврик (kadavr)
==========

## Index

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- *generated with [DocToc](https://github.com/thlorenz/doctoc)* -->

- [Description](#description)
- [Server](#server)
  - [Configuration](#configuration)
    - [Parameters](#parameters)
    - [Options overriding](#options-overriding)
  - [Router](#router)
  - [Logging](#logging)
  - [Errors workaround](#errors-workaround)
- [API](#api)
  - [Public Kadavr-API](#public-kadavr-api)
  - [Programming API](#programming-api)
  - [Mocks](#mocks)
    - [Mocks Routing](#mocks-routing)
    - [Mocks Creation](#mocks-creation)
- [Plugin](#plugin)
- [Debug Proxy](debug-proxy/README.md)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Description

Кадаврик представляет собой сервис для создания моков реальных бэкендов с целью обеспечения стабильного тестового окружения.\
Полное описание можно почитать на [wiki](https://wiki.yandex-team.ru/market/verstka/kadavrcookbook/)

## Server

Кадавр является [NodeJS http.Server](https://nodejs.org/dist/latest-v8.x/docs/api/http.html#http_class_http_server), который принимает и обрабатывает запросы к [API Кадавра](#kadavr-api) и [API Бекендов](#backends-api).

### Configuration

Для конфигурирования сервера используется [gemini-configparser](https://github.com/gemini-testing/configparser).

#### Parameters

- `{string} host`\
**Default:** `'::'`\
Хост или IP-адрес сервера.

- `{number} port`\
**Default:** `8089`\
Порт сервера.

- `{number} clientTimeout`\
**Default:** `10000`\
Время ожидания клиентского запроса к кадаврику.

- `{number} clientQueueTimeout`\
**Default:** `50`\
Время с момента, когда инициировался запрос.

- `{number} clientMaxRetries`\
**Default:** `2`\
Максимальное количество повторений запроса.

- `{number} clientMinRetriesTimeout`\
**Default:** `1000`\
Время в милисекундах перед первым повтором запроса, если опция `clientMaxRetries` больше 0.

- `{number} clientMaxRetriesTimeout`\
**Default:** `Infinity`\
Максимальное количество милисекунд между двумя повторами запроса.

- `{string} socket`\
**Default:** `''`\
Путь к сокету сервера.

- `{string} bodyLimit`\
**Default:** `'4MB'`\
Максимальный объем тела для запросов к API сервера.

- `{string} pageBlank`\
**Default:** `'/blank'`\
Путь до пустой страницы на сервисе.

- `{string} logLevel`\
**Default:** `'trace'`\
Уровень логирования.

- `{string} logFile`\
**Default:** `null`\
Путь, по которому логи будут сохраняться в файл.

- `{string} errorLogFile`\
**Default:** `null`\
Путь, по которому логи ошибок будут сохраняться в файл.

- `{string} errorBoosterLogFile`\
**Default:** `null`\
Путь, по которому логи для Error Booster'a будут сохраняться в файл.

- `{string} metricsLogFile`\
**Default:** `null`\
Путь, по которому будут сохраняться метрики.

- `{boolean} noSessionLog`\
**Default:** `false`\
Отключает логирование сессии.

- `{boolean} noAutoCreateSession`\
**Default:** `false`\
Отключает автоматическое создание сессии.

- `{number} sessionTtl`\
**Default:** `600000`\
Время жизни сессии.

- `{number} proxyTimeout`\
**Default:** `2000`\
Время ожидания запроса к бекенду.

- `{string} microformats`\
**Default:** путь до дирректории, в которой расположен `'microformats/package.json'`\
Директория микроформатов.

- `{string} microformatsRepo`\
**Default:** `'https://github.yandex-team.ru/raw/market/microformats/master/'`\
Путь до raw ветки репозитория с микроформатами.

- `{boolean} storeLogsInRedis`\
**Default:** `false`\
Хранить логи сессии в редисе.

#### Options overriding
Для указания значения параметра можно воспользоваться:
- CLI (посмотреть список опций можно, запустив его с аргументом `-h, --help`);
- переменными среды, префикс `kadavr_`;
- определить значение по умолчанию в [опциях](https://a.yandex-team.ru/arc_vcs/market/front/apps/kadavrique/options/index.js);
- переопределить значение по умолчанию в [парсере](https://a.yandex-team.ru/arc_vcs/market/front/apps/kadavrique/options/parser.js).

### Router

[Susanin](https://github.com/nodules/susanin).

Обработка запросов:
- если в запросе присутствуют непустые заголовки
```
'kadavr-session-id' - уникальный идентификатор сессии
'original-host' - хост оригинального запроса; используется для поиска мока либо для проксирования
'original-port' - порт оригинального запроса; используется при проксировании
'original-protocol' - протокол оригинального запроса; используется при проксировании
```
запрос направляется к [API Кадавра](#kadavr-api);
- иначе запрос направляется к [API Бекендов](#backends-api);

На уровне роутера осуществляется только первичная валидация запроса, дальнейшая обработка происходит на уровне соответствующего API.

### Logging

Для логирования используется [logger](https://a.yandex-team.ru/arc_vcs/market/front/monomarket/lib/lib/logger).

### Errors workaround

Для создания иерархии ошибок используется [BaseError](https://a.yandex-team.ru/arc_vcs/market/front/monomarket/lib/lib/error).

Для того, чтобы проксировать запрос в реальный бэкенд из мока необходимо выбросить ошибку `MethodNotImplemented`, либо отнаследованную от нее

## API

### Public Kadavr-API

Kadavr предоставляет [API](https://a.yandex-team.ru/arc_vcs/market/front/apps/kadavrique/options/route.js) для работы с пользовательскими сессиями

- `PUT /session/<id>`\
Создание сессии.

- `DELETE /session/<id>`\
Удаление сессии и всей связанной с ней информацией (стейт, логи).

- `HEAD /session/<id>`\
Проверка существования сессии.

- `POST /session/<id>/state/<path>`\
Присваивает по указанному пути `path` данные, переданные в теле запроса.

- `GET /session/<id>/log?path=<path>`\
`path` путь в объекте лога, данные откуда нужно получить;\
Получение лога запросов/ответов сессии.

- `GET /ping`\
Пинг сервера кадавра.

### Programming API

Программное API можно посмотреть [здесь](https://a.yandex-team.ru/arc_vcs/market/front/apps/kadavrique/lib/api.js)

- `createSession` создание новой сессии:\
**Параметры:**\
`{string} id` идентификатор сессии;\
**Возвращает:** `{Session}` экземпляр сессии.

- `deleteSession` удаление сессии:\
**Параметры:**\
`{string} id` идентификатор сессии;\
**Возвращает:** `{string}` идентификатор удаленной сессии.

- `getSession` получение существующей сессии:\
**Параметры:**\
`{string} id` идентификатор сессии;\
**Возвращает:** `{Session}` экземпляр сессии.

- `hasSession` проверка существования сессии:\
**Параметры:**\
`{string} id` идентификатор сессии;\
**Возвращает:** `true` если сессия с заданным `id` существует, иначе `false`.

- `setState` запись данных в стейт сессии:\
**Параметры:**\
`{string} id` идентификатор сессии;\
`{string} path` путь в объекте стейта, куда будет установлено значение;\
`{Object} data` данные для добавления в стейт;\
**Возвращает:** `true` если сессия с заданным `id` существует, иначе `false`.

- `getLog` получение данных из лога сессии:\
**Параметры:**\
`{string} id` идентификатор сессии;\
`{string} [path]` путь в объекте лога, данные откуда нужно получить;\
**Возвращает:** `{Object}` данные из лога сессии, расположенные по указанному пути; в случае, если `path` не указан вернет весь лог сессии.

### Mocks

#### Mocks Routing

Для работы с моками необходимо существование сессии с id, соответствующим пришедшему в заголовке запроса `kadavr-session-id`;\
По-умолчанию (в т.ч. в рантайме) кадавр сам создаст сессию, в случае если соотв. заголовок запроса проставлен. Отключить такое поведение можно опцией `noAutoCreateSession`

В случае отсутствия реализации мока целиком или отдельного метода, запрос будет [проксирован](https://github.com/nodejitsu/node-http-proxy#node-http-proxy--) на реальный бэкенд.

#### Mocks Creation

Для создания мока для нового бэкенда (или добавления метода к существующему) необходимо:
1. Добавить реализацию [сюда](https://a.yandex-team.ru/arc_vcs/market/front/apps/kadavrique/mocks).
2. Добавить роут в [соответствующий конфиг](https://a.yandex-team.ru/arc_vcs/market/front/apps/kadavrique/options/mocks.js)
    - `{Object} class` класс с реализацией;
    - `{array} hosts` список хостов;
    - `{array} routes` список роутов для [Susanin](https://github.com/nodules/susanin);
      - `{Object} routes.requiredConditions` дополнительное свойство аналогичное conditions, делающее обязательным наличие указанных параметров (включая квери параметры);
3. Добавить юниттесты на реализованные методы в [/spec](https://a.yandex-team.ru/arc_vcs/market/front/apps/kadavrique/spec).

## Plugin

### Hermione

[Плагин](https://a.yandex-team.ru/arc_vcs/market/front/apps/kadavrique/plugin) для [hermione](https://github.com/gemini-testing/hermione/), предназначенный для работы с сервисом кадавра, а так же для управления состоянием текущей сессии

Для запуска тестов, использующих кадавр, нужно:
- указать у теста `environment: 'kadavr'`;
- указать значение для переменной окружения `KADAVR` (установлена по-умолчанию в [genisys-конфиге](https://genisys.yandex-team.ru/rules/sandbox-ci-market/sandbox_clients));

Функции плагина:
- в `beforeEach` теста происходит создание сессии и добавление соответствующей куки в браузер;
- после каждого теста происходит удаление сессии из кадавра;
- добавляет в контекст браузера свойста:
  - `setState` функция для изменения состояния сессии
  `{string} path` путь в объекте стейта, куда будет установлено значение;
  `{Object} data` данные для добавления в стейт;
  - `getLog` функция для получения логов запросов/ответов (в т.ч. проксированных)
  `{string} path` путь в объекте стейта, куда будет установлено значение;
  - `getKadavrSessionID` id сессии кадавра, созданной перед запуском теста.


### Gemini

Для запуска тестов, использующих кадавр, нужно указать значение для переменной окружения `KADAVR`

Функции плагина:
- `createSession` создать сессию кадавра, (использовать перед запуском теста в `before`).
- `setState` функция для изменения состояния сессии
  `{string} path` путь в объекте стейта, куда будет установлено значение;
  `{Object} data` данные для добавления в стейт;
- `getLog` функция для получения логов запросов/ответов (в т.ч. проксированных)
  `{string} path` путь в объекте стейта, куда будет установлено значение;
- `deleleSession` удалить сессию кадавра, (использовать после запуска теста в `after`).

Пример:

```js
// spec/gemini/test-suites/pages/main/index.gemini.js

module.exports = {
    suiteName: 'Main',
    selector: 'main',
    before(actions) {
        createSession.call(actions);
        setState.call(actions, path, data);
    },
    after(actions) {
        deleteSession.call(actions);
    },
    capture() {},
};
```
