# Утилита подготовки рекламных фидов market-banner-models-ex
Утилита предназначена для создания фидов для баннерокрутилочных систем. Под фидом понимается xml файл, содержащий офферы (модели). Фид может содержать несколько частей (файлов).
Утилита создана на основе market-banner-models для решения задачи разбиения фида на части согласно новой стратении: в каждую часть помещать оффера заданных категорий.

Пример вызова
```
/usr/lib/yandex/market-banner-models-ex 
-i //home/market/testing/indexer/stratocaster/out/banner/blue_offers/20200315_0649
-c //home/market/testing/indexer/stratocaster/in/categories/20200315_0649
-o /var/lib/yandex/indexer/market/20200315_0649/banner/k50-base-blue-bulky-all.xml
-p arnold.yt.yandex.net
-t /etc/datasources/yt-market-indexer
-u market-indexer-testing
-f blue-offers
-l /var/lib/yandex/indexer/market/20200315_0649/log/banner_blue-offers.log
--use-partition True
--is_bulky True
--use-partition-by-field
--partition-config /var/lib/yandex/indexer/market/20200315_0649/banner/partition_configs/k50-base-blue-bulky-all.xml
--feed-parts-stats /var/lib/yandex/indexer/market/tmp/banner_parts_stats_20200315_0649_k50-base-blue-bulky-all.xml.json
```

```-i``` - [in] таблица с офферами, из которой берётся информация об офферах,

```-c``` - [in] таблица с категориями,

```-o``` - [out] путь к создаваемому файлу фида. Фид может содержать несколько частей. В этом случае имя файла в этом пути будем модифицировано и будет включать общее количество частей и номер части (начиная с 1). Например ```k50-base-blue-not_bulky-all-5-part2.xml``` (всего 5 частей, часть 2),

```-p -t -u``` - [in] параметры, задающие доступ к YT,

```-l``` - [out] путь к файлу лога,

```-f``` - [in] тип фида (определяет что икак записывается в выходной файл),

```--use-partition``` - [in] разбивать фид на части,

```--is_bulky``` - [in] флаг, специфичный для типа фида ```blue-offers``` и задающий фильтрацию входной таблицы,

```--use-partition-by-field``` - [in] складывать офферы в части согласно маппингу split_field_value->part_id, задаваемому в конфиге разбиения

```--partition-config``` - [in] путь к файлу конфига разбиения. Готовится с помощью утилиты prepare_partition, либо руками.

```--feed-parts-stats``` - [out] путь к создаваемому файлу со статистикой частей фида (предполагается отправлять в solomon чтобы мониторить размер частей)
