# Merge Queue API

* [`POST /v2/api/queue/disable`](#disable) — остановить очередь в указанных проектах.
* [`POST /v2/api/queue/enable`](#enable) — включить очередь в указанных проектах.

## <a name="disable"></a> `POST /v2/api/queue/disable`

Останавливает очередь в указанных проектах.

### Query-параметры

* `queueId` — ID очереди, проект (`owner/repo`). Если не передан, останавливает очередь для всех проектов.
* `services` — Список сервисов в проекте, через запятую. Если не передан, останавливает очередь для всех сервисов в указанном проекте.

### Примеры использования

Остановить очередь сервисов `@yandex-int/health` и `@yandex-int/ydo` в проекте `search-interfaces/frontend`:

```bash
curl -X POST "https://merge-queue.si.yandex-team.ru/v2/api/queue/disable?queueId=search-interfaces/frontend&services=@yandex-int/health,@yandex-int/ydo"
```

Остановить очередь в проекте `serp/web4`:

```bash
curl -X POST "https://merge-queue.si.yandex-team.ru/v2/api/queue/disable?queueId=serp/web4"
```

Остановить очередь во всех проектах:

```bash
curl -X POST "https://merge-queue.si.yandex-team.ru/v2/api/queue/disable"
```

## <a name="enable"></a> `POST /v2/api/queue/enable`

Включает очередь в указанных проектах.

### Query-параметры

* `queueId` — ID очереди, проект (`owner/repo`). Если не передан, включает очередь для всех проектов.
* `services` — Список сервисов в проекте, через запятую. Если не передан, включает очередь для всех сервисов в указанном проекте.

### Пример использования

Включить очередь сервисов `@yandex-int/health` и `@yandex-int/ydo` в проекте `search-interfaces/frontend`:

```bash
curl -X POST "https://merge-queue.si.yandex-team.ru/v2/api/queue/enable?queueId=search-interfaces/frontend&services=@yandex-int/health,@yandex-int/ydo"
```

Включить очередь в проекте `serp/web4`:

```bash
curl -X POST "https://merge-queue.si.yandex-team.ru/v2/api/queue/enable?queueId=serp/web4"
```

Включить очередь во всех проектах:

```bash
curl -X POST "https://merge-queue.si.yandex-team.ru/v2/api/queue/enable"
```

### Возможные коды ответа

#### `200`

Очереди для всех указанных проектов включены.

#### `500`

При включении очередей могут возникнуть ошибки.
В этом случае сервис вернёт `500` с описанием ошибок для проектов, в которых не удалось включить очередь.
Например:

```json
{
   "error" : "Error: Failure in enable all queues",
   "failedQueuesReasonsDict" : {
      "pelican/schoolbook-frontend" : "RunAndCheckNextJobsError: error details...",
      "search-interfaces/frontend": "QueueEnableError: error details..."
   }
}
```

Виды ошибок:

* `QueueEnableError` — ошибка при активации очереди в проекте.
* `RunAndCheckNextJobsError` — ошибка при запуске MQ job в проекте.

Если проекта нет в `failedQueuesReasonsDict`, это означает, что очередь для него включилась успешно.
