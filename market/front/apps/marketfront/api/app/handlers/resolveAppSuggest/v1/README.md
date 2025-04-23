# Резолвер resolveAppSuggest

## Описание
Резолвер для получения саджеста

\* - обязательный параметр

## Параметры тела запроса
| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| part* | string | строка из формы поиска | - | - |
| highlight* | 1/0 | | - | - |
| count* | integer | | - | - |
| pos | number | позиция курсора | - | - |

## Пример запроса
```
curl --location --request POST 'https://<FAPI_HOST>/api/v1?name=resolveAppSuggest' \
--header 'api-platform: ANDROID' \
--header 'X-Region-id: 213' \
--header 'Content-Type: application/json' \
--data-raw '{
	"params": [{
        "part": "ip",
        "highlight": 1,
        "count": 10
    }]
}'
```

## Полезные ссылки

[Тип Suggest](https://github.yandex-team.ru/market/marketfront/blob/master/src/entities/suggestion/index.js#L141)
