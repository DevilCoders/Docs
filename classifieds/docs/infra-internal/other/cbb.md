# Блокировка по IP через CBB
[Единая База Блокировок](https://wiki.yandex-team.ru/cbb/) (CBB) позволяет блокировать по IP внешние сервисы.
Мы используем [группу 189](https://cbb.yandex-team.ru/groups/189/add_range) в cbb.

Бан происходит на внешних lb раз в 5 минут по крону через конфиг nginx. Конфиги и cron приезжают из пакета `yandex-vertis-config-nginx-cbb`.
**Важно:** По умолчанию баны ставятся на 1 день.

Про доступы и права в CBB можно почитать [тут](https://wiki.yandex-team.ru/cbb/auth/).
