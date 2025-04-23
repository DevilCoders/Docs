# Сервис управления ачивками
## Локальный запуск
- сгенерировать проект, запустив `generate_project.sh`
- открыть как отдельный проект в идее (по дефолту генерится здесь: `/Users/<username>/idea_projects`)
- запустить в докере БД (Postgres) и очередь (SQS): `cd 'dependency-stubs' && docker-compose up -d`
- запустить сервис в IDE (после генерации проекта появится конфигурация запуска)
- UI SQS будет доступен по `http://localhost:9325/`, закинуть сообщение в очередь: `aws --endpoint-url http://localhost:9324 sqs send-message --queue-url http://localhost:9324/queue/sqs_ach_achievement-metrics --message-attributes file://dependency-stubs/sqs-params.json --message-body file://dependency-stubs/sqs-message-body.json`
  )
## Клиенты
- подробно описано [здесь](https://docs.yandex-team.ru/mj-framework/pages/features/clients)
- для создания API-клиента достаточно описать файл `api.yaml` с нужными ручками для соответствующего сервиса и изменить `service.yaml`
- обязательно нужно указать `openapi_spec_path` (путь до файла), `url` (если сервис сторонний, не на MJ), `env` (хосты для тестинга и прода), `tvm` (если есть, то указать `dstId` для соответствующей среды; если нет, то нужно указать `serviceTicketEnabled: false`)
- на данный момент реализовано два клиента: `TtsApiClient` и `StaffApiClient`. Получаются генерацией кода: тэг + префикс `ApiClient`
- для использования надо заинджектить: `@Autowired private val notificationApiClient : NotificationApiClient`

### TtsApiClient
- api клиент до tts
- отправление пуша:
```kotlin
val dto = NotificationMessageDto()
dto.users(listOf("infor_admin"))
dto.message("test message")
dto.actions(listOf("Прочитано"))
ttsApiClient.notificationWarehouseNameTopicNameNotifyPost(
    "SOF", "user-notifications", dto
).schedule()
```
- получение staff логина по логину из wms:
```kotlin
val result = ttsApiClient.employeeStaffWarehouseNameGet("SOF", listOf("user1", "user2")).schedule().get()
```
### StaffApiClient
- api клиент до staff
- получение информации по ачивке:
```kotlin
val result = staffApiClient.apiAchieveryAchievementsIdFieldsiddescriptionRutitleRuiconSmallUrlGet(2160L, "OAuth <oauth-token>").schedule().get()
```
- дать пользователю ачивку (токен должен принадлежать владельцу ачивки):
```kotlin
val dto = GivenStaffAchievementDto()
dto.level(-1)
dto.achievementId(3154)
dto.personLogin("staff-user")
dto.comment("тест")
staffApiClient.apiAchieveryGivenPost("OAuth <oauth-token>", dto).schedule()
```

## Метрики
### Как приходят:
Метрики либо приходят через очередь SQS, либо генерируются и публикуются через [`ru.yandex.market.wms.achievement.service.EventService.publishMetricEvent`](https://arcanum.yandex-team.ru/arc/trunk/arcadia/market/logistics/wms/app/achievement/achievement-app/src/main/kotlin/ru/yandex/market/wms/achievement/service/EventService.kt)

### Создать новую метрику
- добавить в enum [`ru.yandex.market.wms.achievement.model.metric.MetricType`](https://arcanum.yandex-team.ru/arc/trunk/arcadia/market/logistics/wms/app/achievement/achievement-core/src/main/kotlin/ru/yandex/market/wms/achievement/model/metric/metrics.kt?rev=r9400246#L3)
- унаследовать [`ru.yandex.market.wms.achievement.model.metric.Metric`](https://arcanum.yandex-team.ru/arc/trunk/arcadia/market/logistics/wms/app/achievement/achievement-core/src/main/kotlin/ru/yandex/market/wms/achievement/model/metric/metrics.kt?rev=r9400246#L13)
- чтобы можно было "реагировать" на метрику, добавить метод в обработчик [`ru.yandex.market.wms.achievement.model.metric.MetricEventInvoker`](https://arcanum.yandex-team.ru/arc/trunk/arcadia/market/logistics/wms/app/achievement/achievement-app/src/main/kotlin/ru/yandex/market/wms/achievement/model/metric/MetricEventInvoker.kt)

## Условия
### Логика
Условия проверяются по событиям, когда приходит метрика. Как только приходит метрика, проверяются условия, для которых метрика "важна".

### Создать новое условие
- создать в пакете `ru.yandex.market.wms.achievement.model.condition.impl`
- унаследоваться от [`ru.yandex.market.wms.achievement.model.condition.BaseCondition`](https://arcanum.yandex-team.ru/arc/trunk/arcadia/market/logistics/wms/app/achievement/achievement-app/src/main/kotlin/ru/yandex/market/wms/achievement/model/condition/BaseCondition.kt)
- пометить как `@Component`
- реализовать метод, на который нужно реагировать от обработчика метрик [`ru.yandex.market.wms.achievement.model.metric.MetricEventInvoker`](https://arcanum.yandex-team.ru/arc/trunk/arcadia/market/logistics/wms/app/achievement/achievement-app/src/main/kotlin/ru/yandex/market/wms/achievement/model/metric/MetricEventInvoker.kt)

## Ачивки
При изменении состояний для условий пересчитывается state и для ачивок (завязанных на эти состояния)

## Настройки
Конфиги прорастают с помощью [ITS](https://nanny.yandex-team.ru/ui/#/its/locations/market/wms/achievement), и перечитываются в рантайме при изменениях файла.
Чтобы получить настройки - заинжектить бин [`ru.yandex.market.wms.achievement.configuration.settings.provider.SettingsProvider`](https://arcanum.yandex-team.ru/arc/trunk/arcadia/market/logistics/wms/app/achievement/achievement-app/src/main/kotlin/ru/yandex/market/wms/achievement/configuration/settings/provider/SettingsProvider.kt)
