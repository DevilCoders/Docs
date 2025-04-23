
## MDM

- MDM = [Master Data Management](https://wiki.yandex-team.ru/market/sluzhba-rarabotki-kontenta/kontentnye-kontury/kontur-mdm/), компонент бекофиса Маркета по подготовке и управлению данными золотого качества (проверенные данные), критичными для бизнес-процессов маркетплейса с юридической и производственной точки зрения
- [abc](https://abc.yandex-team.ru/services/mbo-mdm)
- [Чаты](https://wiki.yandex-team.ru/market/development/incident-routing/#mdm/mdm)
- [Выгрузка в YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/iris/complete_reference_information/1d/latest)

## Datacamp to MDM

Поля оффера хранилища, помеченные [mdm_subscriber](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/common/extension.proto?rev=r8574143#L105) ST_TRIGGER, при изменении автоматически отправляются в топик логброкера **market-indexer/*/united/datacamp-offers-to-mdm** [prod](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-to-mdm), [testing](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-offers-to-mdm)

Пример подписки (может измениться) из [OfferStatus.proto](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=r8574144#L344):

```
optional VersionCounter master_data_version = 4 [
        (Market.mdm_subscriber) = ST_TRIGGER,
        (Market.mdm_mappings_subscriber) = ST_SHIPMENT,
        (Market.version_counter) = VDT_FOR_MDM
    ];
```

Пример поиска оффера в логфеллер-логах: [yql](https://yql.yandex-team.ru/Operations/YST6ZncszE7-lrpqnFf8hKhAD6W9gFchW08gx3jX8mc)

Подписка `mdm_subscriber` используется для основного транспорта офферных данных в МДМ. Подписка `mdm_mappings_subscriber` используется для передачи только информации о маппингах, которые читаются и обрабатываются на стороне МДМ отдельным процессом, не связанным с основным офферным транспортом. 

## MDM to Datacamp

- [Быстрая доставка данных на склад из MDM и MBO](https://wiki.yandex-team.ru/market/development/indexer/arxitektura-marketnogo-indeksatora/offer-repository/bystraja-dostavka-dannyx-na-sklad-iz-mdm-i-mbo/)
- [Карготипы](https://docs.yandex-team.ru/market-datacamp/model/cargo-types)

МДМ шлет данные для хранилища - изменения оффера и вердикты - в топик логброкера **mdm/*/datacamp/mdm-to-datacamp** [prod](https://lb.yandex-team.ru/logbroker/accounts/mdm/prod/datacamp/mdm-to-datacamp), [testing](https://lb.yandex-team.ru/logbroker/accounts/mdm/test/datacamp/mdm-to-datacamp)

Примеры поиска оффера в логфеллер-логах: [yql1](https://yql.yandex-team.ru/Operations/YP6UOguEI3xk_vNB3hbr9Ot4Wvh-XVbvbpjZkc_LgmI), [yql2](https://yql.yandex-team.ru/Operations/YWboGgVK8PKpfVL8MiCJgUlYJn45qEMxe3k8nXudojI=)

Часть полей хранится в базовом оффере, часть - в сервисном оффере. Как следствие вердикты тоже хранятся в двух частях. Типовое сообщение от МДМ: https://paste.yandex-team.ru/5652360
Сервисные поля:
- min_shipment
- partner_delivery_time
- quantum_of_supply
- supply_schedule
- transport_unit_size

## Метрики
Метрики вычитывания логброкера МДМ: [https://grafana.yandex-team.ru/d/EyppVEZnk/datacamp-mdm-logbroker?orgId=1&from=now-3h&to=now](https://grafana.yandex-team.ru/d/EyppVEZnk/datacamp-mdm-logbroker?orgId=1&from=now-3h&to=now)

## Версионирование
При изменении полей оффера, помеченных [VDT_FOR_MDM](https://a.yandex-team.ru/search?search=VDT_FOR_MDM,%5Emarket%2Fidx%2Fdatacamp%2Fproto%2Foffer.*,,arcadia,,200&repo=arc_vcs), увеличивается версия [status.version.master_data_version](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/offer/OfferStatus.proto?rev=6a19b4745a0b441a3524513bafe54214e8358260#L353).
Значение версии master_data_version отправляется вместе с подпиской в МДМ.

В ответе МДМ передает версию в поле [conten.master_data.version](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/OfferContent.proto?rev=r8699055#L1205). Причем версия передается только в базовой части и вычисляется как максимум от версии сервисных и базовой частей.

## Скрытие
МДМ передает вердикты, но не передает скрытия. Скрытия вычисляются [дампером](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/tasks/dumper/verdicts.cpp?rev=r8682560#L159) при построении поколения. Но кроме этого, применнные в поколении скрытия, [накатываются сканнером](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/scanner/etc/offers_diff_processors.cfg) на таблицы офферного хранилища для показа ошибок партнеру.
