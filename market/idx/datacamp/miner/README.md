# Микросервис переобогащения оферного хранилища(Miner)

Читает офера на переобогащения из топиков:
- [```market-indexer/prod/united/datacamp-offers-to-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-to-miner?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original): [logfeller](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/market-datacamp-miner-log-united), [config](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/logs/market_arnold_logs.json?rev=8134196&blame=true#L2555)
- [```market-indexer/prod/blue/datacamp-qoffers```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-qoffers?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original)

и после переобогащения пишет в выходной [топик](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-from-miner)

Статистики по работе каждого процессора в common proxy - https://yasm.yandex-team.ru/chart/itype=datacampminerwhite;ctype=production,prestable;hosts=ASEARCH;signals=unistat-CategoryTreeValidator_processed_dmmm/

В аркадии есть [скрипт](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/quick/saashub/saas_hub_monitor.html) для просмотра текущего состояния сервиса на common_proxy.
В поле ```url``` нужно вбить полный адрес хоста, на котором поднят common_proxy с портом, по которому он слушает.
Например для одного из инстансов тестинга ```sas3-7081-82f-sas-market-test--a2c-27413.gencfg-c.yandex.net:27413```

## Nanny

Miner живет в Yandex.Deploy [market-datacamp](https://deploy.yandex-team.ru/?my=no&stage=datacamp-miner)

### United

Дашборд в няне - https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_indexer_datacamp_miner_white/

Потребление ресурсов в головане - https://yasm.yandex-team.ru/template/panel/market-porto/itype=datacampminerwhite;ctype=production;prj=market/

## Deploy

### ЦУМ

https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/datacamp-miner

### Руками

1. ```ya package pkg.json```
2. ```ya upload --type=MARKET_DATACAMP_MINER_APP {tar_gz_name}```
3. go to link from prev step, click "Task ID", click "Release"->"Testing"|"Prestable"|"Production"
4. go to link from sandbox info log(```SANDBOX_RELEASE_<ID>_<ENV>```), choose services and click "Activate"


## Добавление новых процессоров

### Добавление ресурсов/файлов для работы процессора
1. ***TODO** Добавить динамический/статический sandbox-ресурс
2. Добавить ресурс [облачного data-getter-а](https://wiki.yandex-team.ru/market/sre/clouddata-getter/):
  - Добавить существующий сервис/файл в [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/sandbox-data-getter/offers-robot2.yaml)
  - Через час бандл будет пересобран по [расписанию sandbox](https://sandbox.yandex-team.ru/scheduler/8791/view)
  - После релиза ресурсов добавить [переменную в окружение](https://a.yandex-team.ru/search?search=CATEGORIES_TREE_PATH,%5Emarket%2Fidx%2Fdatacamp%2Fminer%2Fetc%2Fenv.*,j,arcadia,,5000)

### Добавление процессора
1. создать либу processor/some_enricher:
  Библиотека содержит 3 части:
  1. config:
    - структура данных, отнаследованная от `NCommonProxy::TProcessorConfig`. [Пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/miner/processors/cms_promo_enricher/config.h?rev=7437578)
    - описывает необходимые для работы поля (с дефолтными значениями), должна содержать фича-флаг включения `bool Enabled = false;`
    - описывает инициализацию своих полей из общего конфига, переопределяя метод базового класса `void DoInit(const TYandexConfig::Section& section);`. [Пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/miner/processors/cms_promo_enricher/config.cpp?rev=7437578#L5-15)
    - описывает сериализацию в строку для логирования, переопределяя метод базового класса `void DoToString(IOutputStream& so) const`. [Пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/miner/processors/cms_promo_enricher/config.cpp?rev=7437578#L17-22)
  2. processor:
    - структура данных, отнаследованная от `TDatacampBatchConverter`.
    - описывает инициализацию
    - описывает обработку пачки офферов, переопределяя метод базового класса `bool ConvertDatacampBatch(TDatacampOfferBatch& batch, NCommonProxy::IReplier::TPtr replier, TDatacampOfferBatchProcessingContext& context
    )`
  3. registrar:
    - механика регистрации конфига и процессора для `CommonProxy`
    - определяет строку для связываия типов. [Пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/miner/processors/cms_promo_enricher/registrar.cpp?rev=7437578#L7)
    - это строка должна быть использована для указания конфигов процессора в общем конфиге `miner`
2. **Добавить библиотеку в сборку bin/ya.make**
3. Добавить [настройки процессора в конфиги miner-а](https://a.yandex-team.ru/search?search=CATEGORIES_TREE_PATH,%5Emarket%2Fidx%2Fdatacamp%2Fminer%2Fetc.*cfg,j,arcadia,,5000)
4. Корректно слинковать процессоры в конфигах (`ОffersValidator` должен быть последним процессором)
