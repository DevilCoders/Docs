## Календарь промо
Основное описание проекта [Календарь промо для поставщиков](https://wiki.yandex-team.ru/users/akustareva/Kalendar-promo-dlja-postavshhikov-v-PI/).
Дополнительное описание [Календарь промо для поставщиков](https://wiki.yandex-team.ru/users/elena-dolgova/kalendar-promo-dlja-postavshhikov-v-pi-2.0/).

## Алгоритм работы со стороны хранилища
1. Сканнер каждую минуту проверяет не появилась ли новая таблица в `//home/market/production/mbi/promo/potential_assortment`. Проверяет по таймстампу в названии таблицы. Как только появляется новая, он обновляет стейт ОХ на основании значений из нее. Обновление происходит для каждого оффера по следующим правилам:
    1. В таблице `potential_assortment` есть акция, которой нет в ОХ - она добавляется
    2. В таблице `potential_assortment` нет акции, которая есть в хранилище - она удаляется (включая активные)
    3. В таблице `potential_assortment` есть акция, которая есть в хранилище - обновляем информацию о ней
2. Если в оффере заполнены все [необходимые поля для отправки в SaaS](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/saas_docs/document.cpp?rev=r7842655#L320-355) оффер отправляется в SaaS прямо из сканнера, если же промо акции были удалены из оффера, то оффер удаляется из SaaS.
3. Повторяем пункт 2, но уже в пайпере, так как у оффера могли заполниться необходимые для SaaS поля

То же самое выполняется для белых DBS офферов, акции берем из таблицы `//home/market/production/mbi/promo/potential_assortment_white`. Для белых в качестве имени используется имя оффера name вместо product_name.

Активация/декативация акций происходит через топик /mbi/prod/supplier-promo-offer. Можно [погрепать](https://yql.yandex-team.ru/Operations/Yd2oalZ1OyS7-NZqcma4L7mj9GwwGEom_XbiIAuoRIw=) историю изменения акций оффера.
В топик пишется любое изменение по офферам в акциях:
1. при добавлении акции она первый раз появится в списке anaplan_promos.active_promos или partner_promos или partner_cashback_promos (в зависимости от того, что за промка)
2. если оффер как-то меняется в других акциях, а акция не меняется, то она просто будет продолжать оставаться в списке
3. при удалении оффера из акции будет запись по офферу, в которой этой акции не будет (чтобы посмотреть время удаления нужно брать первую запись, в которой акции уже не было)

## SaaS
Для календаря промо используется отдельный сервис SaaS `market_datacamp_shop`, в качестве `kps` используется `shop_id`, а в качестве урла документа `s/{shop_id}/{offer_id}`.

Поисковый балансер для тестинга: `http://prestable-market-idx.saas.yandex.net:80`, для прода — `http://stable-market-idx.saas.yandex.net:80/`.

## Атрибуты/литералы
### Поисковые литералы
- `s_doc_type` — тип документа, всегда `offer`
- `s_offer_id` — идентификатор оффера
- `s_promo_id` — идентификаторы анаплановских акций, в которых оффер потенциально может принять участие, значение из [offer.promos.anaplan_promos.all_promos.promos](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferPromos.proto?blame=true&rev=r7535207#L108)
- `s_active_promo_id` — идентификаторы активных анаплановских акций, в которых товар принимает участие, значение из [offer.promos.anaplan_promos.active_promos.promos](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferPromos.proto?blame=true&rev=r7535207#L107), а также идентификаторы акций, инициированных самими партнерами, значение из [offer.promos.partner_promos.promos](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferPromos.proto?rev=r8599846#L134)
- `s_partner_cashback_promo_id` — идентификаторы партнерских кэш-бэк акций на товаре, значения из [offer.promos.partner_cashback_promos.promos](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferPromos.proto?rev=b052aa90856dee0a7c73b60ab0a28d9a90a14509#L137)
- `s_market_category_id` — идентификатор маркетной категории, к которой принадлежит товар, значение из [offer.content.market.category_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L196)
- `s_market_vendor_id` — идентификатор производителя товара, значение из [offer.content.market.vendor_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L203)

#### Список зон для полнотекстового поиска
- `z_offer_id` - идентификатор оффера
- `z_title` — заголовок карточки товара, значение из [offer.content.market.product_name](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L214)

### Группировочные атрибуты:
- `promo_id` — идентификаторы потенциальных акций, в которых можно принять участие, значение из [offer.promos.anaplan_promos.all_promos.promos](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferPromos.proto?blame=true&rev=r7535207#L108)
- `active_promo_id` — идентификаторы активных акций, в которых товар принимает участие, значение из [offer.promos.anaplan_promos.active_promos.promos](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferPromos.proto?blame=true&rev=r7535207#L107), а также идентификаторы акций, инициированных самими партнерами, значение из [offer.promos.partner_promos.promos](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferPromos.proto?rev=r8599846#L134)
- `market_category_id` — идентификатор маркетной категории, к которой принадлежит товар, значение из [offer.content.market.category_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L196)
- `market_vendor_id` — идентификатор производителя товара, значение из [offer.content.market.vendor_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L203)

### Свойства документов
- `doc_type` — тип документа, всегда `offer`
- `offer_id` — идентификатор оффера
- `promo_id` — идентификаторы потенциальных акций, в которых можно принять участие, значение из [offer.promos.anaplan_promos.all_promos.promos](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferPromos.proto?blame=true&rev=r7535207#L108)
- `active_promo_id` — идентификаторы активных акций, в которых товар принимает участие, значение из [offer.promos.anaplan_promos.active_promos.promos](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferPromos.proto?blame=true&rev=r7535207#L107), а также идентификаторы акций, инициированных самими партнерами, значение из [offer.promos.partner_promos.promos](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferPromos.proto?rev=r8599846#L134)
- `partner_cashback_promo_id` — идентификаторы партнерских кэш-бэк акций на товаре, значения из [offer.promos.partner_cashback_promos.promos](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferPromos.proto?rev=b052aa90856dee0a7c73b60ab0a28d9a90a14509#L137)
- `market_category_id` — идентификатор маркетной категории, к которой принадлежит товар, значение из [offer.content.market.category_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L196)
- `market_vendor_id` — идентификатор производителя товара, значение из [offer.content.market.vendor_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7830917#L203)
- `ru_price` — цена товара


## Примеры запросов в saas

### Текстовый поиск
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&hr=da&kps=13&text=iphone
```

### Текстовый поиск только по title
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&hr=da&kps=13&text=z_title:iphone
```

### Префиксный поиск по offer_id
Например хотим делать объектный саджест по началу offer_id
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&hr=da&kps=10263850&wizextra=usewildcards%3Dda&text=s_doc_type:%22offer%22+z_offer_id:%22test*%22
```

### Получить список акций для магазина
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&kps=10265867&text=s_doc_type:"offer"&g=2.promo_id.100.0.....rlv.0.&g=2.active_promo_id.100.0.....rlv.0.&hr=json
```

### Получить потенциальные оффера для акции для магазина с 11ый по 20ый оффер (к запросу добавляется p=1 , нумерация страниц с нуля)
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&kps=10265867&text=s_doc_type:"offer"+s_promo_id:"%232534"&gta=offer_id&hr=json&numdoc=10&p=1
```

### Получить потенциальные оффера для акции для магазина с 11ый по 20ый оффер, из конкретной категории FOO, конкретного бренда BAR и с поисковой строкой BAZ(название оффера полонстью/частично или shopsku)
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&kps=10265867&text=s_doc_type:"offer"+s_promo_id:"%232534"+s_market_category_id:"12699910"+s_market_vendor_id:"10715868"+z_title:"Kitekat"&gta=offer_id&hr=json&numdoc=10&p=0
```

### Получить список офферов участвующих в акции Х
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&kps=10265867&text=s_doc_type:"offer"+s_active_promo_id:"%232363"&gta=offer_id&hr=json
```

### Получить список офферов подходящих, но не участвующих в активной акции Y
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&kps=10265867&text=s_doc_type:"offer"+s_promo_id:"%232363"&gta=offer_id&hr=json
```

### Получить список брендов имеющихся у магазина, которые подходят для акции
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&kps=10265867&text=s_doc_type:"offer"+s_promo_id:"%232363"&g=2.market_vendor_id.100.0.....rlv.0.&hr=json
```

### Получить список категорий имеющихся у магазина, которые подходят для акции
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&kps=10265867&text=s_doc_type:"offer"+s_promo_id:"%232363"&g=2.market_category_id.100.0.....rlv.0.&hr=json
```

### Текстовый поиск с фильтром по категориии ([добавляется](https://wiki.yandex-team.ru/jandekspoisk/saas/GroupAttrs/) параметр fa)
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&hr=da&kps=13&text=iphone&fa=market_category_id:1000
```

### Оффер по идентификатору (поисковый литерал s_offer_id)
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&hr=da&kps=13&text=s_offer_id:bbbb
```

### Сортировка выдачи по mtime
За сортировку отвечает параметр ``how``. Сортировать по времени модификации ``how=tm``, так же
можно сортировать по значению целочисленного группировочного атрибута.
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&hr=da&kps=13&text=iphone&how=tm
```

### Сортировка в обратном порядке
Добавляем cgi параметр ``asc=da``
```http request
http://prestable-market-idx.saas.yandex.net/market_datacamp_shop?ms=proto&hr=da&kps=13&text=iphone&how=tm&asc=da
```

### Пагинация выдачи
- `&numdoc=N` задает максимального количество документов в ответе
- `&p=X` задает номер страницы, нумерация идет с нуля

## Troubleshooting

В promo-saas не появилась информация об акциях.
- контроллеры во время отправки в promo-saas завершились по OOM или crash (дедупликация не позволит отправить ранее обновленные документы);
- мы допустили ошибку в реализации подписки (забыли поле в разметке, или допутили ошибку в [коде](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/saas_docs/document.cpp?blame=true&rev=r8268697#L328) формирования документа).

Можно принудительно отправить документы на индексацию (пример в [тикете](https://st.yandex-team.ru/MARKETINDEXER-39993)):
```
curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/send_to_subscriber?business_id=924574&subscriber=PROMO_SAAS_SUBSCRIBER"
```
