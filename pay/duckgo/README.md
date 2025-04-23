# duckgo

DuckGo — микросервис, который выполняет криптографию и проксирование запросов для Yandex Pay в контуре PCI DSS.

Подробности на [Вики](https://wiki.yandex-team.ru/yandexpay/duckgo/)

## Разработка

Для разработки нужно подписывать коммиты GPG ключом. [Документация](https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification/adding-a-new-gpg-key-to-your-github-account) по настройке Git и Github. Также публичную часть GPG ключа нужно добавить на staff.yandex-team.ru

## Сборка релиза

Регламент зафиксирован [в wiki](https://wiki.yandex-team.ru/yandexpay/dev/duckgo/release/).

## Тестирование

Запуск тестов в корне проекта `go test ./...`, дополнительного поднятия зависимостей не требуется.
