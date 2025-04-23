# Резолвер deleteItemsFromEatsCart

## Описание

Резолвер, удаляющий офферы еды из корзины
### Доступные параметры

| Parameter                | Type    | Description                                     | Default | Value |
|--------------------------|---------|-------------------------------------------------|------------------| ------- |
| `shopId`*                  | string  | ид магазина                        | - | - |
| `offerIds`*                  | string[] | список публичные ид офферов еды (feed.offerId)                 | - | - |
| `orderId`*                  | string | из заказа еды                 | - | - |



```bash
curl -k 'https://<FAPI_HOST>/api/v1?name=deleteItemsFromEatsCartByFeedOfferId'
--header 'Content-Type: application/json'
--header 'User-Agent: Beru/2.48 (Android/10; PCT-L29/HONOR)'
--header 'X-App-Version: 2.48'
--header 'X-User-Authorization: OAuth <OAuthToken>'
--header 'api-platform: ANDROID'
--data '{"params": [{shopId: "1233", offerIds: ["1234", "56565"], orderId: "12345-454456"}]}'
```
