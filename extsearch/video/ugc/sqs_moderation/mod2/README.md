### Настройки

Переменные окружения:
* `SQS_MODERATION_ACCOUNT` - аккаунт для доступа к SQS
* `SQS_MODERATION_TOKEN` - персональный токен
* `CLEANWEB_ADDR`- адрес сервера Чистого Веба. Например, <https://router-dev.clean-web.yandex.net/v2/>
* `LOG_COLLECTOR_URL`- адрес сервера сбора логов
* `VH_ADMIN_API_URL`- адрес сервера VH Admin API. Например, <http://vh.test.yandex.net/admin/v1.0/>
* `UGC_ADMIN_API_URL`- адрес сервера UGC Admin API. Например, <http://ugc.vh.test.yandex.net>
* `TOLOKA_URL`- адрес сервера Толоки. Например <https://toloka.yandex.ru>
* `TOLOKA_TOPICS_POOL`- номер эталонного пула в Толоке.
* `TOLOKA_TOPICS_MIN`- минимально количество проголосовавших за тему, чтобы считать её подходящей. По-умолчанию, 2
* `AVATARS_TVM_SECRET` - секрет для доступа к TVM при загрузке в аватарницу
* `AVATARS_TEST`- установите `1`, чтобы использовать тестовую аватарницу.
* `YT_CLUSTER` - какой yt-кластер использовать для записи событий RTX. По умолчанию, "arnold"
* `YT_TOKEN` - токен доступа к YT
* `YT_PATH` - путь в YT для записи событий RTX

Параметры
* `--port` порт для web api
* `--log-dir` папка для логов (больше не используется)

