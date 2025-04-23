# Contributing

## Quick start

1. Необходимые зависимости:

  * [Авторизация для qtools](https://github.yandex-team.ru/maps/qtools#authorization)
  * docker ([авторизация](https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/#avtorizacija))

1. `git clone git@github.yandex-team.ru:maps/sandbox.git`
1. `make`
1. `make local`
1. Open `http://localhost:9080/`

## Архитектура

За основу проекта использован [baby-loris](https://github.yandex-team.ru/islets/baby-loris). Baby-loris — это каркас для карточных [BEViS](https://github.com/bevis-ui/docs) проектов.

### Server-side

При каждой сборке проекта выкачивается специальный репозиторий `https://github.com/yandex/mapsapi-examples-ru`, в котором хранятся все примеры. По умолчанию выкачиваются все доступные ветки (ветка — набор примеров для конкретной версии API и языка, например, `ru-v2.0`), но можно собирать только нужные, для этого используется параметр `EXAMPLES_PARAMS`:

```sh
EXAMPLES_PARAMS="-l ru -v 2.0" make examples-download
```

### Client-side

#### Libraries

Проект использует две внешние библиотеки, исключая зависимости `islets`: [ace](https://ace.c9.io/) — браузерный редактор кода и [zip.js](http://gildas-lormeau.github.io/zip.js/) — для zip'ования примеров на клиенте. Каждая из этих библиотек была собрана отдельным пакетом статики и раскачена на `yastatic.net`. Пакеты:

* ace — [yandex-maps-ui-sandbox-ace-static-1-1-4](http://c.yandex-team.ru/packagesyandex-maps-ui-sandbox-ace-static-1-1-4)
* zip.js — [yandex-maps-ui-sandbox-zip-static-1-0](http://c.yandex-team.ru/packagesyandex-maps-ui-sandbox-zip-static-1-0)

При необходимости поднять версию библиотеки необходимо будет собрать новый пакет, а после раскатки изменить `url` в соответствующих модулях проекта.

#### JS Fiddle

На данный момент песочница позволяет экспортировать примеры на [JS Fiddle](https://jsfiddle.net), для этого используется [JS Fiddle API](http://doc.jsfiddle.net/api/post.html#post-variables).
Но из-за наличия глюков с поддержкой загрузки внешних ресурсов используется [задекларированный хак](http://doc.jsfiddle.net/use/hacks.html).

## Release

### Автоматическая выкатка тестинга

Сборка нового тестинга происходит с помощью [Trendbox CI](https://github.yandex-team.ru/search-interfaces/trendbox-ci/).

После сборки Docker образа он будет залит в реестр и будет задеплоен тестинг с этим образом.

```sh
make patch # minor, major
git push origin master --follow-tags
```

1. При пуше новых тегов в `master` будет собран тестинг.
1. После выкатки тестинга можно раскатывать продакшен

```sh
npx qtools deploy production
```

### Выкатка руками

Для загрузки статики нужно получить ключ `STATIC_CLIENT_KEY` из секретницы. Лучше всего это сделать через утилиту [ya](https://wiki.yandex-team.ru/yatool/).

Для установки `ya` воспользуйтесь следующим снипетом:
```sh
curl -k https://api-gotya.n.yandex-team.ru/ya > /usr/local/bin/ya
chmod +x /usr/local/bin/ya
```

Катим тестинг:

```sh
make patch
git push --follow-tags
STATIC_CLIENT_KEY=$(ya vault get version sec-01cjz2vkw9hqhf3c7skw5g4zxt -o STATIC_CLIENT_KEY) make release-testing
```

Если возникает diff при деплое и он допустим тогда можно указать флаг `force=true`:
```sh
STATIC_CLIENT_KEY=$(ya vault get version sec-01cjz2vkw9hqhf3c7skw5g4zxt -o STATIC_CLIENT_KEY) npx qtools release testing force=true
```

## Codestyle

* JSCS
* JSHint
* `make validate`

## Check pull request

На PR проверяются линтерами с помощью [Trendbox CI](https://github.yandex-team.ru/search-interfaces/trendbox-ci/).
