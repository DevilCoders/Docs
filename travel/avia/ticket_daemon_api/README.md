======================================
#Ticket daemon api
Api для поиска авиабилетов.

## Разработка
1. клонируем
2. `cp ./tools/samples/* ./tools/.`
3. `vim ./tools/environments.sh`
    * AVIA_TICKET_HTTP_API_MDB_API_TOKEN и дргуие можно взять из https://deploy.yandex-team.ru/stages/avia-ticket-daemon-api-testing/config/du-api/box-api
4. `ya make -tt` запуск тестов
5. `./tools/run-shell.sh` запуск manage.py shell
6. `./tools/run-dev.sh` запуск сервиса
7. `Y_PYTHON_ENTRY_POINT="travel.avia.ticket_daemon_api.app:manage" ./bin/app` запуск manage.py

## Документация
Отсутствует

## Посмотреть что лежит в кэше
Для просмотра содержимого кэша можно использовать скрипт `examine-cache`.
Для вывода помощи по запуску скрипта используйте ключ `--help`.
Для вывода дополнительной информации используйте ключ `-v`.

Запуск в проде/тестинге:

`Y_PYTHON_ENTRY_POINT="travel.avia.ticket_daemon_api.scripts.examine_cache:main" /app/app`

Запуск на дев-машинке:

`./tools/examine-cache.sh`

### Режимы работы скрипта

Первый, - обычный, как для поиска, с заданием откуда, куда, когда, партнера, и, возможно, других опциональных параметров.

`./tools/examine-cache.sh --help`

`./tools/examine-cache.sh -f c213 -t SVX -d 2021-07-27 -p pobeda`

Второй, позволяет задать условие выборки where, и limit от 1 до 10.

`./tools/examine-cache.sh select --help`

`./tools/examine-cache.sh select --where "partner_code='pobeda'"`
