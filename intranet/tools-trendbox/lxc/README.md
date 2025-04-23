# LXC-контейнер


## Сборка

Процесс сборки почти эквивалентен описанному в стандартной [инструкции](https://github.yandex-team.ru/search-interfaces/trendbox-ci/blob/master/docs/3-recipes/build-lxc.md).

На последнем шаге, в поле `Shell script to execute during final stage` необходимо вставить код из файла `tools_lxc.sh`.

## Содержимое

Для прокси-сервера используется tinyproxy.

Версия Docker зафиксирована ниже последней, потому что 18.xx ругается на cgroup (см. [заведённый баг](https://github.com/docker/for-linux/issues/219)).

Адрес прокси передаётся в докер как 172.17.0.1. С точки зрения сети докера, это адрес хостовой машины.
