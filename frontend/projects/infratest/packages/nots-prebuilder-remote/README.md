# nots-prebuilder-remote

Удалённый запуск nots-prebuilder. Для указанного локфайла генерирует в фиксированном окружении prebuild-пакеты и проставляет зависимости от них.

## Usage

```
DEBUG=nots-prebuilder-remote:* npx @yandex-int/nots-prebuilder-remote run --lockfile ./path/to/file
```

## Доступы

Для запуска требуется доступ до Sandbox См. https://docs.yandex-team.ru/sandbox/firewall

Пользователь, запускающий CLI должен состоять в Sandbox группе SANDBOX_CI_SEARCH_INTERFACES.

## Используемые квоты

1) Sandbox API запросы на создание задач. См https://docs.yandex-team.ru/sandbox/api#quota.
2) Вычислительную квоту SANDBOX_CI_SEARCH_INTERFACES для запускаемых задач NOTS_PREBUILDER
3) S3 MDS бакет в квоте FEI для доставки локфайлов.
