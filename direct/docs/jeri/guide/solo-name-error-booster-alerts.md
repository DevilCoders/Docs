# Именованные проверки в error booster 

[Алерты в error booster](https://error.yandex-team.ru/projects/direct/settings/alerts) создаются с названием вида `alert-531`.

Чтобы получить проверку с более понятным хостом и сервисом можно использовать solo.

Достаточно добавить проверку в [скрипт](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/errorbooster/__init__.py#L7) и попросить кого-нибудь с правами на namespace `direct.prod` в juggler применить изменения.

В juggler будет создана проверка с нужным хостом и сервисом, агрегирующая соотвествующую проверку из error booster.
