# release-monorepo-cli

Инструмент для работы с релизами сервисов в монорепозитории [frontend](https://github.yandex-team.ru/search-interfaces/frontend).

## Документация

* [Рецепт настройки релизов в проекте](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/release-cli/docs/setup.md)
* [Формат конфигурационного файла](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/release-cli/docs/configuration.md)
* [Настройка доступов](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/release-cli/docs/setup.md)

## Установка

```console
$ npm i -D @yandex-int/release-monorepo-cli
```

## Использование

### Регулярные релизы

Запуск релиза всех сервисов в монорепозитории:

```console
$ npx release-monorepo create
```

Запуск релиза всех сервисов в монорепозитории, кроме указанных:

```console
$ npx release-monorepo create --exclude <service-name1> <service-name2>

Skip release for services/<service-name1>
Skip release for services/<service-name2>
```

### Внеплановые релизы

Запуск релиза одного сервиса в монорепозитории (используется для внеплановых релизов):

```console
# <service-name> — название директории сервиса `services/<service-name>`
$ npx release-monorepo create --service <service-name>
```

Запуск hotfix'а одного сервиса в монорепозитории (используется для внеплановых релизов):

```console
# <service-name> — название директории сервиса `services/<service-name>`
$ npx release-monorepo create --service <service-name> --fix-version 1.2.3
```

### Опции

#### --dry-run

Запуск в `dry-run` режиме. Инструмент проверит возможность отведения релизов и выведет подробную информацию о каждом шаге.

Но отведение релизов не будут запущено.

```console
$ npx release-monorepo -d

Creating release for all changed services

Bumping versions to minor for butterfly service
Checking to create release for services/butterfly
Release check for existing branches in git@github.yandex-team.ru:search-interfaces/frontend.git failed.
Found already existing branches:
release/butterfly/v0.178.0
It is impossible to create release for services/butterfly: previous release in progress
```

## Переменные окружения

### STARTREK_TOKEN 

Используется для поиска и создания релизных задач в [Трекере](https://st.yandex-team.ru/agile/board/10359).

> Для получения OAuth-токена зайдите из под нужного пользователя по ссылке: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b

### ABC_TOKEN

Используется для поиска дежурных для указания их в релизных задачах в [Трекере](https://st.yandex-team.ru/agile/board/10359).

> Для получения OAuth-токена зайдите из под нужного пользователя по ссылке: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=23db397a10ae4fbcb1a7ab5896dc00f6

## Отладка

Чтобы получать дополнительную информацию об ошибках используйте: `DEBUG="release-monorepo-cli:util:print"`.

```console
$ DEBUG="release-monorepo-cli:hooks:on-fail" npx release-monorepo

release-monorepo-cli:hooks:on-fail ServicesBumpVersionError (6 errors)
release-monorepo-cli:hooks:on-fail BumpServiceVersionError { errno: -2,
release-monorepo-cli:hooks:on-fail   code: 'ENOENT',
release-monorepo-cli:hooks:on-fail   syscall: 'open',
release-monorepo-cli:hooks:on-fail   path: '/Users/blond/projects/infratest/services/qapprouter/package.json',
release-monorepo-cli:hooks:on-fail   service: 
release-monorepo-cli:hooks:on-fail    { name: 'qapprouter',
release-monorepo-cli:hooks:on-fail      root: 'services/qapprouter',
release-monorepo-cli:hooks:on-fail      packageFilePath: 'package.json',
release-monorepo-cli:hooks:on-fail      releaseConfigPath: '.config/release.json',
release-monorepo-cli:hooks:on-fail      cwd: '/Users/blond/projects/infratest' } }
...
An error occurred while bump versions for repository "infratest"
```

По умолчанию рекомендуется использовать:

```console
$ DEBUG="release-monorepo-cli:managers:*,release-monorepo-cli:util:exec,release-monorepo-cli:util:print" npx release-monorepo

release-monorepo-cli:managers:repository search services to release in repository "infratest" +0ms
release-monorepo-cli:util:exec executing command: npx --no-install release changelog --config="/Users/blond/projects/infratest/services/zeroline/.config/release.json" +0ms
Could not find last release version in the repository "git@github.yandex-team.ru:search-interfaces/infratest.git".
release-monorepo-cli:util:exec executing command: npx --no-install release check --config="/Users/blond/projects/infratest/services/zeroline/.config/release.json" +3s
All checks completed successfully.
release-monorepo-cli:util:exec command finished: npx --no-install release check --config="/Users/blond/projects/infratest/services/zeroline/.config/release.json" +737ms
release-monorepo-cli:managers:repository services that are ready for release were not found, skip +4s
```
