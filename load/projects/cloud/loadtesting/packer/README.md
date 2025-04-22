# Ручная сборка при помощи packer
## Установка
Установить можно с официального сайта https://learn.hashicorp.com/tutorials/packer/get-started-install-cli?in=packer/docker-get-started
Важно настроит Yubikey https://wiki.yandex-team.ru/cloud/yubikey/ и добиться доступа по ssh (не pssh)
Нужен настроенный CLI (yc)
Для работы нужен токен iam в переменной YC_TOKEN. Получить можно:
    `yc iam create-token`

## Работа
Если всё настроено то можно запустить через:
    `source build-with-packer.sh`
скрипт соберёт server, и создаст образ на препроде.
## Ручная сборка
Можно собрать руками, надо сделать:
     `packer build -var-file=variables-{ENV}.json build-manual.json`
Для авторизации в образе будет использован текущий пользователь.
Базовый образ собирается только в СЦ https://teamcity.aw.cloud.yandex.net/project.html?projectId=YcLoadTesting
## Как использовать образ
Виртуалку из последней версии образа можно создать командой:
    `yc compute instance create --zone ru-central1-b --network-interface subnet-id=blt85l2qkvj26uipt86u,ipv6-address=auto,ipv4-address=auto --create-boot-disk size=15,image-family=lt-server` --metadata enable-oslogin=true
В образе для доступа используется oslogin, он берёт ключи пользователя со стафа и кладёт в метадату
Дальше можно ходить через бастион собой
Через несколько секунд, появится доступ в виртуалку по pssh:
    `pssh --bastion-host lb.bastion.cloud.yandex.net IPV6_ADDRESS`
