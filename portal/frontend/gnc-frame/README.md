# Глобальный Центр Уведомлений: Фрейм

[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/services/gnc-frame&vcs=arc)](https://oko.yandex-team.ru/arc/frontend/services/gnc-frame)

Сервис формирует html-страницу с уведомлениями от сервисов Яндекса.
https://yandex.ru/gnc/frame
https://gnc.yandex-team.ru/frame

Графы:

[`gnc-frame_init` общий хелпер][graph_gnc-frame_init],
### для внешнего интернета
- [`gnc-frame`][graph_gnc-frame],
- [`gnc-frame_sub` внутренний граф][graph_gnc_sub],
- [`gnc-frame_upper` внешний граф][graph_gnc_upper],

### для интранета
- [`gnc-intranet-frame` для интранета][graph_gnc-intranet-frame]


[Бэкенды][backends] (для смены окружения cgi-параметр `env` со значениями: `test`, `priemka`)

Сетапы:
[`gnc_environment` для установки окружения][setup_gnc_environment],
[`gnc_notifications_pre` для формирования запроса в бэкенд][setup_gnc_notifications_pre]

Сервисные балансеры:
- [Внешний](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/gnc.yandex.ru/show/)
- [Внутренний](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/gnc.yandex-team.ru/show/)

Upstream в hamster:
[`gnc-frame` для внешнего интернета][upstream-hamster_gnc-frame],
[`gnc-intranet-frame` для интранета][upstream-hamster_gnc-intranet-frame]

Графики:
* [внешнего балансера](https://yasm.yandex-team.ru/template/panel/balancer-with-upstreams/prj=gnc.yandex.ru;upstreams=gnc-frame/)
* [внутреннего балансера](https://yasm.yandex-team.ru/template/panel/balancer-with-upstreams/prj=gnc.yandex-team.ru;upstreams=gnc-intranet-frame,static/)
* [ошибок][chart_error]
* [скорости][chart_rum]
* [графа `gnc-frame`][chart_gnc-frame]
* [графа `gnc-frame_upper`][chart_gnc-frame_upper]
* [графа `gnc-frame_sub`][chart_gnc-frame_sub]
* [графа `gnc-intranet-frame`][chart_gnc-intranet-frame]

[graph_gnc-frame_init]: https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/SHARED/gnc-frame_init.json
[graph_gnc-frame]: https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/SHARED/gnc-frame.json
[graph_gnc_sub]: https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/SHARED/gnc-frame_sub.json
[graph_gnc_upper]: https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/SHARED/gnc-frame_upper.json
[graph_gnc-intranet-frame]: https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/SHARED/gnc-intranet-frame.json

[backends]: https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/backends/GNC

[setup_gnc_environment]: https://a.yandex-team.ru/arc/trunk/arcadia/web/src_setup/lib/setup/gnc_environment
[setup_gnc_notifications_pre]: https://a.yandex-team.ru/arc/trunk/arcadia/web/src_setup/lib/setup/gnc_notifications_pre

[upstream-hamster_gnc-frame]: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/hamster.yandex.ru/upstreams/list/upstream_gnc-frame/show/
[upstream-hamster_gnc-intranet-frame]: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/hamster.yandex.ru/upstreams/list/upstream_gnc-intranet-frame/show/

[chart_error]: https://error.yandex-team.ru/projects/gnc-frame/projectDashboard
[chart_rum]: https://rum.yandex-team.ru/projects/gnc-frame/projectDashboard
[chart_gnc-frame]: https://yasm.yandex-team.ru/menu/apphost/SHARED/gnc-frame/
[chart_gnc-frame_sub]: https://yasm.yandex-team.ru/menu/apphost/SHARED/gnc-frame_sub/
[chart_gnc-intranet-frame]: https://yasm.yandex-team.ru/menu/apphost/SHARED/gnc-intranet-frame/
