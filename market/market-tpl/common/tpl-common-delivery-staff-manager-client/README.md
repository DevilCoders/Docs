### Описание

Клиент для market-delivery-staff-manager. Использует авторизацию TVM

### Как использовать
1. Подключить библиотеку к себе в проект. В `ya.make` в секцию `PEERDIR` добавить `market/market-tpl/common/tpl-common-delivery-staff-manager-client`
2. Импортировать спринговый конфиг `ru/yandex/market/tpl/common/dsm/client/MarketDeliveryStaffManagerClientConfiguration.java`
```
@Import(MarketDeliveryStaffManagerClientConfiguration.class)
```
3. Добавить необходимые проперти:
```
external.market-delivery-staff-manager.url
external.market-delivery-staff-manager.tvmServiceId
external.market-delivery-staff-manager.connectTimeoutMillis
external.market-delivery-staff-manager.readTimeoutMillis
external.market-delivery-staff-manager.maxConnTotal
```
4. Заинжектить `ru.yandex.market.tpl.common.dsm.client.api.CourierApi`

