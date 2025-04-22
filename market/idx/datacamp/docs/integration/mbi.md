
# Интеграция Datacamp и MBI

## Общее

- [Про MBI](https://wiki.yandex-team.ru/mbi/)
- [Проектная информация про мигратор](https://wiki.yandex-team.ru/users/evlyubimov/datacamp/migrator/)

## Задания на парсинг фидов

Подробное описание [тут](../market/idx/datacamp/parser/README)

## Партнерское АПИ (PAPI)

Случай, когда магазин поддерживает на своем сервере ручки для публикации цен, остатков, контента, скрытий. MBI через эти ручки получает информацию и передает ее в хранилище через топики.
- Ассортиментный топик ([пример](https://yql.yandex-team.ru/Operations/YW_1N5fFtxLpgf6pHvj0M_Mxje5p9U_4OrU9U8zxiXY=))
```
mbi/prod/assortment-market-quick
```

- Топик цен и скрытий ([пример](https://yql.yandex-team.ru/Operations/YRziTwuEI-QKYh1AkY1AulGOnbc-NQtybzXsyaMPjvs=))
```
mbi/prod/market-quick
```

## Партнерский интерфейс через MBI

Отчеты по скрытым товарам строятся на основе:
- выгрузок хранилища
  - [white_out](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/united/white_out)
  - [blue_out](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/united/blue_out)
- ошибок во время индексакции
  - [process_log](https://yql.yandex-team.ru/Operations/X3_yuRpqv9NOMvN3rumPDVRqxKnUvyxxFu-ukfKez10=)

Индексатор передает статистику индексации в MBI ([feedlog](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/library/sessions/feedlog.cpp?rev=r8204462#L287)):
- когда данные были опубликованы
- сколько данных было опубликовано
- сколько было ошибок

## Фидлоги (feedlog)

Файл, со статистикой индексации фида. Используется в MBI для показа статистики индексации в ПИ и на этапе подключения магазина.

Формируются в хранилище, при построении выгрузки. Можно посмотреть [текущие значения](https://yql.yandex-team.ru/Operations/YiDBvgVK8G9C81zKjvYTwfhapXBiv3iY2DFx-7LQbAc=).

Далее на этапе индексации статистика может модифицироваться. В результате сборки поколения получае окончательный feedlog, который можно посмотреть так:
```
evlyubimov@mi01h:/indexer/market/last_complete/input$ /usr/lib/yandex/pbsncat feedlog.mbi.result.pbuf.sn | head
feed_id: 1036
shop_id: 1380
yx_shop_name: "datacampShopStub"
download_retcode: 0
download_status: "200 OK"
parse_log: "This is fine\n"
offers_count: 86
cpa_offers_count: 0
cpa_real_offers_count: 0
offers_hosts: "stub.datacamp.ru"
```

## Добавление новых офферов

При добавлении новых офферов в Офферное Хранилище информация об этом отправляется в MBI в топик ```market-partner-status/prod/datacamp-offer-updates```.

{% note info %}

На самом деле, подписка идёт на любые изменения поля [offer_id](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferIdentifiers.proto?rev=r9166713#L30), а факт "новизны" оффера определяется уже на стороне MBI.

{% endnote %}

## Мигратор

### Процесс миграции

- Мигрирует магазин из одного бизнеса в другой.
- В миграции участвует множество сервисов маркета: MBI, PPP (psku-post-processor), MBOC (КИ), DataCamp. [Схема миграции](https://wiki.yandex-team.ru/users/emgusev/sxema-migracii/).
- Миграцию в хранилище запускает MBI (здесь и далее "мигратор") через ручку [/v1/business/lock](https://docs.yandex-team.ru/market-datacamp/components/stroller-api#blokirovka-biznesa-dlya-migracii-magazina).
- [Состояние](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/business/Business.proto?blame=true&rev=r8248827#L7) миграции сохраняется в таблцие [business_status](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/market/production/indexer/datacamp/united/business_status). Текущее состояние можно получить через ручку [/v1/business/{business_id}/status](https://docs.yandex-team.ru/market-datacamp/components/stroller-api#status-biznesa).
- Для бизнесов, которые участвуют в миграции устанавливается [lock](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/piper/lib/datacamp_message_unpacker/datacamp_message_unpacker.cpp?blame=true&rev=r8248827#L79). Все обновления будут игнорироваться ([кроме обновлений от MBI](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/stroller/lib/handlers/request.cpp?rev=r8246896#L20)). Периодический майнинг [отключен](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/tasks/sender_to_miner/sender_to_miner.cpp?rev=r8248738#L443).
- Во время миграции MBI приходт за офферами в stroller, мержит их контент: проверяет маппинги, категории, названия и пр. Если конфликтов нет, то смерженный оффер сохраняется с привязкой к новому бизнесу. Если найдены конфликты, то устанавливается [запрещающий вердикт](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/utils/united_tx_handler.cpp?rev=8249527&blame=true#L450) на базовую часть (смерженная часть все равно сохраняется). Пользователю необходимо решить конфликт и после этого MBI пришлет сообщение об отмене вердикта.
- Наиболее проблемный шаг - это отправка новых офферов (магазина под новым бизнесом) в MBOC. Дело в том, что мигратор управляет цепочкой локов во всех вышеперечисленных сервисах маркета. MBOC не отпускает lock до тех пор, пока хранилище не перешлет ему все вновь созданные офферы. А мы отправляем в MBOC только консистентные офферы. Но они становятся консистентными только после майнинга. Поэтому мы разрешаем [один майнинг](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/piper/etc/united.cfg?rev=8249527&blame=true#L181) для офферов под локом. Кроме этого, мы сразу отправляем в MBOC офферы после создания мигратором, [даже если они неконсистентны](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/lib/mboc_sender/mboc_sender.cpp?rev=r8196736#L134). Тем не менее залипание лока в этом месте возможно: покрашился пайпер и не успел отправить результат майнинга нового оффера, или mboc пролил данные. Для выхода из этой ситуации см. Troubleshooting.
- MBI завершает миграцию через ручку [/v1/business/unlock](https://docs.yandex-team.ru/market-datacamp/components/stroller-api#razblokirovka-biznesov-posle-migracii-magazina) после того, как локи сняли MBOC и PPP.
- [Через час](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/tasks/config/config.h?rev=8248827&blame=true#L86) после завершения миграции состояние бизнеса [очищается](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/tasks/business_migrator/lib/migration.cpp?rev=r8246896#L357).
- MBI дожидается публикации поколения магазина из нового бизнеса. После этого проставляются флаги [removed](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r8235519#L221) для офферов магазина в старом бизнесе. Признак удаления отправляется подписчикам (SAAS, PPP, MBOC). Офферы удаляются из таблиц [сборщиком](https://wiki.yandex-team.ru/users/evlyubimov/datacamp/cleaner/) мусора.

### Troubleshooting
1. Посмотреть стаус [бизнеса](https://docs.yandex-team.ru/market-datacamp/components/stroller-api#status-biznesa).
2. До MBOC не доехал оффер, залипла миграция.
 - Дернуть ручку отправки в MBOC:
```bash
curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/send_to_subscriber?business_id=1150981&subscriber=MBOC_SUBSCRIBER"
```
  - Если оффер не был отправлен, возможно он неконсистентный. Необходим майнинг, но он залочен. Придется снять лок в храниилще руками и отправить бизнес на перемайнинг. После перемайнинга неконсистентные станут консистентными и отпарвятся в MBOC автоматически.
3. Как снять лок в хранилище руками (нужен [tvm](https://docs.yandex-team.ru/market-datacamp/components/stroller-api#tvm)).
```
curl -XPOST --header "Content-Type: application/json" "http://datacamp.white.tst.vs.market.yandex.net/v1/business/unlock?format=json" --data '
{
  "src_business_id": 10534982,
  "dst_business_id": 10870177
}'
```
4. Завис лок на MDM, т.к. мы не отправили им оффер.
  - Дернуть ручку отправки в MDM.
```
curl -XPOST "https://datacamp-admin.white.vs.market.yandex.net/send_to_subscriber?business_id=1150981&subscriber=MDM_SUBSCRIBER"
```
5. Очистить таблицу статусов:
```
evlyubimov@mi01ht:~$ yt select-rows 'business_id FROM [//home/market/testing/indexer/datacamp/united/business_status]' --format json | yt delete-rows --table //home/market/testing/indexer/datacamp/united/business_status --format json
```
