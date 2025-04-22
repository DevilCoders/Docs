
## Последовательность поиска оффера
1. [Партнерский интерфейс](#katalog-partnerskogo-interfejsa)
2. [Doctor offer-diagnostic](https://doctor.market.yandex-team.ru/)
3. [Otrace](http://active.idxapi.vs.market.yandex.net:29334/v1/otrace)
4. [Внутренние инструменты](#vnutrennie-instrumenty)
5. Изучить пайплайн и искать оффер в промежуточных точках через YQL

## Каталог партнерского интерфейса
- Пример: business_id=1092240, offer_id=CB1803001
- [Оффер в каталоге партнерки](https://partner.market.yandex.ru/supplier/22049144/assortment?activeTab=offers&offerNameOrSku=CB1803001)

{% note info %}

Чтобы просматривать офферы в каталоге партнерского интерфейса Маркета, требуется роль в системе `Маркет / MBI / ADMIN_READER`. IDM выдает роль на аккаунт `yndx-<staff-login>`, под которым надо заходить в партнерку. Пароль на аккаунте должен изменяться каждые 90 дней.

{% endnote %}

## Внутренние инструменты
- Пример: business_id=1092240, shop_id=1092239, feed=1012426, offer_id=CB1803001
- [Doctor offer-diagnostic](https://doctor.market.yandex-team.ru/)
- [Otrace](http://active.idxapi.vs.market.yandex.net:29334/v1/otrace)
- [Otrace example](http://active.idxapi.vs.market.yandex.net:29334/v1/otrace?feed=1012426&offer=CB1803001)
- [Дукалис показывает полный стейт по офферу](http://idxapi.vs.market.yandex.net:29334/v1/admin/dukalis/check_offer_status/)
- [Карта доставки до КД](http://unicorn.market.yandex.net:8181/map?feed_id=1526&offer_id=960303)
- [Datacamp базовый общий контент](http://datacamp.white.vs.market.yandex.net/v1/partners/1092240/offers/basic?offer_id=CB1803001&format=json)
- [Datacamp cервисная магазинная часть](http://datacamp.white.vs.market.yandex.net/v1/partners/1092240/offers/services/1092239?offer_id=CB1803001&format=json)
- [Datacamp SaaS market-datacamp](http://stable-market-idx.saas.yandex.net/market_datacamp?ms=proto&hr=da&kps=1092240&text=s_shop_id%3A%221092239%22%20s_offer_id%3A%22CB1803001%22)

## Пайплайн поставки с промежуточными базами
![Схема поставки офферов](../_images/offer-bases.png "Поставка офферов")

## FAQ

### Неделю назад с офером все было хорошо, но позавчера все стало плохо, что произошло?

Историю по обновлению офера за неделю можно посмотреть в logfeller'e:

- Оферный топик - [https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-offers-log&](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-offers-log&)
- Топик с заданиями на парсинг - [https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-update-task-log-market&](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-update-task-log-market&)
- Топик с данными, переданными через API - [https://yt.yandex-team.ru/hahn/navigation?path=//logs/mbi-market-quick-log&](https://yt.yandex-team.ru/hahn/navigation?path=//logs/mbi-market-quick-log&)
- Топик от синхронного контроллера в saas-hub - [https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-saashub-log&](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-saashub-log&)
- Топик на переобогащение - [https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-miner-log&](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-datacamp-miner-log&)

### Партнер запушил фид, но ничего не работает, ааааа, что делать? { #feed-trouble-shooting }

Есть ли нераспаршенные пуш [задания](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-update-tasks-market?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original)? Может push-parser не успевает обрабатывать или просто умер?

Есть ли нераспаршенные [задания](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-push-feeds-technical-market?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original), которые по каким то нашим причинам упали и пытаются перепарситься. Может push-parser стал фейлить все сессии из за проблем ытя, например?

А [пушили](https://yt.yandex-team.ru/hahn/navigation?path=%2F%2Flogs%2Fmarket-datacamp-update-task-log-market&) ли задание вообще? Может проблема в пуше от MBI или партнер нас обманывает? :)

А может просто фид кривой и он не может попарсится? Посмотрим в [фидархиве](../market/idx/datacamp/parser/README#feed_archives)

Все равно ничего не понятно?
Идти в [контейнеры](../market/idx/datacamp/parser/README#deploy) и грепать логи ```logs/push-robot/push-robot.log```

### Почему цена не обновляется? Почему офер скрыт?

А точно ли цена/скрытия дошли до нас?

Если в хранилище и saas-hub'e "хорошая" цена, но на фронте не она, то проблема с доставкой данных под репорт и не связана с хранилищем

Если в хранилище новая цена, а в saas-hub'e старая, saas-hub возможно не успел прочитал цены:
- Не доезжают цены из **фида**? Есть ли непрочитанные сообщения в [топике](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-offers?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-saashub-consumer) или [топике](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-qoffers?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-saashub-consumer)?
- Не доезжают цены из **Пользовательского Интерфейса(ПИ)**? Есть ли непрочитаннаые сообщения в [топике](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-offers-to-saashub?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-saashub-consumer)?
- Не доезжают цены из **API**? Есть ли непрочитанные сообщения в [топике](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/market-quick?group=all&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-quick%2Fprod%2Fsaashub)?

Если цена в хранилище старая:
- Не доезжают цены из **фида**? А не забилась ли [очередь](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-update-tasks?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original) на парсинг фида? Есть ли непрочитанные сообщение во входном [топике](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-offers?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original) в хранилище или в [топике](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-qoffers?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original) от парсера?
- Не доезжают цены из **Пользовательского Интерфейса(ПИ)**? А не спятисотила ли ручка? А что в логах?
- Не доезжают цены из **API**? Есть ли непрочитанные сообщения в [топике](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/market-quick?group=all&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original)?


Посмотреть стейт в хранилище:
```
http://datacamp.white.vs.market.yandex.net/shops/<shop_id>/offers?offer_id=<offer_id>&whid=<warehouse_id>
http://datacamp.white.tst.vs.market.yandex.net/shops/<shop_id>/offers?offer_id=<offer_id>&whid=<warehouse_id>
```
```bash
$ curl 'http://datacamp.white.vs.market.yandex.net/shops/465852/offers?offer_id=000002.3838471016483&whid=145&format=json' | jq .offer.price.basic
{
  "binary_oldprice": {
    "price": "1190000000",
    "id": "RUR"
  },
  "binary_price": {
    "price": "760000000",
    "id": "RUR"
  },
  "meta": {
    "source": "PUSH_PARTNER_API",
    "timestamp": "2019-10-24T05:08:44.993876Z",
    "ts_ms": "1571893724993"
  },
  "enabled": true,
  "vat": 2
}
$ curl 'http://datacamp.white.vs.market.yandex.net/shops/465852/offers?offer_id=000002.3838471016483&whid=145&format=json' | jq .offer.status
{
  "disabled": [
    {
      "flag": true,
      "meta": {
        "source": "MARKET_STOCK",
        "timestamp": "2019-10-24T10:10:42.451Z"
      }
    },
    {
      "flag": false,
      "meta": {
        "source": "MARKET_IDX",
        "timestamp": "2019-10-24T10:24:36Z"
      }
    },
    {
      "flag": false,
      "meta": {
        "source": "PUSH_PARTNER_FEED",
        "timestamp": "2019-08-22T06:54:29.121Z"
      }
    }
  ],
  "has_gone": {
    "flag": false,
    "meta": {
      "source": "MARKET_IDX",
      "timestamp": "2019-09-02T14:47:40Z"
    }
  },
  "publish_by_partner": "AVAILABLE",
  "publish": "HIDDEN"
}
```
Посмотреть стейт в саасхабе:
```
https://saas-hub.vs.market.yandex.net/doc_state/<feed_id>/<offer_id>
https://saas-hub.tst.vs.market.yandex.net/doc_state/<feed_id>/<offer_id>
```
```bash
$ curl 'http://datacamp.white.vs.market.yandex.net/shops/465852/offers?offer_id=000002.3838471016483&whid=145&format=json' | jq .offer.identifiers.feed_id
493303
$ curl https://saas-hub.vs.market.yandex.net/doc_state/493303/000002.3838471016483 | jq .
{
  "493303/000002.3838471016483/": {
    "offer_disabled": {
      "IDX": {
        "value": false,
        "time": "Thu, 24 Oct 2019 10:04:21 MSK",
        "ts": 1571900661
      },
      "STOCK": {
        "value": true,
        "time": "Thu, 24 Oct 2019 09:40:44 MSK",
        "ts": 1571899244
      }
    }
    .....
    "prices": {
      "old_price": {
        "rate": "1",
        "ref_currency": "RUR",
        "currency": "RUR",
        "value": 1190000000,
        "plus": 0,
        "precision": 7
      },
      "price": {
        "rate": "1",
        "ref_currency": "RUR",
        "currency": "RUR",
        "value": 760000000,
        "plus": 0,
        "precision": 7
      },
      "time": "Thu, 24 Oct 2019 08:08:44 MSK",
      "source": "feed",
      "ts": 1571893724
    }
    .....
  }
}
```

### Расследование проблем с ценами

> Цена и скрытие попадают на витрину через поколение (каждые 3-4 часа) и RTY (минуты). Возможны следующие ошибки: нам не отправили, мы не записали, мы не отправили в RTY (то, что записали), как результат - неправильная цена в каталоге, витрине, заказе.

- Смотрим на то, как менялась цена в [истории офферов](https://yql.yandex-team.ru/Operations/Yi9cqlZ1OyYBjN08utm6VUYrMc0muK1sUHvHLqYGri0=) и/или в [бэкапах хранилища](https://yql.yandex-team.ru/Operations/YjgmO5fFtyRa-9R3nQktbtNC2Ko5Z_Xcanje9H7D3Hg=).

_(при этом гарантии, что в историю попадают все изменения нет, а бэкапы ротируются)_

- Если видим, что цена менялась, то надо убедиться, что она был отправлена через RTY (быстрый пайплайн) [market-quick-log](https://yql.yandex-team.ru/Operations/YjgtddJwbJRnhx050DUeh7ypCdM4j2HRFrVA3nWHdaQ=)
	 - Если цена отправлена, то мы все сделали хорошо. Но:
    	 - возможно товар продали по акции
         - возможно не работал RTY ([график](https://yasm.yandex-team.ru/template/panel/Market_rty_and_report/-/11/?by=prj))
	 - Если цена не отправлена, то либо ошибка в подписке, либо что-то еще более редкое. Действуем по ситуации.

_(подробнее [про быстрые пайплайны](https://docs.yandex-team.ru/market-datacamp/integration/quick-pipelines#logi-otpravki-offerov-pod-report))_

- Если цена не менялась, то надо убедиться, что нам цену присылали:
	 - [из парсера (синие и дбс)](https://yql.yandex-team.ru/Operations/YiMSlAVK8G9C9Ocd-g98kmmVHzyw7-qhD-5PZcX1yqk=)
	 - [из ПИ (строллер)](https://yql.yandex-team.ru/Operations/YjgvJ7q3k77qJ59j6eiYpjZq1-43WmzNlG6s3d2SN9c=)
	 - [из топика ПАПИ (скрытия и цены)](https://yql.yandex-team.ru/Operations/YiH7MdJwbFJB-r4_dj7aEVn6x1hpMI7yBPLPYBSiEBs=)

_(подробнее [про источники цен и скрытий](https://docs.yandex-team.ru/market-datacamp/integration/mbi))_

- Проверяем акции
    - [история изменений акций оффера](https://yql.yandex-team.ru/Operations/Yh86Hrq3k4C_o7likJCh3YKgZNp_IFrIwLsh-PZ6ba0=)
    - кроме того, можно посмотреть список акций (binary_promos_md5_base64) в [генлоге поколения](https://yql.yandex-team.ru/Operations/Yjg0AFZ1O9WruO7fprGA7JttCzv1UTspnRzRZVRigMY=) и [поискать описание акции по ware_md5](https://yql.yandex-team.ru/Operations/Yjgy2ZfFtyRa-95LpDmMcYvrPyFD4lkYf493v4E6FWw=)
    - [пример](https://st.yandex-team.ru/PRICINGSUPPORT-1802#621f1721decdb2229e45b78d) расследования промоакции/скидки не из хранилища

### Как грепнуть и исследовать историческую цену?

Историческая цена сохраняется для подсчёта Честной Скидки ([вики](https://wiki.yandex-team.ru/users/ilya-brodskiy/chestnye-skidki/)).
Алгоритм подсчёта максимального oldprice для оффера на основе исторической цены описан [здесь](https://wiki.yandex-team.ru/users/green-yeti/Sinie-skidki/#proverkapoistorii).

Как эта историческая цена путешествует по Маркету?
- Историческая цена едет через [FlatBuffers файл](https://a.yandex-team.ru/arc/trunk/arcadia/market/flat/indexer/BaseOfferProps.fbs?rev=r8848593#L50) с названием [base-offer-props.fb](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/generation/genlog_dumper/dumpers/BaseOfferPropsDumper.cpp?rev=r8913800).
- Файл заполняется в индексаторе в [TBaseOfferPropertiesDumper](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/generation/genlog_dumper/dumpers/BaseOfferPropsDumper.cpp?rev=r8913800#L25), а читается в репорте в [rty_qpipe](https://a.yandex-team.ru/arc/trunk/arcadia/market/report/library/base_search_document_basic_props/base_search_document_basic_props.cpp?rev=r9144190#L167).
- Цена в репорте на основе невыполнения партнёром правил Честной Скидки фильтруется [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/market/report/library/rty_qpipe/real_qpipe.cpp?rev=r9143642#L69).

Если требуется грепнуть файлик, то понадобится тулза [FBViewer](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/fbviewer/README.md) и рабочие инстансы воркеров индексации idx0[*]h.
Пример дампа:
```bash
green-yeti@idx01h:/indexer/market/mif/offers/20190711_1230-0/workindex$ /usr/lib/yandex/fbviewer base-offer-props.fb | head
{
  "BaseProperties": [
    {
      "Price": 0,
      "CurrencyId": 3,
      "Flags32": 0,
      "HistoryPrice": {
        "Value": 5660000000
      },
      "HistoryCurrencyId": 3,
```
Подробнее о FB-файле можно узнать на [вики](https://wiki.yandex-team.ru/users/green-yeti/flatbuffers-v-marketnom-indeksatore/#bazovyesvojjstvaoferavsharde).

### Много оферов магазина почему то скрыто?

Самый простой способ это пойти и написать YQL с нужными фильтрами. Но YQL работает долго и имеет некоторый лаг от реальных данных.

Если магазин небольшой(и вы не боитесь больших выражений в jq), то можно воспользоваться ручкой [search](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/stroller#post-shopsshop_idofferssearch) синхронного контроллер и получить актуальный список из хранилища

Пример, как получить все скрытые офера магазина и флаг, из за которого предложение скрыто:
```bash
$ curl -XPOST 'http://datacamp.white.vs.market.yandex.net/shops/555854/offers/search?format=json&page_size=400' | jq '.offer | map({disabled:.status.disabled | map(select(.flag == true) | {source:.meta.source, timestamp:.meta.timestamp}), offer_id:.identifiers.offer_id, feed_id:.identifiers.feed_id, warehouse_id:.identifiers.warehouse_id, mksu:.identifiers.extra.market_sku_id}) | map(select(.disabled | length > 0)) | map(select(.warehouse_id == 145))'
[
  {
    "disabled": [
      {
        "source": "MARKET_IDX",
        "timestamp": "2019-11-01T12:24:08Z"
      }
    ],
    "offer_id": "RBX107N",
    "feed_id": 568355,
    "warehouse_id": 145,
    "mksu": null
  },
  {
    "disabled": [
      {
        "source": "MARKET_IDX",
        "timestamp": "2019-11-01T12:24:08Z"
      }
    ],
    "offer_id": "RBT126N",
    "feed_id": 568355,
    "warehouse_id": 145,
    "mksu": "100655787167"
  },
  ...
```

### Почему офер не индексируется?

А есть ли он вообще в хранилище?
```bash
curl 'http://datacamp.white.vs.market.yandex.net/shops/531812/offers?offer_id=17506&whid=145&format=json'
```

А может быть он новый и был создан 20 минут назад?
```bash
curl 'http://datacamp.white.vs.market.yandex.net/shops/531812/offers?offer_id=17506&whid=145&format=json' | jq .offer.meta.ts_created
```

А включен ли этот пуш магазин в shopsdat?
```bash
ymoskalenk0@mi01h:/var/lib/yandex/getter/mbi/recent$ grep '531812' -A40 shops-utf8.dat
```

А есть ли этот магазин в таблице партнеров? Или может быть он выключен? Возможно проблема в создании таблицы или партнер просто находится в PULL режиме
```bash
echo '{"shop_id":531812}' | yt lookup-rows //home/market/production/indexer/datacamp/united/partners --format json --proxy hahn | jq .
```

А попал ли этот офер на вход индексатору?
[https://yql.yandex-team.ru/Operations/XbGJMwlcTgQ13xuFJtG34DRAmomiq20OFyJAPsRpceM=](https://yql.yandex-team.ru/Operations/XbGJMwlcTgQ13xuFJtG34DRAmomiq20OFyJAPsRpceM=)
Если нет, проблема при конвертации из формата хранилище в формат индексатора

А есть ли он в индексе?
```bash
ymoskalenk0@idx-blue01h:/var/lib/yandex/indexer/market/mif/offers/20191024_1220-blue-0/workindex$ /usr/lib/yandex/idx --feed-id 530492 --offer-id 17506
```
Если нет, то в процессе индексации офер был выброшен, надо идти и смотреть логи индексатора
```bash
ymoskalenk0@idx-blue01h:/var/lib/yandex/indexer/market/mif/offers/20191024_1220-blue-0$ grep 'offer_id 17506 ' indexer.log
```

### Как посмотреть, что происходит c офером?

Жизненый цикл офера можно посмотреть в трассировке otrace:
```
http://active.idxapi.vs.market.yandex.net:29334/v1/otrace?feed=<feed-id>&offer=<offer-id>
```

Среди ссылок находим ссылку```index_trace```, которая ведет на трассировку в ЦУМе по оферу

### Когда последний раз обновлялась доставка?

```bash
$ curl 'http://datacamp.white.vs.market.yandex.net/shops/465852/offers?offer_id=000002.3838471016483&whid=145&format=json' | jq .offer.delivery.calculator.meta
{
  "timestamp": "2019-10-24T10:44:37Z"
}
```

### Когда последний раз обновлялся маппинг?

```bash
$ curl 'http://datacamp.white.vs.market.yandex.net/shops/465852/offers?offer_id=000002.3838471016483&whid=145&format=json' | jq .offer.content.market.meta
{
  "timestamp": "2019-10-24T10:44:35Z"
}
```

### Когда последний раз майнился офер?

```bash
$ curl 'http://datacamp.white.vs.market.yandex.net/shops/465852/offers?offer_id=000002.3838471016483&whid=145&format=json' | jq .offer.tech_info.last_mining.meta.timestamp
{
  "seconds": 1590680756
}
```

### Когда последний раз парсился офер?

Последний раз, когда офер был распаршен из фида. Поле может быть пустым, если офер не парсился ниразу и был создан из других мест
```bash
$ curl 'http://datacamp.white.vs.market.yandex.net/shops/614754/offers?offer_id=00000016&whid=48196&format=json' | jq .offer.tech_info.last_parsing.meta.timestamp
{
  "nanos": 619899000,
  "seconds": 1590616377
}
```

### Когда последний раз был майнинг для магазина?

```bash
$ echo '{"key":465852}' | yt lookup-rows //home/market/production/indexer/datacamp/blue/routines/SenderToMiner/mining_state --format json --proxy markov | jq .
{
  "state": "{\"last_touch_time\": 1571912672.358518}",
  "key": 465852
}
$ date -d @1571912672
Чт окт 24 13:24:32 MSK 2019
```

### Недоезд скрытий / раскрытий стоков по быстрому пайплайну

Есть ли запись в таблице StockStorage?
[https://yql.yandex-team.ru/Operations/Yg-pkwVK8CgkJ-p2sGEU9y2h6ugNGYm3JsVZSsRWj1k=](https://yql.yandex-team.ru/Operations/Yg-pkwVK8CgkJ-p2sGEU9y2h6ugNGYm3JsVZSsRWj1k=).
Если её нет, то произошла некая неочевидная для стороннего наблюдателя логика или ошибка в SS.

Если она есть, то запись о стоках должна была отправиться.
В таком случае, проверяем: есть ли запись об этом в логфеллере?
[https://yql.yandex-team.ru/Operations/Yg-yFK5OD3u9QA836h5heENsK9sM_shEu82rbPeOQG4=](https://yql.yandex-team.ru/Operations/Yg-yFK5OD3u9QA836h5heENsK9sM_shEu82rbPeOQG4=)

Если в табличке SS запись есть, а в топике ничего нет, то SS где-то пролил запись - ошибка у них.
Для проверки нужно смотреть на наличие флажка **disabled** в столбце **data** - это свидетельствует об изменении значения поля (и о том, что скрытие/раскрытие записано в топик):

```json
{
  "offer": [
    {
      "status": {
        "disabled": [
          {
            "flag": true,
            "meta": {
              "timestamp": {
                "seconds": 1645045200,
                "nanos": 33612000
              },
              "source": 11
            }
          }
        ]
      }
    }
  ]
}
```

Если в логфеллере запись всё же нашлась, то SS успешно отправил информацию о скрытии/раскрытии стоков.
Но записали ли мы его в Хранилище?
Грепаем бэкапы:
[https://yql.yandex-team.ru/Operations/YgtzJK5OD3u9PQk7P8tXkgEZfdhaIbXNKNq0dsMs_zY=](https://yql.yandex-team.ru/Operations/YgtzJK5OD3u9PQk7P8tXkgEZfdhaIbXNKNq0dsMs_zY=)

Нас интересует столбец status и значение поля **flag** с **source** = 11 (SS):
```json
"disabled": [
    (
        "flag": true,
        "meta": (
            "source": 11,
            "timestamp": (
                "nanos": 474718000,
                "seconds": 1644823703
            )
        )
    )
]
```

Если флажок в бэкапе обновился, то скрытие/раскрытие успешно доехало до Офферного Хранилища.
Дальше нужно смотреть уже в сторону индексатора и поколений.
Если нет, то имеет смысл погрепать retry-топик: [https://yql.yandex-team.ru/Operations/YgumDrq3k9WEkzjjSmYVAeXAI8fsHIdy4lKM5V9evVI=](https://yql.yandex-team.ru/Operations/YgumDrq3k9WEkzjjSmYVAeXAI8fsHIdy4lKM5V9evVI=)

Наличие записей в retry-топике свидетельствует о том, что записать в таблицу ОХ с первого раза не получилось, и произошла вторая попытка.
Тогда, вероятно, сток пролился в [RetrySender](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/retry_sender/retry_sender.h?rev=r9165746#L14) из-за недоступности YT.
