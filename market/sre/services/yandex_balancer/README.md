Yandex Balancer
===============

Данный пакет – лишь DEB-обертка для Балансера.


# Как собирать #

1. Поправить здесь ID ресурса (если обновляем версию yandex-balancer): https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/services/yandex_balancer/pkg.json?rev=r8257761#L104
2. Поправить версию собираемого пакета: https://a.yandex-team.ru/arc_vcs/market/sre/services/yandex_balancer/pkg.json?rev=r8467737#L6
3. Прокатить пайплайн вот здесь (автосборка, запускается сама): <http://tsum.yandex-team.ru/pipe/projects/sre/release/new/yandex-balancer-deploy>

Соблюдайте осторожность и осмотрительность при выкладке пакета.


# Полезные ссылки #

Таски со свежими релизами бинарника yandex-balancer можно увидеть тут: https://sandbox.yandex-team.ru/resources/?type=BALANCER_EXECUTABLE&limit=20&attrs=%7B"released"%3A"stable"%7D

Документация здесь: <https://beta.wiki.yandex-team.ru/JandeksPoisk/Sepe/balancer/Cookbook/>

Документация о yandex-balancer в Маркете доступна здесь: <https://wiki.yandex-team.ru/market/administration/fslb/>

Релизы yandex-balancer: <https://st.yandex-team.ru/BALANCERREL/order:updated:false>
