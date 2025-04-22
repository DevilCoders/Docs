# Автогенерация

При создании и изменении [карты сервиса](service-map.md) запускаются процессы автоматического создания, подготовки и конфигурирования окружения.

Если после генерации для сервиса будут подготовлены переменные окружения, то они они будут описаны в https://docs.yandex-team.ru/classifieds-infra/deploy/default-env и доставлены в контейнеры при деплое. Прочитать все параметры для сервиса можно через [API](deploy/integration/api.md) методом `Envs` или в разделе [Переменные окружения](https://admin.vertis.yandex-team.ru/services/admin-www/envs) соответствующего сервиса.

## TVM ресурс

В [ABC "Сервисы Вертикалей"](https://abc.yandex-team.ru/services/verticals/) будет создано два TVM ресурса с именами `autogen/TEST/my_service` и `autogen/PROD/my_service`. Также сам ABC создаст по секрету на каждый ресурс. Данные секреты будут делегированы от имени [robot-vertis-shiva](https://staff.yandex-team.ru/robot-vertis-shiva?from=suggest).

В системе деплоя будут сохранены две переменные окружения [_DEPLOY_G_TVM_ID](service-preparation/default-env.md#_deploy_g_tvm_id) и [_DEPLOY_G_TVM_SECRET](service-preparation/default-env.md#_deploy_g_tvm_secret), которые будут доставлены в контейнеры сервиса при деплое.

Получить имя сервиса по его TVM ID можно через [открытое АПИ](service-preparation/default-env.md#_deploy_g_tvm_id) методом `ResolveTvmID`

## Sentry project

В [вертикальном sentry](https://sentry.vertis.yandex.net/verticals/) будет создан проект для карта с типом [service](service-map.md#type):
- Имя проекта равно имени из [карты сервисов](service-map.md#name).
- Все проекты будут созданы в одной команде `verticals`.
- Если проект с таким именем уже существовал, то будет использован именно он без перемещения в команду `verticals`.
- У проекта дополнительно создаются два DSN (`_DEPLOY_PROD`, `_DEPLOY_TEST`) для прода и теста с лимитами в 300 msg per minute на каждый.
- Sentry DSN по умолчанию (`DEFAULT`) удален не будет, чтобы старые проекты не потеряли доступ к Sentry. Но использовать его не рекомендуется.
- Sentry DSN будет доставлен в приложение как  [_DEPLOY_G_SENTRY_DSN](service-preparation/default-env.md#_deploy_g_sentry_dsn) в зависимости от слоя.

Дальнейшая работа:
- Для поиска проектов на главной страницы Sentry нужно самостоятельно добавиться в команду `Verticals`
- Проекты можно перенести в другую команду
- Создавать или удалять sentry dsn нельзя, так как проект может быть обновлен по общим правилам

## Grafana Dashboard
Сгенеренные дашборды будут находится в папке [Generated](https://grafana.vertis.yandex-team.ru/dashboards/f/FuR3gWinz/generated)
- Для каждого provides из карты будет сгенерирован график на количество запросов в секунду. Поддерживаются http и grpc протоколы
- В карте можно указать поле [language](service-map.md#language). Для Java, Scala, Go, NodeJs будут сгенерированы графики специфичные для указанного языка, например: `Heap usage`, `GC timings`
- В карте в поле  можно указать зависимость от `mdb_mysql` сервиса. Будут сгенерированы графики для соответствующего кластера базы (`CPU usage`, `Memory usage`, `Read/Write rate`, `Queries rate`, `Replication lag`, `Disk space`)
- Для отображения графика Incoming request timings сервис должен предоставить метрики: `grpc_server_handled_total` типа `counter` с лейблом `grpc_method`; `grpc_server_handling_seconds` типа `histogram` c лейблом `method`
- Будет сгенерирована аннотация на деплои сервисов, указанных в [depends_on](service-map.md#depends_on) в карте
- Можно добавлять на дашборд свои панели, Row, переменные и аннотации, они не будут перетерты при перегенерации
- При перегенерации все значения сгенерированных ранее переменных и аннотаций сбрасываются в дефолтные
- Все Row и панели с префиксом "_" считаются сгенеренными и будут перетерты при изменении карты сервиса
- Кастомные панели в сгенеренных Row будут удалены при перегенерации

{% cut "Deprecated" %}

На графиках Incoming request timings отображается устаревшая метрика типа `histogram` c именем `request_duration_seconds` и c лейблом `method` для обратной совместимости

{% endcut %}

## Секреты
Для каждого сервиса создается 2 секрета: `autogen.TEST.my_service` и `autogen.PROD.my_serivce`. Данные секреты делегированы от имени [robot-vertis-shiva](https://staff.yandex-team.ru/robot-vertis-shiva?from=suggest).
- Все переменные из секретов будут доставлены в контейнер при деплое, ключи переменных соответствуют ключам, указанным в секретнице.
- При деплое используется последняя версия секрета.
- Доступ на чтение и редактирование получают все, кто указан в поле [owners](service-map.md#owners) в карте сервиса. При изменениях владельцев в карте, доступ к секретам так же будет изменен.
- Переменные из секретов имеют самый низкий приориет, и будут перетерты перменными из [конфига манфеста](service-preparation/manifest.md#konfiguraciya-prilozheniya) при коллизии в ключах.
- Что бы переопределить секрет или использовать не последнюю версию, достаточно вписать переменную с нужным значением в конфиг.
- При удалении/переименовании карты секрет будет удален.

