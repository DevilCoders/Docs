# Datacamp API

* Балансер тестинга: [datacamp.white.tst.vs.market.yandex.net:80](http://datacamp.white.tst.vs.market.yandex.net)
* Балансер production: [datacamp.white.vs.market.yandex.net:80](http://datacamp.white.vs.market.yandex.net)

## TVM
В хранилище включена [tvm аутентификация](https://wiki.yandex-team.ru/passport/tvm2/).
Все запросы должны содержать TVM_TICKET в хедере ```X-Ya-Service-Ticket```

На момент активной разработки мы разрешили все read запросы без TVM аутентификации, но в будущем мы уберем эту возможность и обяжем всех ходить с TVM тикетами.

Есть библиотеки на большинстве ЯП, которые позволяют сгенерить TVM тикет, но если вдруг для дебага нужно выполнить запрос без сторонних библиотек, то TVM тикет можно сгенерить с помощью ```ya tool tvmknife```,
указав, от какого сервиса и в какой необходимо сгенерить тикет. Более подробно про дебаг можно почитать [тут](https://wiki.yandex-team.ru/passport/tvm2/debug/).

Пример, как сгенерить TVM_TICKET для похода в тестовый белый датакемп:
- Выбираем [DATACAMP_TVM_CLIENT_ID](https://fcs.yandex-team.ru/#!DATACAMP_TVM_CLIENT_ID,market%2Fidx%2Fdatacamp%2Fcontrollers%2Fetc%2Fenv%2F.*united,jm,arcadia,loadtest,5000) для тестинга — 2002296, production — 2016907
- Выполняем команду для тестинга
```bash
export TVM_TICKET=`ya vault get version sec-01dsfcej668h548vxvxgh8vw41 -o tvm | ya tool tvmknife get_service_ticket client_credentials -d 2002296 -s 2002296`
```
для прода
```bash
export TVM_TICKET=`ya vault get version sec-01dsfcm45eskn30121gqrb99zq -o tvm | ya tool tvmknife get_service_ticket client_credentials -d 2016907 -s 2016907`
```
- Затем с помощью этого тикета можно сходить в строллер и что-нибудь изменить
```bash
curl -XPUT --header "Content-Type: application/json" --header "X-Ya-Service-Ticket: $TVM_TICKET" 'http://datacamp.white.tst.vs.market.yandex.net/shops/10369797/offers/price?offer_id=generatedOffer1&whid=145' --data '
{
  "offer": [
    {
      "price": {
        "basic": {
          "binary_price": {
            "id": "RUR",
            "price": 430000000
          },
          "meta": {
            "source": 3,
            "timestamp": {
              "seconds": 1583496596
            }
          },
          "vat": 7
        }
      }
    }
  ]
}'
```

## Заполнение JSON вместо proto в теле запроса
По умолчанию в теле запроса ручки принимают сериализованный протобуф, если не указано обратное.
В таких запросах есть возможность отправить JSON вместо сериализованного protobuf.

**В production процессе стоит использовать protobuf, а такая возможность оставлена скорее для дебажных целей.**

NB: элементы мапы передаются в виде списка
```
{key_1: val_1, key_2: val_2} => [{"key": key_1, "value": val_1}, {"key": key_2, "value": val_2}]
```

Обобщенный пример:
```bash
curl -XPOST --header "Content-Type: application/json" --data "<json_content>" <handler_path>
```

Пример обновления базового оффера:
```bash
curl -XPOST --header "Content-Type: application/json" --header "X-Ya-Service-Ticket: <tvm-ticket>" "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers/basic?offer_id=dkhavgwdjbka2&format=json" --data '
{
  "identifiers": {
    "shop_id": 10435984
  },
  "content": {
    "partner": {
      "original": {
        "name": {
          "meta": {
            "timestamp": {
              "seconds": 1596467799
            }
          },
          "value": "New name"
        }
      }
    }
  }
}'
```

## Шейпинг ответа { #shaping }

Возвращаемый ответ можно шейпить с помощью параметра `query`, который принимает GraphQl-style запросы

#### Синтаксис запросов

* Получение поля field: ` {field} `

* Если field - сообщение, то можно получить его подполя: ` {field {sub_field1, sub_field2}} `

* Если field - repeated сообщение, то такой запрос применится ко всем элементам сообщения

* Если field - map, то такой запрос применится ко всем значениям в мапе

* Для синтаксически некорректных или для запросов, поля которых отсутсвуют в схеме, вернется полное сообщение

* Запрос обязательно должен быть обернут в {}, иначе он считается некорректным

* Если все неинициализированные поля сообщения из запроса присутсвуют в схеме, то запрос считается корректным и возврщаются только инициализированные поля

## ping
```
GET /ping
```

## Получение базового оффера
```
GET /v1/partners/<business_id>/offers/basic?offer_id=<offer_id>
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id  | int, required | идентификатор партнера
offer_id | string, required  | идентификатор оффера
format | string, optional, default=protobuf | формат ответа json или protobuf

#### Ответ
Возвращает один оффер внутри [GetOffersResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetOffer.proto?rev=7089548#L26).

В случае, если оффер не существует, возвращает пустой результат.

#### Пример
```bash
curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers/basic?offer_id=1621011&format=json"
{
    "offers": [
        {
            "identifiers": {
                "business_id": "<business_id",
                "offer_id": "<offer_id>"
            }
        }
    ]
}
```

## Создание либо обновление базового оффера
```
POST /v1/partners/<business_id>/offers/basic?offer_id=<offer_id>
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id  | int, required | идентификатор партнера
offer_id | string, required  | идентификатор оффера
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | [Offer](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/DataCampOffer.proto?rev=r7766594#L41) | содержимое оффера в прото формате

#### Ответ
Возвращает получившийся в результате мерджа [Offer](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/DataCampOffer.proto?rev=r7766594#L41).

#### Пример
```bash
curl -XPOST "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers/basic?offer_id=1621011&format=json" --data-binary "@body.proto"
{
  "identifiers": {
    "business_id": 10432691,
    "offer_id": "1621011"
  }
}
```


## Удаление базового оффера
```
POST /v1/partners/<business_id>/offers/basic/remove?offer_id=<offer_id>&offer_id=<offer_id>
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id  | int, required | идентификатор партнера
offer_id | string, optional  | идентификатор оффера
force | bool, optional, default=false | безусловно выполнить удаление офферов
format | string, optional, default=protobuf | формат ответа json или protobuf
опциональное тело запроса | [DeleteOfferRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?rev=r8916334#L91) | список идентификаторов офферов

#### Ответ
Возвращает [DeleteOfferResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?rev=8179553&blame=true#L91).

#### Пример
```bash
curl -XPOST "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers/basic/remove?offer_id=1621011&format=json"
```

#### JFYI
Удаляется весь united-оффер, включая все сервисные и складские (актуальные) части. Если у оффера есть сток на каком-либо из fulfillment складов, то оффер удалить можно только в force-режиме.

## Получение сервисного оффера
```
GET /v1/partners/<business_id>/offers/services/<service_id>?offer_id=<offer_id>
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор партнера
offer_id | string, optional | идентификатор оффера
shop_id | int, required | идентификатор сервиса/магазина
format | string, optional, default=protobuf | формат ответа json или protobuf

#### Ответ
Возвращает один оффер внутри [GetOffersResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetOffer.proto?rev=7089548#L26).

В случае, если оффер не существует, возвращает пустой результат.

#### Пример
```bash
curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers/services/10435984?offer_id=1621011&format=json"
{
    "offers": [
        {
            "identifiers": {
                "business_id": "<business_id",
                "offer_id": "<offer_id>",
                "shop_id": "<shop_id>"
            }
        }
    ]
}
```

## Создание либо обновление сервисного оффера
```
POST /v1/partners/<business_id>/offers/services/{service_id}?offer_id=<offer_id>
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id  | int, required | идентификатор партнера
offer_id | string, required  | идентификатор оффера
shop_id | int, required | идентификатор сервиса/магазина
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | [Offer](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/DataCampOffer.proto?rev=r7766594#L41) | содержимое оффера в прото формате

#### Ответ
Возвращает получившийся в результате мерджа [Offer](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/DataCampOffer.proto?rev=r7766594#L41).

#### Пример
```bash
curl -XPOST "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers/services/10293108?offer_id=1621011&format=json" --data-binary "@body.proto"
{
  "identifiers": {
    "business_id": 10432691,
    "offer_id": "1621011",
    "shop_id": 10293108
  }
}
```


## Удаление сервисного оффера
```
POST /v1/partners/<business_id>/offers/services/{service_id}/remove?offer_id=<offer_id>&offer_id=<offer_id>
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id  | int, required | идентификатор партнера
offer_id | string, required  | идентификатор оффера
shop_id | int, required | идентификатор сервиса/магазина
force | bool, optional, default=false | безусловно выполнить удаление офферов
format | string, optional, default=protobuf | формат ответа json или protobuf
опциональное тело запроса | [DeleteOfferRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?rev=r8916334#L91) | список идентификаторов офферов

#### Ответ
Возвращает [DeleteOfferResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?rev=8179553&blame=true#L91).

#### Пример
```bash
curl -XPOST "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers/services/10293108/remove?offer_id=1621011&format=json"
```

#### JFYI
Удаляется сервисная часть united-оффер, включая все складские (актуальные) части. Если у оффера есть сток на каком-либо
из fulfillment складов, то оффер удалить можно только в force-режиме.

## Получение цельного оффера/офферов магазина
```
GET /shops/<shop_id>/offers?offer_id=<offer_id>[&supplemental_id=<supplemental_id>|warehouse_id=<warehouse_id>|whid=<whid>]
```
Возвращает оффер, склеенный из базового, сервисного, актуального сервисного офферов и стоков. Можно передать идентификаторы оффера в теле запроса.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
shop_id | int, required | идентификатор магазина
offer_id | string, optional | идентификатор оффера
warehouse_id, whid, supplemental_id | int, optional | идентификатор склада партнера
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | [ChangeOfferRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?rev=r7942439#L18) | идентификаторы для батчегового запроса офферов.

#### Ответ
Возвращает [GetOfferResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetOffer.proto?rev=7942439&blame=true#L24) при запросе через cgi параметры, при заполненном теле запроса возвращает [FullOfferResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?blame=true&rev=r7942439#L49).

#### Пример
```bash
curl 'http://datacamp.white.tst.vs.market.yandex.net/shops/10264169/offers?offer_id=000002.4003583191017&whid=145&format=json'
{
  "offer": {
    "identifiers": {
      "business_id": 10447296,
      "extra": {
        "classifier_good_id": "9fd941d56215d47067ed1d0aa821ddf9",
        "classifier_magic_id2": "700199a1d207d6563a9025b590488f8d",
        "recent_business_id": 10447296,
        "recent_feed_id": 200344511,
        "recent_warehouse_id": 145,
        "shop_sku": "000002.4003583191017",
        "ware_md5": "lspB2mDm7_e62RjGXjfAUg"
      },
      "feed_id": 200344511,
      "offer_id": "000002.4003583191017",
      "shop_id": 10264169,
      "warehouse_id": 145
    }
  }
}
```


## Листинг офферов с фильтрами { #list-offers-with-filters }
```
GET /v1/partners/<business_id>/offers
```
#### Параметры

##### Общие параметры
Имя | Тип | Описание
:--- | :--- | :---
format | string, optional, default=protobuf | формат ответа json или protobuf
search_tables | bool, optional | активирует выполнение запроса по поисковым таблицам (целевая схема)
query | string, optional | [шейпинг ответа](#shaping)

##### Фильтры
Имя | Тип | Описание
:--- | :--- | :---
offer_id | string, repeated | идентификаторы офферов
allow_removed | bool, optional, default=false | включать удалённые оффера в поиск
verdict | int, repeated | фильтр по наличию вердикта в базовой, сервисной или акт.сервисных частях оффера. Значением нужно передать ui32 хеш, который соответствует колонке hash из таблицы verdicts [prod](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/united/routines/verdicts/recent), [testing](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/testing/indexer/datacamp/united/routines/verdicts/recent). Пример: verdict=2418511978&verdict=2430411283

##### Фильтры по базовой части оффера
Имя | Тип | Описание
:--- | :--- | :---
vendor | string, repeated | фильтр по производителю из original части оффера
category_id | int, repeated | фильтр по партнерской категории оффера, включая родительские категории
market_category_id | int, repeated | фильтр по категории из [маркетной привязки](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMapping.proto?rev=r8174042#L38), только листовые значения
cpa | int, repeated | **deprecated**
allow_model_create_update | bool, optional | фильтр по признаку редактируемости PSKU, использует значение из [ContentSystemStatus](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/ContentStatus.proto?rev=8494358&blame=true#L53)
integral_content_status | int, repeated | фильтр по интегральному контентному статусу, использует значение из [CardStatus](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/ContentStatus.proto?rev=r8837370#L186)
ts_first_added_from | int, optional | фильтр по дате создания оффера, использует значение [ts_first_added](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r9355372#L37), от указанной даты
ts_first_added_to | int, optional | фильтр по дате создания оффера, использует значение [ts_first_added](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r9355372#L37), до указанной даты

##### Фильтры по сервисной части оффера
Имя | Тип | Описание
:--- | :--- | :---
shop_id | int, optional | идентификатор сервиса/магазина, опциональный целочисленный параметр. В фильтрации и ответе будут использованы только те оффера, которые размещаются в данном магазине
disabled_by | int, repeated | источник скрытия, использует значение [DataSource](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r7729581#L139-164)
partner_status | int, repeated | партнерский статус публикации, значение [SummaryPublicationStatus](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r7729581#L164-184)
supply_plan | int, repeated | планы по поставкам, значение [SupplyPlan::Variation](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?blame=true&rev=r7742904#L571-577)
result_status | int, repeated | интегральный статус, учитывает разные типы скрытий и статус индексации, использование этого фильтра возможно только при запросах на уровне магазина, значение [ResultStatus](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r7921117#L112-138)
has_price | bool, optional | наличию либо отсутствию цены оффера

##### Фильтры по актуальной сервисной (складской) части оффера
Имя | Тип | Описание
:--- | :--- | :---
warehouse_id | int, optional | идентификатор склада, офферам которого применять фильтры
has_market_stocks | bool, optional | наличие либо отсутствие товара на складе

Вместе с фильтами по складской части возможно использование только фильтров по сервисной части (за исключением интегрального статуса)

##### Фильтры на основе всех оригинальных сервисных частей партнера
Имеют смысл, только если параметр `shop_id` **НЕ** задан. Запрос на уровне бизнеса.
Имя | Тип | Описание
:--- | :--- | :---
include_shop_id | int, repeated | возвращаем оффера, представленные хотя бы в одной из указанных услуг
exclude_shop_id | int, repeated | возвращаем оффера, не представленные ни в одной из указанных услуг

##### Параметры пагинации и возвращаемого ответа
Ручка поддерживает пагинацию через числовой оффсет (не рекомендуется к использованию, не эффективно) либо через оффсет относительно `offer_id`. Однако нельзя в одном запросе использовать `offset` и `position`.
Имя | Тип | Описание
:--- | :--- | :---
offset | int, optional, default=0 | **deprecated** количественный сдвиг среди всех офферов, которые подходят под фильтры
limit | int, optional, default=10 | количество офферов в ответе, опциональный целочисленный параметр, дефолтное значение 10
scan_limit | int, optional, default=0 | количество офферов, которое будет сканировано в поисках офферов, удовлетворяющим фильтрам, можно использовать совместно с limit, опциональный целочисленный параметр, дефолтное значение 0, рекомендованное 10000, имеет смысл только при использовании фильтра по интегральному статусу
position | string, optional | нижняя граница для offer_id (включительно) используется для относительной пагинации
return_shop_id | int, optional | shop_id услуги, сервисные части которой нужно вернуть (остальные сервисные части не возвращаются)
full | bool, optional | признак возвращения полного united-оффера (с заполнением поля actual)
only_basic | bool, optional, default=false | признак возвращения только базовой части оффера. Нельзя в одном запросе использовать `only_basic=true&full=true`. Также `only_basic=true` нельзя использовать с фильтрами по сервисной и актуальной сервисной частям.

#### Формат ответа
Возвращает [GetUnitedOffersResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetOffer.proto?rev=r7748351#L32-41).
* response.limit — подставляется значения из запроса
* response.offset — подставляется значение из запроса
* response.total — **deprecated**
* response.offers — список офферов с базовой и сервисными частями, орсортированы по возрастанию `offer_id`
* response.current_page_position — подствляется значение из запроса при пагинации через `position`
* response.previous_page_position — позиция предыдущей страницы при позиционной пагинации
* response.next_page_position — позиция следующей страницы при позиционной пагинации

#### Шейпинг ответа

``` bash
curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers?query={limit, offers{basic, service}}&format=json"

{
    "limit": 10,
    "offers": [
        {"basic": {...}, "service": [{"key": 10435984, "value": {...}}]},
        {"basic": {...}, "service": [{"key": 10407624, "value": {...}}]},
        ...
    ]
}
```

#### Примеры запросов

* Получить только базовые и сервисные части оферов
```bash
GET /v1/partners/<business_id>/offers?query={offers {basic, service}}
```

* Получить все id промок из сервисной части
```bash
GET /v1/partners/<business_id>/offers?query={offers {service {promos {promo {id}}}}}
```

* Для каждого склада получить список его shop_id
```bash
GET /v1/partners/<business_id>/offers?query={offers {actual {warehouse {identifiers {shop_id}}}}}
```

#### Пример
```bash
# Получить офферы партнера 10432691
curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers?format=json"
{
    "limit": 10,
    "offset": 0,
    "total": 16,
    "offers": [
        {"basic": {...}, "service": [{"key": 10435984, "value": {...}}]},
        {"basic": {...}, "service": [{"key": 10407624, "value": {...}}]},
        ...
    ]
}

# Получить офферы со второй страницу
curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers?format=json&offset=10"
{
    "limit": 10,
    "offset": 10,
    "total": 16,
    "offers": [
        {"basic": {...}, "service": [{"key": 10435984, "value": {...}}]},
        {"basic": {...}, "service": [{"key": 10407624, "value": {...}}]},
        ...
    ]
}

# Получить офферы, у которых производитель равен my_vendor
curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers?vendor=my_vendor&format=json"

# Получить офферы, которые скрыты в сервисе 123, а источником скрытия являются PUSH_PARTNER_API либо PUSH_PARTNER_OFFICE
curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers?shop_id=123&disabled_by=3&disabled_by=4&format=json"

# Получить офферы, которые предоставлены в сервисе 123 либо 456, при этом сами офферы могут быть скрыты
curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers?include_shop_id=123&include_shop_id=456&format=json"

```

#### JFYI
1. Разница между shop_id и return_shop_id.
   Наличие параметра shop_id подразумевает, что пользователя интересуют оффера только одного конкретного магазина (не всего бизнеса). Поэтому этот параметр учитывается еще в момент чтения данных из таблицы (до фильтрации), другие сервисные части учитываться не будут. В ответе будут возвращены только сервисные части с соотв. shop_id, united-офферов, состоящих только из базовой части - не будет.
   Параметр return_shop_id учитывается в момент формирования ответа (после фильтрации) и не влияет на чтение данных из таблицы (т.е. чиаются все сервисные части). Должен использоваться, когда для фильтрации необходимы все сервисные части, но в качестве результата интересны только сервисные части с заданным shop_id. Допускается возврат офферов, состоящих только из базовой части.
2. Single- и multiple-фильтры для сервисных частей. Подразумевается, что эти два типа - взаимоисключающие (см. первый пункт про работу с shop_id).
3. Интегральный статус оффера возвращается в ответе ручки только при запросах без фильтров (разрешены толькок идентификаторы business_id, shop_id, warehouse_id, offer_id)


## Получение вердиктов оффера (GET)
```
GET /v1/partners/{business_id}/offers/verdicts?offer_id={offer_id}
```

Ручка возвращает собранный в одну кучу список вердиктов для одного оффера. Вердикты для сервисных и складских офферов дедуплицируются в ответе. Можно получить вердикты для конретного магазина задав `shop_id`, `warehouse_id`.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
offer_id | string, required | идентификатор оффера
shop_id | int, optional | идентификатор магазина
warehouse_id | int, optional | идентификатор склада
show_all | bool, optional | отобразить все актуальные вердикты (по которым прошла валидация)
show_pictures | bool, optional | отобразить ошибки скачивания по каждой из картинок оффера
format | string, optional, default=protobuf | формат ответа json или protobuf

#### Ответ
В ответе возвращается протобуфка [GetVerdictsResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/GetVerdicts.proto)


## Получение вердиктов оффера (батч, POST)
```
POST /v1/partners/{business_id}/offers/verdicts
```
Батчевый аналог ручки получения вердиктов оффера.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
shop_id | int, optional | идентификатор магазина
warehouse_id | int, optional | идентификатор склада
show_all | bool, optional | отобразить все актуальные вердикты (по которым прошла валидация)
show_pictures | bool, optional | отобразить ошибки скачивания по каждой из картинок оффера
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | [GetVerdictsBatchRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/GetVerdicts.proto) | список идентификаторов офферов


#### Ответ
В ответе возвращается протобуфка [GetVerdictsBatchResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/GetVerdicts.proto)


#### Пример
```bash
Сохраняем файл 'body.proto' с содержимым
{
    "offer_ids": ["436138"]
}

curl -XPOST 'http://datacamp.white.tst.vs.market.yandex.net:80/v1/partners/10785678/offers/verdicts?format=json&show_all=true&shop_id=10785677' --data-binary "@body.proto" -H "Content-Type: application/json"
```

## Получение рекомендаций по моделям размещения оффера (GET)
```
GET /v1/partners/{business_id}/offers/model_recommendations?offer_id={offer_id}
```

Ручка возвращает список рекомендаций по моделям размещения для одного оффера.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
offer_id | string, required | идентификатор оффера
format | string, optional, default=protobuf | формат ответа json или protobuf

#### Ответ
В ответе возвращается протобуфка [GetRecommendationsResponse](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/api/GetOfferRecommendations.proto?rev=r9180785#L26)

## Получение рекомендаций по моделям размещения оффера (батч, POST)
```
POST /v1/partners/{business_id}/offers/model_recommendations
```
Батчевый аналог ручки получения рекомендаций по моделям размещения оффера.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | [GetRecommendationsBatchRequest](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/api/GetOfferRecommendations.proto?rev=r9180785#L33) | список идентификаторов офферов


#### Ответ
В ответе возвращается протобуфка [GetRecommendationsBatchResponse](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/api/GetOfferRecommendations.proto?rev=r9180785#L37)


#### Пример
```bash
Сохраняем файл 'body.proto' с содержимым
{
    "offer_ids": ["436138"]
}

curl -XPOST 'http://datacamp.white.tst.vs.market.yandex.net:80/v1/partners/10785678/offers/model_recommendations?format=json' --data-binary "@body.proto" -H "Content-Type: application/json"
```

## Батч операции с офферами
```
POST /v1/offers/united/batch
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
format | string, optional, default=protobuf | формат ответа json или protobuf
legacy | string, optional, default=true | копирование складской части из actual в service 
тело запроса | [UnitedOffersBatchRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/OffersBatch.proto?rev=7477757#L42) | один Entry в объекте — один подзапрос

**Текущие ограничения**:
* В рамках одного батч запроса поддерживается только один тип подзапросов

##### GET подзапросы: получить офферы по идентификаторам
Определяются с помощью `entry.method = RequestMethod::GET` и идентификаторами оффера. Обязательные идентификаторы `business_id` и `offer_id`, в таком случае в ответе будет базовый оффер со всеми сервисными офферами. Дополнительно можно определить `shop_id` и `warehouse_id`, чтобы получить офферы только одного сервиса.

##### POST подзапросы: создать либо обновить офферы
Определяются с помощью `entry.method = RequestMethod::POST` и заполненным `entry.offer`. За раскладывание полей оффера в базовую и сервисную часть отвечает поставщик данных.
Для удаления оффера нужно передать [status.removed](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=7960863&blame=true#L166) по той части UnitedOffer, которую хочется удалить.

#### Ответ
В ответе возвращается протобуфка [UnitedOffersBatchResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/OffersBatch.proto?rev=r7477757#L56). Порядок ответов на подзапросы совпадает с порядком самих подзапросов.


## Старая ручка поиска офферов
```
POST /shops/{shop_id}/offers/search
```
Не стоит завязываться на эту ручку.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
shop_id | int, required | идентификатор магазина
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | [SearchRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncSearch.proto?rev=7942439&blame=true#L18)

#### Ответ
Возвращает предложения магазина, удовлетворяющие фильтру поиска, в виде сообщения [SearchResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncSearch.proto?blame=true&rev=r7942439#L29).

#### Пример
```bash
curl -XPOST http://datacamp.white.tst.vs.market.yandex.net/shops/10279753/offers/search?format=json
{
  "total_response": 10,
  "paging": {
    "start": "1555935103_227952",
    "end": "1555935103_161085",
    "is_first_page": true,
    "is_last_page": false
  },
  "total_available": 28,
  "offer": [
    {
      "feed_id": 200401031,
      "offer_id": "227952",
      "shop_id": 10279753,
      "extra": {
        "ware_md5": "fKQlkDdqp0r1p9nW7yIXeg",
        "classifier_magic_id2": "6fcbc3a0a9489189740ef2112ac2854d",
        "recent_feed_id": 200401031,
        "classifier_good_id": "5b01f02c20e49f2f946ce97c56bc9982"
      }
    }
  ]
}
```

## Получение офферов конкретной группы
```
GET /v1/partners/<business_id>/groups/<group_id>
```
Ручка для запроса всех офферов партнера из конкретной группы (для режима запуска mboc возврашает оффера только тогда,
когда все оффера группы находятся в консистентном состоянии). Вернет первые 5000 офферов.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
mode | [default/mboc] | Режим фильтрации полей оффера. При значении mboc возвращаются поля, доступные подписке mboc, иначе все поля
force | bool, default=false | Игнорировать проверку консистентности офферов группы

#### Ответ
Возвращает [GetUnitedOffersResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetOffer.proto?rev=r7748351#L32-41).

#### Пример
```bash
curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/groups/12345?format=json"
{
    "offers": [
        {"basic": {...}, "service": [{"key": 10435984, "value": {...}}]},
        {"basic": {...}, "service": [{"key": 10407624, "value": {...}}]},
        ...
    ]
}
```


## Получение стоков
```
POST /v1/partners/{business_id}/offers/services/{shop_id}/stocks
```

Ручка для получения [стоков](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStockInfo.proto?blame=true&rev=r7828485#L42) офферов заданного пространства.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id  | int, required | идентификатор партнера
shop_id | int, required | идентификатор сервиса/магазина
filter_published_by_partner | bool, optional | вернуть оффера, опубликованные партнером
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | SelectRequest | список идентификаторов офферов

#### Ответ
Возвращает [SelectResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncSelect.proto?blame=true&rev=r7846118#L37).

#### Пример
```bash
curl -XPOST "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers/services/10293108/stocks?filter_published_by_partner=true" --data-binary "@body.proto"
{
    "meta": {
        "next_page_token": "..."
    },
    "offers": [{
        "identifiers": {},
        "stock_info": {
            "partner_stocks": {
            }
        }
    }, ...]
}
```

## Получение стоков по ключам
```
POST /v1/partners/{business_id}/offers/services/{shop_id}/stocks/get
```
Ручка для получения стоков офферов по ключам (номер склада обязателен)

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id  | int, required | идентификатор партнера
shop_id | int, required | идентификатор сервиса/магазина
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | GetOffersRequest | список идентификаторов офферов

#### Ответ
Возвращает заполненный [GetOffersResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetOffer.proto?blame=true&rev=r7828485#L33) офферами из таблицы stock_balance (есть деление по складам).
Для генерации идентификаторов можно использовать ручку identifiers и подставить склад.


## Скрытие и раскрытие оффера
```
PUT /shops/<shop_id>/offers/disabled?offer_id=<offer_id>[&supplemental_id=<supplemental_id>|warehouse_id=<warehouse_id>|whid=<whid>]
```
Скрыть либо раскрыть оффер. Для управления одним оффером можно передать идентификаторы через cgi, для батчевого обновления в теле запроса необходимо передать заполненный [ChangeOfferRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?rev=r7942439#L18).

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
shop_id | int, required | идентификатор магазина
offer_id | string, optional | идентификатор оффера
warehouse_id, whid, supplemental_id | int, optional | идентификатор склада партнера
disabled | bool, optional | целевое значение флага скрытия
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | [ChangeOfferRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?rev=r7942439#L18) | заполненные идентификаторы оффера и заполненный флаг в offer.status.disabled

#### Ответ
Возвращает обновленные оффера в формате [FullOfferResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?blame=true&rev=r7942439#L49).

#### Пример
```bash
curl -XPUT 'http://datacamp.white.tst.vs.market.yandex.net/shops/10252976/offers/disabled?offer_id=4488047&whid=171&status.disabled.flag=false&format=json'
```


## Поменять цену оффера
```
PUT /shops/<shop_id>/offers/price?offer_id=<offer_id>[&supplemental_id=<supplemental_id>|warehouse_id=<warehouse_id>|whid=<whid>]
```
Поменять цену оффера. Для управления одним оффером можно передать идентификаторы через cgi, для батчевого обновления в теле запроса необходимо передать заполненный [ChangeOfferRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?rev=r7942439#L18).

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
shop_id | int, required | идентификатор магазина
offer_id | string, optional | идентификатор оффера
warehouse_id, whid, supplemental_id | int, optional | идентификатор склада партнера
price.basic.binary_price.price | int, optional | целевая цена
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | [ChangeOfferRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?rev=r7942439#L18) | заполненные идентификаторы оффера и заполненный флаг в offer.status.disabled

#### Ответ
Возвращает обновленные оффера в формате [FullOfferResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncChangeOffer.proto?blame=true&rev=r7942439#L49).

#### Пример
```bash
$ curl -XPUT 'http://datacamp.white.tst.vs.market.yandex.net/shops/10252976/offers/price?offer_id=4488047&price.basic.binary_price.price=391400000000&format=json'
```


## Миграция офферов из одного фида в другой
```
POST /v1/partners/{business_id}/shops/{shop_id}/feeds/{feed_id}/migrate?target_feed_id={target_feed_id}&page_token={page_token}
```

Ручка для миграции офферов между фидами (реальными и актуальными). В рамках одного запроса происходит только частичная миграция. Для миграции всех офферов из фида необходимо повторить запрос с токеном следующей страницы из ответа.

Важно!
* Ручка мигрирует как реальные, так и актуальные feed_id. В строке запроса передается реальный feed_id
(real_feed_id). Актуальные feed_id передаются, только если они отличаются от реального (например, виртуальный feed_id
для выделения офферов в отдельный склад).
* Переданный в строке запроса feed_id=0 воспринимается как инструкция к миграции всех офферов всех фидов магазина под заданный target_feed_id.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id  | int, required | идентификатор партнера
shop_id | int, required  | идентификатор магазина
feed_id | int, required | идентификатор реального фида (real_feed_id), из которого мигрируем
target_feed_id | int, required | идентификатор реального фида (real_feed_id), в который мигрируем
page_token | string, optional | токен, полученный из предыдущего запроса
batch_size | int, optional, default=10000 | максимальное количество офферов для чтения из БД
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | [MigrateFeedOffersRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/MigrateFeedOffers.proto) | параметры для миграции виртуальных фидов, специфичных для складов

#### Ответ
Возвращает [MigrateFeedOffersResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/MigrateFeedOffers.proto), с заполненным `page_token` для следующего запроса.


## Скрытие всех офферов фида
```
POST /v1/partners/{business_id}/shops/{shop_id}/feeds/{feed_id}/hide?page_token={page_token}
```

Ручка для скрытия офферов фида. В рамках одного запроса происходит только частичное скрытие. Для скрытия всех офферов из фида необходимо повторить запрос с токеном следующей страницы из ответа.

Внимание! В строке запроса передается реальный feed_id - real_feed_id.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id  | int, required | идентификатор партнера
shop_id | int, required  | идентификатор магазина
feed_id | int, required | идентификатор реального фида (real_feed_id)
page_token | string, optional | токен, полученный из предыдущего запроса
batch_size | int, optional, default=10000 | максимальное количество офферов для чтения из БД
format | string, optional, default=protobuf | формат ответа json или protobuf
search_tables | bool, optional | активирует выполнение запроса по поисковым таблицам (целевая схема)
тело запроса | [HideFeedRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncHideFeed.proto) | параметры скрытия

#### Ответ
Возвращает [HideFeedResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncHideFeed.proto), с заполенным `page_token` для следующего запроса.


## Получение списка партнерских категорий
```
GET /v1/partners/<business_id>/categories
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id  | int, required | идентификатор партнера

#### Ответ
Возвращает список всех партнерских категорий в следующем JSON формате:
```
{
  "category_id": {
    "id": <string>,          # идентификатор категории
    "name": <string>,        # название категории
    "isLeaf": <bool>,        # является ли категория листовой
    "parentid": <string>,    # идентификатор родительской категории
    "children": [<string>],  # идентификаторы дочерних категорий
  }
}
```
Корневая категория идет под идентификатором `rootId`.

#### Пример
```bash
curl -XGET "http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/offers/basic?offer_id=1621011&format=jsonhttp://datacamp.white.tst.vs.market.yandex.net/v1/partners/10432691/categories"
{
    "1": {
        "id": "1",
        "isLeaf": 1,
        "name": "Зоотовары",
        "parentId": "rootId"
    },
    "rootId": {
        "children": [
            "1"
        ],
        "id": "rootId",
        "isLeaf": 0,
        "name": "rootId"
     }
}
```


## Получение партнерских категорий c фильтрами
```
POST /v1/partners/{business_id}/categories/flat_filter
```
Батчевая ручка получения категорий партнера, подходящих под указанный фильтр. Сейчас есть фильтнация по названию категории.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
тело запроса | [GetPartnerCategoriesFlatFilterRequest](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/api/SyncCategory.proto) | фильтры

#### Ответ
Позволяет получить категории партнера с заданным фильтром.
Формат ответа [PartnerCategoriesResponse](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/api/SyncCategory.proto)


## Создание партнерской категории
```
POST /v1/partner_categories
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
тело запроса | [PartnerCategory](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/category/PartnerCategory.proto) | Заполненная информация про новую категорию

#### Ответ
Возвращает описание новой категории в JSON формате, либо `{'message': 'Сообщение об ошибке'}`


## Запросить промо акции из акционного хранилища (АХ)
```
POST /v1/promo/get
```
Батчевая ручка получения промо акций по идентификаторам.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
тело запроса | [GetPromoBatchRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetPromo.proto?blame=true#L12) | идентификаторы промо акций
format | string, optional, default=protobuf | формат ответа json или protobuf
enabled | bool, optional | включена ли акция, рассчитывается по [promo.constraints.enabled](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/promo/Promo.proto?rev=r8443100#L265)
only_unfinished | bool, optional, default=false | для значения true(1) выбирает акции, у которых [promo.constraints.end_date](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/promo/Promo.proto?rev=r8443100#L249) в будущем, значение false(0) игнорируется
type | int, repeated, optional |только акции заданных типов (механики), рассчитывается по [promo.promo_general_info.promo_type](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/promo/Promo.proto?rev=r8443100#L42), возможные значения - [enum PromoType](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/promo/Promo.proto?rev=r8443100#L55-76)

#### Ответ
Сообщение [GetPromoBatchResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetPromo.proto?rev=r8592849#L18). Если ни один оффер не нашелся, HTTP код 404, иначе 200.


## Создание/обновление промо акции в акционном хранилище (АХ)
```
POST /v1/add_promo
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
тело запроса | [PromoDescription](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/promo/Promo.proto?rev=r8734250#L14) | идентификаторы промо акций

#### Ответ
В теле ответа - json, содержащий добавленную/обновлённую акцию, либо json с полем message, содержащий ошибку. В случае ошибки возвращается код 500, в случае успеха - 200.


## Создание/обновление промо акций в акционном хранилище (АХ)
```
POST /v1/partners/<business_id>/promos
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
тело запроса | [UpdatePromoBatchRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetPromo.proto?rev=r7597620#L24) | описание промо акций

#### Ответ
Возвращает обновленные промо акции: [UpdatePromoBatchResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetPromo.proto?rev=r7597620#L27).


## Удаление промо акций из акционного хранилища (АХ)
```
POST /v1/promo/delete
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
тело запроса | [DeletePromoBatchRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetPromo.proto?rev=r8625080#L48) | Идентификаторы промо акций

#### Ответ
Возвращает список идентификаторов акций, которые не получилось удалить: [DeletePromoBatchResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetPromo.proto?rev=r8625080#L52)

#### Пример
Внимание, пример не содежит [partner_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetPromo.proto?blame=true&rev=r8625080#L42-45), если он вам нужен - укажите.
```bash
curl -v -XPOST --header "Content-Type: application/json" --header "X-Ya-Service-Ticket: ${TVM_TICKET_PROD}" http://datacamp.white.vs.market.yandex.net/v1/promo/delete --data '{"identifiers": [{"primary_key": {"promo_id": "1035100_KYRDRAVA", "business_id": 723377, "source": 2}}]}'
```


## Запрос промо акций партнера
```
GET /v1/partners/<business_id>/promos
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
format | string, optional, default=protobuf | формат ответа json или protobuf
enabled | bool, optional | включена ли акция, рассчитывается по [promo.constraints.enabled](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/promo/Promo.proto?rev=r8443100#L265)
only_unfinished | bool, optional, default=false | для значения true(1) выбирает акции, у которых [promo.constraints.end_date](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/promo/Promo.proto?rev=r8443100#L249) в будущем, значение false(0) игнорируется
partner_id | int, optional | рассчитывается по наличию партнера в списке [promo.constraints.offers_matching_rules.supplier_restriction.suppliers](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/promo/Promo.proto?rev=r8443100#L297)
source | int, repeated, optional | только акции от заданных источников, рассчитывается по [promo.primary_key.source](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/promo/Promo.proto?rev=r8443100#L50)
type | int, repeated, optional | если передано, возвращает акции заданных типов (механики), рассчитывается по [promo.promo_general_info.promo_type](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/promo/Promo.proto?rev=r8443100#L42), возможные значения - [enum PromoType](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/promo/Promo.proto?rev=r8443100#L55-76)
limit | int, optional | количество акций в ответе, если не передано, то возвращает все акции
position | string, optional | нижняя граница для promo_id в ответе (включительно), используется для пагинации

#### Ответ
Возвращает [GetPromoBatchResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGetPromo.proto?rev=r7597620#L17):

* promos - список промо акций (акции с механикой `PARTNER_CUSTOM_CACHBACK` выводятся в порядке убывания приоритета)
* next_page_position - позиция следующей страницы при пагинации (нужно передавать в качестве position для следующего запроса). Если пуст, то выдана последняя страница списка акций.

#### Пример
```bash
wget 'http://datacamp.white.tst.vs.market.yandex.net/v1/partners/10503043/promos?enabled=1&only_unfinished=1&type=3&type=15' -O promos.out
```


#### Выход из акции для всех офферов магазина
```
POST /shops/<shop_id>/offers/deactivate_promo?promo_id=<promo_id>&business_id=<business_id>
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
shop_id | int, required | идентификатор магазина
promo_id | string, required | идентификатор промо, из которого удаляются оффера
format | string, optional, default=protobuf | формат ответа json или protobuf
business_id | int, optional | идентификатор бизнеса

Если не указать business_id, то stroller попробует определить его самостоятельно, и если не сможет, то вернется ответ
с кодом 500.

#### Ответ
В качестве подтверждения применения изменений возвращается HTTP код 200 с текстом `Action result will be applied in a minutes`.

#### Пример
```bash
curl -XPOST http://datacamp.white.tst.vs.market.yandex.net/shops/10263850/offers/deactivate_promo?promo_id=%232242
Action result will be applied in a minutes
```


## Генерация фида, которые участвуют в промо акции
```
POST /shops/<shop_id>/generate/promo?promo_id=<promo_id>&business_id=<business_id>
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
shop_id | int, required | идентификатор магазина
promo_id | string, required | идентификатор промо, из которого удаляются оффера
format | string, optional, default=protobuf | формат ответа json или protobuf
business_id | int, optional | идентификатор бизнеса

Если не указать business_id, то stroller попробует определить его самостоятельно, и если не сможет, то вернется ответ
с кодом 500.

#### Ответ
Возвращает заполненный [GenerateFeedResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncGenerateFeed.proto?rev=r7943652#L14).

#### Пример
```bash
curl -XPOST http://datacamp.white.tst.vs.market.yandex.net/shops/10263850/generate/promo?promo_id=%232242&format=json
{"feed_url":"http://market-idx-datacamp-test.s3.mds.yandex.net/upload/promo/10263850_#2242"}
```


## Добавить склад для магазина
```
POST /shops/<shop_id>/add_warehouse?warehouse_id=<warehouse_id>&business_id=<business_id>
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
shop_id | int, required | идентификатор магазина
warehouse_id | int, required | идентификатор нового склада
business_id | int, optional | идентификатор бизнеса

Если не указать business_id, то stroller попробует определить его самостоятельно, и если не сможет, то вернется ответ
с кодом 500.

#### Ответ
При успехе возвращает код 200, и количество скопированных офферов

#### Пример
```bash
curl -XPOST http://datacamp.white.tst.vs.market.yandex.net/shops/10264169/add_warehouse?feed_id=200344511&warehouse_id=145&format=json
{
  "10 offers were copied to warehouse 145"
}
```


## Переключение партнера в пуш схему и обратно
```
#### PUT/POST /shops/{shop_id}/change_schema
```

Ручка для контроллирования процесса перехода партнера из одной схемы в другую (pull to push, push to pull).

#### Параметры
Все параметры передаются в json-формате в теле запроса.
```
{
    change_schema_type -  тип перехода (строка: 'pull_to_push' или 'push_to_pull')
    start_ts_sec - время начала перехода (в секундах)
    finish_ts_sec - время окончания перехода (в секундах)
    feeds - информация о магазине из shopsdat (необходимо, если в таблице хранилища нет информации о партнере)
    feeds: [
        {
            "shop_id": 774,
            "datafeed_id": 1069,
            "is_push_partner": true,
            "warehouse_id": 145,
            ...
        },
        ...
    ]
}
```
Для того, чтобы начать процесс перехода, необходимо передать тип перехода  и время начала (и возможно, информацию из shopsdat).
Для того, чтобы завершить процесс перехода, достаточно передать время завершения.

#### Ответ
При успешном переключении возвращает код 200, при ошибке код 400 с текстовым описанием ошибки.

#### Пример
```
$ curl -XPOST --header "Content-Type: application/json" --data '{"change_schema_type": "pull_to_push", "start_ts_sec": 1000,}' http://datacamp.white.tst.vs.market.yandex.net/shops/10296726/change_schema
{
  "Successfully start new change schema process"
}
```

## Список запрещенных категорий для SMB партнеров
```
GET /categories/forbidden_for_smb
```

#### Параметры
Нет

#### Ответ
Ручка возвращает список категорий, запрещенных для размещения SMB партнерами. В список попали категории с дополнительной логикой обработки офферов, которую не поддержали в начале, см. [MARKETINDEXER-33857](https://st.yandex-team.ru/MARKETINDEXER-33857).

#### Пример
```bash
curl -XGET http://datacamp.white.tst.vs.market.yandex.net/categories/forbidden_for_smb
{"forbidden_categories":[90829,16155381,90802,91441,91735,90924,90490,90925,91216,7308012,16033851,90927,283662,987260,17725598,15754673,91051,17728967,91197,10530882,15683167,15797254,90942,10682497]}
```

## Блокировка бизнеса для миграции магазина
```
POST /v1/business/lock
```

* Input - [LockBusinessRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/proto/BusinessMigration.proto?blame=true&rev=r7849387#L10)
* Output - [LockBusinessResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/proto/BusinessMigration.proto?blame=true&rev=r7849387#L17)


## Разблокировка бизнесов после миграции магазина
```
POST /v1/business/unlock
```

* Input - [UnlockBusinessRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/proto/BusinessMigration.proto?blame=true&rev=r7849387#L23)
* Output - [UnlockBusinessResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/proto/BusinessMigration.proto?blame=true&rev=r7849387#L30)


## Статус бизнеса
```
GET /v1/business/{business_id}/status
```

* Output - [BusinessStatusResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/Business.proto?rev=7849387&blame=true#L12)


## Запуск асинхронного процесса копирования офферов
```
POST /v1/partners/{business_id}/offers/services/{shop_id}/copy
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
shop_id | int, required | идентификатор магазина, в который копируются оффера
format | string, optional, default=protobuf | формат ответа json или protobuf
тело запроса | OffersCopyTask | параметры задания на копирование

#### Ответ
Фоормат ответа: [OffersCopyTaskStatus](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/CopyOffers.proto) с заполненными идентификаторами для поллинга результата. См. ниже.


## Получить статус таски, копирующий офферы
```
GET /v1/partners/{business_id}/offers/services/{shop_id}/copy/{task_id}
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
shop_id | int, required | идентификатор магазина, в который копируются оффера
task_id | int, required | идентификатор таски из запроса на создание таски
format | string, optional, default=protobuf | формат ответа json или protobuf


#### Ответ
Формат ответа: [OffersCopyTaskStatus](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/CopyOffers.proto)


## Добавление/обновление нескольких товарных категорий партнера
```
POST /v1/partners/<business_id>/categories/flat
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
тело запроса | [UpdatePartnerCategories](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncCategory.proto?rev=7949462&blame=true#L8) | описание категорий

#### Ответ
Возвращает обновленные категории: [PartnerCategoriesResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncCategory.proto?blame=true&rev=r7949462#L13).


## Удаление нескольких товарных категорий партнера
```
POST /v1/partners/<business_id>/categories/remove
```

Удаление происходит без каких либо проверок на наличие данной категории в офферах

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
тело запроса | [DeletePartnerCategoriesBatchRequest](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncCategory.proto) | список id категорий для удаления

#### Ответ
200 или сообщение об ошибке


## Получение всех товарных категорий партнера в плоском формате
```
GET /v1/partners/<business_id>/categories/flat
```

#### Ответ
Возвращает все категории партнера: [PartnerCategoriesResponse](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SyncCategory.proto).


## Удалить склад для магазина
```
POST /v1/partners/<business_id>/services/<shop_id>/remove_warehouse?warehouse_id=<warehouse_id>
```

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
shop_id | int, required | идентификатор магазина
warehouse_id | int, required | идентификатор удаляемого склада


#### Ответ
При успехе возвращает код 200, и количество удаленных офферов

## Получение данных о магазине
```
GET /v1/partners/<business_id>/shop/<shop_id>/stats
```

#### Output
Возвращает данные о магазине [ShopStatsResponse](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/api/ShopStats.proto)
- OffersCount - количество офферов (вернее, подсчитанных складских частей) указанного магазина.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
shop_id | int, required | идентификатор магазина

#### Ответ
При успехе возращает 200. Если магазин не найден, возвращает 404

## Получить все карго-типы одного партнера
```
GET /v1/partners/{business_id}/offers/services/{shop_id}/cargotypes
```

#### Output
Позволяет получить список уникальных карготипов, которые есть на офферах заданного партнера.
Формат ответа [GetInt32ListValueResponse](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/api/SyncCommon.proto)

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
shop_id | int, required | идентификатор магазина

#### Ответ
При успехе возращает 200.

## Получить все маркетные бренды одного партнера
```
GET /v1/partners/{business_id}/offers/services/{shop_id}/vendors
```

#### Output
Позволяет получить список уникальных маркетных брендов, которые есть на офферах заданного партнера.
Формат ответа [GetInt32ListValueResponse](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/api/SyncCommon.proto)

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
business_id | int, required | идентификатор бизнеса
shop_id | int, required | идентификатор магазина

#### Ответ
При успехе возращает 200.

## Установка/снятие trace-флага
```
POST /v1/set_otrace_flag?unset
```
Выставляет/снимает trace-флаг в [tech_info оффера](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferTechInfo.proto?#L24) в сервисной таблице, проставляет ```timestamp``` и, если флаг выставляется, ```applier```.

#### Параметры
Имя | Тип | Описание
:--- | :--- | :---
unset | optional | снять флаг, если нет - выставить
тело запроса | [proto](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/SetOtraceFlag.proto) | идентификаторы офферов, для которых выставляется флаг. Требуются ```business_id```, ```shop_id```, ```offer_id```

#### Ответ
Возвращает json с четырьмя параметрами:
* ```requested``` — количество запрошенных для изменения офферов
* ```found``` — количество найденных в таблице офферов
* ```changed``` — количество офферов, для которых флаг не совпадал с выставляемым
* ```updated``` — количество офферов, измененных в таблице. В силу реализации функции ```UpdateUnitedOffers``` может быть даже больше, чем поле ```requested```

#### Примеры
```bash
TVM_TICKET=$(cat tvm_ticket)

DATA=$(echo '{
    "offers" : [
        {
            "business_id" : 1025853,
            "shop_id" : 1025852,
            "offer_id" : "10003272038252030632"
        },
        {
            "business_id" : 10432691,
            "shop_id" : 10426272,
            "offer_id" : "01094666aa4f9b7c15fa"
        },
        {
            "business_id" : 11007481,
            "shop_id" : 10986368,
            "offer_id" : "107093"
        },
        {
            "business_id" : 1025853,
            "shop_id" : 1025852,
            "offer_id" : "10001294836660478647"
        }
    ]
}' | jq -c)

curl -X POST \
    "http://datacamp.white.tst.vs.market.yandex.net/v1/set_otrace_flag" \
    --header "X-Ya-Service-Ticket: $TVM_TICKET" \
    --header "Content-Type: application/json" \
    --data $DATA

curl -X POST \
    "http://datacamp.white.tst.vs.market.yandex.net/v1/set_otrace_flag?unset" \
    --header "X-Ya-Service-Ticket: $TVM_TICKET" \
    --header "Content-Type: application/json" \
    --data $DATA
```
