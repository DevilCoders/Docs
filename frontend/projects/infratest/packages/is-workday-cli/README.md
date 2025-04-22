# is-workday-cli

Утилита для определения является ли указанный день рабочим.
Результат возвращается в виде exit code: `0` — рабочий, `1` — нет.

Предполагается использовать в условных операторах в shell окружении.

## Установка

```bash
npm install @yandex-int/si.ci.is-workday-cli --global --registry=https://npm.yandex-team.ru
```

## Требования

Для работы утилиты требуется доступ до `https://calendar.yandex-team.ru`.

В случаях, когда сервис недоступен, выполнение команды после нескольких неуспешных попыток закончится с кодом `2`.

## Использование

```console
is-workday.js [date]

Determine whether given date is a workday. Exits with 0 code for "true", 1 for
"false", and 2 for "error".

Connection to https://calendar.yandex-team.ru API is required.

EXAMPLES

Install and use globally:
$ npm i -g @yandex-int/si.ci.is-workday-cli
--registry=https://npm.yandex-team.ru
$ is-workday 2018-12-14 && echo workday || echo holiday
workday
$ is-workday 2018-12-15 && echo workday || echo holiday
holiday
$ is-workday && create-release

With npx:
$ npm_config_registry=https://npm.yandex-team.ru npx
@yandex-int/si.ci.is-workday-cli

ENVIRONMENT

Use `export DEBUG=*` for verbose logging.

Positionals:
  date  ISO-8601 calendar date (YYYY-MM-DD). Default is today.          [string]

Options:
  --help         Show help                                             [boolean]
  --version      Show version number                                   [boolean]
  --country, -c  Check for holidays in given country.
       [string] [choices: "Russia", "Ukraine", "Tatarstan", "Belarus", "Turkey",
                                "USA", "Germany", "Finland"] [default: "Russia"]

```
