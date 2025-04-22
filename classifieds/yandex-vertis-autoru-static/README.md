# yandex-vertis-autoru-static

Статика для lb-nginx (favicon, robots.txt, 500.html, 404.html, etc.)

Статика располагается согласно доменам. 

Пакет собирается в [TeamCity](https://t.vertis.yandex-team.ru/buildConfiguration/vs_frontend_Applications_AuroRuFrontendRepo_ArcReleaseYandexVertisAutoruStatic).
Заливать изменения нужно через PR, а собирать прямо из мастера.

После сборки автоматически создается тикет в [кондуктор](https://c.yandex-team.ru/packages/yandex-vertis-autoru-static) на выкладку в тестинг.

После успешной выкладки в тестинг можно катить пакет в прод.

Для этого:
- идем в кондуктор
- клаццаем пакеты
- ищем свой пакет 
- клаццаем тикеты (сверху)

либо идем по короткой [ссылке](https://c.yandex-team.ru/packages/yandex-vertis-autoru-static/tickets) для этой репы

Далее ищем свой тикет и клаццаем "в стэйбл"




