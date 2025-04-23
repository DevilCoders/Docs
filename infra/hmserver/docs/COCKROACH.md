## HOWTO попасть в sql консоль

Для входа в sql консоль нужны серты кластера cockroach, которые лежат на хостах с cockroach в `/var/lib/cockroach/certs`

С хоста с cockroach выполнить:

```shell script
sudo cockroach sql --certs-dir /var/lib/cockroach/certs/ --host <node-hostname>
```

## HOWTO попасть в ui

Для входа в ui нужно создать юзера через консоль.

```sql
CREATE USER hostman WITH PASSWORD '<password>';
GRANT admin TO hostman;
```

Пароль для пользователя hostman лежит в [секрете cockroach.hostman_user](https://yav.yandex-team.ru/secret/sec-01efy99nzq5n09n2bnq0pb599t/explore/versions)

Сам ui cockroach поднят на 8888 порту
* https://hm-prestable.in.yandex.net:8888/
* https://hm-sas.in.yandex.net:8888/
* https://hm-vla.in.yandex.net:8888/
* https://hm-man.in.yandex.net:8888/
* https://hm-msk.in.yandex.net:8888/
