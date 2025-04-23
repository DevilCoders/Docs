# Миграция из Sandbox CI в Arcadia CI

В данной инструкции поговорим про микросервисную часть Sandbox CI, которая запускает Sandbox-задачи.
Рассмотрим как можно сконфигурировать Arcadia CI для запуска существующих Sandbox-задач вместо Sandbox CI.

Для начало рекомендуем ознакомиться с [документацией Arcadia CI][arcadia-ci-doc] и освежить в памяти [документацию Sandbox CI][sandbox-ci-doc].

В документации Arcadia CI обратите особое внимание на разделы [**Action-ы и триггеры**][arcadia-ci-actions] и [**Создание задачи на основе задачи Sandbox**][arcadia-ci-job-sandbox], наши действия будут базироваться на информации описанных в этих разделах.

[arcadia-ci-actions]: https://docs.yandex-team.ru/ci/actions
[arcadia-ci-job-sandbox]: https://docs.yandex-team.ru/ci/job-sandbox
[arcadia-ci-doc]: https://docs.yandex-team.ru/ci/
[sandbox-ci-doc]: https://a.yandex-team.ru/arcadia/frontend/projects/microservices/services/sandbox-ci/docs/universal.md


## Подготовка

У сервисов [web4][web4/a.yaml] и [fiji][fiji/a.yaml] уже есть свои a.yaml файлы, вам нужно:
1. Создать секрет с токентом для робота @robot-serp-bot. Процесс пошагово описан в разделе [*быстрый старт*][arcadia-ci-token].
1. Добавить в a.yaml файл секцию `ci`, указать полученный в предыдущем пункте токен и название Sandbox-группы (`SANDBOX_CI_SEARCH_INTERFACES`).

```yaml
ci:
  secret: sec-XXXXXX # токен
  runtime:
    sandbox-owner: SANDBOX_CI_SEARCH_INTERFACES
```
1. Коммитить a.yaml файл и отправить ревью-реквест.
1. Делегировать токен перейдя по ссылке в комментарии от робота CI. В ревью придёт робот и попросить делегировать токен. Без подтверждения делегации изменения применены не будут.

[web4/a.yaml]: https://a.yandex-team.ru/arcadia/frontend/projects/web4/a.yaml
[fiji/a.yaml]: https://a.yandex-team.ru/arcadia/frontend/projects/fiji/a.yaml
[arcadia-ci-token]: https://docs.yandex-team.ru/ci/quick-start-guide#get-token


## Реестр задач

Для их хранения наших CI-задач в [реестре][arcadia-ci-registry] Arcadia CI мы заранее добавили директорию [projects/search-interfaces].

[arcadia-ci-registry]: https://docs.yandex-team.ru/ci/jobs#registry
[projects/search-interfaces]: https://a.yandex-team.ru/svn/trunk/arcadia/ci/registry/projects/search-interfaces


## Запуск Sandbox задачи из Arcadia CI

### Триггеры

В этом разделе создадим CI-задачу для запуска наших существующих Sandbox-задач.
Рассмотрим миграцию на примере запуска сборки ревью-реквестов в web4 (процесс мало чем будет отличаться от fiji, эти Sandbox-задач почти идентичны).
Данный триггер в sandbox-ci описан следующим образом, [триггер][sandbox-ci-pr-build-trigger]:
```yaml
- filter:
    base_ref_glob: dev
    head_ref_glob:
    - users/**
    - groups/**
    action:
    - opened
    - reopened
    - synchronize
  reject:
    sender_login:
    - robot-merge-queue
sandbox_tasks: *pr-sandbox-tasks
```

Переведём на человеческий — запустить сборку Sandbox-задач описанных в `sandbox_tasks` если был отправлен/обновлён ревью-реквест в `trunk` из веток `{users/**,groups/**}`. Пропустить если автор ревью-реквеста `robot-merge-queue`.
Опишем аналогичный триггер в конфиге Arcadia CI, в отличие от Sandbox CI в триггеры в нём указываются отдельно от запускаемых Sandbox-задач.

```yaml
  actions:
    pr-stand:
      flow: pr-build-flow
      triggers:
        - on: pr
          into: trunk
          filters:
            - feature-branches:
              - users/**
              - groups/**
              not-author-services: abc-service

  flows:
    pr-build-flow:
      jobs:
        run-pr-build:
          task: projects/search-interfaces/web4/build #обёртка для запуска Sandbox-задач
          attempts: 1
          input:
            <параметры таски>
```

[sandbox-ci-pr-build-trigger]: https://a.yandex-team.ru/arcadia/frontend/projects/web4/.config/sandbox-ci.yml?rev=r8943482#L186-198


### Параметры задач

Исторически так сложилось, что в Sandbox CI конфиге параметры Sandbox-задач описываются в `custom_fields` в виде массива объектов `{name, value}`.
Это отличается от принятого в Arcadia CI формата, вам нужно будет переделать `{name, value}` массивы в объект `{name: value}`, например,

