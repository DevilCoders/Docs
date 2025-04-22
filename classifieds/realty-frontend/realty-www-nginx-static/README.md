# realty-www-nginx-static

Статика для lb-nginx (favicon, 500.html, 404.html, etc.)
Статика robots.txt находится в [админке](https://seo.vertis.yandex-team.ru/robots) [документация](https://wiki.yandex-team.ru/vertis-traffic-interfaces/realty-tasks/robots/)

Статика располагается согласно доменам.

Пакет собирается в [TeamCity](https://t.vertis.yandex-team.ru/buildConfiguration/vs_frontend_Applications_RealtyNew_NginxStaticReleaseArc).
Коммитить и собирать лучше прямо из мастера, ветки делать необязательно.

После сборки автоматически создается тикет в [кондуктор](https://c.yandex-team.ru/packages/yandex-vertis-realty-www-nginx-static) на выкладку в тестинг. После успешной выкладки в тестинг можно катить пакет в прод.
