## Описание
В этой директории раньше жил код старого картиночного робота. Код удален.

## Avatars
1. [Документация](https://wiki.yandex-team.ru/mds/avatars/)

## Datacamp
1. [Полная документация](https://docs.yandex-team.ru/market-datacamp/market/idx/datacamp/picrobot/README)

## Расследования картинок
1. [Доктор->ЕОХ->Изображения](https://doctor.market.yandex-team.ru/)
  - [Пример](https://doctor.market.yandex-team.ru/offer-diagnostic?businessId=897861&expandedBlock=PicturesViewer&mainTab=DATACAMP_OFFERS&offerId=4690624028816)

## API
1. [Документация](https://docs.yandex-team.ru/market-datacamp/market/idx/datacamp/picrobot/README#picrobot_http)

## Мониторинги

[Дашборд yasm marketpic](https://yasm.yandex-team.ru/template/panel/avatars_mds/ns=marketpic/)

[Дашборд yasm marketpic_scaled](https://yasm.yandex-team.ru/template/panel/avatars_mds/ns=marketpic_scaled/)

0. [SLO 3h](https://monitoring.yandex-team.ru/projects/market-picrobot/dashboards/monmu48kr3prq8jrtg0p/view/graph/widget_2_4/queries?p.namespace=%2A&range=1d&refresh=60)
1. [Устаревший дашборд в Solomon](https://solomon.yandex-team.ru/admin/projects/market-picrobot)
2. [Новый дашборд](https://docs.yandex-team.ru/market-datacamp/market/idx/datacamp/picrobot/README#dashbord)
3. [Ошибки аватарницы 4xx](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dmarket.indexer%26(service%3Dpicrobot_production_4xx%7Cservice%3Dpicrobot_testing_4xx)) настроены по [графику в головане](https://yasm.yandex-team.ru/template/panel/avatars_mds/ns=marketpic/1/)
- [Логи аватрницы в YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/avatars-mds-access-log)
- [testing](https://yasm.yandex-team.ru/alert/picrobot_testing_4xx?from=1563969599838&to=1563971099838)
- [production](https://yasm.yandex-team.ru/alert/picrobot_production_4xx?from=1563970931437&to=1563972431437)
- Пример расследовния всплесков 4xx [MARKETINDEXER-31004](https://st.yandex-team.ru/MARKETINDEXER-31004)
