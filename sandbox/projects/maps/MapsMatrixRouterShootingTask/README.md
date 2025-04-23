## Планировщики в Sandbox

* [DEPLOY_BINARY_TASK](https://sandbox.yandex-team.ru/scheduler/43940/view) -
  Загрузка этой бинарной задачи в Sandbox в виде ресурса. Автоматически
  запускается раз в сутки, рекомендуется запускать руками после внесения
  изменений.
* [MATRIX_ROUTER_SHOOTING_TASK -- стрельба в роутер на яндексовых данных](https://sandbox.yandex-team.ru/scheduler/43483/view)
* [MATRIX_ROUTER_SHOOTING_TASK -- стрельба в роутер на OSM-данных](https://sandbox.yandex-team.ru/scheduler/699956/view)


## Что делает эта задача

Задача обстреливает
[матричный роутер](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/matrix_router/)
по заданному URL. Для этого используется библиотека
[maps/routing/matrix_router/quality_reporter/shooter](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/matrix_router/quality_reporter/shooter).
Задача
[бинарная](https://docs.yandex-team.ru/sandbox/dev/binary-task).
Это означает, что код задачи собирается аркадийной сборкой в бинарь, который
затем загружается на сервер Sandbox и используется для выполнения всей или части
работы. Только бинарные задачи можно напрямую линковать с библиотеками в аркадии
(такими как `shooter`).


## Требования к коду задачи

1. Весь код должен быть совместим с аркадийным третьим питоном: модуль успешно
   импортироваться, все методы задачи выполняться.
2. Весь код, кроме метода `on_execute`, должен быть также совместим с серверным
   окружением Sandbox. Это второй питон, в котором доступны модули `sandbox.*` и
   [некоторый набор внешних модулей](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/requirements.txt).

Требование (1) нужно для локальных запусков с `--enable-taskbox`. Такие запуски
позволяют очень удобно и быстро протестировать локальные изменения в продуктовом
Sandbox. Весь код при этом выполняется из собранного бинаря, аркадийным Python 3.

Требование (2) нужно для запуска этой задачи через UI Sandbox. В этом случае всё,
кроме `on_execute`, выполняется в серверном окружении, а `on_execute` из
собранного бинаря.


## Секрет TVM-приложения

Для отправки запросов матричному роутеру этой задаче нужен секрет TVM-приложения,
от имени которого делаются запросы. Сам секрет находится в
[Секретнице](https://yav.yandex-team.ru), а задача получает его ID через
параметр `shooter_tvm_secret`. Этот ID можно увидеть как "secret_uuid" в
интерфейсе ABC, если вам выдана роль "TVM менеджер" в соответствующем сервисе.
Ссылки: [обычный матричный роутер](https://abc.yandex-team.ru/services/maps-core-matrix-router/resources/?view=consuming&layout=table&supplier=14&type=47&show-resource=28590920),
[OSM матричный роутер](https://abc.yandex-team.ru/services/maps-core-driving-matrix-router-over-osm/resources/?view=consuming&layout=table&supplier=14&type=47&show-resource=39183528).

Если роли нет, ID секрета можно подсмотреть в уже завершившихся запусках этой
задачи.


## Что сделать после коммита в этот код

Запустить планировщик
[DEPLOY_BINARY_TASK](https://sandbox.yandex-team.ru/scheduler/43940/view).
Созданная в нём задача соберёт свежую версию этой бинарной задачи, и загрузит её
в Sandbox в виде ресурса. Раз в сутки этот планировщик запускается автоматически.


## Как протестировать изменения

### С `--enable-taskbox`

Это самый простой способ протестировать изменения. Рекомендуется всегда.

Стрельба в матричный роутер на данных Яндекса:
```
./bin/maps-matrix-router-shooting-task-runner run --type MATRIX_ROUTER_SHOOTING_TASK --enable-taskbox '{"custom_fields": [{"name": "router_url", "value": "http://core-driving-matrix-router.common.testing.maps.yandex.net"}, {"name": "router_tvm_id", "value": 2017359}, {"name": "shooter_tvm_id", "value": 2026692}, {"name": "shooter_tvm_secret", "value": "<secret_id>"}, {"name": "juggler_host_name", "value": "sandbox.MapsMatrixRouterShootingTask.dev"}]}'
```

Стрельба в матричный роутер на данных OSM:
```
./bin/maps-matrix-router-shooting-task-runner run --type MATRIX_ROUTER_SHOOTING_TASK --enable-taskbox '{"custom_fields": [{"name": "router_url", "value": "http://core-driving-matrix-router-over-osm.common.testing.maps.yandex.net"}, {"name": "router_tvm_id", "value": 2029358}, {"name": "shooter_tvm_id", "value": 2032201}, {"name": "shooter_tvm_secret", "value": "<secret_id>"}, {"name": "juggler_host_name", "value": "sandbox.MapsMatrixRouterShootingTask.osm.dev"}]}'
```

Всё запускается третьим питоном, используется задача из собранного бинаря.

### Без `--enable-taskbox`

Те же строчки, но без параметра `--enable-taskbox`.

Метод `on_execute` выполняется из собранного бинаря. Все остальные методы
выполняются на сервере вторым питоном, используя код из транка. Подойдёт, если
изменения затрагивают только `on_execute`.

Этот вариант хорош тем, что похож на запуск задачи через UI Sandbox.

### В локальном Sandbox

Самый трудоёмкий способ. Может пригодиться, если изменения затрагивают не только
`on_execute`, а тестирование в режиме с `--enable-taskbox` какжется
недостаточным.

Не рекомендуется никому и никогда,
[документация здесь](https://docs.yandex-team.ru/sandbox/dev/local-sandbox)


## Ссылки

[Документация Sandbox](https://docs.yandex-team.ru/sandbox/)  
[Страничка про бинарные таски](https://docs.yandex-team.ru/sandbox/dev/binary-task)
