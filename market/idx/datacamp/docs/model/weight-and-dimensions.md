### Весогабариты (ВГХ) в хранилище - размеры, вес товара

* **Партнерские ВГХ**

Партнер может принести ВГХ каждому товару (фидом, по API, через пользовательский интерфейс), эти данные попадают в поля [offer.content.partner.original.dimensions](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r9275916#L581) - размер и [offer.content.partner.original.weight](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r9275916#L571) вес.

После майнинга поля из original переложены в actual - [offer.content.partner.actual.dimensions](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r9275916#L1122) и [offer.content.partner.actual.weight](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r9275916#L1119)

* **Мастер данные - ВГХ от МДМ**

МДМ присылает ВГХ в хранилище - это основной источник данных. См. [интеграция ЕОХ с МДМ](https://docs.yandex-team.ru/market-datacamp/integration/mdm).
Наполняются поля [offer.content.master_data.dimensions](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r9275916#L1260) и [offer.content.master_data.weight_gross](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r9275916#L1263)

* **Размеры с карточки (MSKU) - для DBS** - временное решение

МДМ еще не умеет работать с DBS офферами, при этом партнеры часто не приносят ВГХ, а они нужны, например, для расчета доставки. В проекте [MARKETINDEXER-43658](https://st.yandex-team.ru/MARKETINDEXER-43658) научили майнер подтягивать ВГХ с карточки на оффер, данные попадают в поле [offer.content.master_data.msku_dimensions](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r9275916#L1392) и [offer.content.master_data.msku_weight_gross](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r9275916#L1397)

* **Размеры от УК** - являются ли legacy?

Майнер при походе в УльтраКонтроллер может получить в ответ размеры оффера. Эти размеры попадают в поле [offer.content.market.dimensions](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r9275916#L207).
Эти ВГХ продолжают использоваться как запасные данные во время отправки на индексацию. Нужны ли - неизвестно?

* **Legacy для старых синих - stock_info.weight_and_dimensions** - в процессе удаления на 03.2022

В старом пайплайне обработки синих в офферном хранилище (не едином) майнер использовал таблицу lbdumper в процессоре MasterDataEnricher, чтобы заполнить поле [offer.stock_info.weight_and_dimensions](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferStockInfo.proto?rev=r9004475#L35) - в актуальной сервисной части оффера. Процессор в майнере уже удален, данные weight_and_dimensions более не заполняются, но остаются старыми - в процессе удаления - [MARKETINDEXER-36511](https://st.yandex-team.ru/MARKETINDEXER-36511)

### ВГХ из хранилища в индексатор

Используются разные алгоритмы для передачи ВГХ для FBx/DBS/ADV офферов.
См. в коде в файле [OfferConversions.cpp](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/lib/conversion/OfferConversions.cpp?rev=f7b55b949d2e4452bca38e143165167569a047e4#L1183)

- Для FBx (синих) берем непустые мастер данные от МДМ, иначе размеры от УК.
- Для DBS берем непустые мастер данные от МДМ, иначе msku_dimensions (только если заполнены все поля weight, width, height и length), иначе партнерские ВГХ.
- Для ADV непустые партнерские ВГХ.  

(Актуально на 03.2022, алгоритм часто меняется)
