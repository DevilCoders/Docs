# Веб интерфейс mCRM
[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=market/lilucrm/campaign/webapp&vcs=arc)](https://oko.yandex-team.ru/arc/market/lilucrm/campaign/webapp)
## Полезные команды
```sh
$ yarn build
```
Production-билд приложения, может использоваться с флагом `--watch`. Для разработки, бандл будет минифицирован, но будут source maps. Не рекомендуется так делать, это очень медленно и не имеет никакого смысла.
```sh
$ yarn serve
```
Запуск `webpack-dev-server` для разработки. Запускает dev-сервер на `https://campaign.local.yandex-team.ru:8080/`, чтоб работала авторизация, нужно настроить nginx на проксирование запросов в этот dev-ceрвер.
При таком запуске запросы к `api` по умолчанию проксируются на первый тестовый стенд (`https://lilucrm.tst.market.yandex-team.ru`)
## Node.js
Использовать версию `12.X.X Node`.
## Зависимости
`yarn install`
## Настройка https в localhost
Для того, чтобы приложение работало c авторизацией, необходимо настроить локально https с сертификатом из [Сертификатора](https://crt.yandex-team.ru/certificates).
Если сертификата нет, его нужно заказать:
![](https://jing.yandex-team.ru/files/loudless/photo_2020-11-19%2018.26.57.jpeg =400x)
И разложить его в /ssl в корне веб проекта`:
```sh
$ mv campaign.local.yandex-team.ru.pem /ssl/campaign.local.yandex-team.ru.pem
$ cd /ssl
$ openssl pkey -in campaign.local.yandex-team.ru.pem -out campaign.local.yandex-team.ru.key
$ openssl crl2pkcs7 -nocrl -certfile campaign.local.yandex-team.ru.pem | openssl pkcs7 -print_certs -out campaign.local.yandex-team.ru.cert
```
## Зависимости

Менеджер зависимостей — `yarn`. После установки или обновления зависимостей обязательно нужно выполнить загрузку пакетов в Sandbox

```sh
sh ../bin/update-node-modules.sh # из корня проекта.
```

Эта команда выполнит `yarn install`, запакует папку `node_modules` в tar-архив и загрузит как ресурс в sandbox и запишет идентификатор ресурса в `node_modules.ya.make`. Далее этот архив будет использоваться во время сборки в ci. Это необходимо потому что в sandbox нельзя сходить в npm (даже внутрияндексовый) за зависимостями. И это самая хрупкая штука во всей сборке, т.к. все postinstall-скрипты выполняются на компьютере разработчика под разными системами (mac os и ubuntu в основном). Никто не может гарантировать того, что собранные локально пакеты для сборки правильно заведутся в ci.

## Если добавлена зависимость

При добавлении зависимости нужно пересобрать node_modules.ya.make

1. Убедиться что сгенерированы ключи `ssh`
2. Убедиться что открытый ключ добавлен на стафе (под датой рождения)
3. Убедиться что приватный ключ добавлен командой `ssh-add` (см. инструкцию на вики)
4. В консоли из папки `webapp` выполнить команду `ssh-agent` (оно вернет управление в консоль)
5. Там же выполнить команду `../bin/update-node-modules.sh`
6. Если пункт 5 не выполняется, то выполнить `yarn install --ignore-engines` и повторить пункт 5
7. После завершения выполнения команды убедиться, что в консоли появилась выдача вроде такой
```
+ ya upload /tmp/tmp.P0DXMzHmdR/node_modules.tgz --ttl=inf
+ awk -F/ /Download link/ {print $4}
+ RES_ID=1506495054
+ printf FROM_SANDBOX(FILE 1506495054 OUT_NOAUTO node_modules.tgz)
+ rm -rf /tmp/tmp.P0DXMzHmdR
```
так же должен измениться файл `node_modules.ya.make` и его содержимое

7.1. значит все хорошо, там же выполнить команду `yarn install`

7.2. если в выдаче только первая строчка `+ ya upload ...` значит что-то пошло не так, см. логи в `/tmp/tmp.xxx/ya_upload.log`, перепроверить все начиная с п. 1
