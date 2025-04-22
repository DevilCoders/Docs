Шпаргалка по решардеру
----------------------

```bash
$ # собрать докер
$ ya package \
    --docker ads/bsyeti/big_rt/demo/resharder/docker/package.json \
    --docker-network host \
    --docker-registry registry.yandex.net \
    --docker-repository bigrt
$ # проверить список изображений
$ docker image ls registry.yandex.net/bigrt/demo-resharder
$ IMAGE=$(docker image ls registry.yandex.net/bigrt/demo-resharder -q | head -1)
$ # запустить шел
$ docker run \
    --network host \
    -it $IMAGE bash
$ # запустить решардер интерактивно
$ docker run \
    --network host \
    -e YT_TOKEN \
    -e RESHARDER_TVM_ID \
    -e RESHARDER_TVM_SECRET \
    -it $IMAGE
$ # запустить решардер в фоне
$ docker run \
    --network=host \
    -e YT_TOKEN \
    -e RESHARDER_TVM_ID \
    -e RESHARDER_TVM_SECRET \
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
