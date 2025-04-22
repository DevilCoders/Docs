#### Директория для тестовых секретов DarkSpirit

Секреты необходимы для работы части функциональности DarkSpirit,
а также для запуска интеграционных тестов на эту функциональность.

Чтобы скопировать секреты в эту директорию - запусти скрипт [download.sh](./download.sh) (из корня проекта!):

```shell script
$ ./secrets/download.sh
mkdir: /etc/yandex/balance-common: Permission denied
Need directory '/etc/yandex/balance-common' with 'write' permission for your user, requesting superuser privileges:
+ sudo mkdir -p /etc/yandex/balance-common
Password:
+ sudo chown prez /etc/yandex/balance-common
+ set +x
Downloading secrets to /Users/prez/work/darkspirit/secrets ...

Downloading secret id=sec-01ec83t0wryy2g774fsx202gwg ...
Secret name: robot-darkspirit-mds-s3-receipts-access-key.txt
Secret version: ver-01ec83t0y7k8a39qrcfck4501c
Secret robot-darkspirit-mds-s3-receipts-access-key.txt was downloaded successfully!

...

All secrets are downloaded
```
Для работы скрипта, должна быть настроена работа [arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
Возникновение ошибки `rsa_signature_error` может означать, что ssh ключ не был добавлен на staff или еще
не успел подцепиться оттуда.

Для запуска DS или тестов требуются секреты в директории `/etc/yandex/balance-common/secrets`.
Это - ограничение фреймворка, который используется в DS.
В случае запуска внутри докера, содержимое папки `secrets` монтируется в нужную директорию в контейнере;
Для локального запуска - скрипт создает symlink в нужную директорию. Для этого скрипт может запросить sudo.
