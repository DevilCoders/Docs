
### Вердикты

Информация об ошибках и проверках хранится в поле оффера [offer.resolution](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/DataCampOffer.proto?rev=r9431769#L79), здесь хранятся вердикты [Verdicts](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/errors/Resolution.proto?rev=r8899475#L46) по источникам [offer.resolution.by_source](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/errors/Resolution.proto?rev=r8899475#L27). 

Внутри поля [meta](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/errors/Resolution.proto?rev=r8899475#L49) источник *source* является ключом хранения вердиктов. Ключ источника - [DataSource](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r9452993#L305). Наиболее распространенные источники: 
 * MARKET_IDX - вердикт хранилища, в актуальной сервисной части оффера, проставляется майнером, содержит ошибки и предупреждения от ОХ
 * MARKET_IDX_GENERATION - вердикт от индексатора, в актуальной сервисной части оффера, проставляется, если оффер не попал в индекс из-за конкретной ошибки
 * MARKET_ABO - вердикт от АБО, в базовой части оффера
 * MARKET_MBO - вердикт от МБО, в базовой части оффера
 * MARKET_MDM - вердикт от MDM, может быть в базовой и/или сервисных частях
 * MARKET_ABO_SHOP_SKU - вердикт от АБО, в сервисной части оффера

Для получения вердиктов оффера предназначена ручка строллера [get_verdicts](https://docs.yandex-team.ru/market-datacamp/components/stroller-api#poluchenie-verdiktov-offera-get). Пример [вызова ручки](http://datacamp.white.vs.market.yandex.net/v1/partners/733119/offers/verdicts?show_pictures=true&format=json&offer_id=5746) и [ответа](https://paste.yandex-team.ru/9362908)


### Вердикты и скрытия

Вердикты с флажком [is_banned](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/errors/ValidationResult.proto?rev=r8899475#L24)=true, дополнительно получают в оффере скрытие с таким же источником в [offer.status.disabled](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r9445530#L92). Однако логика проставления скрытий для разных источников может отличаться. 

### Поисковый запрос

Пример поискового запроса вердикта от майнера по коду: [YQL - miner verdict by code](https://yql.yandex-team.ru/Operations/YmlQw1Z1OxRyj8zoqsXcEkh02NK6PnsiVQd9YizpWis=)
