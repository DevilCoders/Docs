# Сборка ecom логов

Здесь лежат все процессы по сборке еком логов

## graph_generator CLI

```
Usage: ./graph_generator [OPTIONS]

Options:
  --calculator TEXT     calculator_app file name  [required]
  --secret_name TEXT    Nirvana secret_name with credentials to call Nirvana
                        API  [required]

  --pool TEXT           YT pool name  [required]
  --quota TEXT          Nirvana quota name  [required]
  --yt_token TEXT       Nirvana API token  [required]
  --proxy TEXT          YT proxy [hahn, arnold...]  [default: hahn]
  --workflow_guid TEXT  Nirvana workflow GUID
  --log_level TEXT      graph_generator logging level  [default: INFO]
  --mode TEXT           Run mode  [default: dev]
  --root TEXT           root
  --today TEXT          today
  --help                Show this message and exit.
```

## CI/CD
- [Проект в аркадии](https://a.yandex-team.ru/ci/alpaca/releases/timeline?id=feature-factory-release&dir=market%2Fforecast%2Ffeature_factory)
    - [CI/CD config](https://a.yandex-team.ru/arc_vcs/market/forecast/feature_factory/a.yaml)

## Nirvana
Проект в Nirvana
- https://nirvana.yandex-team.ru/project/f8cf874c-6223-477c-a15a-9c3cb33c867e

## Reactor
Реакция запуска графа
- https://reactor.yandex-team.ru/browse?selected=8003188
