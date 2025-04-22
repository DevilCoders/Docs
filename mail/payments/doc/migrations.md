### Как катить миграции
Сейчас у нас есть две базы - для тестового и продакшн стенда, живут они в PGAAS, живут в квоте abc-проекта [Бэкенд Яндекс.Оплаты](https://abc.yandex-team.ru/services/payments/).
* prod: dbname=paymentsdb_prod
* test: dbname=paymentsdb_test

Пользователь DB - payments. Посмотреть пароли пользователя (и вообще всю информацию о базах) можно через API PGAAS.

Здесь и далее примеры работы с PGAAS будут даны через использование из CLI. Доку на CLI можно посмотреть [здесь](https://doc.yandex-team.ru/cloud/mdb/quickstart.html).

```
$ yc mdb cluster List --projectId $PAYMENTS_PROJECT_UUID
{
    "clusters": [
        {
            "createdAt": "2018-09-09T09:18:14.026256+00:00",
            "databaseOptions": {
                "databases": [
                    {
                        "name": "paymentsdb_test",
                        "options": {
                            "extensions": [],
                            "owner": "payments"
                        }
                    }
                ],
...
```

Пароли лучше положить в `.pgpass`, вот так: 
```
$ ls -la ~/.pgpass
-rw-------  1 prez  LD\Domain Users  478 15 окт 20:46 /Users/prez/.pgpass
$ cat ~/.pgpass
*:*:paymentsdb_prod:payments:XXXXXXXXXXXX
*:*:paymentsdb_test:payments:XXXXXXXXXXXX
```

Это позволит не указывать пароль ни при подключении к базе руками, ни при использовании почти любого ПО (в том числе, pgmigrate).
После этого проверить, что все успешно подключается, можно, например, через psql:

```
$ psql 'host=pgaas-test.mail.yandex.net port=12000 dbname=paymentsdb_test user=payments'
psql (10.2, server 10.5 (Ubuntu 10.5-1.pgdg14.04+1))
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES128-GCM-SHA256, bits: 128, compression: off)
Type "help" for help.

paymentsdb_test=>
```

С продакшн-базой сложнее, так как она находится за балансером `pgaas.mail.yandex.net`, в который дырок из офисной сети нет. Соответственно, нужно ходить, например, с разработческой виртуалки.

Применение миграций происходит при помощи [pgmigrate](https://github.com/yandex/pgmigrate) ( [руководство](https://github.com/yandex/pgmigrate/blob/master/doc/tutorial.md) по использованию ).
Например, вот так можно проверить, какие миграции на текущий момент применены к базе:
```
[~/XXX/postgre] $ pgmigrate -c 'host=pgaas-test.mail.yandex.net port=12000 dbname=paymentsdb_test user=payments' info
{
    ...
    "11": {
        "version": 11,
        "description": "Merchant alias",
        "type": "auto",
        "installed_by": "payments",
        "installed_on": "2018-10-15 12:32:48",
        "transactional": true
    },
    "12": {
        "version": 12,
        "type": "auto",
        "installed_by": null,
        "installed_on": null,
        "description": "Change log op types NONTRANSACTIONAL",
        "transactional": false
    }
}
```

Для локальной разработки для поднятия локальной базы paymentsdb используется docker-образ [minipgaas](https://github.yandex-team.ru/mdb/minipgaas). В docker-compose.yml сервис настроен так, что при старте накатывает миграции тем же pgmigrate. Соответственно, проще всего проверить написанную миграцию, перезапустив сервис `paymentsdb`. В случае, если в какой-то из миграций обнаружилась проблема, сервис упадет, а зависимость на его состояние healthy у сервиса `payments` не даст запуститься и ему.
