stout
=====
Публичный интерфейс stout, экземпляр [EventEmitter](https://github.com/B-Vladi/EventEmitter):

```javascript
var stout = require('stout');
stout.emit('Stout is ready!');
```
API `stout` включает в себя:

- [HTTP-сервер](#http-сервер):
  - [server](#server)
  - [HTTPServer](#HTTPServer)
  - [createServer(options)](#createServer)
  - [stopServer()](#stopServer)
- [Роутер](#Роутер):
  - [Router](#Router)
  - [router](#router)
  - [createRouter(routes)](#createRouter)
- [Базовые сущности приложения](#Базовые-сущности-приложения):
  - [cwd](#cwd)
  - [Page](#Page)
  - [Widget](#Widget)
  - [loadPages(path)](#loadPages)
  - [loadWidgets(path)](#loadWidgets)
  - [loadMiddlewares(path)](#loadMiddlewares)
  - [getPage(name)](#getPage)
  - [getWidget(name)](#getWidget)
  - [getMiddleware(name)](#getMiddleware)
- [Логирование](#Логирование):
  - [log(message, level)](#log)
  - [setLogger(logger)](#setLogger)
  - [logger(message, level)](#logger)
  - [logger.LOG_FORMAT](#LOG_FORMAT)
  - [logger.LOG_DEFAULT](#LOG_DEFAULT)
  - [logger.LOG_TRACE](#LOG_TRACE)
  - [logger.LOG_DEBUG](#LOG_DEBUG)
  - [logger.LOG_INFO](#LOG_INFO)
  - [logger.LOG_WARNING](#LOG_WARNING)
  - [logger.LOG_ERROR](#LOG_ERROR)
- [Интерфейс ошибок](#Интерфейс-ошибок):
  - [setErrorLogger(logger)](#setErrorLogger)
  - [Error](#Error)
  - [Error.CODES.ERROR_LOADING_MODULE](#ERROR_LOADING_MODULE)
  - [Error.CODES.MODULE_NOT_FOUND](#MODULE_NOT_FOUND)
  - [Error.CODES.INVALID_EXPORTS](#INVALID_EXPORTS)
  - [Error.CODES.UNCAUGHT_EXCEPTION](#UNCAUGHT_EXCEPTION)
  - [Error.CODES.INTERNAL_PAGE_ERROR](#INTERNAL_PAGE_ERROR)
  - [Error.CODES.INVALID_LOGGER_TYPE](#INVALID_LOGGER_TYPE)
  - [Error.CODES.INVALID_ROUTE_MAPPER_TYPE](#INVALID_ROUTE_MAPPER_TYPE)
- [Пользовательские данные](#Пользовательские-данные):
  - [data](#data)
  - [get(key)](#get)
  - [set(key, data)](#set)
- [События](#События):
  - [EVENT_UNCAUGHT_EXCEPTION](#EVENT_UNCAUGHT_EXCEPTION)
  - [EVENT_PAGE_NOT_FOUND](#EVENT_PAGE_NOT_FOUND)
  - [EVENT_INTERNAL_PAGE_ERROR](#EVENT_INTERNAL_PAGE_ERROR)

###[HTTP-сервер](HTTPServer.md)
API позволяет создавать и управлять HTTP-сервером фреймворка,
а так же связывает его с другими компонентами, обеспечивая их взаимодействие между собой.
Для корректной работы сервера необходимо создать объект [роутера](#Роутер).

#### <a name="server" />{HTTPServer} stout.server = null ####
Экземпляр [HTTPServer](HTTPServer.md), созданный методом [stout.createServer](#createServer).
___

#### <a name="HTTPServer" />{Function} stout.HTTPServer ####
Конструктор [HTTPServer](HTTPServer.md).
___

#### <a name="createServer" />{HTTPServer} stout.createServer(options) ####
Создает и запускает экземпляр [HTTPServer](HTTPServer.md).
После создания сервера все клиентские запросы, которые принимаются сервером,
автоматически проходят через [роутер](#Роутер) и передаются на обработку соответствующей странице.
Этот метод позволяет создавать несколько экземпляров серверов,
но в свойстве [stout.server](#server) будет храниться последний созданный из них.

**Параметры:**
<br />`{String|Object} options` - опции запуска сервера:
- строка воспринимается как [путь к UNIX-сокету](https://nodejs.org/api/http.html#http_server_listen_path_callback).
- если `options` - объект и он содержит свойство `port`, сервер будет слушать [HTTP-сокет](https://nodejs.org/api/http.html#http_server_listen_port_hostname_backlog_callback). Объект может содержать ключи `port`, `host` и `backlog`.
- объект `options` без свойства `port` [воспринимается как stream](https://nodejs.org/api/http.html#http_server_listen_handle_callback).

```javascript
stout
  .createServer({
    port: 1337
    host: 'localhost'
  })
  .then(function () {
    stout.log('Stout server is created!');
  }, function (error) {
    stout.log('Failed create stout server! Reason: ' + error.getFullMessage());
  });
```
___

#### <a name="stopServer" />{Response} stout.stopServer() ####
[Останавливает](https://nodejs.org/api/http.html#http_server_close_callback) [http-сервер](HTTPServer.md#stop)
и удаляет его связи с другими компонентами фреймворка.
Если было создано несколько экземпляров серверов, метод остановит последний созданый из них.

```javascript
stout
  .stopServer()
  .then(function () {
    stout.log('Stout server is stopped!');
  }, function (error) {
    stout.log('Failed stop stout server! Reason: ' + error.getFullMessage());
  });
```
___

### [Роутер](Router.md)
API позволяет создать роутер и получить к нему доступ.
Роутер необходим для корректной работы [http-сервера](HTTPServer.md).

#### <a name="Router" />{Function} stout.Router ####
Конструктор [роутера](Router.md).
___

#### <a name="router" />{Router} stout.router = null ####
Экземпляр [Router](Router.md), созданный методом [stout.createRouter](#createRouter).
___

#### <a name="createRouter" />stout.createRouter(routes) ####
Создает экземпляр роутера [stout.router](router).

**Параметры:**
<br />`{Array} routes` - Массив [объектов](https://github.com/nodules/susanin), описывающих правила роутинга.
___

### Базовые сущности приложения
API предназначено для создания компонентов бизнес-логики вашего приложения в виде высокоуровневых сущностей:
страниц, виджетов и middleware-ов.
Для того, что бы stout мог автоматически перенаправлять пользовательские запросы на выполнение страницам и виджетам,
их необходимо загрузить в кеш фреймворка с помощью соответствующих методов.

#### <a name="cwd" />{String} stout.cwd ####
Текущая рабочая директория, из которой было запущено приложение.
По-умолчанию соответствует [process.cwd()](https://nodejs.org/api/process.html#process_process_cwd).
Относительно этого пути происходит поиск модулей в методах [stout.loadPages](#loadPages), [stout.loadWidgets](#loadWidgets) и [stout.loadMiddlewares](#loadMiddlewares).
___

#### <a name="Page" />{Function} stout.Page ####
Конструктор [страницы](Page.mg).
___

#### <a name="Widget" />{Function} stout.Widget ####
Конструктор [виджета](Widget.mg).
___

#### <a name="loadPages" />{stout} stout.loadPages(path) ####
Загружает страницы в кеш из указанной директории.
Страница является [модулем](https://nodejs.org/api/modules.html), поэтому все директории в `path` воспринимаются как модули.

**Параметры:**
<br />`{String|Array} path` - путь к корневой папке страниц или массив путей.

**Исключения:**
<br />`{stout.Error}` - [MODULE_NOT_FOUND](#MODULE_NOT_FOUND), [ERROR_LOADING_MODULE](#ERROR_LOADING_MODULE), [INVALID_EXPORTS](#INVALID_EXPORTS).
___

#### <a name="loadWidgets" />{stout} stout.loadWidgets(path) ####
Загружает виджеты в кеш из указанной директории.

**Параметры:**
<br />`{String} path` - путь к корневой папке виджетов или массив путей.

**Исключения:**
<br />`{stout.Error}` - [MODULE_NOT_FOUND](#MODULE_NOT_FOUND), [ERROR_LOADING_MODULE](#ERROR_LOADING_MODULE), [INVALID_EXPORTS](#INVALID_EXPORTS).
___

#### <a name="loadMiddlewares" />{stout} stout.loadMiddlewares(path) ####
Загружает middleware-ы в кеш из указанной директории.

**Параметры:**
<br />`{String} path` - путь к корневой папке middleware-ов или массив путей.

**Исключения:**
<br />`{stout.Error}` - [MODULE_NOT_FOUND](#MODULE_NOT_FOUND), [ERROR_LOADING_MODULE](#ERROR_LOADING_MODULE), [INVALID_EXPORTS](#INVALID_EXPORTS).
___

#### <a name="getPage" />{Function} stout.getPage([name]) ####
Возвращает конструктор страницы из кеша.

**Параметры:**
<br />`{String} [name]` - имя страницы. Если имя не было передано, будет возвращен конструктор [Page](#Page).

**Исключения:**
<br />`{stout.Error}` - [MODULE_NOT_FOUND](#MODULE_NOT_FOUND), [ERROR_LOADING_MODULE](#ERROR_LOADING_MODULE), [INVALID_EXPORTS](#INVALID_EXPORTS).
___

#### <a name="getWidget" />{Function} stout.getWidget([name]) ####
Возвращает конструктор виджета из кеша.

**Параметры:**
<br />`{String} [name]` - имя виджета. Если имя не было передано, будет возвращен конструктор [Widget](#Widget).

**Исключения:**
<br />`{stout.Error}` - [MODULE_NOT_FOUND](#MODULE_NOT_FOUND), [ERROR_LOADING_MODULE](#ERROR_LOADING_MODULE), [INVALID_EXPORTS](#INVALID_EXPORTS).
___

#### <a name="getMiddleware" />{Function} stout.getMiddleware(name) ####
Возвращает middleware из кеша.

**Параметры:**
<br />`{String} name` - имя middleware.

**Исключения:**
<br />`{stout.Error}` - [MODULE_NOT_FOUND](#MODULE_NOT_FOUND), [ERROR_LOADING_MODULE](#ERROR_LOADING_MODULE), [INVALID_EXPORTS](#INVALID_EXPORTS).
___

### Логирование
#### <a name="LOG_FORMAT" />{String, const} stout.LOG_FORMAT = 'STOUT:\t%s' ####
Формат вывода логов, используемый [стандартным логером](#logger).

#### <a name="LOG_DEFAULT" />{String, const} stout.LOG_DEFAULT = 'log' ####
Уровень логирования по-умолчанию для [стандартного логера](#logger).
___

#### <a name="LOG_TRACE" />{String, const} stout.LOG_TRACE = 'trace' ####
Уровень логирования `trace`.
___

#### <a name="LOG_DEBUG" />{String, const} stout.LOG_DEBUG = 'debug' ####
Уровень логирования `debug`.
___

#### <a name="LOG_INFO" />{String, const} stout.LOG_INFO = 'info' ####
Уровень логирования `info`.
___

#### <a name="LOG_WARNING" />{String, const} stout.LOG_WARNING = 'warn' ####
Уровень логирования `warn`.
___

#### <a name="LOG_ERROR" />{String, const} stout.LOG_ERROR = 'error' ####
Уровень логирования `error`.
___

#### <a name="log" />{stout} stout.log(message [,level=stout.LOG_DEFAULT]) ####
Логирует сообщение с использование установленного [логера](#logger).

**Параметры:**
Идентичны параметрам [стандартного логера](#logger).
___

#### <a name="setLogger" />{stout} stout.setLogger(logger) ####
Устанавливает новый [логер](#logger).

**Параметры:**
<br />`{Function} logger` - новая функция-логгер. Функции передаются те же параметры, что и в [stout.log](#log).

**Исключения:**
<br />`{stout.Error}` - [INVALID_LOGGER_TYPE](#INVALID_LOGGER_TYPE)
___

#### <a name="logger" />{Function, private} stout.logger ####
Стандартный метод вывода сообщений в лог с использованием нативного объекта `console`.
Параметр `level` указывает на метод объекта `console`, который должен быть вызван.
Сообщения форматируются по маске [stout.LOG_FORMAT](#LOG_FORMAT).

**Параметры:**
<br />`{String} message` - логируемое сообщение.
<br />`{String} level` - уровень логирования: `log`, `trace`, `debug`, `info`, `warn`, `error`.
___

### Интерфейс ошибок
#### <a name="Error" />{Function} stout.Error ####
Конструктор объектов ошибок, используемых в stout.
Наследует от [Terror](https://github.com/nodules/terror).
В качестве логера для экземпляров используется метод [stout.log](#log).

В конструкторе определены следующие коды ошибок:
- <a name="ERROR_LOADING_MODULE" />**ERROR_LOADING_MODULE**: ошибка загрузки модуля базового ресурса
- <a name="MODULE_NOT_FOUND" />**MODULE_NOT_FOUND**: модуль базового ресурса не найден
- <a name="INVALID_EXPORTS" />**INVALID_EXPORTS**: модуль базового ресурса экспортировал некорректный тип
- <a name="UNCAUGHT_EXCEPTION" />**UNCAUGHT_EXCEPTION**: ошибка необработанного исключения процесса
- <a name="INTERNAL_PAGE_ERROR" />**INTERNAL_PAGE_ERROR**: необработанное исключение инициализации экземпляра страницы
- <a name="INVALID_LOGGER_TYPE" />**INVALID_LOGGER_TYPE**: передан некорректный тип логера в метод [stout.setLogger](#setLogger)
- <a name="INVALID_ROUTE_MAPPER_TYPE" />**INVALID_ROUTE_MAPPER_TYPE**: передан некорректный тип маппера роутов в метод [stout.setRouteMapper](#setRouteMapper)

### Пользовательские данные
#### <a name="data" />{Object, readonly} stout.data = {} ####
Объект-хранилище пользовательских данных, с которым взаимодействуют методы [stout.get](#get) и [stout.set](#set).
___

#### <a name="get" />{*} stout.get(key) ####
Возвращает данные из хранилища [stout.data](#data) по ключу `key`.

**Параметры:**
<br />`{String} key` - ключ, по которому хранятся данные.
___

#### <a name="set" />{stout} stout.set(key, data) ####
Сохраняет данные `data` в хранилище [stout.data](#data) по ключу `key`.

**Параметры:**
<br />`{String} key` - ключ, по которому хранятся данные.
<br />`{*} data` - данные.
___

### События
#### <a name="EVENT_UNCAUGHT_EXCEPTION" />{String, const} stout.EVENT_UNCAUGHT_EXCEPTION = 'uncaughtException' ####
Событие процесса "[uncaughtException](https://nodejs.org/api/process.html#process_event_uncaughtexception)".

**Аргументы события:**
<br />`{stout.Error} error` - [UNCAUGHT_EXCEPTION](#UNCAUGHT_EXCEPTION)

```javascript
stout.on(stout.EVENT_UNCAUGHT_EXCEPTION, function (error) {
  this.log('Stout is die! Reason: ' + error.getFullMessage(), 'error');
});
```
___

#### <a name="EVENT_PAGE_NOT_FOUND" />{String, const} stout.EVENT_PAGE_NOT_FOUND = 'pageNotFound' ####
Роутер не смог определить страницу для обработки запроса.

**Аргументы события:**
<br />`{HTTPServer.Request} request` - объект запроса

```javascript
stout.on(stout.EVENT_PAGE_NOT_FOUND, function (request) {
  this.log('Page not found, url: ' + request.url.format(), 'error');
});
```
___

#### <a name="EVENT_INTERNAL_PAGE_ERROR" />{String, const} stout.EVENT_INTERNAL_PAGE_ERROR = 'internalPageError' ####
Возникло исключение во время создания экзэмпляра страницы.

**Аргументы события:**
<br />`{stout.Error} error` - [INTERNAL_PAGE_ERROR](#INTERNAL_PAGE_ERROR)
<br />`{HTTPServer.Request} request` - объект запроса

```javascript
stout.on(stout.EVENT_INTERNAL_PAGE_ERROR, function (error, request) {
  this.log('Internal page error. Request: ' + request.url.format() + '. Reason: ' + error.getFullMessage(), 'error');
});
```
___
