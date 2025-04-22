# YANDEX-HM-COCKROACH deb

### Внутри пакета приносится
* бинарь cockroach из opt/cockroach/cockroach

    При желании версию бинаря можно обновить скриптом `download-cockroach.sh`.
    Скрипт скачивает версию cockroach указаную в скрипте и загружает в sandbox.
    В пакетах бинарь берется из sandbox ресурса
* Юнит файл cockroachdb.service
* cockroachdb.conf уникальный для каждой локации (отличаются адреса нод кластеров и data-dir)

### После установки
* Необходимо нагенерить серты на каждой ноде
```
mkdir my-safe-directory
mkdir certs
# write one of ca.key
# from https://yav.yandex-team.ru/secret/sec-01efy99nzq5n09n2bnq0pb599t
# to "my-safe-directory/ca.key"
```
```
cockroach cert create-node $HOSTNAME --certs-dir="certs" --ca-key="my-safe-directory/ca.key"
cockroach cert create-client root --certs-dir="certs" --ca-key="my-safe-directory/ca.key"
mv "certs/node.key" "/var/lib/cockroach/"
mv "certs/node.crt" "/var/lib/cockroach/"
mv "certs/client.root.key" "/var/lib/cockroach/"
mv "certs/client.root.crt" "/var/lib/cockroach/"
mv "certs/ca.crt" "/var/lib/cockroach/"
```
* Инициализировать кластер cockroach
```
cockroach init --certs-dir=/var/lib/cockroach/certs --host=$HOSTNAME
```
