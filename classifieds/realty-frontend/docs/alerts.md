# Алерты

Используем juggler + prometheus.

## Что делать, если сработал алерт
* Посмотреть на [графики](https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?orgId=1)
* Посмотреть на [трейсы](./tracing.md)
* Посмотреть на [логи](./logs.md)
* Если не получается быстро разобраться, то призвать своего руководителя

## Полезные ссылки
* [Как настроить](https://wiki.yandex-team.ru/vertis-admin/monitoring-from-prometheus/)
* [Список чекеров в juggler](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dvertis_ops_realty-frontend)
* [Список чекеров в prometheus](https://prometheus.vertis.yandex.net/alerts)
* [Наши конфиги](https://github.com/YandexClassifieds/prometheus-config/blob/master/production/alerts), ищи `realty-front-<service-name>.rules.yml`
* [Настройки нотификаций в juggler](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5d13994fdcc66c0068fa64d4)
* [Про FlapDetector](https://wiki.yandex-team.ru/sm/juggler/flapdetector/)
