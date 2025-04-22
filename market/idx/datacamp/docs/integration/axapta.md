
**1P (Axapta)** - это схема взаимодействия Яндекс Маркета с поставщиками, при которой компания самостоятельного закупает и перепродает товары на маркетплейсе (бывший БЕРУ).

* [Поддержка Аксапты](https://wiki.yandex-team.ru/market/pokupka/streamline/erp/sox/support/)
* [Про 1Р-процессы](https://wiki.yandex-team.ru/market/pokupka/streamline/erp/1Pprocesses/)

Все товары 1Р под одним business_id & shop_id:

* **prod** business_id = 924574, shop_id=465852
* **testing** business_id 10447296, shop_id=10264169

[yql - кол-во 1Р офферов в проде](https://yql.yandex-team.ru/Operations/YY1J8gB_AnHA_Vd7c-zXmveENY68HUDdQm9R7PGy334=)
[yql - кол-во 1Р офферов в тестинге](https://yql.yandex-team.ru/Operations/Yi8LTbq3k6WwmKuSVeD1sTNMOE7t3EkL-4d-o9uceFQ=)

В коде хранилища для проверки, относится ли оффер к 1Р, можно использовать функцию [IsFirstPartyBusiness](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/lib/proto_helpers/datacamp_offer.h#L567).

**Взаимодействие ЕОХ-Axapta (новое на 2022-02):**
 * Офферы из Axapta выгружаются в Excel файлы, передаются КИ
 * КИ создает офферы передает данные в ЕОХ топиком **offers-1p-new-and-updates** [test](https://lb.yandex-team.ru/logbroker/accounts/market-mbo/test/datacamp/offers-1p-new-and-updates), [prod](https://lb.yandex-team.ru/logbroker/accounts/market-mbo/prod/datacamp/offers-1p-new-and-updates), [yql-logfeller](https://yql.yandex-team.ru/Operations/YjHeGpfFtyRa95_Lj3MrGHQ-1M-7tFcoEIVCWxBJOAM=)
 * Хранилище создает офферы (отличительное свойство meta.rgb = BLUE, partner_info.supplier_type = 1). Офферы майнятся United Miner-ом, уходят в МДМ и получают мастер-данные как обычные синие.
 * Цены и стоки для офферов приходят от Axapta топиком **mbi/*/market-quick** [test](http://lb.yandex-team.ru/logbroker/accounts/mbi/test/market-quick), [prod](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/market-quick), пример поиска по логфеллеру: [yql](https://yql.yandex-team.ru/Operations/YfAUEC3DcFR7pk1Xsvbz8jvoUiHR-hedD4VO2Pw7010)
 * Офферы обычным путем попадают в выгрузку blue_out и затем в индекс

