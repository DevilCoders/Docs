# Sandbox CI — Sandbox based continuous integration

Проект с Sandbox-тасками для организации процесса непрерывной интеграции.

В данный момент ориентирован преимущественно на фронтенды поисковых сервисов Яндекса — Серп, Картинки, Видео, Новости и общепортальной библиотеки блоков Лего. Но может быть использован и для других сервисов.

## Разработчики

Разработкой занимается [Служба инфраструктуры поисковых интерфейсов](dev-team). Вопросы можно задавать в канал [#sandbox-city] Серпового Slack.

## Как тестировать изменения

Изменения в тасках тестируются с помощью сборки бинаря с тасками. Подробности можно найти [здесь][binary-tasks-wiki].

## Sandbox-таски
Код тасок располагается в корне проекта. Названия всех тасок имеет префикс `sandbox_ci`.

В данный момент реализованы следующие задачи.

Стартовые задачи для запуска процесса непрерывной интеграции для соответствующих проектов:
- [sandbox_ci_fiji] — сборка Fiji (Картинки и Видео)
- [sandbox_ci_web4] — Сборка Серпа

Задачи для запуска тестов:
- [sandbox_ci_fiji_hermione] — запуск Hermione-тестов в Fiji
- [sandbox_ci_fiji_unit_client] — запуск клиентских Unit-тестов в Fiji
- [sandbox_ci_fiji_unit_priv] — запуск Unit-тестов на привы в Fiji
- [sandbox_ci_fiji_unit_tmpl] — запуск тестов на шаблоны(tmpl) в Fiji
- [sandbox_ci_hermione] — запуск Hermione-тестов Серпа
- [sandbox_ci_web4_unit] — запуск Unit-тестов Серпа


## Базовые классы для разработки тасок

Большинство задач следует наследовать от одного из базовых классов тасок. В проекте существуют несколько базовых задач для разных нужд. Большая часть общей функциональности доступна в `BaseTask` через менеджеры (см. ниже).

### sandbox_ci.task.BaseTask

Базовая задача общего назначения. От неё наследуются все остальные базовые таски и большинство тасок проекта.

TBD

### sandbox_ci.task.BuildTask

Базовая задача для работы с исходным кодом проекта. От неё наследуются сборочные задачи проектов.

TBD

## Менеджеры общей функциональности

Все менеджеры доступны в качестве свойств из тасок, наследующихся от любых базовых классов-тасок.

### sandbox.managers.artifacts

Менеджер для работы с артефактами — ресурсами, которые создают таски в определённом формате (`tar.gz`) и с определёнными базовыми атрибутами (например, `project` и `checksum`).

Позволяет:
- создавать артефакты
- искать артефакты по атрибутам
- скачивать и распаковывать артефакты

### sandbox.managers.dependencies

Менеджер для установки зависимостей (в частности, `npm` и `bower`), используя кэш в виде ресурса. Может использоваться с любыми пакетными менеджерами, для которых набор зависимостей можно выразить в виде одного файла, а установку в виде shell-команды.

Используется совместно с `sandbox.managers.lifecycle`.

### sandbox.managers.github_statuses

### sandbox.managers.lifecycle

### sandbox.managers.meta

### sandbox.managers.reports

## Библиотечный и другой общий код

### sandbox_ci.utils.context.BaseEnvironmentContext

Базовый класс для контекстов, устанавливающих переменные окружения (`os.environ`).

### sandbox_ci.utils.context.Node

Контекст для работы с `node` и `npm`, установленых через `nvm` в директории `/opt/nvm`.
На данный момент доступно две версии node в нашем LXC-контейнере: 4 и 6. По умолчанию используется `current`. Также можно проставить версию nodejs с помощью env переменной, пример: `NODEJS=${some-version}`

### sandbox_ci.utils.context.GitRetryWrapper

Контекст для использования прозрачной обёртки над `git` и `git retry`, реализующей retry.

Требует установленных:
- `depot_tools` в директории `/opt/depot_tools`
- скрипта `git`, реализующего прозрачную обёртку над `git retry` в директории `/opt/git-retry-wrapper`

### sandbox_ci.utils.context.ProfiledActionContext

Контекст для измерения длительности операций. Используется методом `self.profiled_action()` базового класса-таски `sandbox_ci.task.BaseTask`.

[dev-team]: https://staff.yandex-team.ru/departments/yandex_search_interface_infra/
[#sandbox-city]: https://serpyandex.slack.com/messages/sandbox-city/
[sandbox_ci_fiji]: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/sandbox_ci_fiji/
[sandbox_ci_web4]: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/sandbox_ci_web4/
[sandbox_ci_hermione]: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/sandbox_ci_hermione/
[sandbox_ci_web4_unit]: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/sandbox_ci_web4_unit/
[sandbox_ci_fiji_hermione]: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/sandbox_ci_fiji_hermione/
[sandbox_ci_fiji_unit_client]: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/sandbox_ci_fiji_unit_client/
[sandbox_ci_fiji_unit_priv]: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/sandbox_ci_fiji_unit_priv/
[sandbox_ci_fiji_unit_tmpl]: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/sandbox_ci_fiji_unit_tmpl/
[binary-tasks-wiki]: https://wiki.yandex-team.ru/search-interfaces/infra/sandbox/binary-tasks/#kaksejjchasprotestirovatservernyjjkodvtaskbox
