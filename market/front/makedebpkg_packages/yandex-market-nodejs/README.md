yandex-market-nodejs
----------------

Пакет с nodejs и бинарными зависимостями маркета.

Является архитектурно (amd64) и дистро-зависимым.

Выкачивает https://github.yandex-team.ru/market/binary-vendor-libs правильной ветки.

### Особенности

  - Везёт npm с собой, потому что npm - неотъемлемая часть nodejs когда дело доходит до разработки чего-либо с её помощью

### Сборка пакета

К этому пакету применимы [общие инструкции по сборке][common-build-info].
В качестве конфига нужно использовать distro.py, где distro — дистрибутив, например `lucid.py` или `trusty.py`

### Загрузка в репозиторий

После сборки пакет нужно загрузить в репозиторий вида `market-distro`, например `market-lucid` или `market-trusty`

[common-build-info]: https://github.yandex-team.ru/market/packages#%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2
[repo-link]: https://github.yandex-team.ru/market/packages/blob/master/README.md#market
[package-upload-info]: https://github.yandex-team.ru/market/packages/blob/master/README.md#%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9
