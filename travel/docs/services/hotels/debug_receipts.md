---
title: Рецепты для отладки
---
## Локальный запуск Travel API и Оркестратора

Как одновременно запустить локально API и Орк описано [здесь](https://docs.yandex-team.ru/travel/services/orders/orc_api_local_dev).
Дополнительно для запуска кода отелей могут понадобиться дополнительные локальные настройки.

* Следующие настройки для API добавляются в файл $ARCADIA/travel/orders/app/src/main/resources/application-local.yml.
Все секреты берутся из Няни, из [окружения](https://nanny.yandex-team.ru/ui/#/services/catalog/travel_hotels_api_testing).

```
# Для получения списка офферов отелей из тестинга Геокаунтера
geo-counter:
  channel:
    mode: TARGETS
    targets: travel-hotels-geocounter-test.yandex.net:14003

# Для вызова тестинга Промо-сервиса
promo-service:
  mode: TARGETS
  targets: travel-hotels-offercache-test.yandex.net:12599
cached-active-promo-service:
  enabled: true

# Для работы с токенами отеля
encryption:
  encryption-key: <Значение секрета>  # из переменной ENCRYPTION_ENCRYPTION_KEY

# Для получения офферов из key-value хранилища
yt:
  keyvalue:
    clusters:
      default:
        new-discovery-service: true
        table-path: //home/travel/testing/offer_data_storage
        user: <Имя своего пользователя>
    min-reads-to-continue: 2
    sink-clusters: seneca-sas,seneca-vla,arnold

hotels-booking-flow:
  # Для хождения к партнерам
  providers:
    travelline:
      debug-show-rate-info: true
      client:
        api-key: <Значение секрета>  # из переменной HOTELS_BOOKING_FLOW_PROVIDERS_TRAVELLINE_CLIENT_API_KEY
        base-url: https://yandex.tlintegration.com
```

* Следующие настройки для Орка добавляются в файл $ARCADIA/travel/orders/app/src/main/resources/application-local.yml.
Все секреты берутся из Няни, из [окружения](https://nanny.yandex-team.ru/ui/#/services/catalog/travel_orders_app_testing).

```
# Для работы с Трастом
trust-hotels:
    callback-url: https://api.travel-balancer-test.yandex.net/api/travel_orders_trust_callback/v1/basket_status_changed/
```

# Отладочный вызов Offercache по HTTP

Можно имитировать вызов GRPC-ручки офферкэша вызовом по HTTP.
Урл прода: http://travel-hotels-offercache.yandex.net.
Урл тестинга: http://travel-hotels-offercache-test.yandex.net.

Пример вызова:
```
http://travel-hotels-offercache-test.yandex.net:11001/read?SHotelId=1056004860&Debug=0&Date=2022-07-06&Nights=1&Ages=88,88&UseSearcher=1&RequestId=0&Full=1&ShowAllBadges=1
```
