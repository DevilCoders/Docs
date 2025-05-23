# configs

## Get started
1. `ya make -rt`
2. `./mdc-server -c config.yaml runserver`

## Структура проекта

* `cmd`: директория с командами, которые будут доступны для вызова из итогового бинаря
* `main.go`: точка входа
* `internal`:
    * `commands`: реализация команд из `cmd`
        * `context.go`: расширение контекста доп. полями для типизированного использования в `actions`
    * `core`: основная логика
        * `actions`: функции, выполняющие какие-то действия и возвращающие результат. Не завязаны на веб-сервер, можно вызвать из любого места. Зависят по входным данным только от кастомного контекста.
        * `entities`: сущности, в частности представление таблиц из базы в коде
        * `config.go`: структура конфига и функция парсинга
    * `interactions`: клиенты к внешним сервисам. Умеют ходить по HTTP наружу, докидывать TVM в заголовки ....
    * `server`: релизация web-сервера
        * `handlers`: функции, обрабатывающие запрос. На вход - http-request, на выходе запись ответа. Вызывают `actions` (см. выше) для формирования ответа
        * `app.go`: оболочка к http-серверу
        * `context.go`: адаптор, преобразующий контекст к кастомному контексту, чтобы не кастить в каждом `handler`'е
        * `middlewares.go`: локальные `middlewares`
        * `router.go`: сопоставление путей и `handler`'ов
    `storage`: работа с хранилищами данных
        * `db`: база данных
            `db.go`: сетап базы, инициализация мапперов
            `mapper_<entity_name>.go`: структура, реализующая методы работу с базой. В ее методах содержится код, который преобразует сущности в SQL-запросы, выполняет их, возвращает результат определенного типа
* `config.yaml`: дефолтный конфиг приложения

## Используемые библиотеки

- Роутер — github.com/go-chi/chi
- Коннектор к базе — golang.yandex/hasql
<!-- - Сбор ошибок — getsentry/sentry-go -->
- Логер — go.uber.org/zap под соусом аркадийного library/go/core/log
- Парсинг конфигов — github.com/heetch/confita
- Запуск команд cli — github.com/spf13/cobra
- Билдер запросов — github.com/Masterminds/squirrel
<!-- - http-клиент для похода наружу — github.com/go-resty/resty -->
