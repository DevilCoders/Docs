# is-vcs-work-tree

## Установка

```console
npm install @yandex-int/si.ci.is-vcs-work-tree --registry=https://npm.yandex-team.ru
```

## Требования

Для корректной работы требуется, чтобы в PATH были определены пути до исполняемых файлов arc|git.

## Использование

```js
const { isArcWorkTree, isGitWorkTree } = require('@yandex-int/si.ci.is-vcs-work-tree');

(async function main() {
    const arcPath = '/arc/mount/project/path';
    const gitPath = '/git/repo/clone/path';
    const noVcsPath = '/some/path';

    console.log('arc repo:', arcPath);
    console.log('isArcWorkTree', await isArcWorkTree(arcPath)); // true
    console.log('isGitWorkTree', await isGitWorkTree(arcPath)); // false

    console.log('git repo:',gitPath);
    console.log('isArcWorkTree', await isArcWorkTree(gitPath)); // false
    console.log('isGitWorkTree', await isGitWorkTree(gitPath)); // true

    console.log('some path', noVcsPath);
    console.log('isArcWorkTree', await isArcWorkTree(noVcsPath)); // false
    console.log('isGitWorkTree', await isGitWorkTree(noVcsPath)); // false
}());
```

Синхронные версии функций

* `isArcWorkTreeSync(path: string)`
* `isGitWorkTreeSync(path: string)`
