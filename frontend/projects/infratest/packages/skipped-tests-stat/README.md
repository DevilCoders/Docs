# skipped-tests-stat

Скрипт собирает информацию по заскипанным тестам и отправляет ее в statface.

## Установка

```shell
$ npm install @yandex-int/skipped-tests-stat --registry=https://npm.yandex-team.ru
```

## Использование

### Отправка стоимости заскипов

```bash
Collect and report cost of manual checks

skips-stat report

Source
  --owner    Repository owner                                         [required]
  --repo     Repository name                                          [required]
  --pull     PR number
  --release  Release version
  --hash     Tree hash for PR
  --service  Service name
  --task-id  Sandbox task id. Will be used when writing to Tracker worklog.

Tools
  --hermione          Platforms for analysis reports of Hermione
  --hermione-e2e      Platforms for analysis reports of Hermione E2E
  --manual            Calculate cost for manual test cases
  --testpalm-project  TestPalm project

ClickHouse settings
  --ch-host   ClickHouse host. You can specify more than one host.
                                                              [array] [required]
  --ch-user   ClickHouse user login. The password is specified via an
              environment variable: FEI_CH_PASSWORD                   [required]
  --ch-table  ClickHouse table                                        [required]
  --ch-db     ClickHouse DB                                           [required]
  --ch-port   Port for ClickHouse hosts                          [default: 8443]

Other
  --dry                               Enables DRY mode (without reporting)
                                                      [boolean] [default: false]
```

### Проверка «бесплатности» тикета

```bash
Determine whether given issue key is a free for manual testing.

Exits with 0 code for "true", 1 for "false", and 2 for "error".

skips-stat is-free-issue <issue>

Options:
  --free-queue                                            [string] [default: []]
  --free-tags                                             [string] [default: []]
  --free-components                                       [string] [default: []]
```

### Установка time-spent в тикеты Трекера

```bash
skips-stat set-time-spent

Fetch issues with time spent from ClickHouse and set time spent to found issues
in Tracker.

Common
  --start-date  Issues search start date, by default current date
                                           [default: "2020-02-25T14:51:09.900Z"]

ClickHouse settings
  --ch-table  ClickHouse table                                        [required]
  --ch-host   ClickHouse host. You can specify more than one host
                                                              [array] [required]
  --ch-user   ClickHouse user login. The password is specified via an
              environment variable: FEI_CH_PASSWORD                   [required]
  --ch-db     ClickHouse DB                                           [required]
  --ch-port   Port for ClickHouse hosts                          [default: 8443]

Other
  --dry  Enables DRY mode (without update issues)     [boolean] [default: false]

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
```

## Пароль для Clickhouse

Пароль указывается в переменной окружения `FEI_CH_PASSWORD`.
