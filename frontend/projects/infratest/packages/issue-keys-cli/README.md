# @yandex-int/si.ci.issue-keys-cli

Утилита командной строки для парсинга списка startrek задач из названия Pull Request-а на github.

## Установка

```shell
npm install @yandex-int/si.ci.issue-keys-cli --registry=https://npm.yandex-team.ru
```

## Использование

```shell
npx @yandex-int/si.ci.issue-keys-cli get --owner=guest --repo=project --pr-branch=pull/123
or
npx @yandex-int/si.ci.issue-keys-cli get --arc --pr-branch=review/123
```

## Описание аргументов

```console
Get options:
  --owner     Github owner                                   [string]
  --repo      Github repository name                         [string]
  --prBranch  Github PR branch name                          [string] [required]
  --arc       Use Arcanum instead of Github                  [boolean]
```
