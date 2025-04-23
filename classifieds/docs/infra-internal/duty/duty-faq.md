# FAQ для дежурного
На этой странице собраны типовые задачи дежурного и ссылки на документацию по их выполнению.

## Проблемы в датацентре и учения

[Проведение учений и закрытие ДЦ в случае проблем](drills.md)

### Работа с Nginx
[Внесение изменения в конфигурацию Nginx](https://docs.yandex-team.ru/classifieds-ops-internal/services/network/nginx/update-config)

### Zookeeper
[Создание znode в zookeeper](https://wiki.yandex-team.ru/vertis-admin/Zookeeper/create-root-node/)
[Переливка данных из старого кластера в новый](https://wiki.yandex-team.ru/vertis-admin/Zookeeper/migrate-from-legacy/)

### Базы данных
[Переливки баз данных](https://wiki.yandex-team.ru/vertis-admin/storage/Perelivka-v-YT/)

### Kafka
Топики в железной Kafka мы заводим только при наличии веской причины и невозможности заехать в Kafka MDB.
[Заведение топиков и пользователей в Kafka MDB](../services/storages/kafka/mdb.md)
[Заведение топиков в железной Kafka](../services/storages/kafka/legacy.md)

## CME

[Настройка проксирования для сервисов CME в сервисы Вертикалей](../cme/cme-proxy-add-cluster.md)
[Действия после увольнения сотрудника](https://wiki.yandex-team.ru/vertis-admin/infra.cm.expert/users/uvolnenie)

### Выдача доступов для сотрудников CME
* [Создание нового пользователя в LDAP](https://wiki.yandex-team.ru/vertis-admin/infra.cm.expert/servisy/ldap/dobavitpolzovatelja)
* [VPN-доступ](https://wiki.yandex-team.ru/vertis-admin/infra.cm.expert/servisy/openvpn/#predostavitpolzovateljudostupkvpn)
* [Приглашение в Mattermost](https://wiki.yandex-team.ru/vertis-admin/infra.cm.expert/servisy/mattermost/priglasitpolzovatelja)
* [Приглашение в PowerBI](https://wiki.yandex-team.ru/vertis-admin/infra.cm.expert/servisy/powerbi/priglasitpolzovatelja)
* [Беспарольный sudo на хосты](https://wiki.yandex-team.ru/vertis-admin/infra.cm.expert/users/sudo)
* [Выдаем доступы к базам данных](https://wiki.yandex-team.ru/vertis-admin/infra.cm.expert/servisy/postgresql/predostavleniedostupasotrudnikam)

## Other

[Операции с dev-виртуалками разработчиков](../iaas/dev-vm.md)
[Работа с тикетами от VertisAptly](../iaas/aptly.md#tiket-ot-vertisaptly)
[Закоп сервиса в Кондукторе](../other/conductor.md)
[Блокировка по IP](../other/cbb.md)

С остальными вопросами можно прийти к ответственным админам, указанным в [зонах ответственности](../areas-of-responsibility.md).
