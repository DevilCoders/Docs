# Шаблон приложения на python для разворачивания в RTC (RunTime Cloud).

## Get started
1. `ya make -tt`
2. `offer-delivery-map --help`
3. `offer-delivery-map -c config.yaml runserver`
4. `offer-delivery-map version`

## Структура проекта

```
.
├── README.md
├── cmd
├── main.go
├── internal
│   ├── commands
│   │   ├── context.go
│   │   ├── root.go
│   │   ├── runserver
│   │   │   ├── runserver.go
│   ├── core
│   │   ├── actions
│   │   ├── config.go
│   │   ├── entities
│   ├── interactions
│   ├── main.go
│   ├── server
│   │   ├── app.go
│   │   ├── context.go
│   │   ├── handlers
│   │   ├── middlewares.go
│   │   ├── solomon.go
│   │   ├── router.go
│   ├── storage
├── config.yaml
├── swagger.yaml
├── package.json
```

* `cmd`: директория с командами, которые будут доступны для вызова из итогового бинаря
* `main.go`: точка входа
* `internal`:
    * `commands`: реализация команд из `cmd`
        * `context.go`: расширение контекста доп. полями для типизированного использования в `actions`
    * `core`: основная логика
        * `actions`: функции, выполняющие какие-то действия и возвращающие результат. Не завязаны на веб-сервер, можно вызвать из любого места. Зависят по входным данным только от кастомного контекста.
        * `entities`: сущности, в частности представление таблиц из базы в коде
        * `config.go`: структура конфига и функция парсинга
    * `interactions`: клиенты к внешним сервисам. Умеют ходить по HTTP наружу, докидывать TVM в заголовки ...
    * `server`: релизация web-сервера
        * `handlers`: функции, обрабатывающие запрос. На вход - http-request, на выходе запись ответа. Вызывают `actions` (см. выше) для формирования ответа
        * `app.go`: оболочка к http-серверу
        * `context.go`: адаптор, преобразующий контекст к кастомному контексту, чтобы не кастить в каждом `handler`'е
        * `middlewares.go`: локальные `middlewares`
        * `router.go`: сопоставление путей и `handler`'ов
    `storage`: работа с хранилищами данных
* `config.yaml`: дефолтный конфиг приложения
* `swagger.yaml`: swagger описание предоставляемого api
* `package.json`: описание сборки пакета

## Поддерживаемые ручки
    - /ping
    - /live
    - /monitoring
    - /solomon/json
    - /pprof/profile
    - /pprof/trace
    - /v1/user/{uid:[0-9]+}
    - /docs

## Используемые библиотеки

- Роутер — github.com/go-chi/chi

- Логер — go.uber.org/zap под соусом аркадийного library/go/core/log
- Парсинг конфигов — github.com/heetch/confita
- Запуск команд cli — github.com/spf13/cobra
- http-клиент для похода наружу — github.com/go-resty/resty

- Коннектор к sql базе — golang.yandex/hasql
- Билдер запросов — github.com/Masterminds/squirrel

## swagger
1. swagger.yaml - описание
2. /docs - swagger UI c описанием API
