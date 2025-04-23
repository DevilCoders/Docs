# Доступы

Доступ до Tunneler сейчас регулируется исключительно правилами [файрвола](https://wiki.yandex-team.ru/noc/product/Firewall/). Любой пользователь со Стаффа может авторизоваться в Tunneler по своему [ssh-ключу](https://wiki.yandex-team.ru/security/ssh/), если есть сетевые доступы.

Для корректной работы необходимы следующие дырки:

- от стороны, которая поднимает туннель:

  - [до балансера](https://puncher.yandex-team.ru/?destination=tun-balancer.si.yandex-team.ru&ports=443&rules=exclude_rejected&values=all&sort=destination).
  - [до машин Tunneler](https://puncher.yandex-team.ru/?destination=_FEI_TUNNELER_WS_NETS_&ports=2022&rules=exclude_rejected&values=all&sort=destination).

- от стороны, которая делает запросы:

  - [до балансера](https://puncher.yandex-team.ru/?destination=tun-balancer.si.yandex-team.ru&ports=443&rules=exclude_rejected&values=all&sort=destination).

Перед тем, как заказывать дырки, поищите существующие по ссылкам выше. Для более точной фильтрации в поле «Источник» укажите:

- ваш логин, если проверяете доступ с вашего ноутбука;
- ip-адрес машины, если проверяете доступ с виртуалки в QYP или другом облаке.

Проверить фактическое наличие дырки с ноутбука или машины в QYP можно с помощью netcat:

```bash
nc -vz tun-balancer.si.yandex-team.ru 443

# Если дырка есть, вывод команды будет содержать строку
# Connection to tun-balancer.si.yandex-team.ru port 443 [tcp/https] succeeded!
```

или telnet:

```bash
telnet tun-balancer.si.yandex-team.ru 443

# Если дырка есть, вывод команды будет содержать строку
# Connected to tun-balancer.si.yandex-team.ru.
```

Чтобы заказать дырки, в поле «Источник» укажите:

- роль «Разработка» (или «Тестирование», или кому вы выдаёте доступ) вашего ABC-сервиса, если доступа нет с вашего ноутбука. Увидеть список ваших ABC-сервисов можно у вас на Стаффе;
- сетевой макрос машины, если доступа нет с виртуалки в QYP или другом облаке. Чтобы узнать сетевой макрос машины, вбейте домен машины в поле поиска в [Racktables](https://racktables.yandex-team.ru/).

Больше информации о том, как заказывать доступы в Puncher, можно почитать [в его документации](https://wiki.yandex-team.ru/noc/nocdev/puncher/spravka/).

## Доступы для CI

Для корректной работы tunneler+hermione в CI необходимы следующие дырки:

- от браузеров [до балансера](https://puncher.yandex-team.ru/?destination=tun-balancer.si.yandex-team.ru&ports=443&rules=exclude_rejected&values=all&sort=destination). Доступы из [общего Selenium-грида](https://docs.yandex-team.ru/devtools/test/selenium) уже есть.
- от хостов, на которых поднимается приложение, [до машин Tunneler](https://puncher.yandex-team.ru/?destination=_FEI_TUN_NETS_&ports=2022&rules=exclude_rejected&values=all&sort=destination). Доступы из сети [Sandbox-агентов](https://docs.yandex-team.ru/sandbox/agents) уже есть.
