# Vasabi - General VASes service

Сервис хранения и обработки доп услуг Я.Объявлений

## API
[VasesService Grpc](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/vasabi/api.proto)

### Балансеры
- `vasabi-api-grpc.vrts-slb.test.vertis.yandex.net:80` (testing)
- `vasabi-api-grpc.vrts-slb.prod.vertis.yandex.net:80` (prod)

## Топик с экспортом изменений
- `vasabi-export` ([VasRecord](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/vasabi/export_model.proto))

## Sentry
- [API](https://sentry.vertis.yandex.net/verticals/vasabi-api/)
- [Scheduler](https://sentry.vertis.yandex.net/verticals/vasabi-scheduler/)

## Графики
- [Дашборд всего](https://grafana.vertis.yandex-team.ru/d/-CsUa2UMk/vasabi?orgId=1&refresh=30s)