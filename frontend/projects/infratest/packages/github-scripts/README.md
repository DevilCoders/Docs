# github-scripts

Общий репозиторий для скриптов связанных с GitHub.

## get-last-release-hashes

Находит предыдущий тег релиза и возвращает его sha и tree-sha.
Поддерживает фильтрацию по префиксу тега, полезно для монорепозиториев.

> :warning: Скрипт работает только с тегами в формате [semver](https://semver.org)

### Установка

```shell
npm install @yandex-int/si.ci.github-scripts --registry=https://npm.yandex-team.ru
```

### Использование

```shell
github-scripts get-last-release-hashes release/images/v1.54.0 -o mm-interfaces -r fiji
```

#### или через npx

```shell
npm_config_registry=https://npm.yandex-team.ru \
 npx -p @yandex-int/si.ci.github-scripts@latest get-last-release-hashes \
 release/images/v1.54.0 -o mm-interfaces -r fiji
```

### Описание аргументов

```shell
get-last-release-hashes [ref]

Positionals:
  ref  Ссылка на текущий релиз (release?/<NAMESPACE?>/<VERSION>).                                             [required]

Options:
  -o, --owner          Владелец репозитория.                                                                  [required]
  -r, --repo           Название репозитория.                                                                  [required]
  -c, --cwd            Путь к Git репозиторию.                                          [default: "<CURRENT_DIRECTORY>"]
  -h, --help           Show help                                                                               [boolean]
  -v, --version        Show version number
```
