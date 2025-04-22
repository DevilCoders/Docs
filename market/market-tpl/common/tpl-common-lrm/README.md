### Описание

Клиент для LRM. Использует авторизацию TVM

### Как использовать
1. Подключить библиотеку к себе в проект. В `ya.make` в секцию `PEERDIR` добавить `market/market-tpl/common/tpl-common-lrm`
2. Импортировать спринговый конфиг `ru/yandex/market/tpl/common/lrm/client/LrmClientConfiguration.java`
```
@Import(LrmClientConfiguration.class)
```
3. Добавить необходимые проперти:
```
external.lrm.returns.url
external.lrm.returns.tvmServiceId
external.lrm.returns.connectTimeoutMillis
external.lrm.returns.readTimeoutMillis
external.lrm.returns.maxConnTotal
```
4. Заинжектить `ru/yandex/market/tpl/common/lrm/client/api/ReturnsApi.java`

