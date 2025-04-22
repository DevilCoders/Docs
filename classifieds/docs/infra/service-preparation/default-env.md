# Базовые переменные окружения

Все переменные начинающие с `_DEPLOY_` являются зарезервированными под систему деплоя. Они будут доставлены в контейнер вместе с пользовательской конфигурацией.
В скобках примеры значений для понимания формата данных.

### _DEPLOY_G_SENTRY_DSN
**Описание:** Sentry DSN для отправки алертов. Не является секретом.

**Тип значения:** string (`https://3dafc7e4cca2415babcacac4b63c8374@sentry.vertis.yandex.net/1313`)

### _DEPLOY_G_TVM_ID
**Описание:** TVM ID приложения

**Тип значения:** integer (`202194044`)

### _DEPLOY_G_TVM_SECRET
**Описание:** Секрет TVM приложения

**Тип значения:** string (секрет из секретницы)

### _DEPLOY_METRICS_PORT
**Описание:** Порт на котором ожидаются метрики. Подробнее о метриках можно прочесть в разделе [Метрики](../observability/metrics.md).

**Тип значения:** integer (`81`)

### _DEPLOY_DC
**Описание:** Текущий дата центр

**Тип значения:** string (`sas`|`vla`)

### _DEPLOY_LAYER
**Описание:** Текущий слой

**Тип значения:** string (`test`|`prod`)

### _DEPLOY_HOSTNAME
**Описание:** Имя сервера, на котором запущен контейнер

**Тип значения:** string (`docker-11-vla.test.vertis.yandex.net`)

### _DEPLOY_ALLOC_ID
**Описание:** Уникальный идентификатор инстанса

**Тип значения:** string (`0a085506-3c9f-fab5-c2a6-f64145ea7a58`)

### _DEPLOY_SERVICE_NAME
**Описание:** Имя сервиса из карты сервисов

**Тип значения:** string (`service-name`)

### _DEPLOY_APP_VERSION
**Описание:** Версия сервиса

**Тип значения:** string (`0.1`)

### _DEPLOY_BRANCH
**Описание:** Имя бранча

**Тип значения:** string (`branch1`)

### _DEPLOY_CANARY
**Описание:** Признак что данный инстанс сервиса является частью канареечного релиза

**Тип значения:** bool (`false`|`true`)

### _DEPLOY_GEOBASE_PATH
**Описание:** Путь до бинарника геобазы. Будет передан при [соотвествующей настройке](manifest.md#geobase_version).

**Тип значения:** string (`/var/cache/geobase/geodata6.bin`)

### _DEPLOY_GEOBASE_TZ_PATH
**Описание:** Путь до директории tzdata для геобазы (zones_bin) [соотвествующей настройке](manifest.md#geobase_version).

**Тип значения:** string (`/var/cache/geobase/zones_bin`)

### _DEPLOY_TRACING_ADDR
**Описание:** Адрес [jaeger-agent](https://wiki.yandex-team.ru/vertis-admin/tracing/#zapis) без порта.

**Тип значения:** string (`localhost`)

### _DEPLOY_TRACING_COMPACT_PORT
**Описание:** Основной порт [jaeger-agent](https://wiki.yandex-team.ru/vertis-admin/tracing/#zapis).

**Тип значения:** integer (`6831`)

### _DEPLOY_TRACING_BINARY_PORT
**Описание:** Порт jaeger-agent для [nodejs-приложений](https://wiki.yandex-team.ru/vertis-admin/tracing/#zapis).

**Тип значения:** integer (`6832`)

### _DEPLOY_TRACING_COMPACT_ENDPOINT
**Описание:** Основной адрес:порт [jaeger-agent](https://wiki.yandex-team.ru/vertis-admin/tracing/#zapis)

**Тип значения:** string (`localhost:6831`)

### _DEPLOY_TRACING_BINARY_ENDPOINT
**Описание:** Адрес:порт jaeger-agent для [nodejs-приложений](https://wiki.yandex-team.ru/vertis-admin/tracing/#zapis)

**Тип значения:** string (`localhost:6832`)

### _DEPLOY_ZOOKEEPER_CONN_STRING
**Описание:** connection string, описывающий адреса и порты **нового** zookeeper-кластера, доступного для использования приложением. [Необходимо использовать аутентификацию](https://wiki.yandex-team.ru/vertis-admin/Zookeeper/#acl).

**Тип значения:** string (`zk-01-vla.test.vertis.yandex.net:2181,zk-01-sas.test.vertis.yandex.net:2181,zk-01-man.test.vertis.yandex.net:2181`)

### _DEPLOY_HPROF_DIRECTORY
**Описание:** Путь для записи дампа памяти при падении jvm. Пример использования: `{JAVA_HOME}/bin/java -XX:HeapDumpPath=${_DEPLOY_HPROF_DIRECTORY}`

**Тип значения:** string (`/alloc/logs/shiva__1.0.1__autotest__true`)

### _DEPLOY_PROXY_URL
**Описание:** Адрес [прокси](https://docs.yandex-team.ru/classifieds-infra/infrastructure/external-proxy) для хождения во внешние ресурсы.

**Тип значения:** string (`proxy-ext.test.vertis.yandex.net:3128`|`proxy-ext.vertis.yandex.net:3128`)
