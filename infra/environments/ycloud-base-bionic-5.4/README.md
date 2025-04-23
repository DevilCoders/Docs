# Базовый образ для сервисов Яндекса, использующих Yandex.Cloud Compute

## Цель

Образ содержит нужные механизмы и контроли безопасности, которые позволяют хостить сервисы Яндекса в Яндекс.Облаке безопасно.

__Неполный список того, что внутри:__

- правильный конфиг sshd (IPv6-only с доступом из Яндексовых сетей, аутентификация только по ключам, отправка логов в SOC)
- яндексовые ntp и dns серверы
- osquery
- различные яндексовые пакетики (%%yandex-internal-root-ca%%, %%yandex-ca-certs%%, ...)
- синхронизация ssh-ключей и разрешений sudo для пользователей (через oslogin и сервис метаданных)
- проверка консистентности настроек (goss-checks)

## Коротко про образ

Ubuntu Bionic (18.04) с поисковым ядром 5.4.*. 

## Как использовать образ?

### Prerequisites

**__Подробнее про общие требования к сервисам, живущим в Яндекс.Облаке, можно почитать [здесь](https://wiki.yandex-team.ru/security/policies/yandex-cloud-rules/).__**

1. Облако, привязанное к федерации YandexTeam и к вашему abc-сервису
2. Beta-доступ к функциональности oslogin, а также флаг `enable_oslogin_update: True` в настройках [iam](https://bb.yandex-team.ru/projects/CLOUD/repos/iam-sync-configs/browse/prod.yaml)
3. IPv6-макрос, дочерний к `_CLOUD_YANDEX_CLIENTS_`, смапленный в виртуальную сеть вашего облака
4. Роль `compute.images.user` в каталоге yandex-images (`b1gv004ochjnp8ddk1ea`) (как - обсуждается в CLOUD-65804)

Создание инстанса Compute в IPv6-сети из веб-интерфейса пока не поддерживается, поэтому его можно создать, например, с помощью yc cli:

```bash
yc compute instance create --name <vm-name> --zone <zone> \
--network-interface subnet-id=<subnet-with-ipv6>,ipv4-address=auto,ipv6-address=auto \
--create-boot-disk image-folder-id=b1gv004ochjnp8ddk1ea,image-family=yandex-golden-image,size=4GB,type=network-hdd \
--cores 2 --core-fraction 100 --memory 2G \
--folder-id <your_folder> --cloud-id <your_cloud> 
```

## Поддержка

TBD

#### Про сборку, особенности использования и ограничения образа - можно почитать на [вики-странице](https://wiki.yandex-team.ru/security/policies/yandex-cloud-rules/golden-image/).

