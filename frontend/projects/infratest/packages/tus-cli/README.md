# tus-cli

Утилита командной строки для работы с [TUS](https://wiki.yandex-team.ru/test-user-service/).

## Установка

Пакет может быть установлен глобально. Тогда после установки окажется доступна комнда `tus-cli`.

```sh
$ npm install -g @yandex-int/tus-cli --registry=http://npm.yandex-team.ru
```

Также пакет может быть установлен на уровне проекта и вызываться через npx или npm scripts.

## Использование

```sh
tus-cli [<tus-cli params>] <command> [<command params>]
```

Параметры tus-cli:

* `--consumer`, `-c` - [`tus_consumer`](https://wiki.yandex-team.ru/test-user-service/#tusconsumer), в контексте которого выполняется команда. Обязательный параметр.
* `--env`, `-e` - [окружение Паспорта](https://wiki.yandex-team.ru/test-user-service/#env), в контексте которого выполняется команда. По умолчанию `test`.

Альтернативно параметры могут быть указаны через переменные окружения, начинающиеся с `TUS_CLI_`, например `TUS_CLI_CONSUMER` для `--consumer`. Таким образом, для часто используемого консьюмера и/или окружения можно зафиксировать необходимое значение, например, в rc-файлах.

### Поддерживаемые команды

#### `create-consumer`

Создание нового консьюмера TUS. В качестве имени используется установленное в параметре `consumer` значение. После создания консьюмера необходимо раздать права заинтересованным пользователям, т.е. тем, кто будет запускать тесты с данным консьюмером ([подробности по предоставлению доступа в документации TUS](https://wiki.yandex-team.ru/test-user-service/#tusiidm)).

#### `show -l <login>`

Получение информации (логин, пароль, uid, время, до которого заблокирован аккаунт) об аккаунте TUS по логину. В случае, если логин интересующего аккаунта начинается с `yandex-team-` или `yndx-`, такой префикс может быть опущен. Например, для логина `yandex-team-login` можно указать просто `login`.

#### `list -l <groupLoginPrefix>`

Получение той же информации, что и для команды `show`, но для группы аккаутов в терминах [`hermione-auth-commands`](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/hermione-auth-commands#authanygrouploginprefix--lockfor-size-) по префиксу группы. Префиксы `yandex-team-` или `yndx-` также могут быть опущены.

#### `unlock -u <uid>`

Разблокировка аккаунта в TUS по uid.

#### `save -l <login> -p <password>`

Сохранение уже существующего в Паспорте аккаунт в TUS по соответствующим логину `login` и паролю `password`.

#### `remove -l <login>` / `remove -u <uid>`

Удаление аккаунта из TUS по логину или uid. Из Паспорта аккаунт при этом не удаляется.

#### `bind-phone -l <login>` / `bind-phone -u <uid>`

Привязка тестового телефона `+70000000007` к тестовому аккаунту по логину или uid.

#### `--help` / `<command> --help`

Посмотреть help по клишке и по конкретным командам.

## Примеры

Создание консьюмера:

```sh
tus-cli -c "some-new-consumer" create-consumer
```

Получение информации об аккаунте в тестовом окружении Паспорта:

```sh
tus-cli -c "some-consumer" show -l "some-login"
```

Получение информации о группе аккаунтов в продовом окружении Паспорта:

```sh
tus-cli -c "some-consumer" -e "prod" list -l "some-group"
```

Разблокировка аккаунта по `uid` в тестовом окружении Паспорта с установкой консьюмера через переменную окружения:

```sh
TUS_CLI_CONSUMER="some-consumer" tus-cli unlock -u "12345"
```
