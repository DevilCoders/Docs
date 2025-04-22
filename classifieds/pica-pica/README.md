Old verticals pica-pica
=======================

**TLDR** Здесь проект старой пики. Активная разработка здесь не ведется.

Архив репозитория до переезда (read-only): https://github.com/YandexClassifieds/pica-pica

Актуальный код в аркадии (tier1): https://a.yandex-team.ru/arcadia/classifieds/pica-pica

[Краткий гайд для дежурного](./Duty.md)

## Arcadia:

Полезные ссылки:
- https://docs.yandex-team.ru/devtools/intro/quick-start-guide
- https://docs.yandex-team.ru/arcadia-tier1/#sborki-bildov-v-teamcity
- https://docs.yandex-team.ru/arcadia-tier1/#zapusk-prekommitnyh-proverok-v-teamcity
- https://wiki.yandex-team.ru/mobvteam/tier1/
- https://wiki.yandex-team.ru/users/darl/arcadia-pervye-shagi

## Разработка:

Создать симлинк на схему `make init`
По следам переезда в аркадию (здесь нет сабмодулей, но есть схема): Схема подключается симлинком но коммитить симлинки в аркадию запрещено, поэтому она добавлена в `.arcignore`, и создавать симлинк нужно локально.


Проверить/создать локальные файлы конфигураций: `application.local.conf`, `core.local.conf`

Разработка ведется в ветках, деплой идет из pr-ов.

В PR для мержа требуется апрув ревьюера и успешные тесты https://t.vertis.yandex-team.ru/buildConfiguration/VertisPicaPica_ArcadiaCiBuild

## Сборка:

Для сборки используется maven.

## Деплой:

После апрува и успешных тестов в PR нужно закоммитить новую версию в changelog. Деплой в тестинг начнется автоматически.
После тестирования нужно толкнуть тикет кондуктора в продакшн.

Пакеты деплоятся на железные машины через кондуктор: https://c.yandex-team.ru/packages/yandex-vertis-pica-pica-api

Пакеты собираются, выкладываются и деплоятся в тестинг через сборку в vertis teamcity (используется autorelease):
https://t.vertis.yandex-team.ru/buildConfiguration/VertisPicaPica_ArcadiaPicaPicaApiRelease

Версия сборки берется из pica-pica-api/debian/changelog

Повторно версия через тимсити (autorelease) не выкладывается.

Из пуллреквеста, в котором изменился changelog сборка в тимсити запустится автоматически.
