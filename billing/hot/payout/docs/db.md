# Какую БД используем

Используется postgresql (mdb).

Кластер тут:

- https://yc.yandex-team.ru/folders/akuhco7rmj3pth5fn765/managed-postgresql

# Как подключиться в БД

```shell
$ mkdir -p ~/.postgresql && \
$ wget "https://crls.yandex.net/allCAs.pem" -O ~/.postgresql/root.crt && \
$ chmod 0600 ~/.postgresql/root.crt
```

## Test

```shell
psql "host=c-mdbjllbb9cqvkdlku2gm.rw.db.yandex.net \
      port=6432 \
      sslmode=verify-full \
      dbname=payoutdb \
      user=payout \
      target_session_attrs=read-write"
```

Пароль тут:

- https://yav.yandex-team.ru/secret/sec-01et7zvf2grek64qf506pp7a34

## Prod

```shell
psql "host=c-mdbrg678bi14u1uf4n1e.rw.db.yandex.net \
      port=6432 \
      sslmode=verify-full \
      dbname=payoutdb \
      user=payout \
      target_session_attrs=read-write"
```

Пароль тут:

- https://yav.yandex-team.ru/secret/sec-01eyx3835xj1xv0he4pgvnd109

Но в скором времени будет интеграция с IDM:

- https://st.yandex-team.ru/MDBSUPPORT-3797

# Добавление миграций

Новые миграции достаточно сохранить в директорию `./postgre/migrations`.

Формат имени файла: `V<номер-из-трех-чисел>__<краткая-суть-миграции>.sql`

# Тестирование миграций

```shell
$ make start-db
```

Оно поднимает бд и накатывает миграции. Если что-то пошло не так, будет видно в логе.

# Накат миграций

Если надо накатить миграции руками (в будущем, будет автоматизировано):

```shell
$ virtualenv -p python3.8 .pgmigrate-env
$ source .pgmigrate-env/bin/activate
$ pip install yandex-pgmigrate
$ export PG_HOSTS="c-mdbrg678bi14u1uf4n1e.rw.db.yandex.net"
# $ export PG_HOSTS="c-mdbjllbb9cqvkdlku2gm.rw.db.yandex.net" # test
$ export PG_PASS="XXXX"
$ pgmigrate -v -d postgre/ -c "host=${PG_HOSTS} dbname=payoutdb user=payout port=6432 password=${PG_PASS}" -t latest migrate
```

# Проверка, что накатилось

```shell
payoutdb=> select * from schema_version;
 version |    description    | type | installed_by |        installed_on
---------+-------------------+------+--------------+----------------------------
       1 | Initial           | auto | payout       | 2021-02-19 16:05:41.05437
       2 | payout            | auto | payout       | 2021-02-19 16:05:41.05437
       3 | request           | auto | payout       | 2021-02-19 16:05:41.05437
       4 | request errors    | auto | payout       | 2021-03-05 17:37:26.843248
       5 | request update dt | auto | payout       | 2021-03-19 16:58:20.0176
       6 | timestamptz       | auto | payout       | 2021-03-19 16:58:20.0176
(6 rows)
```
