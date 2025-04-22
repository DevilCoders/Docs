### Схема балансировки трафика для Веб-Карт

![balancing-scheme](./images/balancing-scheme.png)

**Yandex TLD** — секция управляется и обслуживается командой ["Единого домена"](https://abc.yandex-team.ru/services/appbalancer/). Чтобы внести изменения в эту секцию, нужно создать тикет в очереди [MINOTAUR](https://st.yandex-team.ru/MINOTAUR).

**Service Balancer** — [сервисный балансер](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-maps.slb.maps.yandex.net/show) (L7) развернутый в AWACS, управляется и обслуживается командой ["Инфраструктура фронтенда геосервисов"](https://abc.yandex-team.ru/services/maps-front-infra).

**maps-front-maps_production** — [приложение](https://deploy.yandex-team.ru/stage/maps-front-maps_production), развернутое в Yandex Deploy, управляется и обслуживается командой ["Веб-карты"](https://abc.yandex-team.ru/services/maps-front-maps).

Часть путей проксируется в Landing Page Constructor: [подробнее про это](./landings.md).
