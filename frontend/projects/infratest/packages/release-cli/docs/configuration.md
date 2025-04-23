# Формат конфигурационного файла

Документ описывает формат конфигурационного файла `release.json` для одного проекта.

## Настройте репозиторий

Инструмент взаимодействует с репозиторием с помощью [SSH]. Укажите URL к репозиторию в поле `git.repository` согласно [SSH протоколу][SSH Protocol].

В поле `git.baseBranch` необходимо указать основную ветвь репозитория. Из неё будут отведены релизные ветки.

```json
{
    "git": {
        "repository": "git@github.yandex-team.ru:search-interfaces/frontend.git",
        "baseBranch": "master"
    }
}
```

## Настройте проект

Если ваш проект расположен в монорепозитории, необходимо указать путь к проекту от корня монорепозитория.

```json
{
    "project": {
        "path": "services/my-service"
    }
}
```

## Настройте работу с релизными тегами

Инструмент использует теги для поиска релизов.

Настройте название для релизных тегов в поле `git.releaseTag`.

```json
{
    "git": {
        "releaseTag": "<your-service-name>/v{{version}}"
    }
}
```

Используйте плейсхолдер `{{version}}` в названии. При создании и поиске релизных веток вместо него будет подставлена версия релиза.

## Настройка работу с релизными ветками

Чтобы при создании релиза отводить релизные ветки включите их с помощью опции `commands.create.createBranch`.

```json
{
    "commands": {
        "create": {
            "createBranch": true,
        }
    }
}
```

Настройте название для релизных веток в поле `git.releaseBranch`.

```json
{
    "git": {
        "releaseBranch": "release/<your-service-name>/v{{version}}",
    }
}
```

Используйте плейсхолдер `{{version}}` в названии. При создании и поиске релизных веток вместо него будет подставлена версия релиза.

## Настройте работу с релизными задачами

Чтобы при создании релиза создавать релизные задачи включите их с помощью опции `commands.create.createIssue`. 

```json
{
    "commands": {
        "create": {
            "createIssue": true
        }
    }
}
```

Инструмент использует [Трекер] для хранения релизных задач.

Настройте фильтр для поиска релизных задач в поле `issue`. Значения их поля `issue` будут также использоваться при создании релизных задач.

> Подробнее о поддерживаемых полях читайте в документации [Трекера][issue-query].

```json
{
    "issue": {
        "queue": "MY_QUEUE",
        "summary": "my-service/v{{version}}",
        "tags": ["my-service"]
    }
}
```

Используйте плейсхолдер `{{version}}` в названии. При создании и поиске релизных задач вместо него будет подставлена версия релиза.

Чтобы указать исполнителей и подписчиков релизной задачи, заполните соответствующие поля в `commands.issue.create`.

```json
{
    "commands": {
        "issue": {
            "create": {
                "createdBy": "robot-frontend",
                "assignee": "assignee-login",
                "followers": ["follower-login"]
            }
        }
    }
}
```

Чтобы указать дежурного из вашего [ABC]-сервиса, укажите `abc_members` в соответствующем поле.

```json5
{
    "commands": {
        "issue": {
            "create": {
                "createdBy": "ticket-author-login",
                "assignee": {
                    // https://abc.yandex-team.ru/services/serp-qa-duty/duty/?role=863
                    "abc_members": [{
                        "id": 4882, // id abc-сервиса
                        "schedule_name": "Бабуля" // название дежурства
                    }]
                },
                "followers": ["follower-login"]
            }
        }
    }
}
```

## Настройте проверки при отведении релизов

Чтобы запускать проверки перед созданием релиза включите их с помощью опции `commands.create.check`.

```json
{
    "commands": {
        "create": {
            "check": true
        }
    }
}
```

Чтобы не создавать релиз, если релизная ветка уже существует, включите опцию `failOnReleaseBranchExists`.

```json
{
    "checks": {
        "failOnReleaseBranchExists": false
    }
}
```

Чтобы не создавать релиз, если релизная ветка уже существует, включите опцию `failOnReleaseIssueExists`.

```json
{
    "checks": {
        "failOnReleaseIssueExists": true
    }
}
```

Чтобы разрешить создание релиза только при наличии релизной задачи в разрешённых статусах, укажите их в поле `checks.failOnReleaseIssueExists.allowedStatuses`.

```json
{
    "checks": {
        "failOnReleaseIssueExists": {
            "allowedStatuses": [
                "open",
                "readyForRegress"
            ]
        }
    }
}
```

## Настройте проверки при отведении релизов

При создании релиза инструмент строит changelog из задач, попавших в релиз.

Чтобы изменять статус задач при создании релиза укажите в поле `commands.create.transitRelatedIssues` соответствующие статусы.

```json
{
    "commands": {
        "create": {
            "transitRelatedIssues": {
                "statusKeyFrom": "dev",
                "statusKeyTo": "rc"
            }
        }
    }
}
```

## Пример конфигурации

```json
{
    "git": {
        "repository": "git@github.yandex-team.ru:search-interfaces/frontend.git",
        "baseBranch": "master",
        "releaseBranch": "release/<your-service-name>/v{{version}}",
        "releaseTag": "<your-service-name>/v{{version}}"
    },
    "project": {
        "path": "services/<your-service-name>"
    },
    "issue": {
        "queue": "<YOUR_QUEUE>",
        "summary": "<your-service-name>/v{{version}}",
        "tags": ["<your-service-name>"]
    },
    "checks": {
        "failOnReleaseBranchExists": false,
        "failOnReleaseIssueExists": {
            "allowedStatuses": ["open", "readyForRegress"]
        }
    },
    "commands": {
        "issue": {
            "create": {
                "createdBy": "<ticket-author-login>",
                "assignee": {
                    "abc_members": [{
                        "id": 42,
                        "schedule_name": "Релиз инженер"
                    }]
                },
                "followers": ["<follower-login>"]
            }
        },
        "create": {
            "createBranch": true,
            "createIssue": true,
            "check": true,
            "transitRelatedIssues": {
                "statusKeyFrom": "dev",
                "statusKeyTo": "rc"
            }
        }
    }
}
```

[SSH]: https://ru.wikipedia.org/wiki/SSH
[SSH Protocol]: https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols#_the_ssh_protocol
[Трекер]: https://st.yandex-team.ru
[ABC]: https://abc.yandex-team.ru/
