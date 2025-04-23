## Сборка и выкладка новой версии образа
### С помощью Sandbox
Просто создаем задачу `BUILD_DOCKER_IMAGE_V6` с параметрами:
```
Package path = metrika/admin/docker-images/base/package.json
Tags to publish image = registry.yandex.net/metrika/base:trusty
Yandex login to use with docker login = robot-metrika-test
Vault item with oauth token = robot-metrika-test-docker-registry-token
Vault item owner = METRIKA
```
Или можно склонировать [`задачу`](https://sandbox.yandex-team.ru/tasks/?tags=DOCKER-BASE-TRUSTY&page=1&pageCapacity=20&forPage=tasks).

В идеале еще дополнительно проставить теги `metrika`, `docker-base-trusty`.

### Сборка локально
```
$ ya package --tar metrika/admin/docker-images/base/package.json
$ tar xf metrika-base-docker-trusty.${version}.trunk.tar.gz
$ docker build -t registry.yandex.net/metrika/base:trusty .
$ docker push registry.yandex.net/metrika/base:trusty
```

## Узнать версию изнутри контейнера
```
# docker_base_svn_version
Svn info:
    URL: svn+ssh://zomb-sandbox-rw@arcadia.yandex.ru/arc/trunk/arcadia
    Last Changed Rev: 3543934
    Last Changed Author: iddqd
    Last Changed Date: 2018-04-11 04:15:50 +0300 (Wed, 11 Apr 2018)

Other info:
    Build by: sandbox
    Top src dir: /place/sandbox-data/srcdir/arcadia_cache
    Top build dir: /place/sandbox-data/build_cache/yabuild/build_root/qv70/00047c
    Hostname: linux-ubuntu-12-04-precise
    Host information:
        Linux linux-ubuntu-12-04-precise 4.9.51-13 #1 SMP Wed Sep 20 12:07:38 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
```