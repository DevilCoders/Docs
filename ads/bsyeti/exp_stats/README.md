# Exp Stats

ExpStats поддерживает Monquality (`--from mq` - дефолт) и SBYT (`--from sbyt`, он же `sbyt-ch`  в старом `exp-stats`).
Время работы - 5-20с. Всегда. Поэтому кэша не существует.
В обоих случаях запрос работает через Clickhouse. В случае Monquality используется публичная клика на Hahn.

+ Для начала нужно просто собрать папку и убедиться, что YT_TOKEN либо есть в переменной окружения, либо лежит в .yt/token.
+ Для работы `--from sbyt` нужно заказать дырку от своего хоста до `bsclickhouse.yabs.yandex.ru` по портам 8123 и 9000. По аналогии с https://puncher.yandex-team.ru/?id=5d11146c0d0795266c61a505
+ Простой способ запуска:
`./exp_stats --exp 7230 --range 20190502..20190507`
Вместо 7230 можно указывать любой ExperimentID, вне зависимости от того, поиск это, рся, поведенческая система экспериментов и т.д.
+ Если это не поведенческий эксперимент, то так же нужно указать эталон:
`./exp_stats --exp 13,7296 --range 20190501..20190530 --etalon-exp 13`
+ Для просмотра результата эксперимента из АБшницы с помощью опции `--ab-exp-ticket` можно указать соответствующий тикет:
`./exp_stats --ab-exp-ticket EXPERIMENTS-54455 --range 20200915..20200921`
+ С помощью опции `--key` можно задать дополнительные разрезы:
`./exp_stats --exp 13,7296 --range 20190501..20190530 --etalon-exp 13 --key exp,slot`
+ А если хочется увидеть только конкретный `slot` или `select_type` - то можно задать значения так:
```bash
./exp_stats --exp 13,7296 --range 20190501..20190530 --etalon-exp 13 --key exp,slot --slot 1
./exp_stats --exp 7230 --range 20190502..20190507 --key exp,select_type --select_type 123,98
```

+ Если определить значение ключа, но не указать его в Keys, то это будет равносильно Grep'у. Так, например, для `--place` дефолтное значение `0,542,1542` (это имеет смысл только для `sbyt`, а для `mq` смысла не имееет).

+ Вообще, наличие некого поля `<field>` в `--key` позволяет использовать две аргумента командой строки:
	+ `--<field>` - позволяет четко зафиксировать желаемые ключи
	+ `--etalon-<field>` - при определении etalon'а для данной строки значение ключа `<field>` будет заменено на указанное в данном аргументе значение. Тут нужно быть аккуратным - важно, чтобы значение опции `--<field>` либо не было выставлено вообще, либо включало в себя `--etalon-<field>`. По умолчанию, etalon определен лишь для поведенческих экспериментов для поля `child`. Считается, что эксперимент `child=0` - это всегда дефолт. Если это не так - можно переопределить как `--etalon-child 2`
    + Для экспериментов в A/B-шнице, все разрезы запускаются как отдельный эксперимент с единственным `child`-ом равным нулю, поэтому для сравнения разных корзин эксперимента между собой, необходимо использовать `--etalon-exp`.
        - номер эксперимента в системе `20M + test_id`, где test_id - номер выборки в AB-шнице
        - эксперименты входящие в срез абшницы `--exp <csv experiments list>`
        - эталонный номер эксперимента `--etalon-exp <test_id>`
        - отношение размеров корзин `--force-ratio 1`

```bash
$ ./ads/bsyeti/exp_stats/exp_stats \
    --exp 20262061,20262062 \
    --range 20200806..20200812 \
    --from mq \
    --key exp \
    --fields clicks,cost_d \
    --keep-etalons \
    --etalon-exp 20262062 \
    --force-ratio 1
```

