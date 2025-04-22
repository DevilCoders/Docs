
## Старый TroubleShooting

Документация на вики https://wiki.yandex-team.ru/market/development/indexer/arxitektura-marketnogo-indeksatora/offer-repository/datacamp-trouble-shooting/

## Поменять период обхода фидов
https://st.yandex-team.ru/MBI-64507

## Поменять синхронную реплику
Можно зайти под роботом и выполнить через интерфейс.

Через комадную строчку:
```
table=//home/market/production/indexer/datacamp/united/categories; yt --proxy=markov get $table/@replicas
```
Выбрать идентификатор целевой реплики. Синхронными репликами могут быть только Сенеки.
```
yt --proxy=markov alter-table-replica 8a5a-70788-40502c5-27141cc7 --mode sync
```
- синхронные реплики трех офферных таблиц должны быть в одном кластере, чтобы работали рутины
- автоматика может вернуть реплики в другой кластер, помогает переключение сразу всех таблиц

## Перемонтировать таблицу
Перемонтировать на всех кластерах:
```
green-yeti@mi01h:~$ export YT_TOKEN_PATH=/etc/datasources/yt-market-indexer
green-yeti@mi01h:~$ table=//home/market/production/indexer/datacamp/united/categories; for i in seneca-sas seneca-vla arnold hahn; do yt --proxy=$i unmount-table $table; yt --proxy=$i mount-table $table; done
```
- проверять вывод - таблицы могут не примонтироваться, тогда требует повторения ```mount-table``

Список основных нагруженных таблиц:
```
//home/market/production/indexer/datacamp/united/basic_offers
//home/market/production/indexer/datacamp/united/service_offers
//home/market/production/indexer/datacamp/united/actual_service_offers
//home/market/production/indexer/datacamp/white/blog
```


## Запуск задачи рутин под отладчиком
```
bzz13@dev-idx01vd:~/arcadia/market/idx/datacamp/routines$ YATF_GDB=true ya make -tAF test_datacamp_united_dumper.py --test-debug
```
- проваливается в бинарник и запускает его под gdb
- использует для запуска в yatf тесте тот же env, который используется для запуска в проде

```
bzz13@dev-idx01vd:~/arcadia/market/idx/datacamp/routines$ YATF_GDB=yt ya make -tAF test_datacamp_united_dumper.py::test_export_dump_only_turbo --test-debug
```
- умеет автоматически скачивать с локального ытя все входы/выходы и после этого перезапускать джобу под отладчиком


## Обновить схему логов в логфеллере

Надо запустить [скрипт](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/update_logfeller_protos.sh?rev=r8228023) и закоммитить его изменения. Новые колонки появятся в логах через некоторое время

## Откат на бекап

Откатываемся на бекап:

{% note info %}
Сейчас бекап реализован таким образом, что после бекапа мы теряем все действия, которые проводились с хранилищем с момента создания бекапа то текущего момента
{% endnote %}

- Выбрать интересующий бекап из [доступных](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/blue/backup&)
- Остановить контейнеры [piper'a](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_datacamp_piper_blue/) (prod и prestable)
- Дернуть [ручку](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines#put-rollback_to_backup)
```
curl -XPUT 'http://datacamp-admin.white.vs.market.yandex.net/rollback_to_backup?generation=20191111_0916&reason=just_because_i_can'
```
- Ждать и смотреть логи на машинке, на которой выполняется откат


## Как переобогатить (перемайнить) все данные?

Если нужно срочно переобогатить данные всех магазинов(например, срочно забрать свежий маппинг или поколение доставки), то нужно дернуть [ручку](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines#post-mine) с параметром ```?full```
```
$ curl -XPOST https://datacamp-admin.white.vs.market.yandex.net/mine?full
```
После все включенные магазины отправятся на очередь переобогащения, размер очереди можно посмотреть, дернув ручку
```
$ curl https://datacamp-admin.white.vs.market.yandex.net/monitoring?check=check_force_count_miner_state
$ 0;There are 1 shops with "force=True", they should be touched soon: set([10369797L])
```
При этом надо понимать, что процесс переобогащения ассинхронный и после того, как все магазины отправились на перемайнинг еще не значит, что они перемайнились

Размер очереди на входе майнера можно посмотреть [тут](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-offers-to-miner?page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original&sortOrder=%22default%22)

Либо с помощью [YQL запроса](https://yql.yandex-team.ru/Operations/XsfTohpqv_MDLvk9pWMK5mYkc2dVfayeMeDhLVraDyQ=) посмотреть для оферов, когда был последний майнинг(есть лаг ~15 минут между реальным обновлением данных в динтаблице и появлении их в YQL, для сброса кеша можно сделать freeze/unfreeze таблицы(делается автоматически при сборке поколения))


## Быстрый способ переобогатить (перемайнить) много офферов

Страница перемайнинга:

* Прод: [https://datacamp-admin.white.vs.market.yandex.net/static/remine](https://datacamp-admin.white.vs.market.yandex.net/static/remine)
* Тестинг: [https://datacamp-admin.white.tst.vs.market.yandex.net/static/remine](https://datacamp-admin.white.tst.vs.market.yandex.net/static/remine)

Логика работы:
1) Подготовка таблицы на перемайнинг.
2) Запуск force перемайнинга по этой таблице.

Дополнительно можно отключить регулярный майнинг на время force перемайнинга и запретить выгружать неперемайненные оффера.

### Подготовка таблицы
*ВАЖНО! создавать таблицу нужно на кластере, где нет лага репликации или он минимален.*

#### Способ первый: сделать это через yql запрос.
Например: [yql](https://yql.yandex-team.ru/Operations/Ye-sjQVK8KlC1PwDXXgjkv6zs60WxELjzxINI2Gn0Sk=)

Таблица должна быть отсортироана по `(business_id, shop_sku, shop_id, warehouse_id)`.

Если потом хочется фильтровать *_out выгрузку нужно, чтобы в таблице было поле `last_mine`, в котором записно `offer.tech_info.last_mining.meta.timestamp.seconds`. И чтобы таблица была на хане и арнольде.

#### Способ второй: дернуть [ручку](https://docs.yandex-team.ru/market-datacamp/components/routines/admin#post-/make_offers_force_mine_table)
В ней нужно указать пути для входной/выходной таблицы, и один из параметров, по которым фильтровать оффера: версия майнера, время майнинга. Они указываются диапазоном.
В ответе вернется ссылка на sandbox джобу, в которй фильтруются оффера.

### Запуск перемайнинга по таблице
Делается ручкой mine_parallel.

Пример: `/mine_parallel?num_shards=40&yt_cluster=arnold&ids_table=//tmp/yql/krasnobaev/fa3ead6a-49257a73-5d7ef94b-10840941`

