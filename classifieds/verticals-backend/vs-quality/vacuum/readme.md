### Vacuum - сервис разметки кластеров диалогов

[Дизайн док](./design.md)

[Чат дежурных](https://t.me/joinchat/nkaJg3BGCK4zZDc6)

### Workflow
[[Сервис в админке](https://admin.vertis.yandex-team.ru/services/vacuum-tms)]

[[Релизная джоба](https://a.yandex-team.ru/projects/verticals/ci/releases/timeline?dir=classifieds%2Fverticals-backend&id=vacuum-tms-release&sidebarFilter=vacuu)]

[[Deploy bot](https://t.me/vertis_shiva_bot)]:
- Подписка на деплои: `/sub -l [test/prod] vacuum-tms`
- Выкладка: `/run -l [test/prod] -v [version] vacuum-tms`
  

### Наблюдение

Дашборды:
- [[Лаги обработки](https://grafana.vertis.yandex-team.ru/d/uojZ1ZfGk/vacuum?orgId=1&refresh=30s&var-datasource=Prometheus&var-client_id=hammer-offers-consumer&from=now-6h&to=now)]
- [[Jvm и системные метрики](https://grafana.vertis.yandex-team.ru/d/system-info/system-info?orgId=1&refresh=30s&var-datasource=Prometheus&var-job=vacuum-tms&var-dc=All&var-window=2m&var-gc=All&var-_allocation_id=All)]
- [[Клиентские grpc метрики](https://grafana.vertis.yandex-team.ru/d/grpc-client/grpc-client?orgId=1&refresh=30s&var-datasource=Prometheus&var-job=vacuum-tms&var-dc=All&var-service=vertis.dust.DialogsClusteringService&var-method=All&var-window=2m)]
- [[Клиентские http метрики](https://grafana.vertis.yandex-team.ru/d/http-client/http-client?orgId=1&refresh=30s&var-datasource=Prometheus&var-job=vacuum-tms&var-dc=All&var-service=telepony&var-name=All&var-window=2m)]
- [[Серверные grpc метрики](https://grafana.vertis.yandex-team.ru/d/grpc/grpc-server?orgId=1&refresh=30s&var-datasource=Prometheus&var-job=vacuum-tms&var-dc=All&var-service=vertis.vsquality.vacuum.VacuumApi&var-method=All&var-window=2m)]

[[Логи](https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22refId%22:%22A%22,%22expr%22:%22service%3Dvacuum-tms%20layer%3Dprod%20level!%3Dinfo%22,%22fields%22:%5B%22thread%22,%22context%22,%22message%22,%22rest%22%5D,%22limit%22:100%7D%5D)]

[[Алерты](https://juggler.yandex-team.ru/aggregate_checks/?project=vertis-ops&query=tag%3Dvertis_ops_vacuum)]

[[Sentry](https://sentry.vertis.yandex.net/verticals/vacuum-tms/)]