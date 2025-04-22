# Быстрые пайплайны

## Устройство
@startuml
top to bottom direction

package "Datacamp" {
  [Parser]
  node "Controllers" {
    LB --> [Piper]
    YT --> [Scanner]
    HTTP --> [Storller]
  }
}


package "Report" {
   [Docfetcher] --> [RTY]
}

[Parser] --> [LB]
[Parser] --> [YT]
[Piper] --> [LB market-quick]
[Scanner] --> [LB market-quick]
[Storller] --> [LB market-quick]
[LB market-quick] --> [Docfetcher]
@enduml

Быстрые данные это по сути обычный механизм подписки в хранилище. Репорт в данном случае это подписчик с кастомным форматом данных.
Данные, на которые репорт подписан размечаются: [report_rty_subscriber](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/common/extension.proto?rev=r9004475#L106)

## Расследования проблем

### Поиск примеров старых данных
Все графики и отчеты строятся по данным здоровья. Статистика собирается на каждой машинке репорта раз в 5 минут. Все попадает в табличку rty_stats clickhouse.

{% note warning %}

Надо понимать, что туда попадают не все оффера, а только случайное подмножество.

{% endnote %}

[Пример запроса](https://yql.yandex-team.ru/Operations/YelQ8a5ODzHFjWDd293_Qgl1wO5DTqiIk6vob-4orq8=)

В этом запросе:
- `report_color` - сейчас всегда white, легаси со времен когда было три разных инсталляции репорта
- `processing_type` - логически можно считать, что оно всегда PUSH, нужно было на переходный период из `PULL` модели
- `total_time` - общее время доставки от таймстемпа данных, до момента чтения на репорте
- `before_dcmp_time` - время от таймстемпа данных, до [момента](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/lib/united_to_report_rty_converter/converter.cpp?rev=5b0da092e3d4b55f63485b66e965e708441f2e44#L65) конвертации в `NSaas::TDocument`, высокое число тут обычно говорит о проблемах у нас
- `after_dcmp_time` - время от момента конвертации до чтения документа репортом(каким то), высокое число тут говорит о медленном чтении репортом


### Логи отправки офферов под репорт
Логируется через logfeller
- [arnold //logs/market-quick-log](https://yt.yandex-team.ru/arnold/navigation?path=//logs/market-quick-log)
- [hahn //logs/market-quick-log](https://yt.yandex-team.ru/hahn/navigation?path=//logs/market-quick-log)
- [arnold //logs/market-quick-log-testing](https://yt.yandex-team.ru/arnold/navigation?path=//logs/market-quick-log-testing)

В проде суточные таблицы хранятся за год.

Грепаются логи по `feed_id` + `offer_id`:
- [пример взятия конкретного оффера](https://yql.yandex-team.ru/Operations/YelS_9JwbHujeKd3zjZOk0n4sSGMkbW62SMWWx8QG-k=)
- [получения детализации по типам скрытий](https://yql.yandex-team.ru/Operations/YfW8sNJwbHujjGzvEzjZUkKEGYLb4UUW5Tx-SC7KrYA=)

Найти `feed_id` можно:
1. [внутри оффера](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferIdentifiers.proto?rev=r8945602#L62)
2. [в табличке партнеров](https://yql.yandex-team.ru/Operations/YelSQq5ODzHFjWHlbCkt0VXps1wjSxmTlyag9AgleMo=)

На что смотреть:
- `_logfeller_index_bucket` - позволяет понять в какой шард были отправлены данные
- `source_uri` - содержит в себе ip v6 адрес машины с которой это сообщение было записано в логброкер
- `_logfeller_timestamp` - таймстемп, когда мы начали записывать сообщение в логброкер(creation timestamp)
- `iso_eventtime` - тот же `_logfeller_timestamp` в виде человеко читаемой строки
- `doc_ts` - таймстемп документа, [вычисляется](https://a.yandex-team.ru/arc_vcs/market/idx/quick/library/doc_state/state.cpp?rev=r8922300#L800), как максимум из всех таймстепов быстрых данных
- `feed_id` - id фида, по историческим причинам используется как идентификатор, см. выше как его найти в хранилище
- `offer_id` - id оффера
- `price` - цена
- `old_price` - цена до скидки
- `currency` - валюта
- `download_ts` - таймстемп цены
- `offer_disabled` - флаги скрытий схлопнутые в число
- `offer_disabled_ts` - таймстемп скрытий, выбирается максимальный из скрытий по источникам
- `flags` - флаги оффера, по факту используются только [11й бит](https://a.yandex-team.ru/arc/trunk/arcadia/market/library/interface/indexer_report_interface.h?rev=r9036947#L37) [has_gone](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r9004475#L127) и [31й бит](https://a.yandex-team.ru/arc/trunk/arcadia/market/library/interface/indexer_report_interface.h?rev=r9036947#L64) флаг, который указывает что оффер был вновь создан
- `flags_ts` - таймстемп флагов
- `bid` - значение ставки
- `fee` - значение комиссии
- `bid_ts` - таймстемп ставки
- `dont_pull_up_bids` - не поднимать ставку до минимальной
- `order_method` - [параметры заказа оффера](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferOrderProperties.proto?rev=r8882894#L20)
- `order_method_ts` - таймстемп параметров заказа
- `changed_states` - список, того что изменилось в оффера через запятую, некоторые возможные значения
  - `feed_price` - цена товара
  - `api_price` - API цена _сейчас не используется_
  - `api_price_deleted` - сброс API цены _сейчас не используется_
  - `amore_data`, `amore_beru_supplier_data`, `amore_beru_vendor_data` - авто стратегии
  - `offer_disabled` - скрытие
  - `offer_disabled_**` - скрытие, от конкретного источника
  - ...
- `debug` - лог, записанный в сообщения с помощью [AddDebug в doc_state](https://fcs.yandex-team.ru/?regex=AddDebug&file_regex=%5Emarket%2F.*&exclude=&more_options=no&max=500&max_results_per_file=100&branch=arcadia#!AddDebug,%5Emarket%2Fidx%2Fquick%2F.*,,arcadia,,100)

### Мониторинги
Сейчас основные мониторинги на полный пайплайн это [rty_documents_freshness](https://juggler.yandex-team.ru/aggregate_checks/?project=market.indexer&query=host%3Drty_documents_freshness_production%7Chost%3Drty_documents_freshness_prestable) на них настроены звонки дежурным. Они смотрят на превышение 50го персентилья по всем репортам. Такой низкий персентиль, что бы минимально мигать.

Сами сигналы настроены в соломоне [тут](https://solomon.yandex-team.ru/admin/projects/market-indexer/alerts/rty_documents_freshness)
Помимо этого есть [отдельный скрипт](https://a.yandex-team.ru/arc_vcs/market/idx/devtools/quick_pipelines_monitorings/main.py?rev=r8961310#L99), который создает агрегаты через juggler api c правильными тэгами.

Так же мониторингами покрыты отдельные части пайплайна, например ридлаги топиков.

## Добавление новых быстрых данных
Сейчас есть простой путь только для добавления пооферных данных.

Чеклист:
- подумать и согласовать с инфрой репорта и товарными вертикалями если их затрагивает
  - как часто данные будет меняться, поток быстрых данных это узкое место 
  - сколько они будут занимать места на репортах, памяти сейчас хватает, но она конечна
- [добавить подписку report_rty_subscriber](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/common/extension.proto?rev=r9004475#L106)
- [явно перечислить источник данных в AllowedSources](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/piper/etc/united.cfg?rev=r9076057#L162)
- поддержать данные в doc_state под флажком
  - [новый changed_state](https://a.yandex-team.ru/arc_vcs/market/idx/quick/library/doc_state/changed_state.h?rev=r8922300#L8)
  - [заполнение из DatacampOffer](https://a.yandex-team.ru/arc_vcs/market/idx/quick/library/doc_state/state.cpp?rev=r8922300#L354)
  - [запись в NSaas::TDocument](https://a.yandex-team.ru/arc_vcs/market/idx/quick/library/doc_state/state.cpp?rev=r8922300#L615)
- [написать тест на конвертацию](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/lib/united_to_report_rty_converter/ut/converter_ut.cpp?rev=r9050830#L1193)
- [поддержать чтение данных на репорте](https://a.yandex-team.ru/arc_vcs/market/report/library/rty/doc/doc.h?rev=r9035996#L22) -> данные должны прорасти на дашборде [RTYDataUpdateTime](https://stat.yandex-team.ru/Market/Infrastructure/KPI/RTYDataUpdateTime)
- [поддержать отгрузку метрик скорости доставки](https://a.yandex-team.ru/arc_vcs/market/report/library/rty/stats_logger/stats_logger.cpp?rev=r9035996#L13)
- [поддержать новые данные в парсере logfeller](https://a.yandex-team.ru/arc_vcs/logfeller/lib/log_parser/market_quick_proto_log_parser.h)

{% note warning %}

Для быстрых данных работает opt in включение. В `UnitedToReportRtyConverter` нужно явно добавить в `AllowedSources` источник данных из которого могут приходить быстрые данные. Иначе они просто молча не будут отправляться.

{% endnote %}

## Репорт
Минимальный ликбез про report, что бы в случае факапа знать куда смотреть.

### Дашборды/графики RTY
эти дашборды смотрят только на main репорт
- [production](https://yasm.yandex-team.ru/template/panel/report_and_rty_production/)
- [prestable](https://yasm.yandex-team.ru/template/panel/report_and_rty_prestable/)
- [testing](https://yasm.yandex-team.ru/template/panel/report_and_rty_testing/)

Отдельный важный график это [unistat-backend-df-receive_lag_avvv](https://yasm.yandex-team.ru/chart/itype=marketreport;hosts=ASEARCH;ctype=prestable,production;signals=quant(unistat-backend-df-receive_lag_avvv,95)/?range=7200000) он показывает задержку между записью в логброкер в контроллерах и чтением на репорте.
Если на этом графике видны большие чем обычно значения, значит репорт медленно читает и проблему стоит передать инфре репорта.

{% note tip %}

Полезно смотреть график receive_lag похостово, потому что он не учитывает открыт/закрыт ли от нагрузки репорт, закрытые репорты могут вводить в заблуждение.

{% endnote %}

### Важные особенности
У RTY внутри есть дедупликация, он смотрит на `ModificationTimestamp`(`doc_ts` в логах `logfeller`) Если ему прилетают данные с меньшим таймстемпом они откидываются.
Это осознанное решение, что бы гарантировать отсутствие гонок между разными источниками данных.

Данные в RTY хранятся не более суток. [Настройка](https://a.yandex-team.ru/arc_vcs/market/report/runtime_cloud/rty_configs/rty_config.py?rev=37ec9d886c407735e7321d24a40e40a908f5e050#L204)

Docfetcher не читает данные старше 10 часов. [Настройка](https://a.yandex-team.ru/arc_vcs/market/report/runtime_cloud/rty_configs/rty_config.py?rev=37ec9d886c407735e7321d24a40e40a908f5e050#L350)

Вне зависимости от того с какой скоростью мы пишем в топики с нашей стороны репорт читает с конечной скоростью, ради экономии CPU. [Настройка](https://a.yandex-team.ru/arc_vcs/market/report/runtime_cloud/settings/settings.py?rev=r9049181#L75)

### Черная магия
#### Дропнуть очереди чтения на репортах
Нужно в случае если из-за какого то бага репорт залило быстрыми данными и мы не хотим их считать.

Нужно сходить в ручку `/?command=set_docfetcher_timestamp` по RTY контроллера там можно указывать `age` или `timestamp`
[Код ручки](https://a.yandex-team.ru/arc_vcs/saas/rtyserver/controller/controller_commands.cpp?rev=c109af78e7de099e535adf90f0dab282caba3a1c#L221).

Базовый порт на репорте обычно 17050 или 17058, RTY контроллер [живет на +9](https://a.yandex-team.ru/arc_vcs/market/report/runtime_cloud/settings/settings.py?rev=7e11ebcb19cac78502bdc89996ebed4e73777283#L203), то есть 17059 или 17067

Для обхода хостов репорт удобно использовать [rtc_tool](https://a.yandex-team.ru/arc_vcs/market/tools/develop/rtc/rtc_tool.py)

*Пример:*
Читаем только данные за последние 10 минут на синих репортах, все старше 10 минут игнорируем
```
➜  ~ rtc_tool.py --all --env-type prod --env-type prep --report-type market exec "curl 'localhost:17059/?command=set_docfetcher_timestamp&age=600'"
```
#### Что лежит в RTY для оффера

Что бы залезть в RTY нужно указать 2 флажка.
- `&debug=1` для включения отладочной информации
- `&rearr-factors=ext_debug=1` для того, что бы она была подробнее
С этими флажками, нужно пойти в плейс `print_doc`

{% cut "Пример" %}
```bash
➜  ~ curl 'http://warehouse-report.vs.market.yandex.net:17051/yandsearch?place=print_doc&feed_shoffer_id=475690-598852.000252.90000004583&req_attrs=qdata&rearr-factors=ext_debug=1&debug=1' 2> /dev/null | jq '.documents[].properties.qdata.debug.free_data.doc_info.ERF'
{
  "precision": 7,
  "price_high": 23,
  "offer_disabled": 150994944,
  "fee": 0,
  "offer_disabled_ts": 1573503455,
  "old_price_high": 0,
  "currency": 643,
  "fee_ts": 0,
  "currency_rate": 0,
  "order_method_ts": 1573226702,
  "flags": 0,
  "price_low": 1115752192,
  "dont_pull_up_bids_ts": 0,
  "flags_ts": 1573231435,
  "order_method": 2,
  "old_price_low": 0,
  "bid_ts": 0,
  "dont_pull_up_bids": 0,
  "bid": 0
}
```
{% endcut %}

Данные которые использует репорт сейчас лежат в ERF в RTY индексе.