```yaml
custom_fields:
  - name: param1
    value: true
  - name: param2
    value:
    - a
    - b
  - name: param3
    value: some value
```

```yaml
input:
  param1: true
  param2:
    - a
    - b
  param1: 'some value'
```

Значения параметров в конфигах шаблонизируются, но плейсхолдеры в них разные.
Ниже в таблице приведёны взаимозаменяемые плейсхолдеры.

| sandbox-ci.yaml                                | a.yaml                                                               |
| ---------------------------------------------- | -------------------------------------------------------------------- |
| `{{payload.pull_request.base.ref}}`            | `${context.launch_pull_request_info.vcs_info.upstream_branch}`       |
| `{{payload.pull_request.head.ref}}`            | `${context.launch_pull_request_info.vcs_info.feature_branch}`        |
| `{{payload.pull_request.head.sha}}`            | `${context.launch_pull_request_info.vcs_info.feature_revision_hash}` |
| `{{payload.pull_request.number}}`              | `${context.launch_pull_request_info.pull_request.id}`                |
| `{{payload.pull_request.title}}`               | `${context.launch_pull_request_info.pull_request.summary}`           |
| `{{payload.pull_request.head.repo.full_name}}` | serp/web4 или mm-interfaces/fiji                                     |
| `{{payload.repository.name}}`                  | web4 или fiji                                                        |
| `{{payload.repository.owner.login}}`           | serp или mm-interfaces                                               |
| `{{payload.repository.owner.name}}`            | serp или mm-interfaces                                               |
| `{{payload.repository.full_name}}`             | serp/web4 или mm-interfaces/fiji                                     |
| `{{payload.base_ref}}`                         | `${context.branch}`                                                  |
| `{{payload.head_commit.id}}`                   | `${context.target_commit}`                                           |
| `{{payload.ref}}`                              | `${context.branch}`                                                  |

> :warning:
> Перед миграцией актуализируйте список используемых параметров в Sandbox-задачах.
> Некоторые параметры со временем протухли, их удалили из кода Sandbox-задач, но оставили в sandbox-ci.yml конфигах.

Сейчас Sandbox CI при запуске переопределяет и дополняет некоторые параметры конфига, это было нужно для бесшовного перехода из git → arc.

1. Отключаем отправку статусов в GitHub и включаем в Арканум.

   | Название параметра              | Значение  |
   | --------------------------------| --------- |
   | `report_github_statuses`        | `false`   |

1. Для добавления статуса нужны номера дифф-чета и ревю-реквеста. Вам нужно прописать их в свой конфиг сборки ревью-реквеста.

   | Название параметра              | Значение                                              |
   | --------------------------------| ----------------------------------------------------- |
   | `report_arcanum_checks`         | `true`                                                |
   | `arcanum_diff_set_id`           | `${context.launch_pull_request_info.diff_set.id}`     |
   | `arcanum_review_request_id`     | `${context.launch_pull_request_info.pull_request.id}` |

1. Для правильного чекаута необходимо менять параметры чекаута

   | Название параметра              | Значение                                                              |
   | --------------------------------| --------------------------------------------------------------------- |
   | `project_git_base_ref`          | `dev`                                                                 |
   | `project_git_merge_commit`      | пустая строка                                                         |
   | `project_git_merge_ref`         | `[review/${context.launch_pull_request_info.pull_request.id}`]        |
   | `arc_ref`                       | `${context.launch_pull_request_info.vcs_info.upstream_revision_hash}` |


### Запуск Sandbox-задач

Создайте в [projects/search-interfaces] yaml файл с описанием Sandbox-задачи. Минимальная конфигурация содержит название, описание, ABC сервис ответственных и название Sandbox-задачи:

```yaml
title: BuildWeb4
description: Автосборка Серпа (frontend/projects/web4)
maintainers: serpsearch

sandbox-task:
  name: SANDBOX_CI_WEB4
```

Дальше можно описать параметры: в `required-parameters` укажите список обязательных параметров, а в `parameters` дефолтные значения.

```yaml
title: BuildWeb4
description: Автосборка Серпа (frontend/projects/web4)
maintainers: serpsearch

sandbox-task:
  name: SANDBOX_CI_WEB4
  required-parameters:
    - use_arc
    - path_in_arcadia

parameters:
  project_github_owner: serp
  project_github_repo: web4

  report_github_statuses: false
```

Дополнительно можно добавить теги и настроить уведомления, для подробностей посмотрите на пример задачи для запуска сборки web4 в [web4/build.yaml].
Настроенный и работающий конфиг с триггером можно посмотреть в [review/2702747].

[web4/build.yaml]: https://a.yandex-team.ru/arcadia/ci/registry/projects/search-interfaces/web4/build.yaml
[review/2702747]: https://a.yandex-team.ru/review/2702747/files/1


--------------------

Если возникнуть трудности мы готовы помочь и консультировать, [пишите][infraduty].

[infraduty]: https://wiki.yandex-team.ru/infraduty/form/
