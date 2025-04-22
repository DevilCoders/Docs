# Доступные пресеты для `lama`

<details><summary><b>Table of contents</b></summary>

* [Solomon](#solomon)
    * [Alerts](#alerts)
      * [yt-quota-exceeding](#solomon/alerts/yt-quota-exceeding)
      * [reactor-quota-exceeding](#solomon/alerts/reactor-quota-exceeding)
      * [reaction-failure](#solomon/alerts/reaction-failure)
      * [reaction-delay](#solomon/alerts/reaction-delay)
      * [cofe-metric-delay](#solomon/alerts/cofe-metric-delay)
      * [artifact-publication-delay](#solomon/alerts/artifact-publication-delay)
      * [artifact-publication-delay-user-timestamp](#solomon/alerts/artifact-publication-delay-user-timestamp)
      * [artifact-publication-missed-values](#solomon/alerts/artifact-publication-missed-values)
    * [Channels](#channels)
      * [reactor-juggler](#solomon/channels/reactor-juggler)
      * [reactor-juggler-simple](#solomon/channels/reactor-juggler-simple)
* [Пресеты команды maps-analytics](##maps-analytics)
    * [juggler/check](#projects/maps-analytics/juggler/check)
    * [juggler/check-critical](#projects/maps-analytics/juggler/check-critical)
    * [yql](#projects/maps-analytics/yql)
* [Пресеты команды maps-front](#maps-front)
    * [juggler-check](#projects/maps-front/juggler/check)
    * [simple-scheduler](#projects/maps-front/simple-scheduler)
    * [binary-scheduler](#projects/maps-front/binary-scheduler)
</details>

## Solomon

### Alerts

#### [solomon/alerts/yt-quota-exceeding](solomon/alerts/yt-quota-exceeding.jinja)
Мониторинг квоты для аккаунта в YT.

##### Параметры
| Название | Описание |
|---|---|
| `yt_account` | **Обязательный.** Аккаунт в YT |
| `alert_threshold` | **Обязательный.** Порог срабатывания |
| `channel_ids` | **Обязательный.** Массив ID каналов в Соломоне |
| `channel_id` | (**deprecated**) ~~**Обязательный.** ID канала в Соломоне~~ |
| `solomon_dashboard_id` | ID дашборда в Соломоне |

##### Пример
```
solomon:
  project_id: maps-analytics
  alerts:
  - id: yt-quota-exceeded
    preset: solomon/alerts/yt-quota-exceeding
    preset_options:
      solomon_dashboard_id: infra
      yt_account: maps-analytics
      alert_threshold: 0.9
      channel_ids:
      - MapsAnalyticsMonitorings
```
#### [solomon/alerts/reactor-quota-exceeding](solomon/alerts/reactor-quota-exceeding.jinja)
Мониторинг квоты для проекта в Реакторе.

##### Параметры
| Название | Описание |
|---|---|
| `project_key` | **Обязательный.** Ключ проекта в Реакторе |
| `alert_threshold` | **Обязательный.** Порог срабатывания |
| `channel_ids` | **Обязательный.** Массив ID каналов в Соломоне |
| `solomon_dashboard_id` | ID дашборда в Соломоне |

##### Пример
```
solomon:
  project_id: maps-analytics
  alerts:
  - id: reactor-quota-exceeded
    preset: solomon/alerts/reactor-quota-exceeding
    preset_options:
      solomon_dashboard_id: infra
      project-key: maps-analytics
      alert_threshold: 0.9
      channel_ids:
      - MapsAnalyticsMonitorings
```

#### [solomon/alerts/reaction-failure](solomon/alerts/reaction-failure.jinja)
Алерт на падение реакции в Реакторе.

##### Параметры
| Название | Описание |
|---|---|
| `reaction_path` | **Обязательный.** Путь до реакции в Реакторе |
| `channel_ids` | **Обязательный.** Массив ID каналов в Соломоне |
| `channel_id` | (**deprecated**) ~~**Обязательный.** ID канала в Соломоне~~ |
| `solomon_graph_id` | ID дашборда в Соломоне |
| `message` | Дополнительное сообщение для алерта |

##### Пример
```
solomon:
  project_id: maps-analytics
  alerts:
  - id: tools-duty-failure
    preset: solomon/alerts/reaction-failure
    preset_options:
      reaction_path: /maps/analytics/tools/duty
      solomon_graph_id: reactor-reactions-failures
      channel_ids:
      - MapsAnalyticsMonitorings
```

#### [solomon/alerts/reaction-delay](solomon/alerts/reaction-delay.jinja)
Алерт на отсутствие успешной реакции в Реакторе в заданном промежутке времени.
Точки на графике храняться 31 день (до этого было 7 дней).
Точки на график ставятся в момент завершения реакции, но таймстемп будет начала запуска реакции.

##### Параметры
| Название | Описание |
|---|---|
| `reaction_path` | **Обязательный.** Путь до реакции в Реакторе |
| `channel_ids` | **Обязательный.** Массив ID каналов в Соломоне |
| `channel_id` | (**deprecated**) ~~**Обязательный.** ID канала в Соломоне~~ |
| `solomon_graph_id` | ID дашборда в Соломоне |
| `message` | Дополнительное сообщение для алерта |
| `maximum_unavailability_min` | Промежуток времени в минутах. Значение по умолчанию: 1440 |

##### Пример
```
solomon:
  project_id: maps-analytics
  alerts:
  - preset: solomon/alerts/reaction-delay
    preset_options:
      reaction_path: /maps/analytics/tools/duty
      solomon_graph_id: reactor-reactions-failures
      maximum_unavailability_min: 1440
      channel_ids:
      - MapsAnalyticsMonitorings
```

#### [solomon/alerts/cofe-metric-delay](solomon/alerts/cofe-metric-delay.jinja)
Алерт для метрик [COFE](https://wiki.yandex-team.ru/serp/experiments/cofe/), если метрика не посчитается до `alert_hours`.

##### Параметры
| Название | Описание |
|---|---|
| `cofe_project` | **Обязательный.** Проект в cofe |
| `cofe_task` | **Обязательный.** Название таски в cofe |
| `alert_hours` | **Обязательный.** Порог срабатывания (в часах) |
| `channel_ids` | **Обязательный.** Массив ID каналов в Соломоне |
| `channel_id` | (**deprecated**) ~~**Обязательный.** ID канала в Соломоне~~ | | `solomon_graph_id` | ID дашборда в Соломоне |
| `message` | Дополнительное сообщение для алерта |

##### Пример
```
solomon:
  project_id: maps-analytics
  alerts:
  - preset: solomon/alerts/cofe-metric-delay
    preset_options:
      cofe_project: geo
      cofe_task: main
      alert_hours: 19.5
      solomon_graph_id: cofe
      channel_ids:
      - MapsAnalyticsMonitorings
```

#### [solomon/alerts/artifact-publication-delay](solomon/alerts/artifact-publication-delay.jinja)
Задержка в публикации артефакта в Реакторе. Алерт сработает, если артефакт не был опубликован до `alert_hours`.

##### Параметры
| Название | Описание |
|---|---|
| `reaction_path` | **Обязательный.** Путь до реакции-провайдера артефактов в Реакторе |
| `artifact_path` | **Обязательный.** Путь до артификта в Реакторе |
| `alert_hours` | **Обязательный.** Порог срабатывания (в часах) |
| `channel_ids` | **Обязательный.** Массив ID каналов в Соломоне |
| `channel_id` | (**deprecated**) ~~**Обязательный.** ID канала в Соломоне~~ | | `solomon_graph_id` | ID дашборда в Соломоне |
| `message` | Дополнительное сообщение для алерта |

##### Пример
```
solomon:
  project_id: maps-analytics
  alerts:
  - preset: solomon/alerts/artifact-publication-delay
    preset_options:
      reaction_path: /maps/analytics/logs/cooked-appmetrica-log/daily
      artifact_path: /maps/analytics/logs/cooked-appmetrica-log*
      alert_hours: 10
      solomon_graph_id: reactor-artifacts-logs
      channel_ids:
      - MapsAnalyticsMonitorings
```

#### [solomon/alerts/artifact-publication-delay-user-timestamp](solomon/alerts/artifact-publication-delay-user-timestamp.jinja)
Задержка в публикации артефакта в Реакторе. Алерт сработает, если после последней публикации артефакта прошло более `alert_hours`.

##### Параметры
| Название | Описание |
|---|---|
| `reaction_path` | **Обязательный.** Путь до реакции-провайдера артефактов в Реакторе |
| `artifact_path` | **Обязательный.** Путь до артификта в Реакторе |
| `alert_hours` | **Обязательный.** Порог срабатывания (в часах) |
| `channel_ids` | **Обязательный.** Массив ID каналов в Соломоне |
| `channel_id` | (**deprecated**) ~~**Обязательный.** ID канала в Соломоне~~ | | `solomon_graph_id` | ID дашборда в Соломоне |
| `message` | Дополнительное сообщение для алерта |

##### Пример
```
solomon:
  project_id: maps-analytics
  alerts:
  - preset: solomon/alerts/artifact-publication-delay-user-timestamp
    preset_options:
      reaction_path: /maps/analytics/logs/cooked-appmetrica-log/daily
      artifact_path: /maps/analytics/logs/cooked-appmetrica-log*
      alert_hours: 10
      solomon_graph_id: reactor-artifacts-logs
      channel_ids:
      - MapsAnalyticsMonitorings
```

#### [solomon/alerts/artifact-publication-missed-values](solomon/alerts/artifact-publication-missed-values.jinja)
**Применять только для ежедневных расчетов**
Если при публикации был пропущен хотя бы один день, не считая последнего, то сработает алерт. Нужен для ловли "дырок" в графиках публикации.

##### Параметры
| Название | Описание |
|---|---|
| `reaction_path` | **Обязательный.** Путь до реакции-провайдера артефактов в Реакторе |
| `artifact_path` | **Обязательный.** Путь до артификта в Реакторе |
| `channel_ids` | **Обязательный.** Массив ID каналов в Соломоне |
| `channel_id` | (**deprecated**) ~~**Обязательный.** ID канала в Соломоне~~ | | `solomon_graph_id` | ID дашборда в Соломоне |
| `message` | Дополнительное сообщение для алерта |

##### Пример
```
solomon:
  project_id: maps-analytics
  alerts:
  - preset: solomon/alerts/artifact-publication-delay
    preset_options:
      reaction_path: /maps/analytics/logs/cooked-appmetrica-log/daily
      artifact_path: /maps/analytics/logs/cooked-appmetrica-log*
      alert_hours: 10
      solomon_graph_id: reactor-artifacts-logs
      channel_ids:
      - MapsAnalyticsMonitorings
```

### Channels

#### [solomon/channels/reactor-juggler](solomon/channels/reactor-juggler.jinja)
Создаёт канал для отправки сообщений в Juggler. Заточен под алерты для Реактора.

##### Параметры
Для корректной работы необходимо, чтобы каждый алерт присылал следующие параметры:
| Название | Описание |
|---|---|
| `annotations.juggler_host` | **Обязательный.** host для Juggler |
| `annotations.juggler_service` | **Обязательный.** service для Juggler |
| `annotations.description` | Описание алерта |
| `annotations.message` | Дополнительное сообщение для алерта |
| `annotations.reactor_path` | Путь до сущности в Реакторе. Если задан, то будет сформирована ссылка для Реактора |
| `annotations.solomon_graph_id` | ID графа в Соломоне. Если задан, то будет сформирована ссылка на график в Соломоне |
| `annotations.solomon_dashboard_id` | ID дашборда в Соломоне. Если задан, то будет сформирована ссылка на график в Соломоне |

##### Пример
```
solomon:
  project_id: maps-analytics
  channels:
  - id: MapsAnalyticsMonitorings
    preset: solomon/channels/reactor-juggler
```

#### [solomon/channels/reactor-juggler-simple](solomon/channels/reactor-juggler-simple.jinja)
Создаёт канал для отправки сообщений в Juggler. Проксирует в джаглер только `{{annotations.description}}`.

##### Параметры
Для корректной работы необходимо, чтобы каждый алерт присылал следующие параметры:
| Название | Описание |
|---|---|
| `annotations.juggler_host` | **Обязательный.** host для Juggler |
| `annotations.juggler_service` | **Обязательный.** service для Juggler |
| `annotations.reactor_path` | Путь до сущности в Реакторе. Если задан, то будет сформирована ссылка для Реактора |
| `annotations.description` | Описание алерта |
| `annotations.message` | Дополнительное сообщение для алерта |

##### Пример
```
solomon:
  project_id: maps-analytics
  channels:
  - id: MapsAnalyticsMonitorings
    preset: solomon/channels/reactor-juggler-simple
```

## Проектные пресеты
Пресеты, используемые для нужд конкретной команды/сервиса. Не рекомендуется к использованию соседними командами.

### Пресеты команды [maps-analytics](https://abc.yandex-team.ru/services/maps-analytics)

#### [projects/maps-analytics/juggler/check](projects/maps-analytics/juggler/check.jinja)
Пресет для juggler-проверок в аналитике. Позволяет не задавать `project`, `namespace` и другие второстепенные параметры.

##### Пример
```
juggler:
  checks:
  - service: /maps/analytics/tools/duty_failure
    preset: projects/maps-analytics/juggler/check
```

#### [projects/maps-analytics/juggler/check-critical](projects/maps-analytics/juggler/check-critical.jinja)
Пресет как `check.jinja` + телефонная эскалация


#### [projects/maps-analytics/yql](projects/maps-analytics/yql.jinja)
Базовый пресет для запуска YQL в реакторе с [workflow](https://nirvana.yandex-team.ru/flow/de5de133-dc8b-4bd5-9ba2-434aeebb4138). Позволяет сократить весь конфиг до 10 строчек

##### Параметры
| Название | Описание |
|---|---|
| `path` | **Обязательный.** Путь до реакции (без `scale`) |
| `arcadia_target` | **Необязательный.** Путь до папки в Аркадии. По дефолту берет `path` |
| `queue` | **Необязательный.** Название пресета для очереди |
| `scale` | **Необязательный.** Scale для расчета. Default: `daily` |
| `trigger_cron` | **Необязательный.** Крон выражения по которому запускать реакцию |
| `trigger_artifacts` | **Обязательный.** Список артефактов по таймстемпу которых нужно запускать реакцию. Если не указан, то должен быть указан `trigger_cron` |
| `trigger_artifact_date_index` | **Небязательный.** Индекс откуда брать дату из артефакта (`triggered.data.path.splitToArtifact("/")[trigger_artifact_date_index];`) Берется первый из списка артефакт и у него берется из `yt path`. Если параметр не указывать, то будет взят userTime также у первого артефакта. |
| `on_success_path` | **Небязательный.** YT path, который будет записан в артефакт. |
| `libs` | **Небязательный.** Список библиотек, которые хочется добавить в `YQL`. В воркфлоу пробрасываются под таким же именем |

##### Пример 1: зависимость от артефакта
```
preset: projects/maps-analytics/yql
preset_options:
  path: /maps/analytics/data/apps-installs/ios
  arcadia_target: maps/analytics/data/apps-installs/ios/1d
  trigger_artifacts:
    - /maps/analytics/tools/artifact-helpers/all-30min-tables-ready/appmetrica-yandex-events/1d
    - /maps/analytics/tools/artifact-helpers/all-30min-tables-ready/taxi-metrika-mobile-log/1d
  trigger_artifact_date_index: 3
  libs:
    - analytics/geo/maps/common/clicks_extractor.py
    - analytics/geo/maps/common/clicks_description.json
```

##### Пример 2: зависимость от крона
```
preset: projects/maps-analytics/yql
preset_options:
  path: /maps/analytics/data/company-pretty-format
  arcadia_target: maps/analytics/data/company-pretty-format
  trigger_cron: 0 0 1 * * ?
  queue: reactor/queues/one-in-queue
  scale: weekly
```


### Пресеты команды [maps-front](https://abc.yandex-team.ru/services/maps-front)

#### [projects/maps-front/juggler/check](projects/maps-analytics/juggler/check.jinja)
Пресет для juggler-проверок во фронтенде геосервисов. Позволяет не задавать `project`, `namespace` и другие второстепенные параметры.

##### Пример
```
juggler:
  checks:
  - service: /maps/analytics/tools/duty_failure
    preset: projects/maps-front/juggler/check
```

#### [projects/maps-front/simple-scheduler](projects/maps-front/simple-scheduler.jinja)
Создание простых шедулеров, которые по крону запускают воркфлоу в нирване.

##### Параметры
| Название | Описание |
|---|---|
| `reaction_path` | **Обязательный.** Путь до реакции в Реакторе |
| `cron_expression` | **Обязательный.** СRON выражение |
| `nirvana_workflow_id` | **Обязательный.** ID воркфлоу в нирване |
| `block_results_ttl` | **Небязательный.** Время жизни результатов (кешей) блока в днях (по умолчанию 1) |

##### Пример
```
preset: projects/maps-front/simple-scheduler
preset_options:
  reaction_path: /maps/front/maps/infra/maps-zbp
  cron_expression: 0 0 2 ? * MON,TUE,WED,THU,FRI *
  nirvana_workflow_id: 19f2635b-fa23-41bf-b34a-c6df57f1a99a
```

#### [projects/maps-front/binary-scheduler](projects/maps-front/binary-scheduler.jinja)
Создание простых шедулеров, которые по крону запускают воркфлоу с бинарником в нирване.

##### Параметры
| Название | Описание |
|---|---|
| `reaction_path` | **Обязательный.** Путь до реакции в Реакторе (артефакт в YT будет лежать тут: `//home/maps/front/schedulers/binary/{{reaction_path}}` |
| `version` | **Обязательный.** Версия бинарника |
| `cron_expression` | **Обязательный.** СRON выражение |
| `nirvana_workflow_id` | **Необязательный.** Строка с указанием id воркфлоу |
| `globals` | **Небязательный.** Словарь глобальных переменных |
| `expressions` | **Небязательный.** Словарь выражений |
| `block_results_ttl` | **Небязательный.** Время жизни результатов (кешей) блока в днях (по умолчанию 1) |
| `no_alerts` | **Небязательный.** Eсли true выключает любые виды нотификаций от шедулера |
| `enable_failure_alerts` | **Небязательный.** Если true включает нотификации о падении шедулеров (по умолчанию false) |
| `maximum_unavailability_min` | **Небязательный.** Время, за которое алерт должен хотя бы раз успешно выполниться, иначе будет алерт. (по умолчанию 1440)  |

##### Пример
```
preset: projects/maps-front/binary-scheduler
preset_options:
  name: maps-zbp
  cron_expression: 0 0 3 ? * MON,TUE,WED,THU,FRI *
  version: 1.0.0
  nirvana_workflow_id: abcdef
  globals:
    secret:
      type: CONST
      value: your-secret-name
```
