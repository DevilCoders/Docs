#Создание нового контейнера

- Заходим в sandbox.yandex-team.ru
- Жмем "Create a new task"
- Выбираем TRENDBOX_CI_LXC_BETA и жмем "Create"
- В "Description" пишем любое человеко-понятное описание пакета, например: "PASSPORT FRONTEND"
- В "Shell script to execute during final stage" пишем: 
```bash
#!/usr/bin/env bash

set -ex

apt-get -qq update && apt-get -y install repo-yandex-xenial-stable repo-yandex-xenial-prestable repo-yandex-xenial-testing repo-yandex-xenial-unstable repo-common-stable
apt-get -qq update && apt-get install -y uatraits-nodejs>=1.2.2-12 yandex-lang-detect-nodejs>=1.6-57 libgeobase6-nodejs>=6.0-34 uatraits-data

curl -o /var/cache/geobase/geodata6.bin "https://proxy.sandbox.yandex-team.ru/last/GEODATA6BIN_STABLE?owner=GEOBASE&attrs=%7B%22released%22:%22stable%22%7D"

curl -O https://bootstrap.pypa.io/get-pip.py
python get-pip.py --user
export PATH=~/.local/bin:$PATH

pip install --upgrade -i https://pypi.yandex-team.ru/simple/ pip
pip install -i https://pypi.yandex-team.ru/simple/ awscli==1.16.14
```

- В "Components" выбираем "node_js"
- В "Ubuntu release" выбираем 'trusty'
- Жмем "Run"
- По окончанию сборки контейнера заходим в раздел "CHILD TASKS"
- Находим подзадачу SANDBOX_LXC_IMAGE и переходим в нее
- Заходим в раздел "RESOURCES"
- Находим там наш ресурс под названием TRENDBOX_CI_LXC_IMAGE_BETA
- Копируем номер ресура в конфиг `.trendbox.yml` в свойства `container:resource:`
