# Дашборды

## Метрики сервисов
Список общих графиков в Grafana, генерируемых из монорепы:

1) [Системные метрики](https://grafana.vertis.yandex-team.ru/d/system-info/system-info?orgId=1&refresh=30s)

2) [Серверные метрики gRPC](https://grafana.vertis.yandex-team.ru/d/grpc/grpc-server?orgId=1&refresh=30s)

3) [Клиентские метрики gRPC](https://grafana.vertis.yandex-team.ru/d/grpc-client/grpc-client?orgId=1&refresh=30s)

4) [Серверные метрики http](https://grafana.vertis.yandex-team.ru/d/http-server/http-server?orgId=1&refresh=30s)

5) [Клиентские метрики http](https://grafana.vertis.yandex-team.ru/d/http-client/http-client?orgId=1&refresh=30s)

6) [Графики лага kafka-консьюмеров](https://grafana.vertis.yandex-team.ru/d/kpdUo1ank/burrow-kafka-consumer?orgId=1&refresh=1m)

7) [Метрики kafka-клиентов](https://grafana.vertis.yandex-team.ru/d/k3s7s-cMk/kafka-clients?orgId=1&refresh=1m)

8) [Метрики Hikari-пула](https://grafana.vertis.yandex-team.ru/d/hikari-pool/hikari-pool?orgId=1&refresh=30s)

Описание дашбордов лежит в [репозитории](https://a.yandex-team.ru/arc_vcs/classifieds/verticals-backend/common/dashboards).

## Метрики bazel-таргетов
У нас есть [дашборд](https://datalens.yandex-team.ru/lyacag96q7dad-ci?tab=LW) для анализа bazel-таргетов.

На нем можно посмотреть в разрезе по дням:
- как часто запускаются и как долго выполняются ваши тесты
- как часто они флапают
- как часто перекомпилируются ваши таргеты и сколько времени это занимает
