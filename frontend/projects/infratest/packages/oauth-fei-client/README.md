# Консольный клиент для [oauth-middleware](https://arcanum.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/oauth-middleware?rev=r7831243)

## Установка

```bash
npm install [-g] @yandex-int/oauth-fei-client --registry=https://npm.yandex-team.ru/
```

## Использование

Утилита для работы с делегированными токенами для сервисов в системе [OAuth](https://oauth.yandex-team.ru/). Позволяет получать токены для заданного пользователя и проверять их наличие.

Опции:

* `--user` –– пользователь, для которого запрашивается токен. Опцию можно переопределить переменной окружения `OAUTH_FEI_CLIENT_USER`.
* `--endpoint` –– http endpoint, где развернут подсервис oauth-middleware. Опцию можно переопределить переменной окружения `OAUTH_FEI_CLIENT_ENDPOINT`.
* `--app-password` –– пароль зарегистрированного в oauth системе приложения. Опцию можно переопределить переменной окружения `OAUTH_FEI_CLIENT_APP_PASSWORD`.

## Пример

```bash
$ oauth-fei-client --help
oauth-fei-client <command>

Commands:
  oauth-fei-client check  Check token existence for particular user
  oauth-fei-client get    Get token for particular user

Options:
  --version        Show version number                                   [boolean]
  --user           User which will be checked                  [string] [required]
  --endpoint       HTTP URL with OAuth middleware endpoint     [string] [required]
  --app-password   Password for oauth application              [string] [required]
  --help           Show help                                             [boolean]


$ OAUTH_FEI_CLIENT_APP_PASSWORD=<password> oauth-fei-client get --user user1 --endpoint http://merge-queue.si.yandex-team.ru/v2/oauth/token
```
