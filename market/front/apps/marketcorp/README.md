# Остановись!

Корп портал закопан и вместо него поставлена заглушка, обновлять его
не имеет смысла. Работоспособность того, что находится под заглушкой,
не гарантируется. Заглушка, хоть и статическая, выдаётся из этого самого
репозитория динамически - здесь можно её поправить, если что.

Подробнее [читай здесь](MARKETFRONTECH-2276).

## Разработка


[Старт разработки](https://wiki.yandex-team.ru/redmarket/web/quickstart/)

[Правила разработки](https://wiki.yandex-team.ru/redmarket/web/development/)

[Ссылка на прод](https://yandexmarketgroup.ru)

## Ресуры
Конфиги в няне (nginx, pkg.json, variables) - /trunk/arcadia/market/sre/nanny/front/marketcorp
Таск MARKET_CORPSITE_FRONT_CONFIG упаковывает конфиг приложения в ресурс


Таск MARKET_YA_PACKAGE упаковывает все приложение в ресурс для доставки в няню


### Платформа блогов
За постами можно ходить:
 - http://yablogs-api.yandex.net
 - http://yablogs-api-production.yandex.net

Доступ в puncher заказывать до: yablogs-api.stable.qloud-b.yandex.net:80
Ответственный на стороне блогов: Денис Чистяков.

