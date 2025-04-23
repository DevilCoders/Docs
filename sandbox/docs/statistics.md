# Статистика в ClickHouse

У Sandbox есть собственная инсталляция ClickHouse, куда отгружаются различные сигналы со всего кластера.
Доступ на чтение из этой базы данных открыт всем.

## Где найти данные?

### REST
```
https://clickhouse-sandbox.n.yandex-team.ru
https://clickhouse-sandbox1.n.yandex-team.ru
```

### Источники данных в Grafana { #grafana-sources }
- `clickhouse-sandbox`
- `clickhouse-sandbox-prestable`

Для обоих источников отключено проксирование, чтобы запросы делались напрямую к балансеру ClickHouse, минуя графану.

### YQL over ClickHouse { #yql-sources }
Добавьте в YQL-запрос строчку `use sandboxclickhouse;` и работайте как обычно.

#### Примеры запросов { #yql-examples }
- [поиск медленных запросов в API](https://yql.yandex-team.ru/Operations/YBAX_QuEI0Wipoh-e_e5GnIKh_FmPB2uzUI9CZ3ExDM=)
- [p95 потребление группой по дням](https://yql.yandex-team.ru/Operations/XzqaLJ3udvKO51H7clk3KkFYz0vyvANnZ7ATkFByRlA=)
- [самые тяжёлые по потреблению задачи за последние 7 дней](https://yql.yandex-team.ru/Operations/YPWKhQuEI3xk-teWYNvIszfIHodvlDoK3wrb9XV2XpQ=)
- [медленные скачивания ресурсов](https://yql.yandex-team.ru/Operations/X2JE-Rpqv9masXINyKE4WdmZuwHwjCuzmWkOHtsyiVA=)

### DataLens { #datalens-sources }

[Настроенное подключение к ClickHouse](https://datalens.yandex-team.ru/connections/gbobvjn91n30c-sandbox-production-statistics)

## Схема БД { #schema }
Схема таблиц в ClickHouse описана в репозитории в
[sandbox/services/modules/statistics_processor/schemas/clickhouse.py](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/services/modules/statistics_processor/schemas/clickhouse.py)

### Графики в Grafana своими руками { #grafana-how-to }

Если взять и написать `SELECT timestamp * 1000 AS t`, график получится тощим и пилообразным.
В его сглаживании помогут описанные ниже нехитрые манипуляции.

#### $timeSeries
Макрос, разворачивающийся в `(intDiv(toUInt32(timestamp), $interval) * $interval) * 1000`,
что приводит к выбору округлённого времени с шагом в `$interval`.

#### $interval
Шаг, с которым вы хотите рисовать график. Сюда можно вставить, например, `5m`,
а в запросе написать `SELECT $timeSeries as t, sum(value) / $interval as value` и получить график,
где будет нарисовано значение `value`, усреднённое с шагом в 5 минут.

С интервалом связано значение `Resolution`, масштабирующее временной шаг.
`Resolution = 1/4` в связке с вышеупомянутым примером приведёт к огрублению графика и его отрисовке с шагом в 20 минут.

#### $timeFilter
Временной фильтр для сужения результатов, значения для которого берутся из контрола в верхнем правом углу.
Примечателен тем, что его левую границу можно округлить вниз с помощью поля `Round` (может помочь избавиться от всплесков на графиках).

## Дашборды в Grafana { #grafana-dashboards }
Фильтры на все дашборды:
- [production](https://grafana.yandex-team.ru/?tag=sandbox&tag=production&query=&search=open&orgId=1)
- [preproduction](https://grafana.yandex-team.ru/?tag=sandbox1&query=&search=open&orgId=1)

| **Описание** | **Источник сигналов** | **production** | **preproduction**
| :--- | :--- | :--- | :---
| Здоровье продакшн-инсталляции ClickHouse | ClickHouse / Solomon | [Sandbox Clickhouse Health](https://grafana.yandex-team.ru/d/lG_xYIjmk/sandbox-clickhouse-health) | -
| Типы и read preference запросов, RPS и RDPS по методам, топ потребителей серверного времени, число запросов к серверам | Сервер и ServiceAPI | [Sandbox API](https://grafana.yandex-team.ru/dashboard/db/sandbox-api-production) | [Sandbox API](https://grafana.yandex-team.ru/dashboard/db/sandbox-api-preproduction)
| Машиночасы, которые кластер тратит на операции с svn и REST. Суммарное время, разбивка по типам задач, среднее время для типа задачи | Task executor | [Sandbox task operations](https://grafana.yandex-team.ru/dashboard/db/sandbox-task-operations-production) | -
| Статистика по Service Q: количество клиентов приходящих за задачами и получившими задачи на исполнение разбитые по клиентским PURPOSE-тегам, RPS и RDPS по методам, счетчики конфликтов и ошибок | ServiceQ | [Service Q RPC Production](https://grafana.yandex-team.ru/dashboard/db/sandbox-service-q-rpc-production) | [Service Q RPC Preproduction](https://grafana-dev.yandex-team.ru/dashboard/db/sandbox-service-q-rpc-preproduction)
| Статистика по месту, которое потребила задача | Task executor | [Sandbox tasks disk usage](https://grafana.yandex-team.ru/dashboard/db/sandbox-tasks-disk-usage-production) | -
| Задержка регулярных запусков планировщиков | Сервисный процесс `scheduler` | [Sandbox templates run delay](https://grafana.yandex-team.ru/dashboard/db/sandbox-templates-run-delay-production) | -
| Квотирование и потребление ресурсов кластера по группам: число исполняющихся задач, общая картина потребления | ServiceQ | [Quota Consumption Production](https://grafana.yandex-team.ru/dashboard/db/sandbox-quota-consumption-production) | [Quota Consumption Preroduction](https://grafana.yandex-team.ru/dashboard/db/sandbox-quota-consumption-preproduction) ||
| Состояние очереди: разбивка задач в очереди по типам, владельцам | Сервисный процесс `tasks_statistics` | [Queue statistics](https://grafana.yandex-team.ru/dashboard/db/sandbox-queue-statistics-production) | -
| Статистика по запущенным задачам: сколько сейчас исполняется, сколько задач в статусах `*ING` или `WAIT_*` | Сервисный процесс `tasks_statistics` | [Execution statistics](https://grafana.yandex-team.ru/dashboard/db/sandbox-execution-statistics-production) | -
| Статистика по клиентам: число свободных слотов, живость, состояние диска, текущая выполняемая сервисная команда | Сервисный процесс `client_slots_monitor` | [Client statistics](https://grafana.yandex-team.ru/d/000017411/sandbox-client-statistics-production) | [Client statistics](https://grafana.yandex-team.ru/d/eTXQn0Diz/sandbox-client-statistics-preproduction)
| Квотирование и использование REST API | Сервисный процесс `api_usage_statistics` | [API quota consumption](https://grafana.yandex-team.ru/d/DvczOKwmz/sandbox-api-quota-consumption) | -
| Количество и размеры созданных ресурсов в статусе READY | AgentR | [Resources](https://grafana.yandex-team.ru/d/m9S-Bp5ik/sandbox-resources) | -
| Статистика по ресурсному кэшу | AgentR | [Resource cache hit](https://grafana.yandex-team.ru/d/SVf_Op5iz/sandbox-resource-cache-hit?orgId=1) | -
| Задержка переключения задач из `WAIT`-статусов | Сервисный процесс `task_state_switcher` | [WAIT_* statuses delay](https://grafana.yandex-team.ru/d/Rnjngmtmz/sandbox-wait_-statuses-delay-production?refresh=1m&orgId=1) | -
| Статистика по ошибкам | Отовсюду из `common.log.ExceptionSignalsSenderHandler` | [Exception statistics](https://grafana.yandex-team.ru/d/dYMWfapik/sandbox-exception-statistics?refresh=30s&orgId=1) | [Exception statistics](https://grafana.yandex-team.ru/d/33fjBapmk/sandbox-exception-statistics-preproduction?orgId=1)
| Утилизация CPU/RAM/Disk/Network | Solomon | [Tasks' resources usage](https://grafana.yandex-team.ru/d/GljDI2nWk/sandbox-tasks-resources-usage-production) | -
| Taskbox: RPS/RDPS по методам/пользователям, потребление системных ресурсов, счётчик исключений по типам, число запущенных worker-ов | Taskbox dispatcher/worker | [Taskbox health](https://grafana.yandex-team.ru/d/xKaT0kSWz/sandbox-taskbox-health-production) | -
| Уведомления в sandbox | Сервисный процесс `mailman` | [Notifications](https://grafana.yandex-team.ru/d/23jxfR1Wz/sandbox-notifications?orgId=1) | -
| Сервисные процессы (времена итераций) | `sandbox.services.base.service` | [Services](https://grafana.yandex-team.ru/d/000020611/sandbox-services) | -

