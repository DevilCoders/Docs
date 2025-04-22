# Робосклад

Сервис управления умным складом.

Основной стек: Python 3, FastAPI, SQLAlchemy, asyncpg

## Инструменты

### АПИ

Основное АПИ сервиса. Приложение находится в [./bin/api](./bin/api). Для быстрого запуска можно воспользоваться
командой `make run-dev-api` (для запуска в qyp `make run-dev-api args="-b [::]:8080"`)

### CLI

CLI с полезными командами. Приложение находится в [./bin/cli](./bin/cli). Список команд можно получить
через `./bin/cli/robowarehouse-cli --help`

### Migrator

Приложение, которое локально генерирует изменения схем таблиц в базе данных. Приложение находится
в [./bin/migrator](./bin/migrator). Для корректной работы нужно создать в корне проекта (`taxi/robowarehouse`) файл `.env`
и указать`APP_MIGRATION_PATH=<полный путь до каталога ./bin/migrator/migrations>`

* **Локальное применение миграций**. `make run-dev-migrator args="upgrade head"`. Применяет миграции для базы, указанной
  в конфигах.
* **Генерация изменений**. `make generate-migrations name='<{YOUR MIGRATION NAME}>'`. Генерирует новый файл миграций с
  именем `<{YOUR MIGRATION NAME}>`. Для генерации новых изменений нужно локально иметь базу, в которой уже есть
  изменения прошлых миграций. **Обязательно нужно добавить новый файл
  в `RESOURCE_FILES` [./bin/migrator/ya.make](./bin/migrator/ya.make)**

## Локальная разработка

Общие настройки приложений лежат в каталоге [./lib/config/files](./lib/config/files). По умолчанию используется `dev`
окружение для разработки и `ci` – для тестирования. Параметры, которые получатся из env переменных можно переопределять
через файл `taxi/robowarehouse/.env`.

По умолчанию используется локальная версия postgresql в докере (`minipgaas`). Для ее запуска можно воспользоваться
командой `make start-local-pg`.

## Релизы

Приложения деплоятся в rtc, через nanny. Есть три
окружения [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_robowarehouse_testing/)
, [pre-stable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_robowarehouse_pre_stable/)
, [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_robowarehouse_stable/). **Престейбл является частью
стейбл окружения и использует продовые данные**

Для выкатки ПР в тестинг, нужно проставить лейбл в ПР `taxi/deploy:testing` и нажать Run в [Teamcity](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_ArcadiaProjects_Taxi_Robowarehouse_Customs_CustomTesting?mode=builds).

Для сборки релиза нажать Run в [Teamcity](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_ArcadiaProjects_Taxi_Robowarehouse_Releases_AutoRelease).

Более подробно про релизы можно почитать на [wiki](https://wiki.yandex-team.ru/taxi/backend/deploy).
