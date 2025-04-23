# npm-owners

Управления владельцами npm пакетов.

## Установка

```shell
npm install @yandex-int/si.ci.npm-owners-cli --global --registry=https://npm.yandex-team.ru
```

## Использование

```shell
npm-owners sync --packages=/tmp/packages --owners=/tmp/owners
```

C npx

```shell
npx @yandex-int/si.ci.npm-owners-cli sync --packages=<(lerna list -a) --owners=<(abc members list --role=developer --format="%l" -- FEI | sort | uniq)
```

## Описание аргументов

```console
Options:
  --packages     packages list file path.                    [string] [required]
  --owners       package owners list file path.              [string] [required]
```
