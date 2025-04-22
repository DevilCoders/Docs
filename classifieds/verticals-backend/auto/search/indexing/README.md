## auto-index-updater

Сервис для отправк офферов из шарда на индексацию, [диздок](docs/design.md)

## Локальный запуск c docker

application.conf пока настроен на использование тестовой таблицы в БД.

Если хочется запустить локально с [ydb-docker](https://ydb.yandex-team.ru/docs/getting_started/self_hosted/ydb_docker?searchQuery=docker),
в Main надо закомментировать строки про tvmYdb и раскомментировать строки в [application.development.conf](resources/application.development.conf)



