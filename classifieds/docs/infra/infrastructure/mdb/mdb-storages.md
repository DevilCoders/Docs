{% note warning %}

**Disclaimer:** Данный документ представляет собой дизайдок, который сейчас в разработке. Обратную связь можно дать в [чатик](https://t.me/joinchat/AjIsiU18w7cXOX6Cmsjxwg) или в [задаче](https://st.yandex-team.ru/VERTISADMIN-27333)

{% endnote %}

# Описание

Ниже приведена концепция карты для внешних хранилищ данных, карта должна быть однообразна для всех типов: mysql, kafka, redis, mongo. Это накладывает некоторые органичения на формат.
Текущий вид карты обсуждался в [тикете](https://st.yandex-team.ru/VERTISADMIN-26596).

## Пример сервиса с зависимостью от нескольких поставщиков данных: kafka, MySQL, redis

### Структура

```txt
├── conf
│  └── application-foo
│     ├── prod.yml
│     └── test.yml
├── deploy
│  └── application-foo.yml
└── maps
   ├── application-foo.yml
   ├── kafka
   │  └── shared-01.yml
   ├── mysql
   │  └── application-foo-mysql.yml
   └── redis
      └── application-foo-redis.yml
```

{% cut "deploy/application-foo.yml" %}

```yaml
name: application-foo
image: application-foo-image
general:

common_params:
  HTTP_PORT: 80
  GENERAL_REDIS: ${application-foo-redis::application-foo-redis-db-01:conn_string}
  GENERAL_REDIS_PORT: ${application-foo-redis::application-foo-redis-db-01:port}

  APP_MYSQL_DB2_CONN: ${application-foo-mysql::application-foo-mysql-db-02:conn_string}
  APP_MYSQL_DB2_DBNAME: ${application-foo-mysql::application-foo-mysql-db-02:name}

  # -- эта секция генерируется автоматикой, это пример env доступных приложению внутри контейнера --
  KAFKA_HOSTS: "man-308u4mj3ge5gje3c.db.yandex.net:9091,man-74nse2v9tbcjgmdp.db.yandex.net:9091,..."
  KAFKA_USER: "application-foo"
  KAFKA_PASSWORD: "myPa$$word1"
  # -- эта секция генерируется автоматикой, это пример env доступных приложению внутри контейнера --

test:
  config:
    files:
      - application-foo/test.yml
    params:
      UPSTREAM_HOST: "up.test.vertis.yandex.net"
  resources:
    memory: 2048
  datacenters:
    vla:
      count: 1
    sas:
      count: 1

prod:
  config:
    files:
      - application-foo/prod.yml
    params:
      UPSTREAM_HOST: "up.prod.vertis.yandex.net"
  resources:
    memory: 4096
  datacenters:
    vla:
      count: 1
    sas:
      count: 1
```

{% endcut %}

{% cut "maps/application-foo.yml" %}

```yaml
name: application-foo
description: application-foo descr
type: service
owners:
  - https://staff.yandex-team.ru/departments/yandex_personal_vertserv_infra_mnt/
src: https://github.com/YandexClassifieds/nul

sox: false
provides:
  - name: http
    protocol: http
    port: 8080
    description: http api

depends_on:
  - service: kafka/shared-01
    interface_name: rent-diff-events
    kafka_producer: True

  - service: kafka/shared-01
    interface_name: glue
```

{% endcut %}

{% cut "maps/kafka/shared-01.yml" %}

```yaml
name: kafka-shared-01
description: kafka shared-01 cluster
owners:
  - https://staff.yandex-team.ru/departments/yandex_personal_vertserv_infra_mnt/

type: kafka
mdb_cluster:
  prod_id: mdb4u82hc7bsaq7cq1tc
  test_id: mdb9adu18n492urt7kuk

provides:
  - name: rent-diff-events
    description: rent-diff-events kafka topic
    options:
      partitions: 12 # int, default 12
      retention.ms: 30000 # int, default 0

  - name: glue
    description: glue kafka topic
    options:
      partitions: 8 # int, default 12
      retention.ms: 43200000 # int, default 0
```

{% endcut %}

{% cut "maps/mysql/application-foo-mysql.yml" %}

```yaml
name: application-foo-mysql
description: application-foo databases
owners:
  - https://staff.yandex-team.ru/departments/yandex_personal_vertserv_infra_mnt/

type: mdb_mysql
mdb_mysql:
  prod_id: xxxxxxxxxxxxxxxxxxxx
  test_id: yyyyyyyyyyyyyyyyyyyy

provides:
  - name: application-foo-mysql-db-01
    protocol: tcp
    port: 3306
    description: application-foo-mysql-db-01 database

  - name: application-foo-mysql-db-02
    protocol: tcp
    port: 3306
    description: application-foo-mysql-db-02 database
```

{% endcut %}

{% cut "maps/redis/application-foo-redis.yml" %}

```yaml
name: application-foo-redis
description: application-foo redis cache
owners:
  - https://staff.yandex-team.ru/departments/yandex_personal_vertserv_infra_mnt/

type: mdb_redis
mdb_redis:
  prod_id: xxxxxxxxxxxxxxxxxxxx
  test_id: yyyyyyyyyyyyyyyyyyyy

provides:
  - name: application-foo-redis-db-01
    protocol: redis
    port: 26379
    description: application-foo-redis-db-01 database
    options:
      type: replica # [replica|sharding]
      hosts_count: 3
```

{% endcut %}

Пояснение:

- Cервис `application-foo` запрашивает доступ к топикам `rent-diff-events` и `glue`;
- Автоматика создает пользователя `application-foo` (по имени сервиса) в кластере kafka;
- Данному пользователю будут выданы права **producer** + **consumer** на топик `rent-diff-events`;
- Данному пользователю будут выданы права **consumer** на топик `glue`;
- Если 2(и более) разных сервиса захотят произвести запись в один топик сработает "защита". Подтверждение на вылив такого сервиса нужно будет получить у **ВСЕХ** ответственных за сервисы в которых уже есть право на запись. (Сервис В хочет писать в топик А, в который уже пишет сервис А - потребуется ОК ответственного за А. Сервис С хочет писать в топик А - нужен ОК от сервисов А и В. И тд);
- Переменные окружения `KAFKA_HOSTS`, `KAFKA_USER`, `KAFKA_PASSWORD` - генерируются автоматикой, их не нужно прописывать вручную;
