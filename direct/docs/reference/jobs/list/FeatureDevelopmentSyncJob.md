## FeatureDevelopmentSyncJob

### Продукт/подсистема

Синхронизация изменений фич из production на разрабоческие среды.


### Роль в работе продукта/подсистемы

При полном включении/выключении фичей в production, изменяет фичи и на разработческих средах.


### Датафлоу

Джоба запущена в окружениях `testing`, `devtest`, `dev7`.

- Получает события об обновлении фичей из production intapi (ручка `GET /features_history`).
- Для каждого события
    - Добавляет/обновляет измененную фичу в базе.
    - Если фича была одновлена на ТС, создает тикет на актуализацию тестов.
    - Обновляет ppc-property `features_sync_last_event_id`.
    - Отправляет уведомление об изменении фичи в канал [direct-features](../../chats.md#direct-features).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка testing](https://juggler.yandex-team.ru/project/direct.prod/aggregate?host=checks_auto.direct.yandex.ru&service=jobs.FeatureDevelopmentSyncJob.working.test&project=direct.test)
- [Логи](https://test.direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'sync.FeatureDevelopmentSyncJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Как пользователи (или команда) заметят проблему и через какое время

Фичи не будут автоматически включаться/выключаться на разрабоческих средах.


### Контакты разработчиков и менеджеров

Разработчики: [darkkeks](https://staff.yandex-team.ru/darkkeks).


### Желательное время исправления в случае поломки

В течении недели.


### Способы регулирования работы джобы

Ppc-property:
- `features_sync_last_event_id` &mdash; последнее обработанное события (pkey таблицы `features_history` в production).
- `features_sync_ignored_features` &mdash; названия фичей, события которых будут игнорироваться джобой.
