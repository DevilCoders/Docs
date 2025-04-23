# Metric-collector: сбор yasm-метрик из нескольких источников

Утилита, входящая в состав [базового образа](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/baseimage/README.md).
Используется как единая точка входа для yasm-агента, собирает и аггрегирует метрики из следующих источников:
- yacare-сервисы,
- pycare-сервисы,
- версия базового образа (читается на старте из файла `/etc/base_image_revision`),
- метрики со всех указанных в конфиге эндпоинтов (если такие есть).

Если нужно собирать метрики в [yasm-формате](https://wiki.yandex-team.ru/golovan/userdocs/stat-handle/#tipydannyx) с кастомного эндпоинта (порт + ручка), то можно поместить по пути
`/etc/yandex/maps/metric_collector/config.yaml` конфиг c содержимым следующего формата:
```
aux_stat_endpoints:
    - port: 7080
      path: /stats
      vhost: example.maps.yandex.net
      prefix: stats
    - port: 8999
      path: /yasm_stats
```
Параметры `vhost` и `prefix` являются необязательными. Первый отвечает за выставление хэдера `Host` при опрашивании
кастомного эндпоинта. Второй за добавление всем полученным из эндпоинта метрикам соответствующего префикса, т.е.
метрика `my_metric_avvv` превратится в `aux-<prefix>_my_metric_avvv` (префикс `aux-` в любом случае проставит yasm).

Если нужно собирать метрики с grpc-сервиса, то в конфиге необходимо написать следующее:
```yaml
grpc_metrics:
  - unix:/path/to/socket
  - localhost:1234
```

Также, в конфиге можно указать любой валидный [grpc uri](https://grpc.github.io/grpc/cpp/md_doc_naming.html)

В сервисе должен быть поднят grpc-сервер, написанный на вашем любимом языке со следующей [спекой](https://a.yandex-team.ru/arc_vcs/maps/infra/metric_collector/proto/metric_collector.proto)

Логи метрик-коллектор пишет в stdout/-err, а в составе базового образа они сохраняются в `/var/log/supervisor/metric-collector-std*.log`
