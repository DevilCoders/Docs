# GitHub plugin: get-actual-file

## Описание

Плагин к пакету [GitHub](https://github.com/octokit/rest.js/tree/v8.2.1)

Плагин позволяет получить свежую версию файла относительно указанного ПР.
Он стягивает файл из base ветки если он изменился относительно ПР.
Если файл изменился только в ПР, то он возьмет именно его.
Если файл имеет изменение и в base ветке и в ПР, то будет брошена ошибка с просьбой выполнить ребейз.

> **Примечание**
>
> Плагин предназначен для пакета [github](https://github.com/octokit/rest.js/tree/v8.2.1)

## Использование

```js
// Подключить модуль GitHub
const GitHubApi = require('github');

// Настроить модуль GitHub
const github = new GitHubApi({ ... });

// Подключить плагин
const githubPluginInit = require('@yandex-int/si.ci.github-actual-file');

// Инициализировать плагин передав ему экземпляр GitHubApi
const githubPlugin = githubPluginInit(github);

const content = githubPlugin.getActualFileFromPullRequest(pullRequest, 'path/to/file');
```
