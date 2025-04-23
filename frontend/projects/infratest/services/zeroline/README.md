<p align="center">
  <img src="logo.png" height="200px" />
</p>

# zeroline

Сервис для диспетчеризации тикетов в очереди MQ. См. [coroner](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/coroner).

[Страница на wiki](https://wiki.yandex-team.ru/search-interfaces/infra/infrasre/duty/zeroline).

## Документация
* [Принцип работы](docs/general.md)
   * [HTTP API v1](docs/general.md#http-api-v1)
   * [Coroner: источники, анализаторы и правила резолюции](docs/general.md#coroner-источники-анализаторы-и-правила-резолюции)
* [Как писать свои правила](docs/how-to-add-rule/how-to-add-rule.md)
* [Сигналы и метрики](docs/metrics.md)

## Разработка

```sh
npm i
cp .env.example .env
```

В `.env` нужно задать все пустые переменные, а комментарии удалить.

Запуск сервера:

```sh
npm run dev
```
Локальный сервер запускается в режиме dry-run, так что разработка и локальное тестирование не будут влиять на реальные ресурсы (MQ-таски, статистика в ClickHouse и т.п.)

## Выпуск релиза

После влития пулл-реквеста [сделайте релиз в Arcadia CI](./docs/how-to-release/how-to-release.md).

## Развертывание

[Окружение](https://deploy.yandex-team.ru/stage/zeroline). Образ – `registry.yandex.net/search-interfaces/zeroline`.

Необходимые переменные окружения:
```sh
ABC_TOKEN
SANDBOX_AUTH_TOKEN
STARTREK_TOKEN
CLICKHOUSE_HOSTS
CLICKHOUSE_DATABASE
CLICKHOUSE_USER
CLICKHOUSE_PASSWORD
```
