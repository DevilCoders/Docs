# Настройка доступов

## Настройте доступ к репозиторию

CLI взаимодействует с git-репозиторием с помощью [SSH].

Для создания релизных веток необходимо, чтобы у пользователя был доступ на `push` в репозиторий.

Для публикации релизных коммитов в основную ветвь репозитория необходимо, чтобы у пользователя был доступ на `push` в репозиторий. Если в основной ветви репозитория настроен режим `protected brunch` нужны права с ролью `admin`.

## Настройте доступ к Трекеру

### Настройте доступ к API Трекера

Для работы CLI нужен [доступ][tracker_api_access] к `st-api.yandex-team.ru:443`.

### Настройте доступ к очереди Трекера

Для работы CLI нужен доступ в вашу очередь в Трекере с правами на чтение и создание задач.

> О том как настроить доступы читайте в [Руководстве пользователя Трекера][tracker_guide].

## Настройте доступ к API ABC

Для работы CLI нужен [доступ][abc_api_access] к `abc-back.yandex-team.ru:443`.

[SSH]: https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols#_the_ssh_protocol
[tracker_guide]: https://doc.yandex-team.ru/tracker/external/manager/queue-access.html#queue-access
[tracker_api_access]: https://puncher.yandex-team.ru?create_destinations=st-api.yandex-team.ru&create_protocol=tcp&create_locations=office&create_locations=vpn&create_ports=443
[abc_api_access]: https://puncher.yandex-team.ru?create_destinations=abc-back.yandex-team.ru&create_protocol=tcp&create_locations=office&create_locations=vpn&create_ports=443
