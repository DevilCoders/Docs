# Как дебажить docker-контейнер

## Базовые понятия

При падении в админке и в боте есть ссылки на логи падающего контейнера. В первую очередь надо смотреть туда.

Также логи можно погрепать самостоятельно в [графане](https://grafana.vertis.yandex-team.ru/explore).
Например, вот таким запросом `service=af-cabinet layer=test version=23fec6bd24`.

Чтобы запустить контейнер руками на виртуалке нужно знать базовую команду

`docker run registry.yandex.net/vertis/af-<project>:<version>`

* `af-<project>` - название проекта. Например, `af-cabinet`.
* `<version>` - версия контейнера. По факту - это коммит, из которого был собран контейнер.
  Если надо, можно счекатуть то состояние репозитария, из которого был собран контейнер: `git checkout <version>`.

Полная документация по [docker run](https://docs.docker.com/engine/reference/commandline/run/).

## Проверка, что докер работает

```
$ docker run hello-world
```

Если ты получаешь ошибку `Got permission denied while trying to connect to the Docker daemon socket at`,
то надо добавить себя в группу `docker` выполнив команду `sudo usermod -aG docker <login>`. После этого перезапустить терминал (перезайти на виртуалку).

Если ты получаешь ошибку `Error response from daemon: Get https://registry.yandex.net/v2/vertis/af-cabinet/manifests/23fec6bd24: no basic auth credentials.`,
то надо [залогиниться в яндексовый registry](https://wiki.yandex-team.ru/docker-registry/#authorization).


## Примеры операций

### Зайти внутрь контейнера, не запуская приложение

Можно походить по файлам и посмотреть что где лежит.

```
$ docker run -it registry.yandex.net/vertis/af-cabinet:23fec6bd24 /bin/bash

root@1e34e9d7387f:/opt/af-cabinet# ls -l
total 32
drwxr-xr-x  7 root root 4096 Jan 21 11:31 app
drwxr-xr-x  4 root root 4096 Jan 21 11:31 build
drwxr-xr-x  5 root root 4096 Jan 21 11:31 bundles
drwxr-xr-x  4 root root 4096 Jan 21 11:31 configs
drwxr-xr-x 13 root root 4096 Jan 21 11:31 data
drwxr-xr-x  3 root root 4096 Jan 21 11:31 lib
drwxr-xr-x  1 root root 4096 Jan 21 11:31 node_modules
drwxr-xr-x 11 root root 4096 Jan 21 11:31 react
```

* `-it` - Assign name and allocate pseudo-TTY. Запускает терминал.
* `/bin/bash` - указывает, что надо запустить bash при старте контейнера.

Выход из терминала - `ctrl+D`. При выходе контейнер останавливается.

### Запуск приложения

```
$ docker run -e APP_ROOT=/opt/af-cabinet -e NODE_PORT=8080 -e _DEPLOY_METRICS_PORT=8081 -e _DEPLOY_DC=sas -e SENDER_KEY=1 -v /var/cache/geobase/:/var/cache/geobase/ registry.yandex.net/vertis/af-cabinet:2676e313e8

{"_level":"INFO","_time":"2021-01-21T09:38:11.598Z","env":{"NODE_PORT":"8080","_DEPLOY_METRICS_PORT":"8081","_DEPLOY_DC":"sas"},"_message":"Starting container with process.env (_DEPLOY*, NODE_*)"}
{"_level":"INFO","_time":"2021-01-21T09:38:11.665Z","_context":"luster-prometheus","_message":"setup master"}
{"_level":"INFO","_time":"2021-01-21T09:38:11.669Z","_context":"luster-prometheus","_message":"server is listening port=8081"}
{"_time":"2021-01-21T09:38:11.695Z","_thread":"master","_level":"DEBUG","_message":"[luster-bunker] Bunker data loaded from file /opt/af-cabinet/configs/bunker-cache.json"}
{"_time":"2021-01-21T09:38:12.998Z","_thread":"worker:1","_level":"INFO","env":{"NODE_PORT":"8080","_DEPLOY_METRICS_PORT":"8081","_DEPLOY_DC":"sas"},"_message":"Starting container with process.env (_DEPLOY*, NODE_*)"}
{"_time":"2021-01-21T09:38:16.411Z","_thread":"worker:1","_level":"DEBUG","_message":"[luster-bunker] Nodes data updated"}
{"_time":"2021-01-21T09:38:16.413Z","_thread":"worker:1","_level":"INFO","_context":"http_server","_message":"The HTTP server is running at port 8080"}
{"_time":"2021-01-21T09:38:16.547Z","_thread":"worker:1","_level":"DEBUG","_message":"[luster-bunker] Nodes data updated"}
```

* `-e <name>=<value>` - Set environment variables. Установка переменных окружения. Все конфиги (ключи, хосты бекендов и т.п.) поставляются в контейнер через переменные окружения.
  Для запуска контейнера надо выставить необходимые переменные. В примере указаны базовые переменные для запуска. В будущем, они скорее всего будут меняться.
* `-v <local_path>:<container_path>` - Mount volume. Монтирует локальную папку внутрь контейнера. В данном примере, мы монтируем папку с геобазой.

### Зайти внутрь контейнера с запущенным приложением

1. Запускаем приложение как указано выше.
2. В соседнем терминале получаем список запущенных контейнеров
```
$ docker ps
CONTAINER ID        IMAGE                                              COMMAND                  CREATED              STATUS              PORTS               NAMES
9c8a009521b3        registry.yandex.net/vertis/af-cabinet:2676e313e8   "node --max-http-hea…"   About a minute ago   Up About a minute                       happy_pike
```
3. Подключаемся по ID контейнера
```
$ docker exec -it 9c8a009521b3 /bin/bash

root@9c8a009521b3:/opt/af-cabinet# ps ax | grep node
    1 ?        Ssl    0:01 node --max-http-header-size=16384 ./node_modules/.bin/luster configs/production/luster.js
   16 ?        Sl     0:10 /opt/nodejs/14/bin/node --max-http-header-size=16384 /opt/af-cabinet/node_modules/.bin/luster configs/production/luster.js
```


