# Быстрый старт с Merge Queue

Чтобы подключить Merge Queue в свой проект вам нужно:

1. Создать конфигурационный файл в проекте.
2. Настроить обязательные проверки в ветке для которой вы настраиваете Merge Queue.
3. Настроить хук в GitHub.
4. Настроить доступы.

## Конфигурационный файл

Для корректной работы сервиса в репозитории должен быть конфигурационный файл `.config/merge-queue.json`.

> В документации для удобства описания структуры конфигурационного файла используется нотация [JSONPath](http://goessner.net/articles/JsonPath/).

:warning: Конфигурация всегда берётся из дефолтной ветки репозитория.

Конфигурационный файл должен удовлетворять [JSON-схеме](schema/merge-queue.json).

### Настройка для Sandbox CI

Пример минимальной конфигурации:

```json
{
  "requiredChecksBranchName": "master",
  "mergeQueueTask": {
      "type": "SANDBOX_CI_MERGE_QUEUE",
      "owner": "SANDBOX_CI_SEARCH_INTERFACES",
      "priority": { "class": "SERVICE", "subclass": "HIGH" }
  },
  "projectTask": {
      "type": "<название проектной задачи>",
      "owner": "SANDBOX_CI_SEARCH_INTERFACES",
      "priority": { "class": "SERVICE", "subclass": "HIGH" },
      "custom_fields": [
          { "name": "project_git_base_ref", "value": "dev" },
          { "name": "report_github_statuses", "value": false },
          { "name": "project_build_context", "value": "merge-queue" }
      ]
  }
}
```

По умолчанию сервис Sandbox CI не фильтрует события, генерируемые GitHub-ом для действий, производимых роботами. Такое поведение приводит к тому, что после ребейза сервис Sandbox CI запустит сборку пулл-реквеста параллельно со сборкой проекта, созданной из MQ. В некоторых случаях такое поведение приводит к ложным срабатываниям проверок состояния статусов коммита.

Необходимо удостовериться, что конфигурационный файл [`sandbox-ci.json`](../../sandbox-ci/docs/universal.md) имеет фильтр на событие пулл-реквеста для пользователя [@robot-merge-queue].

Фильтрация событий по пользователю выглядит следующим образом. Подробнее о фильтрации можно прочитать в документации к сервису Sandbox CI в секции [«Фильтрация событий»](../../sandbox-ci/docs/universal.md#Фильтрация-событий).

```json5
{
    "github_event_handlers": {
        "pull_request": [
            {
                // ...
                "reject": {
                    "sender_login": ["robot-merge-queue"]
                },
                // ...
            }
        ],
        // другие события
    }
}
```

### Настройка для Trendbox CI

Пример минимальной конфигурации:

```json
{
    "requiredChecksBranchName": "master",
    "mergeQueueTask": {
        "type": "SANDBOX_CI_MERGE_QUEUE",
        "owner": "<MY_OWNER>"
    },
    "poll": {
        "maxRetries": 30,
        "attemptDelay": 30000
    }
}
```

Merge Queue инициирует запуск обязательных проверок изменением пулл-реквеста (ребейз от базовой ветки). После изменения Merge Queue ожидает прокраски GitHub-статусов с обязательными проверками.

Важно, чтобы после ребейза пулл-реквеста Trendbox CI запускал сборку, а по её окончании выставлял статусы на GitHub'е. Это поведение Trendbox CI по умолчанию. Если это не так – проверьте [настройки запуска сборок](https://github.yandex-team.ru/search-interfaces/trendbox-ci/blob/master/docs/2-features/triggers.md) в вашем `.trendbox.yml` файле.

## Настройка обязательных проверок

Необходимо добавить ветку, для которой настраивается Merge Queue, в список защищенных:

![protected branch](./assets/protected-branch.png)

Далее включить проверку статусов перед merge и выбрать, какие статусы являются обязательными:

![required checks](./assets/required-checks.png)

Если по каким-то причинам вам не подходят `required checks` в настройках GitHub'а, вы можете указать названия обязательных GitHub-статусов явно в поле `requiredChecks` MQ-конфига.

## Настройка хука

В настройках репозитория (`https://github.yandex-team.ru/<owner>/<repo>/settings/hooks/`) добавьте новый вебхук. В качестве адреса (**Payload URL**) укажите:

```
https://merge-queue.si.yandex-team.ru/v2/github/issue-comment
```

![URL вебхука](./assets/add-webhook.png)

Включите доставку событий **Issue comment** и **Status**:

![События](./assets/events.png)

## Настройка доступов

### GitHub

Добавьте пользователя [@robot-merge-queue] в **Collaborators** вашего проекта с **Admin** правами.

### Sandbox

На [странице групп](https://sandbox.yandex-team.ru/admin/groups) в Sandbox выдайте доступ роботу [@robot-merge-queue] вашей группе.

![URL вебхука](./assets/add-robot-to-sandbox-group.png)

Группа указывается в поле `mergeQueueTask.owner`:

```json
{
    "mergeQueueTask": {
        "type": "SANDBOX_CI_MERGE_QUEUE",
        "owner": "<MY_OWNER>"
    }
}
```

### Стартрек

В Стартреке откройте настройки очереди (`https://st.yandex-team.ru/admin/queue/{ключ очереди}/permissions`) и дайте роботу [@robot-merge-queue] доступы **Read** и **Write**.

## Арканум

* Обязательные проверки берутся из GH если они явно не указаны в конфие MQ;
* MQ на текущий момент никак не учитывает галочки проверок в Аркануме;
* Отсутствующие проверки в Аркануме обрабатываются как pending статусы в GH (Бывает, что проверка пропадает если убрать галочку);
* Галочки в Аркануме занесли в search-interfaces/infratest#1911, они никак не учитываются. Скорее были добавлены ради прозрачности и дублирования обязательных проверок в UI.

[@robot-merge-queue]: https://staff.yandex-team.ru/robot-merge-queue