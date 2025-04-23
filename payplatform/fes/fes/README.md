# Fiscal Event Service (FES)

## Get started

1. `make build`
2. `make start-db`
3. `make runserver`

## Структура проекта

```
.
├── Makefile
├── README.md
├── cmd
├── docker-compose.yml
├── main.go
├── pkg
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
│   │   ├── example
│   │   │   ├── impl
│   │   │   ├── mocks
│   │   ├── root.go
│   ├── main.go
│   ├── server
│   │   ├── app.go
│   │   ├── context.go
│   │   ├── handlers
│   │   ├── middlewares.go
│   │   ├── router.go
│   ├── storage
│   │   ├── db
│   │   │   ├── db.go
│   │   │   ├── mapper_user.go
├── fes.yaml
```

* `Makefile`: различные полезные команды для сборки, локального запуска, тестирования, сборки образа
* `cmd`: директория с командами, которые будут доступны для вызова из итогового бинаря
* `docker-compose.yml`: запуск локального окружения для разработки
* `main.go`: точка входа
* `pkg`:
    * `commands`: реализация команд из `cmd`
        * `context.go`: расширение контекста доп. полями для типизированного использования в `actions`
    * `core`: основная логика
        * `actions`: функции, выполняющие какие-то действия и возвращающие результат. Не завязаны на веб-сервер, можно вызвать из любого места. Зависят по входным данным только от кастомного контекста.
        * `entities`: сущности, в частности представление таблиц из базы в коде
        * `config.go`: структура конфига и функция парсинга
    * `interactions`: клиенты к внешним сервисам. Умеют ходить по HTTP наружу, докидывать TVM в заголовки
    * `server`: релизация web-сервера
        * `handlers`: функции, обрабатывающие запрос. На вход - http-request, на выходе запись ответа. Вызывают `actions` (см. выше) для формирования ответа
        * `app.go`: оболочка к http-серверу
        * `context.go`: адаптор, преобразующий контекст к кастомному контексту, чтобы не кастить в каждом `handler`'е
        * `middlewares.go`: локальные `middlewares`
        * `router.go`: сопоставление путей и `handler`'ов
    `storage`: работа с хранилищами данных
        * `db`: база данных
            `db.go`: сетап базы, инициализация мапперов
            `mapper_<entity_name>.go`: структура, реализующая методы работу с базой. В ее методах содержится код, который преобразует сущености в SQL-запросы, выполняет их, возвращает результат определенного типа
* `fes.yaml`: дефолтный конфиг приложения

## Используемые библиотеки

- Роутер — github.com/go-chi/chi
- Сбор ошибок — getsentry/sentry-go
- Логер — go.uber.org/zap под соусом аркадийного library/go/core/log
- Парсинг конфигов — github.com/heetch/confita
- Запуск команд cli — github.com/spf13/cobra
- Билдер запросов — github.com/Masterminds/squirrel
- http-клиент для похода наружу — github.com/go-resty/resty

## Swagger

### Генерация

```shell
make swagger
```

### Запуск

```
http://{{host}}:{{port}}/docs
```


## Cheat sheet

### Локальное тестирование
Чтобы не ждать пока ya привезет рецепт YDB (а это очень долго), можно поднять докер контейнер с YDB и
прописать в переменную окружения путь до ручки ydb, тогда тесты будут ходить в этот контейнер.
1. Отключаем подгрузку рецепта YDB в ya.make:
   ```yamake
   SET(LOCAL_TESTING_DB true)
   ```
2. Поднимаем докер контейнер с ydb:
   ```shell
   make start_db
   ```
3. Проставляем ручку YDB для тестов
   ```shell
   export YDB_CONNECTION_STRING="grpc://localhost:2135?database=local"
   ```
4. Запускаем тесты
