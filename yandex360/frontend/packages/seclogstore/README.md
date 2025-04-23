[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/packages/seclogstore&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/seclogstore)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/packages/seclogstore&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/packages/seclogstore)

# SecLogstore

Утилита для выгрузки ящиков для ограниченного круга лиц.
Все закрыто tvm доступами на [ABC группу](https://abc.yandex-team.ru/services/seclogstore/)

### Использование
```sh
ssh seclogstore.sas.yp-c.yandex.net

# Устанавливаем необходимые deb пакеты
sudo apt-get update
sudo apt-get install yandex-passport-vault-client

# Устанавливаем nodejs через nvm
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash

# Подключаем nvm в текущей сессии
source ~/.bashrc

# Устанавливаем 14 ноду
nvm install 14

# Глобально устанавливаем seclogstore из внутреннего репозитория
npm i -g seclogstore --registry=https://npm.yandex-team.ru

# Читаем инструкцию
seclogstore --help
# Usage:
#   seclogstore [dump|update] [options]
#
#
# Command dump:
#   Dumps mailbox for selected uid or login.
#   This is default behavior - command name can be skipped.
#   ABC link https://abc.yandex-team.ru/services/seclogstore
#
#   Example:
#     seclogstore dump -u 123
#     seclogstore -u 123
#     seclogstore -u 123 -r 100/1000
#
#   Options:
#     Name            Default     Description
#
#     -u, --uid                   User puid to dump
#     -l, --login                 User login to dump. Will be used if uid is not set.
#     -t, --threads   5           Number of parallel requests to database
#     -r, --rate      500/60000   Number of requests for window (requests/window)
#                                 (Default is 500 for 1 minute)
#     -o, --output    ./output    Directore to dump messages.
#                                 (Absolute or relative to current working directory)
#     -e, --env       intranet    Environment type.
#     --corp                      Shortcut for '--env intranet'
#     --test                      Shortcut for '--env testing'
#
#     -d, --debug     /dev/null   File to log debug info
#
#     --help                      Print this help and exit
#
# Command update:
#   Downloads latest seclogstore version from npm.
#
#   Example:
#     seclogstore update
```

### Разработка

Сборка:
```sh
make build
```

Сборка в режиме отслеживания
```sh
make watch
```
