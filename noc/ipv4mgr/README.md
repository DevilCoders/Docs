При использовании Arc у вас могут возникнуть проблемы с запусктом `make run` и `make tox`. Чтобы все работало корректно, аркадия должна быть смонтирована с опцией `--allow-other`, наприме р так:
```
arc mount --allow-other --mount arcadia/ --store store/
```

Предварительно стоит удостовериться, что в `/etc/fuse.conf` включена опция `user_allow_other`.

## Dev

Для проверки tvm аутентификации нужно:

1) Установить [tvmtool](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#izpypi):

2) Сделать [конфиг для tvmtool](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#konfig) dev_tvm.json, секрет можно посмотреть тут https://abc.yandex-team.ru/resources/?show-resource=22381186 :
    ```json
    {
        "BbEnvType": 0,
        "clients": {
            "me": {
                "secret": "<SECRET>",
                "self_tvm_id": 2023165,
                "dsts": {
                    "passport": {
                        "dst_id": 223
                    },
                    "abc" : {
                        "dst_id" : 2012190
                    },
                    "staff": {
                        "dst_id": 2001974
                    }
                }
            }
        }
    }
    ```

3) TVMTOOL_LOCAL_AUTHTOKEN=00000000000000000000000000000000 tvmtool -c dev_tvm.json --port 13948

Для разработки также нужны кластера `zk` и `mongo`.

1) Нужно поднять через docker-compose кластера и настроить mongo:

```bash
make dev
```

2) Добавить в `/etc/hosts`:

```
127.0.0.1 mongo1
127.0.0.1 mongo2
127.0.0.1 mongo3
```

3) При запуске сервера нужно передать следующие переменные окружения:

```
RT_APP_AUTH_TYPE=ALLOW_ANY;
AUTHORIZATION_TYPE=ALLOW_ANY;
MONGO_URL=mongodb://localhost:27011,localhost:27012,localhost:27013/?replicaSet=rs0;
ZOO_NODES=localhost:2181,localhost:2182,localhost:2183;
TVMTOOL_LOCAL_AUTHTOKEN=00000000000000000000000000000000;
TVM_PORT=13948;
```
