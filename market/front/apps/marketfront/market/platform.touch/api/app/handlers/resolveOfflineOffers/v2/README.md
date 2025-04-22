# Резолвер resolveOfflineOffers

## Описание

Возвращает оффера оффлайн магазинов для заданного productId и координат

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `productId`* | number | id товара | - | - |
| `geoLocation`* | string | гео-координаты пользователя вида `long,lat` | - | - |
| `how` | `aprice|dprice|distance`| сортировка | - | - |
\* - обязательный параметр


## Пример запроса
```sh
curl --request POST \
  --url '<FAPI host>/api/v2?name=resolveOfflineOffers' \
  --header 'content-type: application/json' \
  --data '{
	"params": [{
		"productId": 163584171,
		"geoLocation": "55.73,37.58"
	}]
}'
```
## Пример ответа
```json
{
  "results": [
    {
      "handler": "resolveOfflineOffers",
      "result": "7lz05hrndgj"
    }
  ],
  "collections": {
    "offlineOffersSearchResult": Array(),
    "offlineOffer": Array(),
    "offlineShop": Array(),
    "offlineOutlet": Array()
  }
}
```

## Ссылки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/resolveOfflineOffers/v2/index.js)
- [Описание сущности `offlineOffer` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/offlineOffer/index.js)
