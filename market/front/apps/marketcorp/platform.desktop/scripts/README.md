Скрипты сборки
--------------------------

Каждый из скриптов(`*.bash`) поддерживает флаг `-h`, это наилучший источник информации, не бойтесь их запускать.

### Переменные окружения

У всех переменных есть своё значение по умолчанию. Если вам потребуется их менять, то лучше посмотреть код нужного скрипта, чтобы знать что вы делаете именно то что нужно.

Общие:

  - `YENV` Окружение в котором запускаются те или иные команды
  - `NPM_CONFIG_REGISTRY` URI npm реестра

Build/Start и любой скрипт, выполнение которого приводит к выкачке зависимостей:

  - `NODEJS_MAJOR_VER` Мажорная версия(в формате 0.10) node.js для которой нужно выполнить перепаковку биндинга
  - `COMMON_REPO` URI репозитория с общими между проектами(маркетом на xscript и node.js) компонентами
  - `COMMON_REV` Ревизия репозитория [common][common]
  - `VENDOR_REPO` URI репозитория с вендорными(node_modules) библиотеками
  - `VENDOR_REV` Ревизия репозитория [marketnode-vendor-libs][marketnode-vendor-libs]
  - `*_SCHEME` Схема для выкачки зависимости, например `git+ssh` или `git+https` и .т.д.

Start:

  - `start_socket_addr` Сокет, который будет прослушивать приложение или enb-server.

[marketnode-vendor-libs]: https://github.yandex-team.ru/market/marketnode-vendor-libs
[common]: https://github.yandex-team.ru/market/common
