# Переменные окружения шаблонов для конфигов push-client в Здоровье #

- `PUSH_CLIENT_LOG_FILES` - указывается список файлов через запятую, размещенный в `/var/log/yandex`, например: `nginx/access.log,nginx/error.log`.

- `PUSH_CLIENT_LOG_LEVEL` - уровень логирования, от 0 до 7, из [официальной документации](https://wiki.yandex-team.ru/logbroker/docs/push-client/config/#logger). Вариант по-умолчанию равен 5.

