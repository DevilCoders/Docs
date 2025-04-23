
## Мониторинги (Juggler):
[Введение в Juggler](https://wiki.yandex-team.ru/sm/juggler/introduction/)
- [Проверки maya (public)](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaya)
- [Проверки maya (corp)](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaya-corp)
- [Неймспейс mail.maya](https://juggler.yandex-team.ru/namespaces/?query=namespace=mail.maya)
- [Дашборд mail.maya](https://juggler.yandex-team.ru/project/mail.maya/dashboard?project=mail.maya)
- [Правила нотификации для неймспейса mail.maya](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5e34473166a34600768dfe02)

Ansible-конфиги для настройки Juggler ([как готовить](https://wiki.yandex-team.ru/sm/juggler/ansible/)):
- [Ansyble maya](https://github.yandex-team.ru/mail-admin/ansible-juggler-configs/blob/master/maya.yml)
- [Ansyble maya-corp](https://github.yandex-team.ru/mail-admin/ansible-juggler-configs/blob/master/maya-corp.yml)
  
Активные мониторинги:
- [скрипты monrun в контейнере](https://github.yandex-team.ru/personal-services/frontend/tree/dev/services/maya/docker/fs/usr/lib/juggler/maya)
- [конфиги monrun в контейнере](https://github.yandex-team.ru/personal-services/frontend/tree/dev/services/maya/docker/fs/etc/monrun/)

[CDN Static](https://cdn-static.yandex-team.ru/projects/s3_mail/projectDashboard?componentSettings=%7B%22row_1_col_0_con_0_charts%22%3A%7B%22scale%22%3A%22month%22%7D%7D&filter=uri%20startsWith%20%2Fs3%2Fmail%2Fmaya&period=2hour)

## Логи
[Подробно тут](./logs/README.md)

### Краткая сводная таблица
| Тип лога              | Местонахождение на файловой системе    | Путь к логу в YT Hahn                                      |
| --------------------- |:--------------------------------------:| ----------------------------------------------------------:|
| nginx access          | `/var/log/nginx/access_log.tskv`       | `logs/calendar-(yt_или_public)-maya-nginx-access-log`      |
| duffman access        | `/var/log/duffman/duffman-access.tskv` | `logs/calendar-(yt_или_public)-maya-duffman-access-log`    |
| duffman http          | `/var/log/duffman/duffman-http.tskv`   | `logs/calendar-(yt_или_public)-maya-duffman-http-log`      |
| duffman master        | `/var/log/duffman/duffman-master.tskv` | —                                                          |
| duffman client        | `/var/log/duffman/duffman-client.tskv` | `logs/calendar-(yt_или_public)-maya-duffman-client-log`    |
