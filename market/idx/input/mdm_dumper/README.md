# Микросервис lbdumper

## Abstract

Микросервис строился в рамках [задачи](https://st.yandex-team.ru/MARKETINDEXER-30892): по добавлению потребления ВГХ от
MDM в индексатор.

Назначение: чтение данных из различных источников (топики logbroker, статические таблицы YT и т.п.), конвертация и
последующая запись в динамические таблицы YT или другие топики logbroker.

## Рекомендации

#### Сравнить стейт записи в дампере и в mdm
1. Грепаем дневную таблицу mdm https://yql.yandex-team.ru/Operations/X5ftlpdg8tLNxZ7GLvnuO12CZKyfTdk_hxafrGc8YT8=
2. Грепаем стейт оффера в mdmdumber https://yql.yandex-team.ru/Operations/X5gg9pdg8tLNxdgtSUDS-6hXV102-ZBrGHVlmCzyWtM=
3. Актуальный стейт в mdm
```http request
http://cm-api.vs.market.yandex.net/proto/deliveryParams/searchFulfilmentSskuParams?q={warehouse_id:172,return_master_data:true,keys:[{supplier_id: 648587,shop_sku:"7930085470104"}]}
```

#### Данные в таблице некорректны. Что делать?

Удаляем таблицы и снимаем локи:
```console
evlyubimov@mi01h:~$ yt --proxy arnold remove //home/market/production/indexer/common/lbdumper/mdm
evlyubimov@mi01h:~$ yt --proxy hahn remove //home/market/production/indexer/common/lbdumper/mdm
evlyubimov@mi01h:~$ yt --proxy markov remove //home/market/production/indexer/common/lbdumper/mdm
evlyubimov@mi01h:~$ yt --proxy markov remove //home/market/production/indexer/common/lbdumper/lock/0/@timestamp
```

Идем в контейнер и перезапускаем lbdumper:
```console
pkill -9 lbdumper
```

Смотрим график записи данных MDM Item в динамическую таблицу на панели в Голован.

#### Хочу сравнить ВГХ от MDM и от SS. Как это сделать?

```console
evlyubimov@mi01v:~$ /usr/lib/yandex/market-yt-data-upload -t sku_availability_yt -i //home/market/production/mstat/dictionaries/stock_sku/1h/latest -i //home/market/production/indexer/common/lbdumper/mdm -d //tmp/evlyubimov/sku_availability_production_mdm -p arnold.yt.yandex.net -k /etc/datasources/yt-market-indexer -u market-indexer-production --threads 1
INFO: 2020-01-09 11:31:55.912 +0300 StockAvailability.cpp:268 Map stock availability to: //tmp/evlyubimov/sku_availability_production_mdm
INFO: 2020-01-09 11:31:55.913 +0300 YtHelpers.cpp:87 Creating directory //tmp/evlyubimov
INFO: 2020-01-09 11:31:56.029 +0300 YtHelpers.cpp:108 Creating the table //tmp/evlyubimov/sku_availability_production_mdm
INFO: 2020-01-09 11:31:57.509 +0300 StockAvailability.cpp:284 Start MapReduce operation https://yt.yandex-team.ru/arnold/operation?mode=detail&id=e69d324e-434e7971-41103e8-3ed1c0c3
INFO: 2020-01-09 11:33:32.672 +0300 StockAvailability.cpp:291 Stock availability MapReduce has been completed in 96 seconds
evlyubimov@mi01v:~$ /usr/lib/yandex/market-yt-data-upload -t sku_availability -i /var/lib/yandex/getter/stock_storage/recent/sku-availability.pbuf.sn -d //tmp/evlyubimov/sku_availability_production_ss -p arnold.yt.yandex.net -k /etc/datasources/yt-market-indexer -u market-indexer-production --threads 1
INFO: 2020-01-09 11:34:01.302 +0300 StockAvailability.cpp:114 Uploading stock availability to: //tmp/evlyubimov/sku_availability_production_ss
INFO: 2020-01-09 11:34:01.302 +0300 YtHelpers.cpp:87 Creating directory //tmp/evlyubimov
INFO: 2020-01-09 11:34:01.387 +0300 YtHelpers.cpp:108 Creating the table //tmp/evlyubimov/sku_availability_production_ss
INFO: 2020-01-09 11:34:31.182 +0300 StockAvailability.cpp:133 Successfully uploaded 1649829 records, it took 29 seconds
```

Сравниваем данные в полученных таблицах:
https://yql.yandex-team.ru/Operations/Xhbn4Z3udhMzBmtoBkbJghTiTAzUrmfQAdU3PJnjaDA=

## Общая информация

#### [Панели](https://st.yandex-team.ru/MARKETINDEXER-31519) в Голован

   * [production](https://yasm.yandex-team.ru/template/panel/Market_LbDumper_mdm_production/)
   * [testing](https://yasm.yandex-team.ru/template/panel/Market_LbDumper_mdm_testing/)

#### Релизный pipeline
https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/lbdumper

#### Balancers
   * [lbdumper.vs.market.yandex.net](https://st.yandex-team.ru/CSADMIN-30047)
   * [lbdumper.tst.vs.market.yandex.net](https://st.yandex-team.ru/CSADMIN-30048)

#### [Контейнеры](https://st.yandex-team.ru/MARKETINDEXER-30912) в RTC
   * [production (sas)](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_lbdumper_sas/)
   * [production (vla)](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_lbdumper_vla/)
   * [testing (sas)](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_lbdumper_sas/)
   * [testing (vla)](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_lbdumper_vla/)

## Текущая реализация

   * Чтение [топиков](https://lb.yandex-team.ru/crossdc/producer/market-mdm/topics) logbroker от MDM:
       - [production](https://lb.yandex-team.ru/crossdc/topic/market-mdm%2Fprod%2Fmdm-to-iris-records)
       - [testing](https://lb.yandex-team.ru/crossdc/topic/market-mdm%2Ftest%2Fmdm-to-iris-records)

   * Чтение дневной выгрузки данных от MDM:
       - [production](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mdm/dictionaries/reference_item/1d/latest)
       - [testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/testing/mdm/dictionaries/reference_item/1d/latest)

   * Запись ВГХ от MDM в динамическую реплицированную таблицу YT:
       - [production](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/common/lbdumper/mdm)
       - [testing](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/testing/indexer/common/lbdumper/mdm)
