# Резолвер resolveActiveBonusesCount

Резолвер для выдачи активных бонусов юзера
Параметров нет

Данные получаются отсюда
http://market-loyalty.tst.vs.market.yandex.net:35815/swagger-ui.html@self/platform/coins-controller/getCoinsCountForPersonUsingGET

## Пример запроса

```
curl --location --request POST 'https://<FAPI_URL>/api/v1?name=resolveActiveBonusesCount' \
--data-raw '{
	"params": [{}]
}'
```

## Пример успешного ответа

```json
{
    "results": [
        {
            "handler": "resolveActiveBonusesCount",
            "result": {
                "total": 0
            }
        }
    ],
    "collections": {}
}
```

## Пример ответа с ошибкой

```json
{
    "error": {
        "kind": "FrontApiAuthError",
        "message": "There is no auth data"
    }
}
```
