# sandbox-shovel-cli

Инструмент для работы с Sandbox-ресурсами и Sandbox-задачами.

:warning: На данный момент `sandbox-shovel-cli` корректно работает с ресурсами только при использовании на Sandbox-агентах во время исполнения Sandbox-задач, так как требует наличия `skynet`.

## Установка

```shell
npm i @yandex-int/si.ci.sandbox-shovel-cli --registry=https://npm.yandex-team.ru
```

## Использование

```shell
sandbox upload-resource /path/to/resource --type=TRENDBOX_CI_RESOURCE
sandbox download-resource --id=100500
sandbox create-task < task.json | sandbox start-task
```

## Команды

Работа с ресурсами:

* [`upload-resource`](#upload-resource)
* [`find-resource`](#find-resource)
* [`download-resources`](#download-resources)

Работа с задачами:

* [`create-task`](#create-task)
* [`start-task`](#start-task)
* [`poll-task`](#poll-task)

### `upload-resource`

Создать Sandbox-ресурс из указанных файлов и загрузить в Sandbox-хранилище.

```console
sandbox upload-resource <path> [type] [description]

Upload files to sandbox resource

Positionals:
  path  Local path to file or folder                                             [string] [required]

Upload options:
  --type         Sandbox resource type                                           [string] [required]
  --description  Sandbox resource description                                               [string]
  --os-family    Operating system family                   [string] [choices: "any", "linux", "osx"]
  --attr-<key>   Use any key to add into resource attributes                                [string]

Sandbox options:
  --sandbox-base-url       URL to Sandbox server[string] [default: "https://sandbox.yandex-team.ru"]
  --synchrophazotron-path  Path to synchrophazotron binary (details on https://nda.ya.ru/3UVEbW)
                                                                                            [string]

Common options:
  --help, -h       Show help                                                               [boolean]
  --version, -v    Show version number                                                     [boolean]
  --output-format  Format of the output, could be text for people or json for pipes
                     [string] [choices: "text", "json"] [default: "json" if piped, "text" otherwise]

Examples:
  sandbox upload-resource /path/to/file-or-folder --type=TRENDBOX_CI_RESOURCE
  sandbox upload-resource /path/to/file --type=MY_RESOURCE --attr-key1=value1 --attr-key2=value2
```

Если не указать `description`, по умолчанию будет сгенерировано по шаблону `Resource created from "${path}" by @yandex-int/sandbox-shovel-cli@${version}`.

### `find-resource`

Найти Sandbox-ресурс по параметрам.

```console
sandbox find-resource

Find sandbox resources by query parameters

Related tasks identifiers:
  --task-ids           Task IDs which created resource                                       [array]
  --dependent-task-id  Task ID which depends on resource searching for                      [number]

Dates:
  --created.from  ISO 8601 Date from which resource was created                             [string]
  --created.to    ISO 8601 Date till which resource was created (now by default)            [string]
  --created       Resource created date interval

Common options:
  --help, -h       Show help                                                               [boolean]
  --version, -v    Show version number                                                     [boolean]
  --output-format  Format of the output, could be text for people or json for pipes
                     [string] [choices: "text", "json"] [default: "json" if piped, "text" otherwise]

Sandbox options:
  --sandbox-base-url  URL to Sandbox server     [string] [default: "https://sandbox.yandex-team.ru"]

Options:
  --os-family            Operating system family           [string] [choices: "any", "linux", "osx"]
  --attr-<key>           Add attribute named <key> to search query                          [string]
  --type                 Sandbox resource type                                              [string]
  --owner                Resource owner                                                     [string]
  --limit                Limit amount of records to return                     [number] [default: 1]
  --state                Resource state
                    [string] [choices: "READY", "NOT_READY", "BROKEN", "DELETED"] [default: "READY"]
  --strict-attrs-search  Join attribute filters by logical AND             [boolean] [default: true]
  --sortBy               Specify  SortBy.<fieldname>: asc for ascending sort by <fieldname> (or desc
                         for descending)

Examples:
  sandbox find-resource --type=TRENDBOX_CI_RESOURCE
  sandbox find-resource --type=TRENDBOX_CI_RESOURCE --attr-key1=value1 --attr-key2=value2
  sandbox find-resource --created.from=2019-04-10T23:59:59.000Z --sortBy.id=desc
  sandbox find-resource --type=TRENDBOX_CI_RESOURCE | sandbox download-resources
```

По умолчанию находится последний созданный ресурс, соответствующий указанным параметрам.
Для поиска нескольких ресурсов нужно указать опцию `--limit`.

При указании атрибутов в результат поиска войдут только те ресурсы, которые имеют все переданные атрибуты.
Для отключения этого поведения используется опция `--no-strict-attrs-search`.
В таком случае будет выполнен поиск ресурсов, у которых есть хотя бы один из указанных атрибутов.

Опция `--dependent-task-id <task id>` позволяет искать среди ресурсов, от которых зависит указанная задача.

### `download-resources`

Скачать один или несколько Sandbox-ресурсов.

Ресурсы будут скачаны по отдельности (не упаковываются в один архив). Указать директорию, в которую будут скачаны все указанные ресурсы можно при помощи опции `--dest-dir`.

```console
sandbox download-resources [ids]

Download sandbox resources

Download options:
  --ids  Resource ids                                                                        [array]

Sandbox options:
  --sandbox-base-url       URL to Sandbox server[string] [default: "https://sandbox.yandex-team.ru"]
  --synchrophazotron-path  Path to synchrophazotron binary (details on https://nda.ya.ru/3UVEbW)
                                                                                            [string]

Common options:
  --help, -h       Show help                                                               [boolean]
  --version, -v    Show version number                                                     [boolean]
  --output-format  Format of the output, could be text for people or json for pipes
                     [string] [choices: "text", "json"] [default: "json" if piped, "text" otherwise]

Options:
  --dest-dir  Path to destination folder                                                    [string]

Examples:
  sandbox download-resources --ids 1 2 3
```

### `create-task`

Создать Sandbox-задачу в статусе **DRAFT**.

```console
sandbox create-task [input] [type] [owner]

Create draft of sandbox task

Create options:
  --input  Task config .json                                                                [string]
  --type   Task type (overrides type defined in task config)                                [string]
  --owner  Task owner (overrides type defined in task config)                               [string]

Sandbox options:
  --sandbox-base-url  URL to Sandbox server     [string] [default: "https://sandbox.yandex-team.ru"]
  --token             Sandbox oauth token. Can be set by environment variable SANDBOX_OAUTH_TOKEN
                                                                                            [string]

Common options:
  --help, -h       Show help                                                               [boolean]
  --version, -v    Show version number                                                     [boolean]
  --output-format  Format of the output, could be text for people or json for pipes
                     [string] [choices: "text", "json"] [default: "json" if piped, "text" otherwise]

Examples:
  sandbox create-task --input="~/draft.json" --owner="guest"
```

Конфигурация задачи описывается с помощью JSON в формате [модели `TaskNew` Sandbox API][task-new-model].
Дополнительно можно использовать сокращённый способ описания входных параметров,
указывая их в виде объекта в свойстве `input_parameters`, а не в виде
массива объектов в свойстве `custom_fields`:

```json
{
  "input_parameters": {
    "foo": "bar"
  }
}
```

вместо

```json
{
  "custom_fields": [
    { "name": "foo", "value": "bar" }
  ]
}
```

Конфигурация задачи может быть передана в утилиту несколькими способами:

```shell
# Через опцию `input` с указанием пути к JSON-файлу с конфигурацией:
sandbox create-task --input=../path/to/my-task.json

# Если опция не указана, конфигурация считывается из `stdin`:
sandbox create-task < my-task.json

# Если опция не указана и `stdin` в интерактивном режиме (не pipe),
# то конфигурация считается пустой.
# В этом случае требуется указать как минимум опцию `type`:
sandbox create-task --type=TRENDBOX_CI_JOB
```

[task-new-model]: https://sandbox.yandex-team.ru/api/redoc#operation/task_list_get

### `start-task`

Запустить выполнение задачи в статусе **DRAFT** по её идентификатору.

```console
sandbox start-task [id]

Start sandbox task

Start options:
  --id  Task id                                                                             [string]

Sandbox options:
  --sandbox-base-url  URL to Sandbox server     [string] [default: "https://sandbox.yandex-team.ru"]
  --token             Sandbox oauth token. Can be set by environment variable SANDBOX_OAUTH_TOKEN
                                                                                            [string]

Common options:
  --help, -h       Show help                                                               [boolean]
  --version, -v    Show version number                                                     [boolean]
  --output-format  Format of the output, could be text for people or json for pipes
                     [string] [choices: "text", "json"] [default: "json" if piped, "text" otherwise]

Examples:
  sandbox start-task --id=42
```

Идентификатор задачи может быть передан несколькими способами:

```shell
# Через опцию `id`:
sandbox start-task --id=42

# Если опция не указана, конфигурация считывается из `stdin`:
sandbox start-task <<< '{ "id": 42 }'

# Последний способ позволяет комбинировать создание и запуск задачи:
sandbox create-task < my-task.json | sandbox start-task
```

### `poll-task`

Дождаться перехода задачи в указанный статус или истечения максимального время ожидания.

> Со списком возможных статусов задач можно ознакомиться [в документации Sandbox](https://wiki.yandex-team.ru/sandbox/tasks/statuses/).

Если по истечению времени ожидания `--timeout` задача не перейдёт в указанный статус, команда завершится с ошибкой, содержащей информацию о текущем статусе задачи.

:warning: Нельзя указать одновременно и статус, и группу статусов.

```console
sandbox poll-task [id] [status] [status-group]

Wait for sandbox task to move to the specified status

Poll options:
  --id             Task id                                                                  [string]
  --status         Expected task status                                          [string] [required]
  --status-group   Expected task status group                                               [string]
  --timeout        Timeout for task polling (ms)                                            [string]
  --retry-timeout  Timeout for single retry (ms)                                            [string]

Sandbox options:
  --sandbox-base-url  URL to Sandbox server     [string] [default: "https://sandbox.yandex-team.ru"]
  --token             Sandbox oauth token. Can be set by environment variable SANDBOX_OAUTH_TOKEN
                                                                                            [string]

Common options:
  --help, -h       Show help                                                               [boolean]
  --version, -v    Show version number                                                     [boolean]
  --output-format  Format of the output, could be text for people or json for pipes
                     [string] [choices: "text", "json"] [default: "json" if piped, "text" otherwise]

Examples:
  sandbox poll-task --id=42 --status=SUCCESS
```

## Опции

* [`token`](#token)
* [`sandbox-base-url`](#sandbox-base-url)
* [`synchrophazotron-path`](#synchrophazotron-path)
* [`output-format`](#output-format)

### `token`

OAuth-токен для работы с Sandbox-сервисом.

> О получении токена читайте в разделе «[Авторизация](https://wiki.yandex-team.ru/sandbox/#avtorizacija)» документации Sandbox.

:warning: Опция `--token` не является безопасным способом передачи токена, воспользуйтесь переменной окружения `SANDBOX_OAUTH_TOKEN`.

### `sandbox-base-url`

Базовый URL Sandbox-сервера.

Можно определить с помощью переменной окружения `SANDBOX_BASE_URL`. По умолчанию `https://sandbox.yandex-team.ru`.

### `synchrophazotron-path`

Путь к исполняемому файлу `synchrophazotron` на Sandbox-агенте.
Нужен для работы с ресурсами во время исполнения Sandbox-задачи.

> Подробнее читайте в [документации к Sandbox](https://wiki.yandex-team.ru/sandbox/cookbook/#kakpoluchitdannyesinxronizirovatresursizpodprocessazadachi).

В Sandbox-окружении значение доступно и будет взято из переменной окружения `SANDBOX_SYNCHROPHAZOTRON_PATH`.

### `output-format`

В каком виде команды будут писать в `stdout` о результатах своей работы: `text` или `json`.
Данная опция доступна для всех команд.
`json` априори содержит больше информации, так как включает в себя все поля задачи, а `text` — зачастую только ссылку на неё.

Значение по умолчанию зависит от окружения.
В интерактивном режиме терминала, значением выбирается человеко-читаемый `text`.
Если `stdout` команды перенаправлен (pipe), то формат автоматически переключается на `json` для удобства композиции команд, которые могут считать JSON из `stdin`.
