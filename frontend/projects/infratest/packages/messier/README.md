# messier

Инструмент для отправки в ClickHouse sqlite-отчетов гермионы.

# CLI

```
messier upload

Uploads hermione reports

Options:
  --help             Show help                                         [boolean]
  --version          Show version number                               [boolean]
  --reports, -r      Paths of reports                         [array] [required]
  --sandbox-task-id  Id of test task                         [string] [required]
  --project          Project name                            [string] [required]
  --tool             Tool name                               [string] [required]
  --build-context    Build context (dev/pull-request/etc.)   [string] [required]
  --commit-sha       Commit SHA                              [string] [required]
  --branch           Branch name                                        [string]
  --batch-size       Count of suites to upload in one time
                                                        [number] [default: 5000]
```

Доступы и БД ClickHouse указываются через env переменные:
- `CLICKHOUSE_HOSTS`
- `CLICKHOUSE_USER`
- `CLICKHOUSE_PASSWORD`
- `CLICKHOUSE_DATABASE`

### Схема таблицы

Схему таблицы можно найти в schema.sql. Создавать её нужно на всех хостах.

### messier?

> Charles Messier was a French astronomer. He published an astronomical catalogue consisting of 110 nebulae and faint star clusters, which came to be known as the Messier objects. The purpose of the catalogue was to help astronomical observers, in particular comet hunters like himself, distinguish between permanent and transient visually diffuse objects in the sky.
