# Хэлперы для Slack приложений на основе @slack/bolt

## Список хэлперов
- `utils/installationStore` - хэлпер для записи/чтения из базы данных токенов авторизации (см. https://slack.dev/bolt-js/concepts#authenticating-oauth). Запись и чтение производится в PostgreSQL базу данных.
- `utils/getSlackUserId` - с помощью Slack API резольвит displayName пользователя во внутренний идентификатор пользователя в Slack.
- `utils/getSlackDisplayName` - с помощью Slack API резольвит внутренний идентификатор пользователя в его Display Name.
- `utils/getInstallationIfno` - получить InstallationInfo для указанного Slack приложения
- `utils/getMetricPusher` - фабрика фукции для пуша метрик в Solomon, с predefined project/cluster.
- `utils/getReqLogginMiddleware` - фабрика middleware, для логгирования всех входящих запросов в Solomon
- `utils/logger` - утилиты для логгирования  
- `utils/cache` - кэш поверх Redis
- `utils/escapeMrkdown` - энкодит специальные символы как html entities (https://api.slack.com/reference/surfaces/formatting#escaping)

## Необходимые переменные окружения
- *DB_HOST* - главный хост PostgreSQL (используется для записи)
- *DB_HOST_REPLICAS* - реплики PostgreSQL (используются для чтения)
- *DB_PORT* - порт PostgreSQL
- *DB_USERNAME* - имя пользователя для авторизациия в PostgreSQL
- *DB_PASSWORD* - пароль для авторизациия в PostgreSQL
- *DB_NAME* - имя базы в PostgreSQL
- *REDIS_HOSTS* - список хостов Redis, разделенных запятой
- *REDIS_PORT* - порт, на котором слушают Redis инстансы
- *REDIS_NAME* - имя master инстанса Redis
- *REDIS_PASSWORD* - пароль для доступа к Redis
- *SOLOMON_OAUTH_TOKEN* - токен для записи метрик в Solomon
- *LOGGER_PROJECT_NAME* - имя проекта, используемое при создании логгера
