# Резолвер resolveEatsActualizedCart

## Описание

Резолвер, балково актуализирующий данные из Еды по магазинам. Не более 10 магизнов за раз, все остальные игнорируются.
### Доступные параметры



```bash
curl -k 'https://<FAPI_HOST>/api/v1?name=resolveEatsActualizedCart' --header 'Content-Type: application/json'   --header 'User-Agent: Beru/2.48 (Android/10; PCT-L29/HONOR)'   --header 'X-App-Version: 2.48'   --header 'X-User-Authorization: Guest'   --header 'api-platform: ANDROID'   --data '{"params": [{"shopId": 1234, {"data": [{"items": [{"count": 1, "feedOfferId": "2323232"}]}]}}]}'
```
