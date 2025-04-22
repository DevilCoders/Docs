# @yandex-int/si.ci.startrek-cli

Инструмент для работы со [Startrek](https://st.yandex-team.ru). Требует наличия переменной окружения [STARTREK_TOKEN](#startrek_token).

## Установка

```console
npm install @yandex-int/si.ci.startrek-cli --save-dev --registry=https://npm.yandex-team.ru
```

## Использование

```console
$ npx startrek --help

startrek [command]

Commands:
  startrek comment [issue] [comment] Add comment to the issue

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
```

### Команды

* [startrek comment](./docs/commands/comment.md) — отправляет комментарий в задачу.

## Переменные окружения

### STARTREK_TOKEN

Используется для авторизации в [API Трекера](https://doc.yandex-team.ru/tracker/external/user/API.html).

> Для получения OAuth-токена зайдите из под нужного пользователя по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b).
