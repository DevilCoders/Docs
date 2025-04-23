Checkout-Referee
================

https://wiki.yandex-team.ru/market/marketplace/dev/checkout-referee АПИ, схема данных

https://wiki.yandex-team.ru/market/development/abo/cpa/arbitrage/ Арбитражи в АБО

http://checkout-referee.tst.vs.market.yandex.net:33484/swagger-ui.html Документация API

Запуск
------
```
# локальный запуск
ru.yandex.market.checkout.referee.DebugMain
curl localhost:33484/arbitrage/conversations/ping

# загрузка на дев
ssh-agent && ssh-add
./upload-to-dev.sh

# сборка пакета
ya package package.json
```

Релиз
------
[Автоматически в ЦУМе](https://tsum.yandex-team.ru/pipe/projects/abo/release/new/checkout-referee)


Liquibase
---------
Команды:
- `update` - применить
- `updateSQL` - посмотреть применение
- `changelogSync` - обновить мета-данные без применения ченж-сетов
- `changelogSyncSQL` - тоже самое, без реальных изменений

Окружения:
- `dev`
- `testing`
- `production`

dev:
```
cd checkout-referee
./liquibase-dev.sh updateSQL
```
testing: https://sandbox.yandex-team.ru/task/324196794/view
production: https://sandbox.yandex-team.ru/task/324202010/view

Checkstyle
----------

[@SuppressWarnings](https://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-suppress_warnings.htm)
