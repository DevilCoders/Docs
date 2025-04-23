# Резолвер resolveRegionById

## Описание

Возвращает информацию о регионе, в частности правильное склонение названия региона

## Параметры

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `regionId`* | number | id региона | - | - |

\* - обязательный параметр

## Пример запроса
```sh
curl --request POST \
  --url '<FAPI host>/api/v2?name=resolveRegionById' \
  --header 'content-type: application/json' \
  --data '{
	"params": [{
		"regionId": 213,
	}]
}'
```

## Пример ответа
```json
{
  "results": [
    {
      "handler": "resolveRegionById",
      "result": 213
    }
  ],
  "collections": {
    "regions": [
      {
        "id": 213,
        "name": "Москва",
        "country": 225,
        "linguistics": {
          "ablative": "",
          "accusative": "Москву",
          "dative": "Москве",
          "directional": "",
          "genitive": "Москвы",
          "instrumental": "Москвой",
          "locative": "",
          "nominative": "Москва",
          "preposition": "в",
          "prepositional": "Москве"
        },
        "data": {
          "zoom": 10,
          "latitude": 55.753215,
          "longitude": 37.622504
        }
      }
    ]
  }
}
```

## Полезные ссылки
- [Описание сущности `region` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/region/index.js)
