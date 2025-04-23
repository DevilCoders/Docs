## Резолвер resolveRedirectSearch

Ручка получения параметров редиректа для репорта
Данные в ответе резолвера нормализованы.


## Параметры из тела запроса

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `text`* | string | Поисковый запрос пользователя | - | - |
| `page`** | number |  Номер страницы | 1 | - |
| `hid`* | number| Идентификатор товарного дерева | - | - |

\* - обязательно наличие хотя бы одного параметра

\** - обязательный параметр

## Пример запроса


```text
curl --location --request POST 'https://front-blue-unified--bluemarket-12562-prestableapi.demofslb.beru.ru/api/v1?name=resolveRedirectSearch' \
--header 'api-platform: ANDROID' \
--data-raw '{
	"params": [{
		"page": 2,
        "adult": 1,
		"numdoc": 2,
		"text": "iphone X",
        "billingZone": "default",
		"fapiParams": {
			"cartSnapshot": []
		}
	}]
}'
```


## Пример ответа

```json
{
    "results": [
        {
            "handler": "resolveRedirectSearch",
            "result": {
                "params": {
                    "text": [
                        "iphone X"
                    ],
                    "hid": [
                        "91491"
                    ],
                    "rt": [
                        "9"
                    ],
                    "nid": [
                        "54726"
                    ],
                    "slug": [
                        "mobilnye-telefony"
                    ],
                    "was_redir": [
                        "1"
                    ],
                    "srnum": [
                        "16"
                    ],
                    "rs": [
                        "eJwzYgpgBAABcwCG"
                    ]
                },
                "target": "search"
            }
        }
    ],
    "collections": {}
}
```

## Полезные ссылки
[Все параметры репорта](https://wiki.yandex-team.ru/Market/Verstka/report-query-params/)
[Price drop](https://wiki.yandex-team.ru/users/realtim/PriceDrop/LimitedEdition/)
