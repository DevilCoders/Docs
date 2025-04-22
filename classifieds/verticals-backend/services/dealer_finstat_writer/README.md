# Dealer-finstat-writer

## Описание проекта

Сервис формирования событий для [финансовой статистики (finstat-api)](https://github.com/YandexClassifieds/verticals-backend/tree/master/billing/finstat). Работает с потоком транзакций юридических лиц (дилеров).

Весь сервис состоит из следующих частей:
1. Консьюмер топика [broker-billing-billing-raw-operation-event](http://kafka-01-sas.test.vertis.yandex.net:9000/clusters/testing/topics/broker-billing-billing-raw-operation-event). Читает события в формете [прото-модели BillingOperation](https://github.com/YandexClassifieds/verticals-backend/blob/4dc0b817abb82b84e6d2b5a9edc55d1119a1178e/schema-registry/proto/vertis/billing/billing-event.proto#L426).
2. Обогащение данных с помощью других сервисов (сейчас dealer-finstat-writer ходит в [cabinet-api](https://github.com/YandexClassifieds/cabinet-api) для обогащения списаний по звонкам)
3. Преобразование данных в [прото-модель AutoruDealersFinstat](https://github.com/YandexClassifieds/verticals-backend/blob/dc78bd91fa4c5bfb5d97d6f43b09161f9876b120/schema-registry/proto/billing/finstat/autoru_dealers.proto#L9)
4. Запись AutoruDealersFinstat в [broker](https://github.com/YandexClassifieds/verticals-backend/tree/master/etc-mono/services/broker), который пишет в кликхаус.


Если смотреть на общий пайплайн поставки событий в finstat-api, то он представляет собой следующее:

```
billing --> broker(BillingOperation) --> dealer-finstat-writer --> broker(AutoruDealersFinstat) --> ClickHouse --> finstat-api
```

Одна из особенностей dealer-finstat-writer -- остановка поставки при встрече события, которое сервис не может корректно обработать.
При встрече такого сообщения загорается алерт.

Исторические данные для дилеров autoru собирали запросами:
- [запрос собирающий данные по событиям indexing](./docs/upload_indexing)
- [запрос собирающий данные по звонкам](./docs/upload_phones)

Если понадобится в исторические данные добавить новое поле, эти запросы нужно будет модифицировать.
## Для разработчика

### Адрес сервиса

- Сервис живет в шиве ([ссылка на админку](https://admin.vertis.yandex-team.ru/services/dealer-finstat-writer)).

### Дебаг

- Логи можно смотреть в [графане](https://nda.ya.ru/t/giepn6GO4ptuqn).
- Трейсы можно смотреть в Jaeger ([test](https://jaeger.test.vertis.yandex.net/search?service=dealer-finstat-writer) и [prod](https://jaeger.vertis.yandex.net/search?service=dealer-finstat-writer)).

### Метрики

- [Дашборд в графане c алертами](https://grafana.vertis.yandex-team.ru/d/5kMyUi-nz/dealer-finstat-writer-monitoring?orgId=1).
