# @yandex-int/si.ci.arcadia-github

> `Record<Arcadia path, GitHub Repo>`

Коллекция для хранения соответствий поддиректорий в `/frontend` в Аркадии на репозитории в GitHub.
Данные берутся либо из секции `search-interfaces.arcadia-github` в Genisys, либо из локального файла `data/pairs.json`.

## Установка

```bash
npm install @yandex-int/si.ci.arcadia-github --registry=https://npm.yandex-team.ru
```

## Использование

Пример использования:

```js
const pairs = require('@yandex-int/si.ci.arcadia-github');

const web4 = await pairs.findByGitHubRepo('serp', 'web4');

console.log(web4);
// {
//   "github": {
//     "role": "main",
//     "owner": "serp",
//     "repo": "web4",
//     "branch": "dev",
//     "defaultBranch": "dev"
//   },
//   "arcadia": {
//     "role": "mirror",
//     "path": "frontend/projects/web4"
//   }
// }

const ci = await pairs.findByArcadiaPath('frontend/projects/ci');

console.log(ci);
// {
//   "github": {
//     "role": "main",  
//     "owner": "search-interfaces",
//     "repo": "ci",
//     "branch": "master",
//     "defaultBranch": "master"
//   },
//   "arcadia": {
//     "role": "mirror",
//     "path": "frontend/projects/ci"
//   }
// }

const frontend = await pairs.findByArcadiaPathPrefix('frontend/services');

console.log(frontend);
// {
//   "github": {
//     "role": "main",
//     "owner": "search-interfaces",
//     "repo": "frontend",
//     "branch": "master",
//     "defaultBranch": "master"
//   },
//   "arcadia": {
//     "role": "mirror",
//     "path": "frontend"
//   }
// }
```

## Отладка

Включить вывод отладочной информации можно с помощью переменной окружения:

```bash
export DEBUG=si:ci:arcadia-github
```
