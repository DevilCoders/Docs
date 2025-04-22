# arc-transplant

Набор утилит для трансплантации арковых коммитов в гит репозиторий.

## Установка

```console
npm i @yandex-int/si.ci.arc-transplant --registry=https://npm.yandex-team.ru
```

## Использование

```js
const mountPath = '~/arc/mount'
const storePath = '~/arc/store'
const projectPathInArcadia = 'frontend/projects/ci'

const gitRepoPath = '~/ci';

const paths = {
    arcMountPath: mountPath,
    arcStorePath: storePath,
    projectPathInArcadia,
    gitRepoPath,
};

// Инициализируем шеллы git/arc
const gitShell = new GitShell(gitRepoPath);
const arcShell = new ArcShell({ mount: mountPath, store: storePath, workingDir: projectPathInArcadia });

const reviewRequestId = 123456;

// Переносим коммиты из ветки ревью-реквеста 123456 в гит
await cloneAndTransplant(reviewRequestId, paths, { gitShell, arcShell });

// Определяем название текшей ветки
const branch = await gitShell.getCurrentBranch();

// Пушим ветку в ремоут
await gitShell.push(branch);
```
