yandex-market-skipper
----------------

Пакет с инструментом для установки и журналирования demo-стендов.

###Особенности сборки

  - В пакет собираются два инструмента(skipper, skipper-ssh-receiver)
  - В пакете едет python 3, который используется для запуска skipper.
  - Конфигурации демостендов едут в [config-cs-nginx](https://github.yandex-team.ru/cs-admin/config-cs-nginx/tree/master/cs/etc/nginx/sites-available)

Собирается из репозиториев:
  - https://github.yandex-team.ru/market/skipper
  - https://github.yandex-team.ru/market/skipper-ssh-receiver

###Переменные окружения

  - `rev`(master) хэш коммита или имя ветки/тега в git репозитории skipper

### Сборка пакета

К этому пакету применимы [общие инструкции по сборке](https://github.yandex-team.ru/market/packages#%D0%A1%D0%B1%D0%BE%D1%80%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2).

###Загрузка в репозиторий

Этот пакет нужно загрузить в репозиторий [market-amd64](https://github.yandex-team.ru/market/packages/blob/master/README.md#market-amd64).

Информация о том [как загружать пакеты](https://github.yandex-team.ru/market/packages/blob/master/README.md#%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B0-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2-%D0%B2-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B9).
