# abyssync

Инструмент для закрытия приложения по командам из ZK

https://st.yandex-team.ru/CHEMODAN-67557
https://st.yandex-team.ru/CHEMODAN-75204

## Деплой

Установка производится пакетом:
* Conductor: https://c.yandex-team.ru/packages/abyssync
* Облака: https://a.yandex-team.ru/search?search=abyssync%3D,%5Edisk%2Fadmin%2Fdocker.*,,arcadia,,5000

Настройки запуска едут с пакетом из папки `conf`.
Сейчас `supervisor.conf` написан для Qloud, поэтому в докер-образах есть оверрайды для деплоя: https://a.yandex-team.ru/search?search=command%3D%2Fusr%2Fbin%2Fabyssync,%5Edisk%2Fadmin%2Fdocker.*,,arcadia,,5000

### Настройки

- На железе конфиг варится солтом с добавлением секрета zookeeper:creds: https://a.yandex-team.ru/arc/trunk/arcadia/disk/admin/salt/disk/roots/units/abyssync/files/etc/yandex/abyssync.yaml
- На базах своим солтом: https://a.yandex-team.ru/arc/trunk/arcadia/disk/admin/salt/pg/salt/components/abyssync/conf/abyssync.yaml
- В облаках конфиг общий: https://a.yandex-team.ru/arc/trunk/arcadia/disk/admin/docker/disk/common/common-settings/etc/yandex/abyssync.yaml а пароли берутся из jaas файла, либо из переменной окружения ZOOKEEPER_CREDS

## Сборка

Автоматическая по коммиту в Аркадию: https://beta-testenv.yandex-team.ru/project/disk-admin-packages/job/BUILD_DISK_ABYSSYNC/history

## Разработка

Весь код лежит в `lib`, собирается через `ya make`.
Для локальной работы можно положить `config.yaml` вида:
```yaml
---
logging:
  level: 10
  filename: abyssync.log
sleep: 1
appname: test_app
dc: man
env: testing
isdbpresent: False
zookeeper:
  hosts:
    - zk1e.dst.yandex.net:2181
  jaas: ~/arcadia/disk/support/common/src/main/java/ru/yandex/chemodan/global/jaas-testing.conf
commands:
  open: echo Open
  close: echo Close
```
и запускать abyssync: `./abyssync config.yaml`
