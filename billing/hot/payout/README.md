# payout

Система выплат нового биллинга.

## Для чего?

Микро сервис для взаимодействия с OEBS (отправка и трекинг статуса выплат).

## ABC

- https://abc.yandex-team.ru/services/newbillingpayout/

## Где посмотреть?

- Test:
    - http://payout.test.billing.yandex.net/docs

- Prod:
    - http://payout.billing.yandex.net

## Deploy

Проект:

- https://deploy.yandex-team.ru/projects/billing-payout

CI:

- https://a.yandex-team.ru/projects/newbillingpayout

[Подробнее тут](docs/deploy.md).

## Мониторинги

MaaC:
- https://a.yandex-team.ru/arc/trunk/arcadia/paysys/sre/tools/monitorings/configs/billing30/stable/payout.py

Графана:
- https://grafana.yandex-team.ru/d/MnJ7j4_Mz/payouts?orgId=1&var-env=prod&refresh=10s

Juggler:
- https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dbilling30.payout.stable

Конфиги для solomon:
- https://a.yandex-team.ru/arc/trunk/arcadia/billing/hot/scripts/solomon/configs/payout

## Тесты

### С локальной БД (быстрее работают)

```sh
# Запуск локальной БД
$ make start-db

# Тесты
$ make test
```

### БД из рецепта

```shell
$ ya make -t
```

### Посмотреть покрытие тестами

```shell
$ make test-with-coverage

Total 54 suites:
	54 - GOOD
Total 192 tests:
	192 - GOOD
Ok
find . -iname "*.cover.go" -delete

	Please, open file: /tmp/report/go.coverage.report/report.html
```

Далее, открыть в браузере `/tmp/report/go.coverage.report/report.html`.

## Структура проекта

```
.
├── Makefile
├── README.md
├── cmd
├── docker-compose.yml
├── main.go
├── internal
│ ├── context
│ ├── core
│ ├── cpf
│ │ ├── client
│ ├── interactions
│ ├── notifier
│ │ ├── config
│ ├── netting
│ ├── oebsgate
│ │ ├── config
│ ├── payout
│ ├── request
│ ├── server
│ │ ├── handlers
│ ├── storage
│ │ ├── db
├── postgre
├── payout.yaml
```

* `Makefile`: различные полезные команды для сборки, локального запуска, тестирования, сборки образа
* `cmd`: директория с командами, которые будут доступны для вызова из итогового бинаря
* `docker-compose.yml`: запуск локального окружения для разработки
* `main.go`: точка входа (отсюда бинарник собирается)
* `internal`:
    * `context`: расширение контекста доп. полями
    * `core`: общие компоненты
        * `config.go`: структура конфига и функция парсинга
        * `db.go`: интерфейсы для работы с БД
        * `solomon.go`: структуры для работы с Соломоном
    * `cpf`: пакет для работы сash-payment-fact
        * `client`: пакет для отправки данных в баланс
    * `interactions`: инициализация клиентов к внешним сервисам. Умеют ходить по HTTP наружу, докидывать TVM в заголовки
    * `notifier`: пакет для отправки нотификаций о статусе выплаты
    * `netting`: пакет для работы со взаимозачетами
    * `oebsgate`: пакет для получения/отправки данных и/из ОЕБС
    * `payout`: пакет для работы с выплатами
    * `request`: пакет для работы с заявками на выплату
    * `server`: реализация web-сервера (api)
        * `handlers`: функции, обрабатывающие запрос. На вход - http-request, на выходе запись ответа. Вызывают `actions` (см. выше) для формирования ответа
        * `app.go`: оболочка к http-серверу
        * `context.go`: адаптер, преобразующий контекст к кастомному контексту, чтобы не кастить в каждом `handler`'е
        * `middlewares.go`: локальные `middlewares`
        * `router.go`: сопоставление путей и `handler`'ов
    * `storage`: работа с хранилищами данных
        * `db`: база данных
            `db.go`: сетап базы, инициализация мапперов
* `postgre`: миграции
* `payout.yaml`: дефолтный конфиг приложения

## Остальные детали

- [БД, подключение, миграции](docs/db.md)
- [Основные компоненты](docs/components.md)

## Используемые библиотеки

- Роутер — github.com/go-chi/chi
- Коннектор к базе — golang.yandex/hasql
- Сбор ошибок — getsentry/sentry-go
- Логер — go.uber.org/zap под соусом аркадийного library/go/core/log
- Парсинг конфигов — github.com/heetch/confita
- Запуск команд cli — github.com/spf13/cobra
- Билдер запросов — github.com/Masterminds/squirrel
- http-клиент для похода наружу — github.com/go-resty/resty

## Контакты

- shorrty@
- asanikushin@
