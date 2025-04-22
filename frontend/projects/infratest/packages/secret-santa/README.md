# secret-santa-cli

Случайным образом выбирает пары из переданного списка доменных логинов людей. Первому человеку отправляется письмо о том, что он дарит подарок второму. Каждый единожды является поздравляющим и принимающим.

Тема и шаблон письма [захардкожены](./lib/email-template.js).

## Установка

```bash
npm install @yandex-int/si.ci.secret-santa-cli --global --registry=https://npm.yandex-team.ru
```

## Требования

Для рассылки писем команда требует наличия корректно выставленных переменных окружения `SMTP_USERNAME` и `SMTP_PASSWORD`.

Изменить видимое имя отправителя можно переменной `SMTP_DISPLAY_NAME`.

Для отладки можно использовать флаг `--dry-run` вместе с переменной `DEBUG=*`.

## Использование

```console
secret-santa <names..>

Draw random pairs from list of names and send emails about their Secret Santa
target.

ENVIRONMENT

Required environment variables are `SMTP_USERNAME` and `SMTP_PASSWORD`.
`SMTP_DISPLAY_NAME` can be used to customize sender display name.

Use `export DEBUG=*` for verbose logging.

EXAMPLES

$ secret-santa name1 name2 name3
$ secret-santa $(< names.txt)

Positionals:
  names  List of names to shuffle from

Options:
  --help     Show help                                                 [boolean]
  --version  Show version number                                       [boolean]
  --dry-run  Do not send any emails                                    [boolean]
```
