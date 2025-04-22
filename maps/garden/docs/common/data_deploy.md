# Деплой данных

Для примера рассмотрим деплой дорожного графа:

![](img/data_deploy.png)

В `stable`-контуре в Огороде работают стабильные версии модулей `ymapsdf`, `road_graph_build`, `road_graph_deployment` (они были зарелизены в `stable` через Sedem).

Результатом их работы являются стабильные данные, которые заливаются в [стабильный экстатик](http://ecstatic.maps.yandex.net/). В [конфиге экстатика](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ecstatic/stable) настроены 3 ветки, к которым привязаны разные Няня-сервисы.

* Сначала данные деплоятся в `testing`-ветку и попадают в сервис `maps_core_driving_router_datavalidation`. Далее запускаются автотесты, которые проверяют, что в данных нет критичных ошибок.
* Далее данные деплоятся в `prestable`-ветку и попадают в сервис `maps_core_driving_router_dataprestable`. На этот сервис направляется доля реальных запросов пользователей.
* Через 2 часа данные деплоятся в `stable`-ветку и попадают в сервисы `maps_core_driving_router_prestable` и `maps_core_driving_router_stable`.

Далее сервисы `maps_core_driving_router_dataprestable`, `maps_core_driving_router_prestable` и `maps_core_driving_router_stable` работают все одновременно. В случае обнаружения проблем в данных дежурный должен вручную через UI запустить деплой более старой версии данных в ветки `prestable` и `stable`.

---

Контур `datatesting` в Огороде настроен симметрично. Там работают тестовые версии модулей `ymapsdf`, `road_graph_build`, `road_graph_deployment` (они были зарелизены в `testing` через Sedem).

Результатом их работы являются тестовые данные, которые заливаются в [datatesting экстатик](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/). В [конфиге экстатика](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ecstatic/datatesting) настроены 3 идентичные ветки, к которым привязаны разные Няня-сервисы.

* Ветка `testing` - для автотестов.
* Ветка `prestable` - туда зеркалируется доля реальных запросов пользователей.
* Ветка `stable` - для проверки, что стабильный софт роутера корректно работает с тестовыми данными.

Данные из пользовательских контуров попадают в [unstable экстатик](http://core-ecstatic-coordinator.unstable.common.maps.yandex.net), но никуда не деплоятся.

---

Для других модулей и других сервисов схемы деплоя очень похожи на эту, хотя некоторые ветки в экстатике могут отсутствовать.

Описание принципиальной структуры окружений: [https://wiki.yandex-team.ru/maps/dev/core/environment/](https://wiki.yandex-team.ru/maps/dev/core/environment/).

---

Подробнее про настройку деплоя в Огороде - на отдельной [странице](deploy.md).
