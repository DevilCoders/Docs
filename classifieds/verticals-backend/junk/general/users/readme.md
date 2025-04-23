# Сервис хранения пользовательских профилей

- Хранит адреса и публичное имя пользователя.
- Обогащает ответ данными из `Я.Паспорта` (Регистрация в сервисе не обязательна. Однако хранимые у нас данные имеют больший приоритет).
- Изменение паспортных данных требует прямого похода в `Я.Паспорт`.

## API
[gRPC service](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/users/api.proto)

### Балансеры
- `general-user-api-grpc.vrts-slb.test.vertis.yandex.net:80` (testing)

## Топик с экспортом изменений
- `general-user-updates` (модель сообщения [UserView](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/users/model.proto#L9))

## Sentry
- https://sentry.vertis.yandex.net/verticals/general-user/
