# Запуск hm-reporter сервера

## Полуавтоматический запуск
Перед запуском скрипта запустить cockroach кластер (шаг 1), подготовить cockroach (5 шаг)

Скрипт запуска hm-reporter кластера `a.yandex.team.ru/infra/hmserver/bootstrap/hm-reporter/cmd/hm-reporter-server-bootstrap`

## Ручной запуск
### 1. Запустить cockroach db кластер ([Как это сделать](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hmserver/pkg/reporter/cockroach/START_CLUSTER.md))
### 2. Принести на машину hm-reporter-server.service
```shell script
scp hm-reporter-server.service /etc/systemd/system/hm-reporter-server.service
```
### 3. Принести на машину бинарник hm-reporter-server
```shell script
scp hm-reporter-server /opt/hm-reporter-server/hm-reporter-server
```
### 4. Принести env
```shell script
scp hm-reporter-server.conf /etc/hm-reporter-server.conf
```
### 5. Завести юзера в cockroach, раздать ему права, и создать базку reports
```sql
CREATE database reports;
CREATE USER hm_reporter_server WITH PASSWORD 'wow-this-is-my-password';
GRANT ALL ON DATABASE reports TO hm_reporter_server;
```
### 6. Запустить hm-reporter-server
```shell script
systemctl start hm-reporter-server
```
