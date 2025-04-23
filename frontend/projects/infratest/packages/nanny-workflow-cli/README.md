# CLI для @yandex-int/trendbox-ci.nanny-workflow

## Установка

```console
npm i @yandex-int/trendbox-ci.nanny-workflow-cli --registry=https://npm.yandex-team.ru
```

## Примеры

```console
nanny-workflow create-release --resource-path=/path/to/resource --resource-type=TRENDBOX_CI_ARTIFACT --nanny-service-id=renderer_multi_multi_test --sandbox-owner=TRENDBOX_CI_TEAM
```

В данном случае будет создан ресурс в Sandbox из указанного локального файла или папки. Если требуется зарелизить уже готовый ресурс в Sandbox, можно указать его `id`:

```console
nanny-workflow create-release --resource-id=100500 --nanny-service-id=renderer_multi_multi_test --sandbox-owner=TRENDBOX_CI_TEAM
```

В этом случае флаг `--resource-type` необязательный — тип ресурса и так будет известен, т.к. указан конкретный ресурс.

### Команды

### create-release

Позволяет создать релиз-реквест в Nanny для любого произвольного ресурса (в том числе локальной папки или файла) и дождаться переключения снапшота в указанном сервисе в Nanny. [Подробнее](../nanny-workflow/README.md#Как-это-работает) о том как это работает.

```console
Creates Nanny release (https://nda.ya.ru/3UWDev)

Release resource:
  --resource-path  path to local file or folder                         [string]
  --resource-type  Sandbox resource type to use for remote resource created from
                   local one                                            [string]
  --resource-id    Sandbox resource id in case of no local one          [string]

Nanny:
  --nanny-service-id        Nanny service id which will be used to check
                            snapshot activation                         [string]
  --email-notify-to         emails to send notifications on release, includes in
                            "to" field                                   [array]
  --email-notify-cc         emails to send notifications on release, includes in
                            "cc" field                                   [array]
  --webhook-urls            Webhook URLs to send payload on release      [array]
  --component               Nanny component                             [string]
  --nanny-tags              Nanny release tag                            [array]
  --webhook-type            Webhook type                                [string]
  --ensure-deploy           Ensure that release deployed to Nanny      [boolean]
  --ensure-deploy-interval  Interval for polling Nanny status, in secs  [number]
  --ensure-deploy-attempts  Number of attempts for polling Nanny status [number]

Sandbox:
  --sandbox-owner           Sandbox owner to run Sandbox tasks
                                                             [string] [required]
  --sandbox-tags            Sandbox task tag                             [array]
  --sandbox-base-url        Sandbox base URL (https://sandbox.yandex-team.ru by
                            default)                                    [string]
  --sandbox-token-env-name  Sandbox token environment name (SANDBOX_AUTH_TOKEN
                            by default) [string] [default: "SANDBOX_AUTH_TOKEN"]

Release info:
  --title                Release name                                   [string]
  --identifier           Release identifier (release branch for instance)
                                                                        [string]
  --description          Release description (a changelog for instance) [string]
  --startrek-ticket-ids  Tracker tickets to send comments on release     [array]
  --release-type         Release type                                   [string]

Options:
  --help, -h               Show help                                   [boolean]
  --version, -v            Show version number                         [boolean]
  --duplicate-policy-type  Duplicate policy type                        [string]
  --stdin-input            read options from stdin                     [boolean]
  --dry-run                dry run mode                                [boolean]

Examples:
  nanny-workflow create-release --resource-id=100500
  --identifier=release/v0.0.1 --nanny-service-id=renderer_multi_multi_test
  --sandbox-owner=TRENDBOX_CI_TEAM
```

Также все настройки можно передать как JSON через stdin:

```console
cat config.json | nanny-workflow create-release --stdin-input
```

#### Переменные окружения

##### NANNY_TOKEN

Токен пользователя от имени которого будет создан релиз в Nanny. Узнать свой токен можно на [странице oauth][nanny-oauth] в Nanny.

##### SANDBOX_AUTH_TOKEN

Токен пользователя от имени которого будет релизиться ресурс в Sandbox. Узнать свой токен можно на [странице oauth][sandbox-oauth] в Sandbox.

> :warning: Переопределить название переменной можно с помощью флага `--sandbox-token-env-name`

[sandbox-oauth]: https://sandbox.yandex-team.ru/oauth
[nanny-oauth]: https://nanny.yandex-team.ru/ui/#/oauth/
