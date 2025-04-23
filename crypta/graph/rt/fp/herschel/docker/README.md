Шпаргалка
---------

```bash
$ # собрать докер
$ ya package \
    --docker crypta/graph/rt/fp/herschel/docker/package.json \
    --docker-network host \
    --docker-registry registry.yandex.net \
    --docker-repository crypta
$ # проверить список изображений
$ docker image ls registry.yandex.net/crypta/rtfp-herschel
$ IMAGE=$(docker image ls registry.yandex.net/crypta/rtfp-herschel -q | head -1)
$ # запустить шел
$ docker run \
    --network host \
    -it $IMAGE bash
$ # запустить интерактивно
$ docker run \
    --network host \
    -e YT_TOKEN \
    -e CRYPTA_TVM_ID \
    -e CRYPTA_TVM_SECRET \
    -it $IMAGE
$ # запустить в фоне
$ docker run \
    --network=host \
    -e YT_TOKEN \
    -e CRYPTA_TVM_ID \
    -e CRYPTA_TVM_SECRET \
    -d $IMAGE
$ # подключится к работающему контейнеру
$ docker exec -it $(docker ps -q) bash
$ # прочитать логи
$ docker logs $(docker ps -q) -f
$ # остановить контейнер
$ docker stop $(docker ps -q)
```

- `./env.sh` - Установить необходимые переменные окружения.
- `./run.sh` - Пересобрать и запустить в докере.
- `../bin/run.sh` - Пересобрать и запустить приложение.
