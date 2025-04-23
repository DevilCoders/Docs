### Туннель до КредитЕвропаБанка
#### Что это
Кластер машинок для создания защищенного канала с КредитЕвропаБанком

#### Зачем это
Еще один партнёр auto.ru (сервис shark). Тикет: https://st.yandex-team.ru/VERTISADMIN-27560

#### Где это
Развернуты в ЯОблаке, в каталогах с dualstack сетями.
Кластер машинок в тестинге: [%vertis_vtest_crediteuropebank_proxy](https://c.yandex-team.ru/groups/vertis_vtest_crediteuropebank_proxy)
Кластер машинок в проде: [%vertis_vprod_crediteuropebank_proxy](https://c.yandex-team.ru/groups/vertis_vprod_crediteuropebank_proxy)

#### Как это
Машинки создаются терраформом.
Модули тестинга: [ссылка](https://bb.yandex-team.ru/projects/YANDEX-CLASSIFIEDS/repos/terraform/browse/compute/vertis_vtest_crediteuropebank_proxy).
Модули прода: [ссылка](https://bb.yandex-team.ru/projects/YANDEX-CLASSIFIEDS/repos/terraform/browse/compute/vertis_vprod_crediteuropebank_proxy).

Для конфигурирования используются одноименные кластерные плейбуки из ``vertis-ansible``, с двумя основными ролями:
1. Роль [ipsec](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/ipsec).
Устанавливает IPsec соединение с банком.
2. Роль [envoy](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/envoy-new).
Проксирует запросы по безопасному соединению в банк.
Над envoy подняты NOC SLB.
Тестинг: ``http://crediteuropebank-proxy-test-int.noc-slb.vertis.yandex.net:8080``
Прод: ``http://crediteuropebank-proxy-prod-int.noc-slb.vertis.yandex.net:8080``

#### Про графики
Дашборд с метриками IPSec: [ссылка](https://grafana.vertis.yandex-team.ru/d/Zo5fa6y7k/ipsec?orgId=1).
Дашбор с метриками Envoy: [ссылка](https://grafana.vertis.yandex-team.ru/d/000000610/envoy?orgId=1)
