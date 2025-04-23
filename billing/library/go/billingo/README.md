```
    __     _  __ __ _
   / /_   (_)/ // /(_)____   ____ _ ____
  / __ \ / // // // // __ \ / __ `// __ \
 / /_/ // // // // // / / // /_/ // /_/ /
/_.___//_//_//_//_//_/ /_/ \__, / \____/
                          /____/
```

## Get started
См. шаблон [billing/library/go/template](https://a.yandex-team.ru/arc/trunk/arcadia/billing/library/go/template)

## Структура библиотеки

```
.
├── Makefile
├── README.md
├── mock
├── pkg
│   ├── commands
│   │   ├── base.go
│   │   ├── main.go
│   │   ├── storage.go
│   │   ├── swagger.go
│   ├── common
│   │   ├── cast
│   │   ├── errors
│   │   ├── once_notify.go
│   │   ├── registry
│   │   ├── slice_map.go
│   │   ├── string_utils.go
│   │   ├── sync_map.go
│   │   ├── time.go
│   │   ├── timer
│   │   ├── typing
│   │   ├── xrand
│   ├── config
│   ├── configops
│   │   ├── type
│   │   └── vars
│   ├── extracontext
│   ├── interactions
│   │   ├── accounts
│   │   ├── blackbox
│   │   ├── configshop
│   │   ├── payout
│   │   ├── processor
│   │   └── startrek
│   ├── lock
│   ├── queue
│   ├── sentry
│   ├── storage
│   │   ├── logbroker
│   │   ├── mongo
│   │   ├── sql
│   │   │   ├── backends
│   │   │   │   └── pg
│   │   │   ├── mixins
│   │   │   └── wrappers
│   │   └── ydb
│   ├── task
│   ├── taskapp
│   ├── template
│   │       └── sql
│   ├── testing
│   │   └── load
│   │       └── generator
│   ├── tvm
│   ├── web
│   │   ├── mw
│   │   │   ├── cors
│   │   │   ├── logging
│   │   │   ├── swagger
│   │   │   ├── tracing
│   │   │   ├── tracker
│   │   │   └── tvm
│   │   ├── router
│   │   └── schema
│   │       ├── errors
│   │       └── json
│   ├── webapp
│   │   └── handlers
│   ├── workerpool
│   ├── xjson
│   ├── xlog
│   │   ├── gorm
│   │   └── ua
│   ├── xtrace
│   └── xyaml




```
* `mock`: замоканные структуры из библиотеки
* `pkg`
    * `commands`: абстракция над cli-командой
        * `base.go`: интерфейс
        * `storage.go`: расширение интерфейса, cli-команда, использующая базу
        * `swagger.go`: расширение интерфейса, cli-команда с поддержкой Swagger
    * `common`: типичные снипеты
      * `cast`: снипеты для работы с рефлексией и кастами
      * `errors`: обработка ошибок
      * `once_notify.go`: примитив синхронизации, для однократного уведомления
      * `registry`: работа с метриками
      * `slice_map.go`: создание мапы из слайса
      * `string_utils.go`: утилиты для работы со строками
      * `sync_map.go`: потокобезопасная реализация мапы
      * `time.go`: утилиты для работы с представлением времени
      * `timer`: таймер, позволяющий выполнять произовольную функцию с указанной переодичностью
    * `config`: загрузка/парсинг конфигов
    * `configops`: реализация логики и задания переменных в конфигах
    * `extracontext`: расширение контекста
    * `interations`: абстракция для хождения наружу по http. Поддерживает выписывание tvm-тикетов
    * `lock`: примитив синхронизации lock
    * `queue`: работа с очередями SQS
    * `sentry`: обвязка для zap ядра, позволяющая отправлять логи в sentry
    * `storage`: работа с СХД
        * `connector.go`: структура, занимающаяся подключением/отключением нескольких бекендов
        * `logbroker`: работа с писателями/читателями Logbroker
        * `mongo`: MongoDB. Под капотом `mongo-driver`
        * `sql`: SQL ДБ
          * `backends`: бекенды
              * `pg`: PostgreSQL. Под капотом `pgx` и `hasql`
          * `database.go`: интерфейс базы данных, транзакции и запроса
          * `mixins`: поддержка фабрики SQL-запросов squirrel.
          * `wrappers`: обертки для бекендов
        * `ydb`: YDB. Под капотом `ydb-go-sdk`
    * `tvm`: создание штатного tvm-клиента и middleware для проверки входящих запросов
    * `web`: абстракция над веб-сервером
        * `schema`: абстракция над ответом
            * `json`: ответы в формате `json`
        * `mw`: мидлвари
        * `router`: роутер, используется `chi`
        * `context.go`: проброс кастомного контекста в `handler`
        * `handlers.go`: общие хендлеры
        * `middlewares.go`: общие мидлвари
        * `server.go`: обертка над веб-сервером
        * `tracker.go`: утилита для измерения показателей запроса
    * `webapp`: веб-приложение. В текущей реализации оболочка к `web`, но может держать под капотом что-нибудь еще.
    * `workerpool`: воркеры, выполняющие таски из очереди

## Что делать, если я вдруг хочу разрабатывать на `Python`?
Библиотека с похожими идеями: [mail/python/sendr-qtools](https://a.yandex-team.ru/arc/trunk/arcadia/mail/python/sendr-qtools)
