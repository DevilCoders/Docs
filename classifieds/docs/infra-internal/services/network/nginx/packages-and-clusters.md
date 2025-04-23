# Доставка конфигов Nginx на кластера lb

## Кластера lb

* `vertis_prod_lb`, `vertis_vtest_lb` - `внешние` балансеры, на которые попадает пользовательский трафик;
* `vertis_vprod_lb_int_nginx`, `vertis_vtest_lb_int_nginx` - `внутренние` балансеры для внутренних админок;
* `vertis_vtest_lb_ext` - балансеры для сервисов, которые в `тестинге` открыты `наружу`.

## Пакеты с конфигами Nginx

* [yandex-vertis-config-nginx-common](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-common)  - common include, например форматы логов. Живет на всех кластерах lb;
* [yandex-vertis-config-nginx-front](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front)  - конфиги auto.ru, rabota, banker. Живет на `vertis_prod/vtest_lb`;
* [yandex-vertis-config-nginx-front-external](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front-external)  - external сервисы, которые открыты в тестинге наружу (например, hub и chat-api). Живет на `vertis_vtest_lb_ext`;
* [yandex-vertis-config-nginx-front-internal](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front-internal)  - конфиги внутренних сервисов (например, uploader и octopus). Живет на `vertis_vprod/vtest_lb_int_nginx`;
* [yandex-vertis-config-nginx-front-realty](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front-realty)  - конфиги Яндекс.Недвижимости. Живет на `vertis_prod/vtest_lb`;
