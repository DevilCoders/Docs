# pretty_fares
https://wiki.yandex-team.ru/avia/dev/services-table/ticket-daemon-processing/doc/

### Установка:
1. `cp ./tools/samples/* ./tools/.`
2. если нужно, то правим настройки: `vi ./tools/environments.sh`

#### python manage.py shell: `./tools/run-manage.sh shell`
#### Запускать на деве можно из корня так: `./tools/run-dev.sh`
#### Для запуска воркера на отдельных очередях добавить -Q <you_queue>
