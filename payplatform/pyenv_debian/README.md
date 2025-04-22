## Дебианизация готового окружения pyenv
Используется готовый собранный pyenv из сборочного образа Биллинга `registry.yandex.net/balance/basic-debuild:14.04`

За основу сборки взяты скрипты [отсюда](https://gist.github.com/mnach/9ab2f6381d23ddfe70891f25b5ca888e).

Запустить конвейер: `make docker-clean-build-upload`

Результаты будут залиты в `yandex-trusty` из-под робота `robot-billing-ci`.
Для создании подписи и заливки в репо нужны `.ssh` и `.gnugp` auth-creds робота, а также файл `.dupload.conf`. Все это можно взять из домашней директории робота на сборочных машинках.