+ Для управления сортировкой ответа существуют опции `--order-by exp,select_type` и `--descend`.
+ Для управления набором столбиков существуют опции `--fields` а так же `--remove-fields`. Первое - список желаемых метрик, второе - список полей, которые зачем-то нужно удалить из вывода (например, если хочется удалить расшифровку select_type'а). Поддерживаются метрики как `_r`, так и `_d`. В данный момент есть набор полей `default`, который раскрывается в `default_sbyt`, либо в `default_mq` в зависимости от режима.

+ По умолчанию etalon'ые строки выкидываются из ответа, но их можно оставить с опцией `--keep-etalons`.

+ Для управления форматом вывода существует опция `--print` со значениями `pretty`, `wiki`, `tab`. Кстати, вывод в режиме `tab` полностью совместим с утилитами `tabpp` и т.п.

+ Для отключения подсчета ошибок существует `--no-errors`. Для погрешностей пока используется `--assert net` или `--assert search`. Числа взяты из assert-stats-net и assert-stats-search-all.

+ Нет необходимости управляться с ratio: размеры экспериментов будут автоматически вытащены из имени эксперимента (если он заканчивается на X%), либо из параметров Begin/End для поведенческих экспериментов. Если же возникла необходимости зафиксировать отношение экспериментов к эталону, то можно использовать опцию `--force-ratio`.

+ Опция `--sum_key <field>` создаст новые строчки, в которых будет аггрегат (сумма метрик) всех строк, где совпадают все ключи, кроме `<field>`. При чем в значение этого поля будет записана `-1`. Довольно специфическая и пока экспериментальная опция, но с её помощью можно, например, посмотреть долю всех select_type'ов от всей РСЯ:
`./exp_stats --key select_type -v --sum_key select_type --etalon-select_type total --range last_3_days --fields clicks,cost_r,clicks_r,shows_r,cpm_r,ctr_r,cpc_r,bounces_ratio_r,ctr_factor,vclicks_r --order-by cost_r --descend --remove-fields exp,exp_description,child,weight --from sbyt --force-ratio 1`


Известные проблемы:
+ Если задать несуществующий набор ключей, запрос в итоге упадет по таймауту. В CHYT какой-то баг в http проксе.
+ Не все метрики описаны - добавляйте сами или просите mikari добавить
+ ~~Нет поддержки ключа date~~ (Добавили поддержку ключей day,hour)
+ Нет тестов - ждем появления CHYT в YtStuff
+ В качестве etalon'а нельзя указать сумму двух экспериментов
+ Пока что нет человекопонятной ошибки “какие-то метрики отсутствуют за желаемые даты”.

# Сlickhouse Clique
Инструкция могла устареть, см: https://clubs.at.yandex-team.ru/yt/3975

Для работы exp_stats --from mq необходима живая клика на YT. Иногда её нужно поднимать и перезапускать, хотя обычно она переживает любые обновления YT.
Команда для подъёма:
`YT_DETACHED=1 ya tool yt clickhouse start-clique --instance-count 16 --cpu-limit 16 --spec '{clickhouse_config={"engine"={"subquery"={"max_data_weight_per_subquery"=1670000000000}}}; acl=[{subjects=[bs-read;bs;"idm-group:201326";"sankear";"idm-group:87210";"idm-group:81880"];permissions=[read;manage];action=allow;}]; title="Ads CHYT Clique";max_failed_job_count=10000; alias="*ads_chyt"; pool="ads-research"}' --cypress-geodata-path '//sys/clickhouse/geodata/geodata.tgz' --proxy hahn --operation-alias "*ads_chyt" --clickhouse-config '{engine={subquery={max_data_weight_per_subquery=1670000000000;};};}' --abort-existing`

Иногда последняя версия clique не достаточно хорошая, тогда нужно добавить путь до конкретной правильной, например так:
`--cypress-ytserver-clickhouse-path '//sys/clickhouse/bin/ytserver-clickhouse-19.5.30868-local-ya~1e79128da9+max42'`

# Clickhouse over YQL
В обоих случаях запрос работает через Clickhouse.
Запрос, который формирует exp_stats можно увидеть в режиме -verbose

Если очень хочется, то можно через yql сходить в оба инстанса Clickhouse
- mq:
  ```yql
  use chyt.hahn/ads_chyt;
  ```
  [Пример запроса mq ClickHouse over YQL](https://yql.yandex-team.ru/Operations/YDjw1AuEI3VG_fbCzj_SM_HDVGKlJh2FcZRhGJ5QfUM=)
- sbyt:
  ```yql
  use yabsclickhouse;
  ```
  [Пример запроса sbyt ClickHouse over YQL](https://yql.yandex-team.ru/Operations/YDjhI_MBw4M40ivg0AFT2CDB9zyyDFwll-_ZlbUA0pY=)

