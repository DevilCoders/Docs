# Сервис для проведения аукционов

## Назначение

Сервис аукционов - общее решение для проведения различных аукционов.

Изначально предназначен для аукционов по стоимости звонков для дилеров авто.ру.
Бизнес-задача: https://st.yandex-team.ru/VERTISMETA-308

Диз. док: https://wiki.yandex-team.ru/users/alexkonygin/aukciony-na-zvonki.-komanda-monetizacii/

## Модули
- api –– API сервиса
- scheduler –– модуль, отвечающий за выгрузку актуальных ставок аукциона в другие сервисы

## Релиз в тестинг

Мержим свои изменения в master и запускаем в TeamCity джоб для соответствующего сервиса:
- [auction-api](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_AutoRuExp_auction_api_release?mode=builds#all-projects)
- [auction-scheduler](https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_AutoRuExp_auction_scheduler_release?mode=builds#all-projects)

### Как выкатить в тестинг свою ветку
См. [deploy-custom-branch](../../docs/how-to/deploy-custom-branch.md)

## SOX и релиз в прод

Сервис катится через шиву, с обязательным апрувом от одного из разработчиков [ответственной команды](https://staff.yandex-team.ru/departments/yandex_personal_vertserv_auto_autoru_4431_dep64201).

- [api в шиве](https://admin.vertis.yandex-team.ru/services/auction-api)
- [scheduler в шиве](https://admin.vertis.yandex-team.ru/services/auction-scheduler)

## Интеграции и процесс
- Ставки хранятся в howmuch
- Настройки параметров проведения аукционов в palma
  - [testing](https://palma.test.vertis.yandex-team.ru/dictionaries/vsmoney/auction/params)
  - [prod](https://palma.vertis.yandex-team.ru/dictionaries/vsmoney/auction/params)
- Журнал ставок пишется через брокер в YT и kafka
  - [YT testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/test/warehouse/vsmoney/auction_bids)
  - [YT prod](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/vsmoney/auction_bids)
  - [Kafka testing](http://kafka-01-man.test.vertis.yandex.net:9000/clusters/testing/topics/broker-vsmoney-auction-bids)

## Production metrics

- [grpc server](https://grafana.vertis.yandex-team.ru/d/grpc/grpc-server?var-job=auction-api)
- [Сгенеренный дашборд auction-api](https://grafana.vertis.yandex-team.ru/d/_bmLFWm7k/auction-api)
- [Сгенеренный дашборд auction-scheduler](https://grafana.vertis.yandex-team.ru/d/MQufFZm7z/auction-scheduler)

## Production alerts
- [juggler alerts](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dvertis_ops_auction_api%7Chost%3Dvertis_ops_auction_scheduler)

## Sentry
- api
  - [testing](https://sentry.vertis.yandex.net/verticals/auction-api/?query=environment%3A%22test%22)
  - [prod](https://sentry.vertis.yandex.net/verticals/auction-api/?query=environment%3A%22prod%22)
- scheduler
  - [testing](https://sentry.vertis.yandex.net/verticals/auction-scheduler/?query=environment%3A%22test%22)
  - [prod](https://sentry.vertis.yandex.net/verticals/auction-scheduler/?query=environment%3A%22prod%22)

## Debug
- jaeger
  - [prod](https://jaeger.vertis.yandex.net/search?service=auction-api)
  - [testing](https://jaeger.test.vertis.yandex.net/search?service=auction-api)
- api logs
  - [prod](https://grafana.vertis.yandex-team.ru/goto/1LnmO3Hnk)
  - [testing](https://grafana.vertis.yandex-team.ru/goto/b55VOqNnk)
- scheduler logs
  - [prod](https://grafana.vertis.yandex-team.ru/goto/duKSOqHnz)
  - [testing](https://grafana.vertis.yandex-team.ru/goto/zHS7OqNnk)
