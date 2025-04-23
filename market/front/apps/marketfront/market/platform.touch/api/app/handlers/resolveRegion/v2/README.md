# Резолвер resolveRegion

## Описание

Возвращает информацию о регионе, в частности правильное склонение названия региона

## Параметры

Без параметров


## Пример запроса
```sh
curl --request POST \
  --url '<FAPI host>/api/v2?name=resolveRegion' \
  --header 'content-type: application/json' \
  --data '{
	"params": [{}]
}'
```

## Пример ответа
```json
{
  "results": [
    {
      "handler": "resolveRegion",
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
