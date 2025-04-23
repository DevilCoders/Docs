yandex-market-skipper-configs
----------------

Пакет с конфигурацией demo-стендов для [yandex-market-skipper](https://github.yandex-team.ru/market/packages/tree/master/yandex-market-skipper)

  - Все конфигурационные данные хранятся внутри PKGBUILD.
  - Версия меняется руками, внутри PKGBUILD.

### Особенности

  - Присваивает(postinst) указанному внутри PKGBUILD пользователю папку, в которую skipper будет загружать demo-стенды.
    *Но пользователя не создаёт, нужно использовать [роботного](https://beta.wiki.yandex-team.ru/diy/zombik/#zavestirobota)*

### Сборка пакета

К этому пакету применимы [общие инструкции по сборке](https://github.yandex-team.ru/market/packages#%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2). Но учтите, что он не поддерживает переменную rev.

### Загрузка в репозиторий

Этот пакет нужно загрузить в репозиторий [market](https://github.yandex-team.ru/market/packages/blob/master/README.md#market).

Информация о том [как загружать пакеты](https://github.yandex-team.ru/market/packages/blob/master/README.md#%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9).
