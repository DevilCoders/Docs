# Резолвер resolveFoodtechOrders

## Описание

Резолвер для получения объединенного списка заказов из Еды и Лавки.
### Доступные параметры

Без параметров


- [Описание сущности `foodtechOrder` в проекте](https://github.yandex-team.ru/market/marketfront/blob/master/market/src/entities/foodtechOrder/index.js)

```bash
curl -k 'https://<FAPI_HOST>/api/v1?name=resolveFoodtechOrders' --header 'Content-Type: application/json'   --header 'User-Agent: Beru/2.48 (Android/10; PCT-L29/HONOR)'   --header 'X-App-Version: 2.48'   --header 'X-User-Authorization: OAuth <OAuthToken>'   --header 'api-platform: ANDROID'   --data '{"params": [{"limit": 10, "page": 1, "eatsOffset": 0, "lavkaOffset": 1}]}'
```
