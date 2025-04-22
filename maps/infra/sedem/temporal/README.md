# Temporal
### Настройка бд

Перед началом работы нужно один раз настроить схему:
```
# set up db variables
export DB_CLUSTER="mdb2ndoji5bvg0gc6d87"
export DB_HOST="c-${DB_CLUSTER}.rw.db.yandex.net"
export DB_PORT="6432"
export DB_USER="sedem-user"
export DB_PASSWORD=<PASSWORD>

# set up environment variables
export SQL_TLS=true
export SQL_TLS_DISABLE_HOST_VERIFICATION=true
export SQL_CONNECT_ATTRIBUTES='binary_parameters=yes'

# setup schema
export DB_NAME=sedem-temporal
./temporal-sql-tool --plugin postgres --ep "${DB_HOST}" -u "${DB_USER}" -p "${DB_PORT}" --db "${DB_NAME}" -pw "${DB_PASSWORD}" setup-schema -v 0.0
./temporal-sql-tool --plugin postgres --ep "${DB_HOST}" -u "${DB_USER}" -p "${DB_PORT}" --db "${DBNAME}" -pw "${DB_PASSWORD}" update-schema -d /etc/temporal/schema/temporal/versioned/

# setup schema temporal-visibility
export DB_NAME=sedem-temporal-visibility
./temporal-sql-tool --plugin postgres --ep "${DB_HOST}" -u "${DB_USER}" -p "${DB_PORT}" --db "${DB_NAME}" -pw "${DB_PASSWORD}" setup-schema -v 0.0
./temporal-sql-tool --plugin postgres --ep "${DB_HOST}" -u "${DB_USER}" -p "${DB_PORT}" --db "${DBNAME}" -pw "${DB_PASSWORD}" update-schema -d /etc/temporal/schema/visibility/versioned/
```
Все перенные окружения можно найти [здесь](https://a.yandex-team.ru/arcadia/vendor/go.temporal.io/server/tools/sql/main.go?rev=r9108409#L108)

### Также необходимо настроить default namespace с помощью tctl

В аркадии находится [здесь](https://a.yandex-team.ru/arcadia/vendor/go.temporal.io/server/cmd/tools/cli)

Сначала запустить temporal, tctl взаимодействует с сервером
```
./cli --ns default namespace register
```
Так нужно регистрировать не только дефолтный, но и любые новые неймспейсы
