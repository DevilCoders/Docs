# Рутина для разметки трассируемых офферов

Читает таблицу [```service_offers```](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/united/service_offers) в YT, проставляя флаг ```should_trace``` от имени *Сканнера* части не<span style="color:blue">синих</span> офферов и убирая его у офферов, если он был проставлен ей и "просрочился".
Выбранные офферы пишутся в YT-ёвую таблицу ([параметр *yt_offers_tracer_table_dir* в конфиге](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/routines/etc/conf-available/production.white.ini?rev=r8591774#L246)).

Гарантируется, что выбирается не более чем [```offers_trace_limit```](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/routines/etc/conf-available/production.white.ini?rev=r8591774#L247) офферов.

### Ручные фильтры по *business_id* и *shop_id*
Есть возможность указать списки *business_id* и *shop_id*, и офферы, идентификаторы которых в них попадают, будут выбираться приоритетно. Списки указываются в [конфигах рутин](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/etc/conf-available/testing.white.ini?rev=8607876#L265), есть возможность указать их через ITS. Если оффер попадает под текущие списки, он будет выбран при очередном запуске *offers_tracer*. Флаг у таких офферов останется поднятым в течение [```offers_trace_flag_ttl```](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/etc/conf-available/testing.white.ini?rev=8607876#L264) (2 недели) и будет снят самой рутиной.

## Как выбираются офферы

Все офферы, у которых недавно (за последние нескольких часов) менялся какой-либо из флагов среди serviceOffer->status->disabled, а также офферы, которые попадают под фильтр вручную проставленных *business_id* и *shop_id*, выбираются вне очереди.

Из ```service_offers``` для каждого не<span style="color:blue">синего</span> оффера выделяются следующие параметры:
- <u>идентификаторы</u>
- <u>цвет, флаг *is_dsbs* </u>\
для определения типа оффера
- <u>**cpa_fee** = serviceOffer->bids->fee $\times$ serviceOffer->price </u>\
комиссия за *dsbs* оффер (**TODO**: сейчас не учитывается валюта)
- <u>**cpc_bid** = serviceOffer->bids->bids </u>\
ставка для *cpc* оффера
- <u>**business_size** = <кол-во_различных_shopId_у_данного_businessId> </u>\
размер партнёра
- <u>**random_weight** = <[захардкоженный_вес_цвета](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/tasks/offers_tracer/lib/pick_logic.cpp?rev=8583196#L26)> $\times$ <random_value> </u>\
пока используется для не<span style="color:grey">белых</span> офферов

Значения флага *is_dsbs* и **business_size** берутся из файла *shops-utf8.dat*.

Далее для каждого оффера вычисляется <span style="color:orange"> *score* </span> следующим образом:

\- Для каждого из параметров **cpa_fee**, **cpc_bid** вычисляется примерное разбиение значений по квантилям (грубо говоря, для каждого значения вычисляется его индекс в отсортированном по возрастанию порядке, немного подробнее на [схеме](https://jing.yandex-team.ru/files/yegyegorov/Перцентили.pdf)).

- Для *dsbs* офферов: \
<span style="color:orange"> *score* </span> = линейная комбинация <индекс_квантиля_**cpa_fee**> и **business_size**

- Для <span style="color:grey">белых</span> не*dsbs* офферов (*cpc*): \
<span style="color:orange"> *score* </span> = линейная комбинация <индекс_квантиля_**cpc_bid**> и **business_size**

- Для не<span style="color:grey">белых</span> офферов: \
<span style="color:orange"> *score* </span> = линейная комбинация **random_weight**

Значения всех параметров, используемых при вычислении, нормируются.

Затем для каждого из этих типов выбираются:
- фиксированное кол-во офферов с наибольшим значением <span style="color:orange"> *score* </span>
- не более чем фиксированное кол-во случайных офферов из оставшихся
