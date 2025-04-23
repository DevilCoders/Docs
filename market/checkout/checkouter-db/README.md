### checkouter-db

Миграции для storage

[Миграции БД без downtime'а](https://wiki.yandex-team.ru/users/ivvakhrushev/dbmigrationswithoutdowntime/)

[Инструкция для релиз-мастера по выкатке миграций БД](https://wiki.yandex-team.ru/users/ivvakhrushev/how-to-roll-out-database-migrations/)

В скриптах описаны миграции для трёх баз данных:
- основной чекаутера (basic)
- архивной чекаутера (archive)
- OMS

и нескольких окружений:
- development
- testing
- production

Сначала для базы данных выполняется общая для всех окружений миграция, потом (при наличии) миграция для конкретного окружения.

Для основной и архивной баз чекаутера бОльшая часть миграций обобщена в `/changelog/changelog.xml`

"Точки входа" миграций перечислены в [85_app.properties](src/main/properties.d/85_app.properties)

XXX: миграции основной базы для разных окружений находятся в `/changelog/checkout/` вместо `/changelog/basic/`. Перенести нельзя, так как в `/changelog/checkout/production/` есть выполненные миграции.
