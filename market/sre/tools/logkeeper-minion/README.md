# Logkeeper-minion

[Документация](https://wiki.yandex-team.ru/market/sre/logkeeper-minion/)

## Nanny
```shell script
# Запуск
./bin/logkeeper-minion.sh
```
* Миньон представляется координатору как `${NANNY_SERVICE_ID}`.
* В сервисе логи ищутся в каталоге `/var/logs/yandex/`.
* Логи после отправки будут доступны в папке с именем `${BSCONFIG_IPORT}@${NODE_NAME}`.

## Y.Deploy
```shell script
# Запуск
/usr/local/bin/logkeeper-minion.sh
```
* Миньон представляется координатору как `${DEPLOY_STAGE_ID}.${DEPLOY_UNIT_ID}`.
* В сервисе логи ищутся в каталоге `/var/log/yandex/`.
* Логи после отправки будут доступны в папке с именем `${DEPLOY_POD_PERSISTENT_FQDN}`.
