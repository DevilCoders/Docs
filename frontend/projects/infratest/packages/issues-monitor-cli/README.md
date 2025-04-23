# @yandex-int/si.ci.issues-monitor-cli

Опрашивает Трекер по указанному запросу, накладывает на заданный шаблон и отправляет результат разными транспортами.

## Использование

```console
$ npx @yandex-int/si.ci.issues-monitor-cli --help

Search for issues in Tracker, use results in message templates and send
notifications using various transports.

Search:
  --query             Fetch issues for given query in Tracker. STARTREK_TOKEN
                      env must be set.                       [string] [required]
  --issue-status-key  Look only for issues with given status key.       [string]

Templating:
  --template  Name of the JSON template file inside
              @yandex-int/si.ci.ejs/templates, see README for examples.
                                                             [string] [required]
  --project   Project name (can be used as `projectName` in templates). [string]

Notifications:
  --transports  Transports to use to send notifications. Eg: slack,mail.
                                                             [string] [required]
  --recipients  Recipients list. Eg: @user1,#channel1,*channel2.
                @user — send direct message;
                #channel — send message to Slack channel;
                *channel — add user names from given Slack channel topic to
                recipients.                                  [string] [required]
  --dry-run     Do not really send notifications.     [boolean] [default: false]
  --empty       Send notifications even when no issues were found.
                                                      [boolean] [default: false]

Options:
  --help     Show help                                                 [boolean]
  --version  Show version number                                       [boolean]
```

Хорошая практика помечать места использования в Sandbox тегом [`issues-monitor`](https://sandbox.yandex-team.ru/schedulers/?tags=ISSUES-MONITOR).

JSON-шаблоны представляют собой массив из объектов с обязательным полем `transport`. Остальные поля в объекте специфичны для каждого транспорта. См. подробнее в документации к транспортам.

```json
[
  {
    "transport": "transport1",
    "transport1Specific": "field"
  },
  {
    "transport": "transport2",
    "transport2Specific": "field"
  }
]
```

## Требования

Для базовой функциональности (поиска задач) обязательны:

* доступ до `st-api.yandex-team.ru:443`;
* переменная окружения `STARTREK_TOKEN` с внутренним доменным OAuth токеном, который даёт доступ на чтение в нужные очереди.

Для транспорта `mail` нужны:

* доступ до `smtp.yandex-team.ru:465`;
* переменная окружения `SMTP_USERNAME` с доменным логином;
* переменная окружения `SMTP_PASSWORD` с доменным паролем.

Для транспорта `slack` и чтения имён пользователей из заголовков каналов, указанных через `*channel`:

* переменная окружения `SLACK_TOKEN`.
