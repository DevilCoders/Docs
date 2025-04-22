# Sedem

Sedem - система управления жизненным циклом сервисов. Sedem умеет:
- создавать новые [няня-сервисы](services/nanny) и ограниченно модифицировать существующие;
- создавать [балансеры](services/balancers) для няня-сервисов и управлять их конфигурацией;
- создавать и обновлять [шедулеры и шаблоны для бинарных sandbox-задач](services/sandbox);
- [релизить](releases) няня-сервисы, огородные модули и sandbox-задачи;
- [настраивать мониторинги](monitorings/alerts_metrics) для этих типов сервисов.

{% note tip %}

Воспользуйтесь [каталогом sedem-сервисов (Sedem Service Directory)](https://proxy.sandbox.yandex-team.ru/last/SEDEM_SERVICE_TOC/index.html), чтобы прочесть сгенерированный readme сервиса, просмотреть статус алертов или провести [нагрузочный тест по кнопке](services/nanny#manual-load-test-sedem).

{% endnote %}

## Сетевые доступы для Sedem CLI { #firewall }

Если вы используете Sedem CLI с вашего ноутбука, то достаточно [добавиться в `abc:maps-core-sedem-users`](https://abc.yandex-team.ru/services/maps-core-sedem-users/).

Для дев-машинок из макроса `_MAPS_DEV_RTC_NETS_` все необходимые доступы уже имеются.

Для других макросов необходимо запросить доступы до перечисленных API:
- sedem-api — `core-sedem-machine.maps.yandex.net:80`;
- arc-api — `api.arc-vcs.yandex-team.ru:6734`;
- sandbox-api — `sandbox.yandex-team.ru:443`;
- juggler-api — `juggler-api.search.yandex.net:80`;
- nda-api — `nda.ya.ru:443`;
- nanny-api — `nanny.yandex-team.ru:443` (только для релизов няня-сервисов);
- garden-api — `core-garden-server.maps.yandex.net:80` (только для релизов огородных модулей).


## Полезные ссылки { #links }

* [Контакты](contacts)
* [Исходный код](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/sedem)
