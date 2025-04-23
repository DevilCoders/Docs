# messenger.uniproxy

![version](https://badger.yandex-team.ru/npm/@yandex-int/messenger.uniproxy/version.svg)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/messenger.uniproxy)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/messenger.uniproxy)<br>
[![dep health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/messenger.uniproxy)](https://oko.yandex-team.ru/pkg/@yandex-int/messenger.uniproxy)

## Пакет для работы с `Uniproxy`

В качестве сетевого транспорта можно использовать `Websocket` из пакета `@yandex-int/messenger.websocket` или реализовать интерфейс свой (например для тестов)

## `Uniproxy`

Базовый класс для работы с uniproxy соединением. Поддерживает промисифицированные запросы, отпраку и получение событий, работу со стримами, синхронный и асинхронный StateSync

## `UniproxyService`

Прокся для упрощения одновременной работы сразу с несколькими сервисами через одно соединение uniproxy

## `UniproxyError`, `UniproxyExceptionError`, `UniproxySyncStateError`

Удобные расширения стандартного класса `Error` для упрощения обработки ошибок