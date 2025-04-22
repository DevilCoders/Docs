## Библиотека для подключения клиента mbi-api

1. ```ru.yandex.market.adv.config.MbiApiAutoconfiguration``` - автоконфигурация для подключения к mbi-api
   через ```ru.yandex.market.mbi.open.api.client.MbiOpenApiClient```.

## Подключение mbi-api

1. Сделать в puncher дырки
   для [Прода](https://puncher.yandex-team.ru/?destination=mbi-api.market.yandex.net&rules=exclude_inactive&sort=source&source=_MARKET_PROD_ADV_PLATFORM_NETS_)
   и [Тестинга](https://puncher.yandex-team.ru/?destination=mbi-back.tst.vs.market.yandex.net&rules=exclude_inactive&sort=source&source=_MARKET_TEST_ADV_PLATFORM_NETS_)
   по аналогии.
2. Прописать в настройках приложения ```mbi.api.url```. Для тестинга обычно
   это ```http://mbi-back.tst.vs.market.yandex.net:34820```, для прода ```http://mbi-api.market.yandex.net```.
