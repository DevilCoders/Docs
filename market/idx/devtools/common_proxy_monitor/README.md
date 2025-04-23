# Демон мониторинга common-proxy сервисов

## Как работает

* периодически опрашивает сервис по ручке /info_server
* анализирует граф процессоров common-proxy
* пуляет события в Juggler:
    * testing https://juggler.yandex-team.ru/raw_events/?query=service%3Dmarket-indexer-common-proxy_testing
    * prestable https://juggler.yandex-team.ru/raw_events/?query=service%3Dmarket-indexer-common-proxy_prestable
    * production https://juggler.yandex-team.ru/raw_events/?query=service%3Dmarket-indexer-common-proxy_production

Демон не использует информацию о конкретном сервисе и может быть использован для любого сервиса, построенного на common-proxy.

## Как деплоить
Притащить бинарь на RTC-хост и запустить в фоне рядом со своим сервисом. По умолчанию, демон пытается самостоятельно сконфигурироваться, анализируя переменные окружения.
