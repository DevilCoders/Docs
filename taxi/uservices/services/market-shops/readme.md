# Что это?
Магазинный микросервис

# Информация

Wiki: https://wiki.yandex-team.ru/market/report/infra/shop/

Путь в Аркадии: ((https://a.yandex-team.ru/arc/trunk/arcadia/taxi/uservices/services/market-shops taxi/uservices/services/market-shops))
Пайплайны в ЦУМе: ((https://tsum.yandex-team.ru/pipe/projects/report/pipelines/shop shop)), ((https://tsum.yandex-team.ru/pipe/projects/report/pipelines/shop-hotfix shop-hotfix))
Релизная машина в ЦУМе: ((https://tsum.yandex-team.ru/pipe/projects/report/delivery-dashboard/shop shop pipeline))

Дашборды в графане:
* https://grafana.yandex-team.ru/d/o4fwnkA7z/market-shop-auto-graph
Конфиги логшаттера:
* https://health.market.yandex-team.ru/projects/market_report/logshatter/configs/shop
Конфиги кликфита:
* https://health.market.yandex-team.ru/projects/market_report/clickphite/configs/shop

**PRODUCTION**

Сервисы в Деплое:
* https://yd.yandex-team.ru/stages/production_market_shop

**TESTING**

Сервисы в Деплое:
* https://yd.yandex-team.ru/stages/testing_market_shop

**Локальная сборка и отладка**
Для локальной отладки служит директория dev. Там находятся скрипты:
* dev/acquire_data.sh - собирает market access, запускает, получает ресурс, создает symlink в dev/pdata
* dev/run_config_service.sh - собирает сэмпл конфиг сервиса и запускает (без этого будет работать, но сервис постоянно будет пытаться стучать сюда и будут шибки в логе)
* dev/run_market_shops.sh - генерит и собирает сервис, запускает
