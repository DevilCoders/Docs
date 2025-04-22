# Релизный чувак спешит на помощь

[![npm version](https://badger.yandex-team.ru/npm/release-dude/version.svg)](https://npm.yandex-team.ru/release-dude)
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=travel/frontend/release-dude&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/release-dude)
[![oko vulnerabilities](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=travel/frontend/release-dude&vcs=arc)](https://oko.yandex-team.ru/arc/travel/frontend/release-dude)

### Как использовать

```
npx release-dude --cn=<command_name> --st_queue=<startrack_queue> --st_board=<startrack_board_id>
```

Для общения с API стартрека и гитхаба необходимо знать oAuth токен (либо, в случае гитхаба, можно использовать персональный ключ).
Перед использованием `release-dude` необходимо экспортировать переменные окружения `STARTRACK_TOKEN`, `GITHUB_TOKEN`, `TEAMCITY_TOKEN`

```
export STARTRACK_TOKEN=<oAuth_token>
export GITHUB_TOKEN=<deployKey>
export TEAMCITY_TOKEN=<oAuth_token>
```

---

### Создание релизного тикета

Тикет создается основываясь на разнице веток `git_head` и `git_base`. Список связных задач будет сформирован в результате анализа названий коммитов (предполагается, что они содержат идентификаторы задач)

Параметры:

-   `cn=create-release-issue`
-   `st_queue` - соответствующая очередь в стартреке (переменная окружения `STARTRACK_QUEUE`)
-   `st_board` - доска в стартреке (переменная окружения `STARTRACK_BOARD_ID`)
-   `git_owner` - пользователь или организация (переменная окружения `GITHUB_OWNER`)
-   `git_repo` - название репозитория (переменная окружения `GITHUB_REPO`)
-   `git_head` - ветка из которой будет сделан pr
-   `git_base` - ветка в которую будет сделан pr
-   `git_commit_blacklist` - регулярное выражение для фильтрации служебных коммитов (переменная окружения `GITHUB_COMMIT_BLACKLIST`)
-   `git_commit_whitelist` - регулярное выражение для фильтрации коммитов основываясь на измененных файлах (переменная окружения `GITHUB_COMMIT_WHITELIST`)

##### Пример

`npx release-dude --cn=create-release-issue --st_queue=TRAVELFRONT --git_base=master --git_head=dev --git_commit_blacklist='build \d+'`

### Поиск релизного тикета

Вернёт активный релизный тикет.

Параметры:

-   `cn=get-release-issue`
-   `st_queue` - соответствующая очередь в стартреке (вместо использования параметра можно задать переменную окружения `STARTRACK_QUEUE`)
-   `st_board` - доска в стартреке (вместо использования параметра можно задать переменную окружения `STARTRACK_BOARD_ID`)

##### Пример

`npx release-dude --cn=get-release-issue --st_queue=TRAVELFRONT --st_board=5007`

### Изменение статуса задачи

Изменит статус задачи на указанный (если позволяет воркфлоу).

Параметры:

-   `cn=change-issue-status`
-   `st_issue` - идентификатор или ключ задачи
-   `st_status` - статус задачи

##### Пример

`npx release-dude --cn=change-issue-status --st_issue=TRAVELFRONT-1341 --st_status=opened `

### Создание PR

Параметры:

-   `cn=create-pr`
-   `git_owner` - пользователь или организация (вместо использования параметра можно задать переменную окружения `GITHUB_OWNER`)
-   `git_repo` - название репозитория (вместо использования параметра можно задать переменную окружения `GITHUB_REPO`)
-   `git_head` - ветка из которой делаем pr
-   `git_base` - ветка в которую делаем pr
-   `git_title` - заголовок pr
-   `[git_body]` - описание pr
-   `[git_labels]` - бейджи, которые будут добавлены к pr после его создания

### Поиск PR

Параметры

-   `cn=find-pr-by-branch`
-   `git_branch` - имя ветки по которой найти PR

##### Пример

`npx release-dude --cn=create-pr --git_owner=data-ui --git_repo=ya-travel --git_head=release-branch --git_base=master --git_title='Релиз' --git_body='Новый релиз' --git_labels=release`

### Мерж веток

Мержит head в base

Параметры:

-   `cn=merge-pr`
-   `git_owner` - пользователь или организация (вместо использования параметра можно задать переменную окружения `GITHUB_OWNER`)
-   `git_repo` - название репозитория (вместо использования параметра можно задать переменную окружения `GITHUB_REPO`)
-   `git_head` - вливаемая ветка (или коммит)
-   `git_base` - ветка, куда вливаем

##### Пример

`npx release-dude --cn=merge-pr --git_owner=data-ui --git_repo=ya-travel --git_head=master --git_base=dev`

### Добавление лейблов к пулл реквестам привязанным к задаче

Параметры:

-   `cn=add-labels-to-issue-prs`
-   `st_issue_key` - ключ задачи в стартреке
-   `git_labels` - бейджи, которые будут добавлены к pr

##### Пример

`npx release-dude --cn=add-labels-to-issue-prs --st_issue_key=TRAVELFRONT-1523 --git_labels="Testing: complete, goodpr"`

### Удаление лейблов с пулл реквестов привязанных к задаче

Параметры:

-   `cn=remove-labels-from-issue-prs`
-   `st_issue_key` - ключ задачи в стартреке
-   `git_labels` - бейджи, которые будут удалены с pr

##### Пример

`npx release-dude --cn=remove-labels-from-issue-prs --st_issue_key=TRAVELFRONT-1523 --git_labels="Testing: requires fixes"`
