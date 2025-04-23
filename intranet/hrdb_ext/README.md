## Локальная разработка

Базовый функционал джанги `./manage.py runserver` не сработает, потому что мы используем аркадийную джангу с аркадийными зависимостями.
Поэтому нам нужно:
- Создать полноценный бинарь
- Положить его в докерный образ
- Запустить сервис в `docker-compose` используя этот готовый образ.

Подробнее см. в `docker-compose.yml`

Итого, чтобы запустить локально:
 - `make install` - собирает бинарь, кладёт в docker image, запускает этот image в docker-compose.
 - `make run` - запускает последний собранный image.
 - Заходим в браузере на http://127.0.0.1:8000/

## Тесты
`make test` - запустить все тесты

Памятка для запуска тестов через `ya make`:
 - `ya make -A` - запустить все тесты
 - `ya make -AP` - запустить все тесты и показать результат для успешных
 - `ya make -A -F intranet.hrdb_ext.tests.amo.test_request_log.py` - запустить конкретный модуль
 - `ya make -A -F "intranet.hrdb_ext.tests.amo.test_request_log.py::test_log*"` - запустить конкретный тест

## Миграции
 - `make makemigrations` - создаёт файлы миграций.
 - При локальной разработке - применяются автоматически (см. `command` в `docker-compose.yml`)
 - Чтобы применить в проде - надо зайти в любую машинку по ssh и запустить `hrdb_ext migrate <app>` для каждой аппки

## Сборка и деплой

- `make deploy-to-testing` - собрать и выкатить в тест.
- `make deploy-to-production` - собрать и выкатить в прод.

Notes:
- От файлов вида `libpyhrdb_ext.a` и `libpyhrdb_ext.global.a` - [никуда не деться](https://st.yandex-team.ru/DEVTOOLSSUPPORT-13870#6197ca66834ce9073ae8768f).
- Используем тулзовый `ya tool releaser`, но не полностью (например, пока не работаем с changelog.md)