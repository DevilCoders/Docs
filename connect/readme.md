# Приложения Коннекта

**portal**<br>
[connect.yandex.ru](https://connect.yandex.ru)<br>
портал Коннекта, основной публичный UI Коннекта

**catalog**<br>
[catalog.ws.yandex-team.ru](https://catalog.ws.yandex-team.ru)<br>
каталог организаций в Директории, внутренняя админка Коннекта

## Запуск приложения

Необходимое для запуска на локальной машине:<br>
*NodeJS*, *Docker for Mac*, *git*, *[magicdev](https://github.yandex-team.ru/toolbox/magicdev)*

```
# app_name = portal | catalog

# приготовление
$ npm i && cd <app_name> && npm i

# запуск
$ npm run dev
# → https://localhost.msup.yandex.ru:8443/       # portal
# → https://localhost.msup.yandex-team.ru:8443/  # catalog

# обновление локализации из Танкера
$ npm run i18n

# сборка и заливка докер-образа в Qloud
# с обновлением версии в текущей git-ветке
$ npm run push -- -v 0.0.1
```

npm-скрипты `i18n` и `push` общие для всех приложений и могут вызываться из корня репозитория с указанием имени приложения:

```
$ npm run i18n -- --app <app_name>
$ npm run push -- --app <app_name> -v 0.0.1
```

## Актуальность зависимостей

[![oko health](https://badger.yandex-team.ru/oko/repo/yandex-directory/connect/health.svg)](https://oko.yandex-team.ru/repo/yandex-directory/connect)

### Сервисы

* [![oko catalog](https://badger.yandex-team.ru/oko/repo/yandex-directory/connect/health.svg?repoFilter=catalog)](https://oko.yandex-team.ru/repo/yandex-directory/connect?&repoFilter=catalog) –– catalog
* [![oko portal](https://badger.yandex-team.ru/oko/repo/yandex-directory/connect/health.svg?repoFilter=portal)](https://oko.yandex-team.ru/repo/yandex-directory/connect?&repoFilter=portal) –– portal
* [![oko portal/server](https://badger.yandex-team.ru/oko/repo/yandex-directory/connect/health.svg?repoFilter=portal/server)](https://oko.yandex-team.ru/repo/yandex-directory/connect?&repoFilter=portal/server) –– portal/server

### Пакеты

* [![oko packages/react-header](https://badger.yandex-team.ru/oko/repo/yandex-directory/connect/health.svg?repoFilter=packages/react-header)](https://oko.yandex-team.ru/repo/yandex-directory/connect?&repoFilter=packages/react-header) –– react-header
* [![oko packages/react-scrollarea](https://badger.yandex-team.ru/oko/repo/yandex-directory/connect/health.svg?repoFilter=packages/react-scrollarea)](https://oko.yandex-team.ru/repo/yandex-directory/connect?&repoFilter=packages/react-scrollarea) –– react-scrollarea
* [![oko packages/store](https://badger.yandex-team.ru/oko/repo/yandex-directory/connect/health.svg?repoFilter=packages/store)](https://oko.yandex-team.ru/repo/yandex-directory/connect?&repoFilter=packages/store) –– store
