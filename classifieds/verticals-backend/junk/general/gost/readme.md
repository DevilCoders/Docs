# GOST - General Offer Storage

Система для хранения объявлений сервиса Яндекс.Объявления.

## API
[Draft gRPC service](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/gost/draft_api.proto)
[Offer gRPC service](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/gost/offer_api.proto)

### Балансеры
- `gost-api-grpc.vrts-slb.test.vertis.yandex.net:80` (testing)

## Топик с экспортом изменений
- `gost-offer-updates` ([OfferUpdateRecord](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/gost/offer_model.proto))

## Топики для заливки фидов
- `gost-feed-requests` ([формат](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/gost/feed_api.proto#L18))
- `gost-feed-responses` ([формат](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/gost/feed_api.proto#L80))

## Sentry
- https://sentry.vertis.yandex.net/verticals/gost/

## Скрипт добавления всех объявления в очередь стейджа
https://yql.yandex-team.ru/Operations/X9fG_p3udlHEq0Za5Y4UrCHq7StO1RPgQedMnblzQoU= 