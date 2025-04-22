# Bonsai

Каталог для сервиса яндекс.объявления.

## Компоненты
`bonsai` состоит из трех сервисов:
  - `api` – api для других сервисов
  - `internal-api` – api для админки
  - `scheduler` — различные периодические задачи

## API
[Public gRPC service](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/bonsai/public_api.proto)
[Internal gRPC service](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/bonsai/internal/internal_api.proto)

### Балансеры
#### Public API
- `bonsai-api-grpc.vrts-slb.test.vertis.yandex.net:80` (testing)

#### Internal API
- `bonsai-internal-api-grpc.vrts-slb.test.vertis.yandex.net:80` (testing)

### Экспорт в S3
Формат экспорта – write-delimited protobuf

Model – [export_model.proto](https://github.com/YandexClassifieds/schema-registry/blob/master/proto/general/bonsai/export_model.proto)

#### Testing
- `classified-test/export/bonsai_export_master_{version}` – периодический экспорт текущего состояния каталога
- `classified-test/export/bonsai_export_prod` – ручной экспорт каталога в продакшен

#### Production
- `classified/export/bonsai_export_master_{version}` – периодический экспорт текущего состояния каталога
- `classified/export/bonsai_export_prod` – ручной экспорт каталога в продакшен

### Данные в YT
https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/general/export/catalogs

 * avito – матчинг на категории авито
 * market - матчинг на категории маркета
 * categories - экспорт категорий
 * attributes - экспорт атрибутов

#### Загрузка матчинга в YT
- json-файл: `cat avito.json | yt --proxy hahn write --table //home/verticals/general/export/catalogs/avito --format '<encode_utf8=%false>json'` 
- csv-файл (с "шапкой" в первой строке и разделителем точка с запятой): `cat avito.csv | sed -e '1d' | yt write --proxy hahn //home/verticals/general/export/catalogs/avito --format '<columns=[avitoId;generalName;generalId];field_separator=";">schemaful_dsv'`

## Админка
- `general.test.vertis.yandex-team.ru` (testing)
- `general.vertis.yandex-team.ru` (production)

## Sentry
- https://sentry.vertis.yandex.net/verticals/bonsai/