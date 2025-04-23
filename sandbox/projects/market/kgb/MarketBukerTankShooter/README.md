Задача представляет собой клон [задачи Market-buker](https://jenkins-load.yandex-team.ru/view/Market-backend/job/Market-buker) из jenkins-load, созданной для для ручных/исследовательских стрельб разработчиков в букер.
Скрипты для задачи в дженкинсе лежат [в гитхабе](https://github.yandex-team.ru/netort/load_tools/tree/master/regression/market/backend/buker)

## Патроны
Сейчас используется файл с патронами, сгенерированными из access-логов 2015 года.
Он хранится в виде ресурса в сендбоксе [id#719976543](https://sandbox.yandex-team.ru/resource/719976543/view)

Патроны сгенерированы в request-style, размечены тегами, соответствующими uri,
содержат заголовок User-Agent, уникальный для каждого запроса.

## Мишень
kgb-load01vt.market.yandex.net:29310

## Конфиги
Лежат в sandbox/projects/market/kgb/MarketBukerTankShooter/configs

## Запуск
Стрельбы регулярно запускаются с помощью сендбоксового шедулера (запуск задачи SHOOT_VIA_TANKAPI)

## Результаты
[Графики регрессии](https://lunapark.yandex-team.ru/regress/MARKETOUT?service=market_backend%20buker)