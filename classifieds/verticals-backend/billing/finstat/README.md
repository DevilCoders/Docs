# Finstat-api

## Описание проекта

Сервис для подсчета финансовой статистики на основе данных в кликхаусе.
Основное преимущество сервиса -- дедупликация событий и их агрегация.

Больше документации собрано [здесь](docs).

## Для пользователя

Подробная документация сервиса для потребителей [написана здесь](docs/guides/user_guide.md).

### Чат поддержки

- [чат поддержки биллинга](t.me/joinchat/DN5j4EhyeEtKVkNXcFUDsg)
- [чат для интеграции с финстатой](https://t.me/+y_dHHmRz1eU1ZDgy)

### Описание api

Финстата предоставляет grpc-api:

- Балансер в тестинге: [finstat-api-grpc.vrts-slb.test.vertis.yandex.net:80](finstat-api-grpc.vrts-slb.test.vertis.yandex.net:80)
- Балансер в проде: [finstat-api-grpc.vrts-slb.prod.vertis.yandex.net:80](finstat-api-grpc.vrts-slb.prod.vertis.yandex.net:80)
- [proto-схема](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/billing/finstat/api_model.proto)

### Адреса сервисов

Сервис живет в шиве ([ссылка на админку](https://admin.vertis.yandex-team.ru/services/finstat-api)).


## Для разработчика

### Как сделать фикс

- Для разработки ответвляем ветку от мастера, называем ее с номером тикета в префиксе (например `VSBILLING-12345_finstat_tracing`).
- Делаем pull-request в trunk. В названии pr рекомендуется указывать номер тикета.
- Ждем апрува pull-request (или договориваемся о пост-ревью с людьми из команды).
- Мержим pull-request в trunk.

### Как выкатить фикс в прод

Катить фикс в прод можно только из trunk. Подробный гайд [здесь](https://docs.yandex-team.ru/classifieds-infra/verticals-backend/ci/intro#reliz-iz-trunka).

### Как выкатить фикс в тестинг из ветки

Можно выкатить фикс в тестинг из любой ветки. Подробный гайд [здесь](https://docs.yandex-team.ru/classifieds-infra/verticals-backend/ci/intro#reliz-iz-vetki).

### Как поднять сервис локально

Подробный гайд [здесь](../../docs/how-to/run-service-locally.md).

### Дебаг

- Логи можно смотреть в [графане](https://nda.ya.ru/t/25fW23vO4puNDL).
- Трейсы можно смотреть в Jaeger ([test](https://jaeger.test.vertis.yandex.net/search?service=finstat-api) и [prod](https://jaeger.vertis.yandex.net/search?service=finstat-api)).

### Метрики

- [Дашборд с алертами](https://grafana.vertis.yandex-team.ru/d/YpCgvZY7z/finstat-api-monitoring?orgId=1).
- [Дашборд с таймингами апи](https://grafana.vertis.yandex-team.ru/d/grpc/grpc-server?var-job=finstat-api&orgId=1).
- [Дашборд с прочими графикам](https://grafana.vertis.yandex-team.ru/d/ZZPYQknnz/finstat-api?orgId=1).

### Кликхаус

#### Авто.ру

- Кластер кликхауса: [тестинг](https://cloud.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-clickhouse/cluster/mdbnd60l3n2iuh37euvg/view) и [прод](https://cloud.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-clickhouse/cluster/mdb6j6tjrvrlprutgmiu/view).
- Секрет с кредами: [тестинг](https://yav.yandex-team.ru/secret/sec-01fjkb1jnq68fz64d3wxhzpa8c/explore/versions) и [прод](https://yav.yandex-team.ru/secret/sec-01fjkbb8r34s53mf9391c2n68f/explore/versions).

#### СM.Expert

- Кластер кликхауса: [тестинг](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-clickhouse/cluster/mdbccils8ii99ut1ddai/view) и [прод](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-clickhouse/cluster/mdbmpgg34f4bm8dij6e5/view).
- Секрет с кредами: [тестинг](https://yav.yandex-team.ru/secret/sec-01fx2erjsd1g5ahmv96wr291zs) и [прод](https://yav.yandex-team.ru/secret/sec-01fxcpghvgm24pr2yf4a88qwbr).

#### Realty

- Кластер кликхауса: [тестинг](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-clickhouse/cluster/mdbb9mopioht81e970rk/view) и [прод](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-clickhouse/cluster/mdbo5mt3p8ppeadjp8vq/view).
- Секрет с кредами: [тестинг](https://yav.yandex-team.ru/secret/sec-01fxth8mfb1zpb2gzq6t58mjjw) и [прод](https://yav.yandex-team.ru/secret/sec-01fxthbjmxjy2natkh196z8q0t).
