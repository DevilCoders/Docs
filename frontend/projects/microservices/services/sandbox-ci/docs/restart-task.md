# Клонирование задач

Ручка, запускающая полный перезапуск сборки.

Адрес ручки:

```
https://sandbox-ci.si.yandex-team.ru/restart-task
```

При успешном перезапуске сборки пользователя редиректит на фильтр с тасками Sandbox.

## Ссылка на перезапуск сборки

Для перезапуска сборки пользователю необходимо отправить GET-запрос с параметрами `githubRepoOwner`, `githubRepoName` и `githubPullRequestNumber`:

* `githubRepoOwner` _string_ - Owner GitHub репозитория
* `githubRepoName` _string_ - Имя GitHub репозитория
* `githubPullRequestNumber` _number_ - Номер пулл-реквеста

```
/restart-task?
  githubRepoOwner=owner
  &githubRepoName=repo
  &githubPullRequestNumber=666
```

