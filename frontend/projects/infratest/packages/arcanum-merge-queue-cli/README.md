# Arcanum Merge Queue CLI

Часть реализации Sandbox-задачи [SANDBOX_CI_MERGE].

CLI вливает ревью-реквесты [Арканума][Arcanum].

[Arcanum]: https://arcanum.yandex-team.ru/
[SANDBOX_CI_MERGE]: https://a.yandex-team.ru/arc_vcs/sandbox/projects/sandbox_ci/sandbox_ci_merge/__init__.py

## Установка

```console
npm i --save-prod @yandex-int/arcanum-merge-queue-cli
```

## Использование

```console
npx arcanum-merge-queue merge --pr 42#9339c2c29811f43bbcaa18726bfb41cb43ef9f87 --config ./config.json
```

## CLI

```
arcanum-merge-queue-cli merge

Merge arcanum review requests

Options:
  --help, -h              Show help                                                                          [boolean]
  --version, -v           Show version number                                                                [boolean]
  --pr                    Id of review request to merge                                             [array] [required]
  --config                Path to Merge Queue config of project (.config/merge-queue.json)         [string] [required]
  --oauthStoreEndpoint    URL for MQ OAuth store (for autopublish only)                                       [string]
  --arcMountPath          Absolute path to arc mount directory (for autopublish only)                         [string]
  --arcStorePath          Absolute path to arc store directory (for autopublish only)                         [string]
  --arcanumApiOauthToken  Arcanum API OAuth token                                                             [string]

Examples:
  Merge one review request by id:
  npx arcanum-merge-queue-cli.js merge --pr 42#9339c2c29811f43bbcaa18726bfb41cb43ef9f87

  Merge several review requests sequentially by ids:
  npx arcanum-merge-queue-cli.js merge --pr 42#9339c2c29811f43bbcaa18726bfb41cb43ef9f87 --pr 43#3e546d9c2923bd475f72de2e58478aec6cf85a2e
```

## Переменные окружения

* CLI использует переменные окружения из [arcanum-review-request][arcanum-review-request_docs-env].
* Также используется переменная окружения `OAUTH_APP_PASSWORD` для получения токена авторизации, который нужен для запросов делегированных токенов пользователей.

[arcanum-review-request_docs-env]: ../arcanum-review-request/README.md#Переменные-окружения

## Требования к merge-queue.json конфигу

Секция `beforeMerge` может быть использована только для репозиториев где разрешена эта секция. Смотри переменную окружения [ALLOW_BEFORE_MERGE в YDeploy](https://deploy.yandex-team.ru/stages/merge-queue/config/du-merge-queue/box-merge-queue/wl-merge-queue).

В секции `beforeMerge` необходимы следующие поля:
* command: полная команда запуска скрипта автопубликации

Пример:
```json
{
    "beforeMerge": {
        "command": "NPM_USERNAME=robot-frontend NPM_EMAIL=robot-frontend@yandex-team.ru DEBUG=* npx @yandex-int/frontend.ci.autopublish-cli release --refs-to-merge=\"$REFS_TO_MERGE\" --npm-registry-hostname 'npm.yandex-team.ru' --npm-username robot-frontend --npm-email robot-frontend@yandex-team.ru --npm-password=\"$ROBOT_FRONTEND_NPM_PASS\" --toolchain pnpm"
    }
}
```

Секреты должны быть определены в Sandbox vault и доступны для owner, от которого запущена задача.

Для корректной работы должны быть определены в окружении MQ в Y.Deploy:

  * `OAUTH_STORE_ENDPOINT` (default: http://merge-queue.si.yandex-team.ru/v2/oauth/token).
  * `OAUTH_APP_PASSWORD`.