Параметры:
* `num_shards`: колличество шардов, которые отправляют оффера на перемайнинг, по дефолту 40
* `yt_cluster`: кластер, на котором лежит таблица на перемайнинг
* `ids_table`: путь к таблице на перемайнинг

### Как следить за прогрессом:
* [График force перемайнинга](https://yasm.yandex-team.ru/chart/itype=marketdatacamppiper;hosts=ASEARCH;ctype=prestable,production;signals=hcount%28unistat-force_service_mining_time_dhhh%29/)
* [Ручка в рутинах](https://datacamp-admin.white.tst.vs.market.yandex.net/docs/#/default/get_force_mine_progress) показывает сколько перемайнилось, сколько осталось, примерное время до завершения
* [Тулза](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/dev/force_mining_state_util), способ запуска: `./force_mining_state_util --token-path ./ydb_token --endpoint ydb-ru.yandex.net:2135 --coordination-node-path force_mining --ydb-path /ru/marketindexer/prod/market-indexer`

### Дополнительно можно:
* Отключить _out выгрузку неперемайненных офферов:
Для этого в конфиг рутин нужно добавить путь к ids_table и включить фильтрацию:
```
"routines": {
    "force_mine_ids_table": "<path/to/table>",
    "skip_offers_in_mine_ids_table": True
}
```

* Отключить регулярный майнинг, пока идет force перемайнинг:
Для этого в конфиг рутин добавить:
```
"routines": {
    "auto_disable_regular_mining": True
}
```
Регулярный майнинг продолжит работать после окончания force перемайнинга, либо через 6 часов после старта.






## Все очень плохо для одного партнера и я знаю, как это подхачить, как это сделать?

Тулза [update_push_offer](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/update_push_offer)

Использовать с умом при крайней необходимости

- меняем [запрос](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/update_push_offer/main.py?rev=5874698#L22), по которому необходимо достать офера
- меняем [функцию](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/update_push_offer/main.py?rev=5874698#L29) изменения конкретного офера
- далее действуем по инструкции для [тестинга](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/update_push_offer/update_offer_testing.sh) или [прода](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/update_push_offer/update_offer_prod.sh)

## Как погрепать логи сразу на всех инстансах?

```
# push-parser
sky portorun --stream "grep -r 'ERROR' logs/"  f@prestable_market_datacamp_parser_blue_sas f@prestable_market_datacamp_parser_blue_vla f@production_market_datacamp_parser_blue_sas f@production_market_datacamp_parser_blue_vla

# piper
sky portorun --stream "grep -r 'ERROR' logs/"  f@prestable_market_datacamp_piper_blue_vla f@prestable_market_datacamp_piper_blue_sas f@production_market_datacamp_piper_blue_vla f@production_market_datacamp_piper_blue_sas

# stroller
sky portorun --stream "grep -r 'ERROR' logs/"  f@prestable_market_datacamp_stroller_blue_sas f@prestable_market_datacamp_stroller_blue_vla f@production_market_datacamp_stroller_blue_sas f@production_market_datacamp_stroller_blue_vla

# miner
sky portorun --stream "grep -r 'ERROR' logs/"  f@prestable_market_indexer_datacamp_miner_blue_sas f@prestable_market_indexer_datacamp_miner_blue_vla f@production_market_indexer_datacamp_miner_blue_sas f@production_market_indexer_datacamp_miner_blue_vla

# routines
sky portorun --stream "grep -r 'ERROR' logs/"  f@prestable_market_datacamp_routines_blue_sas f@prestable_market_datacamp_routines_blue_vla f@production_market_datacamp_routines_blue_sas f@production_market_datacamp_routines_blue_vla

```

## Как перепушить фид?

{% note info %}
Надо понимать, что, в отличии от pull модели, push модель подразумевает, что за время изменения данных полностью отвечает партнер.
В push схеме нет приоритетов между различными источниками(например API цены и цены из фида) и поэтому запушив фид(просто, чтобы он перепарсился у нас) с самым свежим таймстемпом можно потерять изменения партнера

Если парнтер фид запушил и фид по каким то нашим причинам не распарсился, хотя должен был, то рекомендуется указывать явно таймстемп фида, с которым оно будет воспринято хранилищем, тем самым не потеряя более свежие изменения
{% endnote %}

Тулза [push_update_task](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/push_update_task)

```
export TVM_SECRET=<tvm_secret>
export FEED_WHID="622523,171 577379,147 530492,145"
./push_update_task --shop-id 531812 --feedurl "https://market-mbi-prod.s3.mds.yandex.net/supplier-feed/suppliers/531812/feeds/530492/data" --feeds $FEED_WHID --topic "market-indexer/prod/united/datacamp-market-update-tasks" --tvm-client-id 2011642 --timestamp 1571746065
```

## Как вычитать все данные из топика и забыть про них?

Тулза [pqtool](https://a.yandex-team.ru/arc/trunk/arcadia/market/tools/pqtool) для чтения и записи в топики.
TVM токен можно найти на любом инстансе продового окружения

```
./pqtool --host sas.logbroker.yandex.net --lb-client-id market-indexer/prod/blue/datacamp-consumer-original --only-original --mode read --output-format raw --topic market-indexer/prod/blue/datacamp-offers --tvm-client-id 2011642 --tvm-secret-path ./token_prod 1>/dev/null 2>/dev/null
./pqtool --host vla.logbroker.yandex.net --lb-client-id market-indexer/prod/blue/datacamp-consumer-original --only-original --mode read --output-format raw --topic market-indexer/prod/blue/datacamp-offers --tvm-client-id 2011642 --tvm-secret-path ./token_prod 1>/dev/null 2>/dev/null
```

Если нужно прочитать данные, распарсить их в правильном формате и просто посмотреть на них, то не нужно коммитить данные,
НО лучше смотреть данные, прошедшие через топик через logfeller(описано выше в FAQ)

```
./pqtool --host logbroker.yandex.net --lb-client-id market-indexer/prod/blue/datacamp-consumer-original --only-original --mode read --no-commit --output-format json --topic market-indexer/prod/blue/datacamp-offers --tvm-client-id 2011642 --tvm-secret-path ./token_prod --message-format Market.DataCamp.Offer 2>/dev/null | jq .
```
