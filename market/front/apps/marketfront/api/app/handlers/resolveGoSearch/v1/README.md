# Резолвер resolveGoSearch

Возвращает список экспресс-товаров по категории

## Пример запроса

```
curl --request POST \
  --url 'https://<FAPI_HOST>/api/v1?name=resolveGoSearch&dictionary=1&gps=37.541305%2C55.756761' \
  --header 'Authorization: OAuth ...' \
  --header 'Content-Type: application/json' \
  --header 'api-platform: ANDROID' \
  --data '{
	"params": [ { "nid": 23282330 } ]
}'
```

## Пример ответа

https://paste.yandex-team.ru/7286388
