Здесь суммируется экспертиза полученная в ходе работы над компонентой, а также различного рода советы и инструменты.

# Процедура добавления нового типа действия ставки PLACE

*generate.groovy* - groovy-скрипт для генерации исходников при добавлении нового Place (кодогенератор)

Чеклист:

- добавить в [протокол обмена с Индексатором](https://svn.yandex.ru/market/proto/trunk/bidding_exchange.proto) новый тип Place
- [собрать новую версию ru.yandex.market-proto](https://svn.yandex.ru/market/libraries/trunk/protobuf-compiler/) и опубликовать в maven-репозиторий
- изменить в mbi-bidding-common/ivy.xml версию для нового ru.yandex.market-proto 
- добавить новый тип в enum-класс Place
- запустить кодогенератор *generate.groovy*
- в классе AuctionResultStorage в методе validate убедиться, что хватает места для всех Place
- в классе N0Bid убедиться что хватает места в поле flags для всех Place
- учесть новый тип в классе BiddingRemoteAuctionService, константа SQL_AUCTION_BID_EFFECTIVE
- скомпилировать mbi-bidding
- добавить тесты с участием нового Place
- прогнать тесты на mbi-bidding-common, mbi-bidding
- собрать пакет mbi-bidding
- добавить SQL-скрипты в mbi-db для нового Place (auction_offer_bid, auction_category_bid)
- учесть новый place в приборах

# Чтение protobuf-файла

*prototext.sh* - выводит protobuf-файл (полученный через Exchange API) в текстовый вид (JSON)

Например,

```
prototext.sh <path-to-exchange-proto-file>
```

*proto.groovy* - groovy-скрипт используемый скриптом prototext.sh

# Нагрузочное тестирование

Папка tank - скрипты для создания ленты для нагрузочного тестирования (см. README.md).

# Тестирование failover-механизма

Папка stress - скрипты для тестирования failover-механизма (см. README.txt).

# Приборы и мониторинг

Для тестинга приборы можно взять те, что используются для нагрузочного тестирования (см. *tank/README.md*).

Для продакшн приборы можно посмотреть на дашборде телевизора в комнате группы разработки MBI.

Исходники в git:market/chrot, где надо смотреть файл pages/mbi-bidding.html.

## Метрики на основе лога Nginx

Логи Nginx используются для построения различных метрик, в т.ч. таймингов и rps.

Построение и публикация метрик на *market-graphite* выполняется парсером *logshatter* и инструментом *clickphite*.

[Парсер logshatter для bidding](https://github.yandex-team.ru/cs-admin/market-health/blob/master/config-cs-logshatter/src/43_mbidding_nginx.json) использует логи nginx для извлечения информации.

Данные попадают в *clickhouse* после парсинга.

Для построения и публикации метрик в *market-graphite* используется *clickphite*.

Метрики определяются конфигами кликфита, как например это сделано для [rps и таймингов](https://github.yandex-team.ru/cs-admin/market-health/blob/master/config-cs-clickphite/src/market_bidding_dynamic.json). 

Для соответствия каждой сервисной операции Bidding API своего идентификатора *page_id* используется мэтчинг в файле *market_bidding_routes.tsv*, который выложен в [общедоступное место](https://market-mbi-prod.s3.mds.yandex.net/routes/market-bidding-routes) в *MDS-S3*.

Мэтчинг прописывается в файле [page-matcher.properties](https://github.yandex-team.ru/market-infra/market-health/blob/master/config-cs-logshatter/src/configs/page-matcher.properties).

Кликфит по заданным конфигурациям строит метрики и публикуют их на *market-graphite*.
 
При добавлении новой операции в Bidding API следует изменить файл market_bidding_routes.tsv, а затем перезалить его на MDS-S3  c любого хоста с помощью команды: 

```
aws --endpoint-url=http://s3.mds.yandex.net --region=us-east-1 s3 --profile=prod cp market_bidding_routes.tsv s3://market-mbi-prod/routes/market-bidding-routes
```
Нужные креденшилы можно взять в [репе](https://github.yandex-team.ru/market-java/mbi-tools/tree/master/s3)

Убедиться, что возвращается корректно его содержимое по урлу:
```
https://market-mbi-prod.s3.mds.yandex.net/routes/market-bidding-routes
```
 
# Тюнинг GC

Был впервые проведен в рамках работы над задачей [MBI-12506](https://st.yandex-team.ru/MBI-12506).

В комментариях к указанному тикету приводятся размышления в пользу выбора тех или иных параметров JVM.

Там же есть первые логи GC по которым можно проводить сравнение с имеющимися логами.

## Подборка статей для понимания работы и настройки CMS GC

[Java GC Handbook](https://plumbr.eu/java-garbage-collection-handbook)

[Сборщик мусора Concurrent Mark-Sweep](https://blogs.oracle.com/vmrobot/entry/%D1%81%D0%B1%D0%BE%D1%80%D1%89%D0%B8%D0%BA_%D0%BC%D1%83%D1%81%D0%BE%D1%80%D0%B0_concurrent_mark_sweep)

[Рецепты для больших хипов включая понимание демографии](https://dzone.com/articles/how-tame-java-gc-pauses)

[Фрагментация хипа](http://blog.ragozin.info/2011/10/java-cg-hotspots-cms-and-heap.html) и 
[эксперименты](http://blog.ragozin.info/2011/10/cms-heap-fragmentation-follow-up-1.html)

CMS GC log [здесь](http://xmlandmore.blogspot.ru/2013/04/understanding-cms-gc-logs.html), 
[здесь](https://blogs.oracle.com/poonam/entry/understanding_cms_gc_logs) и 
[здесь](https://blogs.oracle.com/jonthecollector/entry/the_unspoken_cms_and_printgcdetails), а также 
[тут](http://www.cubrid.org/blog/dev-platform/understanding-java-garbage-collection/)

[Матан](http://blog.ragozin.info/2011/06/understanding-gc-pauses-in-jvm-hotspots.html) и его 
[продолжение](http://blog.ragozin.info/2011/06/understanding-gc-pauses-in-jvm-hotspots_02.html)

[Cheat sheet](http://blog.ragozin.info/2013/11/hotspot-jvm-garbage-collection-options.html)

[Опыт LinkedIn по тюнингу GC](https://engineering.linkedin.com/garbage-collection/garbage-collection-optimization-high-throughput-and-low-latency-java-applications)

[Очень популярно про тюнинг GC](https://plumbr.eu/handbook/gc-tuning-in-practice)
 
### Инструменты
[Визуализатор логов GC - GCViewer](https://github.com/chewiebug/GCViewer)

Лог GC пишется в /var/log/auction/gc.log

В директории *gc* полезные скрипты (см. файл README.md).
 
[Набор инструментов для решения проблем JMV, мониторинга и профилирования](https://github.com/aragozin/jvm-tools)
