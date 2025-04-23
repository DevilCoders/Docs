Скрипты в этой папке не зависят от TeamCity Runtime. Также здесь используется NodeJS 14 версии (во внешних скриптах
используется 10-я версия).

## Быстрый старт

```bash
# По умолчанию будут использованы "package.json" и "package-lock.json" из корня:
tools/docker/node/bootstrap.sh

# Будут использованы "package.json" и "package-lock.json" из папки "tools/docker/node":
PACKAGE_JSON_DIR="tools/docker/node/" tools/docker/node/bootstrap.sh
```

```bash
# Запускаем скрипт "bar.js" с параметром "baz=qux":
tools/docker/node/run.sh tools/foo/bar.js --baz=qux
```