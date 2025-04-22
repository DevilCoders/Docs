# @yandex-int/si.ci.release-cli

Инструмент для работы с релизами сервисов поисковых интерфейсов.

## Документация

* [Рецепт настройки релизов в проекте](./docs/setup.md)
* [Формат конфигурационного файла](./docs/configuration.md)
* [Настройка доступов](./docs/access.md)

## Установка

```console
npm install @yandex-int/si.ci.release-cli --save-dev
```

## Использование

```console
$ npx release -h

release <command>

Commands:
  release changelog          Build changelog
  release check              Check whether a new release issue can be created
  release close              Close release issue
  release create             Create release
  release issue <command>    Manages startrek release issue
  release version <command>  Manages release versions

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
```

### Команды

* [release changelog](./docs/commands/changelog.md) — Строит changelog.
* [release check](./docs/commands/check.md) — Проверяет, можно ли создавать новый релиз.
* [release close](./docs/commands/close.md) — Закрывает указанный релиз.
* [release create](./docs/commands/create.md) — Создаёт новый релиз.
* [release issue find](./docs/commands/issue/find.md) — Находит релизный тикет.
* [release version find](./docs/commands/version/find.md) — Находит релизную версию.

## Переменные окружения

### STARTREK_TOKEN 

Используется для поиска и создания релизных задач в [Трекере](https://st.yandex-team.ru/agile/board/10359).

> Для получения OAuth-токена зайдите из под нужного пользователя по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b).

### ABC_TOKEN

Используется для поиска дежурных иw указания их в релизных задачах в [Трекере](https://st.yandex-team.ru/agile/board/10359).

> Для получения OAuth-токена зайдите из под нужного пользователя по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=23db397a10ae4fbcb1a7ab5896dc00f6).
