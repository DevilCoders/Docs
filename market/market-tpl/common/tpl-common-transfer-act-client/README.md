### Описание

Клиент для market-transfer-act. Использует авторизацию TVM

### Как использовать
1. Подключить библиотеку к себе в проект. В `ya.make` в секцию `PEERDIR` добавить `market/market-tpl/common/tpl-common-transfer-act-client`
2. Импортировать спринговый конфиг `ru/yandex/market/tpl/common/transferact/client/MarketTransferActClientConfiguration.java`
```
@Import(MarketTransferActClientConfiguration.class)
```
3. Добавить необходимые проперти:
```
external.market-transfer-act.url
external.market-transfer-act.tvmServiceId
external.market-transfer-act.connectTimeoutMillis
external.market-transfer-act.readTimeoutMillis
external.market-transfer-act.maxConnTotal
```
4. Заинжектить `ru.yandex.market.tpl.common.transferact.client.api.TransferApi` или `ru.yandex.market.tpl.common.transferact.client.api.SignatureApi`

