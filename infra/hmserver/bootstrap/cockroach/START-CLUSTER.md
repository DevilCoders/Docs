# Запуск Cockroach кластера

## Полуавтоматический запуск
Скрипт запуска кластера `a.yandex.team.ru/infra/hmserver/bootstrap/cockroach/cmd/cockroach-bootstrap`

Переходим к шагу 5

## Ручной запуск
### [Инструкция с сайта Cockroach](https://www.cockroachlabs.com/docs/v19.2/deploy-cockroachdb-on-premises.html)
### 1. Сгенерировать сертификаты (CA, node, client)
Скрипты генерации `a.yandex.team.ru/junk/vaspahomov/cockroach/scripts`

```shell script
# Создаем CA и node cert
./create-cluster-certs.sh <node1> <node2> <node3>

# Создаем client сертификат для root
./create-client-certs.sh root
```

### 2. Написать systemd unit файл
Шаблон `a.yandex.team.ru/junk/vaspahomov/cockroach/cockroachdb.service`
#### Настроки
* `--store=<store>` The file path to a storage device.
* `--http-addr :8888` The hostname or IP address to bind to for HTTP requests.
* `--cache=50GB` Total size in bytes for caches, shared evenly if there are multiple storage devices.
* `--max-sql-memory=50GB` Maximum memory capacity available to store temporary data for SQL clients,
including prepared queries and intermediate data rows during query execution.

### 3. Запуск нод cockroach

На каждой ноде выполняем эти команды

1. Переносим сертификаты и systemd unit файл на ноду
    ```shell script
    scp -r kek1-1111.search.yandex.net kek1-1111.search.yandex.net:~/certs
    scp cockroachdb.service kek1-1111.search.yandex.net:~/
    ```
2. Загружаем бинарник cockroach
    ```shell script
    wget -qO- https://binaries.cockroachdb.com/cockroach-v20.1.0.linux-amd64.tgz | tar  xvz
    mv cockroach-v20.1.0.linux-amd64/cockroach /usr/local/bin/
    ```
3. Подготовка окружения
    ```shell script
    mkdir /var/lib/cockroach
    # cockroach store
    mkdir /place/cockroach_data
    mv certs /var/lib/cockroach/
    mv cockroachdb.service /etc/systemd/system/
    useradd cockroach
    chown -R cockroach.cockroach /var/lib/cockroach
    chown -R cockroach.cockroach /place/cockroach_data
    ```
4. Запускаем ноду
    ```shell script
    systemctl start cockroachdb
    ```

### 4. Инициализируем кластер (с локальной машины)
```shell script
cockroach init --certs-dir=kek1-1111.search.yandex.net --host=kek1-1111.search.yandex.net
```

### 5. Создаем пользователя
```shell script
cockroach sql --certs-dir=cluster/myt1-0074.search.yandex.net/certs --host=myt1-0074.search.yandex.net
```
```sql
CREATE USER vaspahomov WITH PASSWORD 'wow-this-is-my-password';
-- если надо, даем пользователю права админа
GRANT admin TO vaspahomov;
```
### 6. Меняем дефолтные настройки
```sql
ALTER RANGE default CONFIGURE ZONE USING gc.ttlseconds = 600;
SET CLUSTER SETTING kv.snapshot_recovery.max_rate = '24mb';
```
### 7. Смотрим в ui
https://kek1-1111.search.yandex.net:8888/
