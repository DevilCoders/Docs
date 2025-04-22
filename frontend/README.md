# Монорепозиторий фронтенда

Oko: [![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend&vcs=arc)](https://oko.yandex-team.ru/repo/frontend/search) |
[пакеты](./packages/README.md) | [сервисы](./services/README.md)

## 👶 Хочу завести новый сервис/пакет
Выполните в корне `npm run create-leaf` и ответьте на вопросы визарда.

## 📘 Документация

Подробные руководства для разработчиков и ответы на частозадаваемые вопросы («как работает X»/«как сделать Y») можно найти в [директории `docs`](./docs/README.md).

## 🚀 Быстрый старт

> ⚠️ Внимание! В репозитории используется система контроля версий `arc`. Не используйте `git` в работе и скриптах.

* [Как работать с `arc`](https://wiki.yandex-team.ru/search-interfaces/arc/)
* [Как перенести существующий GitHub Pull Request в Arcanum](https://wiki.yandex-team.ru/search-interfaces/arc/#git-to-arc)

Установить корневые npm-пакеты:

```bash
npm ci
```

С одним проектом можно работать прямо из директории проекта:

```bash
cd services/health
npm ci
npm run build
```

С несколькими проектами нужно работать с помощью инструмента монорепозитория (`lerna`):

```bash
lerna bootstrap --scope @yandex-int/health --scope @yandex-int/bem-page-object
lerna run build --scope @yandex-int/health --scope @yandex-int/bem-page-object
```

### Команды для код-ревью

См. в [документации сервиса](https://a.yandex-team.ru/arcadia/frontend/projects/devexp/README.md#поддерживаемые-команды).

## Зафиксированные версии пакетов

Для некоторых пакетов в монорепозитории зафиксированы версии зависимостей.

Для проверки используется пакет [depslint](./packages/depslint).
Запуск встроен в pre-commit хук, а также в CI проверку **Linters**.

## Поддержка

Поддержка осуществляется в Slack-канале [#si_frontend](https://yndx-all.slack.com/archives/CFFAR0VR6).

Если там не смогли помочь, стоит сообщить о проблеме [дежурному инфраструктуры](https://wiki.yandex-team.ru/infraduty/).
