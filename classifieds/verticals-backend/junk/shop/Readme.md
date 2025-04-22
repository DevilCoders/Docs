# Shop - сервис управления доп услугами Я.Вертикалей

[Design Doc](docs/design.md)

## Запуск тестов

`bazel test //billing/shop/...:all`

Про запуск конкретного теста см. в [readme](/README.md#как-запустить-именно-свой-тест).

## Релизы

Описание релизного процесса написано [здесь](/docs/how-to/deploy.md).

## SOX

За базу ydb отвечают админы, т.к. база под SOX. Следовательно, при проблемах с ресурсами базы нужно писать админам.
Но вообще, они [замониторили](https://st.yandex-team.ru/VERTISADMIN-26487) ресурсы, так что скорее всего, отреагируют раньше нас.

Доступа в базу у нас нет, можно заказать через тикет админам в очередь VASUP.

## Api

[TeamCity](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_AutoRuExp_shop_api_release?mode=builds)

`Метрики: `
[gRpc Server](https://grafana.vertis.yandex-team.ru/d/grpc/grpc-server?orgId=1&refresh=30s&var-datasource=Prometheus&var-job=shop-api&var-dc=All&var-service=billing.shop.GoodsService&var-method=All&var-window=2m) \ 
[http Server](https://grafana.vertis.yandex-team.ru/d/http-server/http-server?orgId=1&refresh=30s&var-datasource=Prometheus&var-job=shop-api&var-dc=All&var-name=All&var-window=2m) \ 
[http Client](https://grafana.vertis.yandex-team.ru/d/http-client/http-client?orgId=1&refresh=30s&var-datasource=Prometheus&var-job=shop-api&var-dc=All&var-service=trust&var-name=All&var-window=2m) \ 
[System](https://grafana.vertis.yandex-team.ru/d/system-info/system-info?orgId=1&refresh=30s&var-datasource=Prometheus&var-job=shop-api&var-dc=All&var-window=2m&var-gc=All&var-instance=All)

`gRPC схемы для работы с` 
[активными услугами](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/billing/shop/goods_service.proto),
[продуктами](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/billing/shop/product_service.proto) и
[покупками](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/billing/shop/purchase_service.proto)

`testing: [gRpc](shop-api-grpc.vrts-slb.test.vertis.yandex.net) / [http](shop-api-http.vrts-slb.test.vertis.yandex.net)`

`production: [gRpc](shop-api-grpc.vrts-slb.prod.vertis.yandex.net) / [http](shop-api-http.vrts-slb.prod.vertis.yandex.net)`

## Scheduler

[TeamCity](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_AutoRuExp_shop_scheduler_release?mode=builds)

`Метрики: `
[Очереди и задачи](https://grafana.vertis.yandex-team.ru/d/JQwgV4eGz/shop-scheduler?orgId=1&refresh=30s) /
[http Client](https://grafana.vertis.yandex-team.ru/d/http-client/http-client?orgId=1&refresh=30s&var-datasource=Prometheus&var-job=shop-scheduler&var-dc=All&var-service=trust&var-name=All&var-window=2m) / 
[System](https://grafana.vertis.yandex-team.ru/d/system-info/system-info?orgId=1&refresh=30s&var-datasource=Prometheus&var-job=shop-scheduler&var-dc=All&var-window=2m&var-gc=All&var-instance=All)

`Топик событий в брокере:` [test](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/test/warehouse/billing/product_event) / [prod](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/billing/product_event)

## Production alerts

- [api alerts dashboard](https://grafana.vertis.yandex-team.ru/d/oAg84RS7k/shop-api-alerts)
- [scheduler alerts dashboard](https://grafana.vertis.yandex-team.ru/d/s_8qj7m7z/shop-scheduler-alerts)

## Sentry

- [api test](https://sentry.vertis.yandex.net/verticals/shop-api/?query=environment%3A%22test%22)
- [api prod](https://sentry.vertis.yandex.net/verticals/shop-api/?query=environment%3A%22prod%22)
- [scheduler test](https://sentry.vertis.yandex.net/verticals/shop-scheduler/?query=environment%3A%22test%22)
- [scheduler prod](https://sentry.vertis.yandex.net/verticals/shop-scheduler/?query=environment%3A%22prod%22)

## Debug
- [Jaeger prod](https://jaeger.vertis.yandex.net/search?service=shop-api)
- [Jaeger test](https://jaeger.test.vertis.yandex.net/search?service=shop-api)
- [api logs prod](https://nda.ya.ru/t/MISKxmfb4JyZ95)
- [scheduler logs prod](https://nda.ya.ru/t/p8UYBh2B4JyZQt)
- [api logs test](https://nda.ya.ru/t/YvIYIUFq4JyZDj)
- [scheduler logs test](https://nda.ya.ru/t/9yBP5b1X4JyZNG)
- [База ydb в тестинге](https://ydb.yandex-team.ru/db/ydb-ru-prestable/verticals/testing/common/browser/billing/shop)
