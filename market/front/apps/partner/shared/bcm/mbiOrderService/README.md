# MbiOrderService

http://mbi-order-service.tst.vs.market.yandex.net/swagger-ui/

https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/order-service/order-service-api/src/main/resources/openapi/

https://wiki.yandex-team.ru/mbi/newdesign/components/mbi-order-service/

### pageable

```
Alexander Feoktistov, [15 Oct 2021, 16:58:21]:
Я сейчас заметил хитрую сигнатуру pageable
Мы прям объект должны присылать? pageable={"page":0,"size":0} ?

Olga Didenko, [15 Oct 2021, 16:59:25]:
Нет, это раскрывается в отдельные параметры
http://mbi-order-service.tst.vs.market.yandex.net/returns/?partnerId=1&page=1&size=100
```
