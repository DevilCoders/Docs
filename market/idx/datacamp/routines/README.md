# Микросервис периодических задач оферного хранилища(Routines)

## Deploy

Рутины полностью живут в Deploy

 - [prod](https://deploy.yandex-team.ru/stages/production_market_datacamp-routines/status/routines/)
 - [prestable](https://deploy.yandex-team.ru/stages/prestable_market_datacamp-routines/status/routines/)
 - [testing](https://deploy.yandex-team.ru/stages/testing_market_datacamp-routines/status/routines/)

## Yasm

Потребление ресурсов в головане:
 - [prod](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketdatacamproutines;ctype=production;prj=market/)
 - [prestable](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketdatacamproutines;ctype=prestable;prj=market/)
 - [testing](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketdatacamproutines;ctype=testing;prj=market/)


### ЦУМ

https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/datacamp-routines

### Руками

1. ```ya package pkg.json```
2. ```ya upload --type=MARKET_DATACAMP_ROUTINES_APP {tar_gz_name}```
3. go to link from prev step, click "Task ID", click "Release"->"Testing"|"Prestable"|"Production"
4. go to link from sandbox info log(```SANDBOX_RELEASE_<ID>_<ENV>```), choose services and click "Activate"

## HTTP API

https://docs.yandex-team.ru/market-datacamp/support/admin

## Monitorings

### *-lb-length

Размер входных очередей в сервис. [Метрика](https://logbroker.yandex-team.ru/docs/reference/metrics/#MessageLagByCommitted)

### *-lb-commit-time-lag

Отставания последнего закомиченного сообщения от текущего времени, при условии, что очередь не пустая. [Метрика](https://logbroker.yandex-team.ru/docs/reference/metrics/#CreateTimeLagMsByCommitted)

### *-lb-read-time-lag

Максимальное отставание между временем записи и временем чтения. [Метрика](https://logbroker.yandex-team.ru/docs/reference/metrics/#ReadTimeLagMs)

### *-lb-total-messages

Количество записанных сообщений за промежуток времени. [Метрика](https://logbroker.yandex-team.ru/docs/reference/metrics/#MessagesWrittenOriginal)


### check_united_1p_available_offers

Проверяет, что для 1р поставщика на есть хотя бы N не скрытых(доступных для продажи) товаров

### check_united_tables_modification_time

Проверяет, что таблицы ЕОХ менялись за последние N минут.

### check_united_out_tables_modification_time

Проверяет, что таблицы индексаторной выгрузки ЕОХ менялись за последние N минут.

### check_system_feed_service_price_freshness

Проверяет, что цена в сервисной части офферов системного фида не старее N секунд.

### check_system_api_offer_service_price_freshness

Проверяет, что цена в сервисной части оффера (обновленного через API) с price_source = PUSH_PARTNER_API не старее N секунд.

### check_system_http_offer_service_price_freshness

Проверяет, что цена в сервисной части оффера ((обновленного через HTTP ручку)) с price_source = PUSH_PARTNER_OFFICE не старее N секунд.

### check_blue_system_feed_freshness

Проверяет, что время офферов системного фида не старее N секунд.
Для случаев, когда сломалось регулярное обновление фида, можно запустить скрипт;

```market/idx/datacamp/dev/push_update_task/push_system_feed_testing.sh```

### check_blue_system_api_offer_freshness

Проверяет, что время обновления оффера (обновленного через API) с price_source = PUSH_PARTNER_API не старее N секунд.

### check_blue_system_http_offer_freshness

Проверяет, что время обновления оффера ((обновленного через HTTP ручку)) с price_source = PUSH_PARTNER_OFFICE не старее N секунд.
Для случаев, когда сломалось регулярное обновление оффера, можно отправить запрос:

```curl -XPUT 'http://datacamp.white.tst.vs.market.yandex.net/shops/10336543/offers/price?offer_id=push-monitor-check-http-price&whid=171&price.basic.binary_price.price=100000000000000&format=json'```

### check_blue_system_mining_freshness

Проверяет обновление оффера после посылки на переобогащение.

### check_system_disabled_api_united_offer_freshness

Проверяет, что время обновления оффера, обновленного через API, с disabled[i].source = PUSH_PARTNER_API не старее N секунд. [white only]

### check_system_disabled_http_united_offer_freshness

Проверяет, что время обновления оффера, обновленного через http ручку, с disabled[i].source = PUSH_PARTNER_OFFICE не старее N секунд. [white only]

### check_failed_async_jobs

Проверяет количесто ошибок в асинхронных задачах и поджигает мониторинг, если такое число будет больше заданного порога.

### check_sender_to_miner_state

Проверяет, что все магазины, которые должны отправится на переобогащение, недавно отправлялись на переобогащение

### check_force_count_miner_state

Проверяет, сколько есть магазинов, которым проставлен флажок force майнинга, и они еще не отправились на перемайнинг

### check_getter_data_freshness

Проверяет свежесть датагеттера в няне машины хранилища

### check_system_no_service_price_for_inclusive

Проверяет, что для белых офферов цена обновляется только в базовой части для INCLUSIVE режима (OfferScope).

### check_unique_verdict_hashes

Проверяет, что в таблице вердиктов все хеши уникальные (иначе просим авторов вердикта сменить строковый код, чтобы обеспечить уникальность)

### yasm дашборды с сигналами, по которым строятся мониторинги в джаглере

#### service-5ХХ

https://yasm.yandex-team.ru/template/alert/market_datacamp_stroller_blue_testing/

https://yasm.yandex-team.ru/template/alert/market_datacamp_stroller_blue_stable/

https://yasm.yandex-team.ru/template/alert/market_datacamp_stroller_white_testing/

https://yasm.yandex-team.ru/template/alert/market_datacamp_stroller_white_stable/


#### OOM, crashes

https://yasm.yandex-team.ru/template/alert/market_datacamp_ooms_and_crashes_testing/

https://yasm.yandex-team.ru/template/alert/market_datacamp_ooms_and_crashes_stable/

#### Miner exceptions (5xx)

https://yasm.yandex-team.ru/template/alert/market_datacamp_miner_stable/

https://yasm.yandex-team.ru/template/alert/market_datacamp_miner_testing/

#### SaaS alerts

https://yasm.yandex-team.ru/template/alert/market_datacamp_saas/

#### IsAlive alerts

https://yasm.yandex-team.ru/template/alert/marketindexer-datacamp-is-alive/

Количестов живых сервисов. В настоящее время лаер срабатывает по 10 процентам от регулярныйх значений.

## Tasks

### DcoUploader

Построение [таблицы](https://yt.yandex-team.ru/markov/navigation?path=//home/market/production/indexer/datacamp/united/dco&) динамического ценообразования на основе 1р оферов из хранилища

### OffersBackup

Создание бекапов оферного хранилища

[hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/blue/backup&offsetMode=key)

[arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/blue/backup&offsetMode=key)

### PartnerInfoUploader

Выгрузка push-партнеров из ```shops-utf8.dat``` в [таблицу](https://yt.yandex-team.ru/markov/navigation?path=//home/market/production/indexer/datacamp/united/partners&) ```partners``` оферного хранилища

### SenderToMiner

Посылает офера на переобогащение в [miner](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-to-miner-regular?group=own&page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&topicCluster=all%20original)

### StatsCalc

Собирает статистику о хранилище


### VerifiedOfferSender

Регулярно посылает тестовый оффер на переобогащение для проверки мониторингом **check_verified_offer_delivery_update_time**.

### Dumper

Берет basic offers и оверрайдит в нем поля из service offer и actual service offer.
Готовит таблицу с оферами для конкретного сервиса: синий индекс, белый индекс, турбо индекс.

Input tables:
  datacamp/united/basic_offers
  datacamp/united/service_offers
  datacamp/united/actual_service_offers

Output tables:
  datacamp/united/white_out
  datacamp/united/blue_out
  datacamp/united/turbo_out
  datacamp/united/direct_out
  datacamp/united/routines/verdicts

### DeliveryDiff

Готовит таблицу с разницей по вердиктам доставки (39A, 39B).
Наличие вердиктов в таблицах хранилища versus свежий расчет наличия доставки с помощью компонента NordStream

Input tables:
  datacamp/united/basic_offers
  datacamp/united/service_offers
  datacamp/united/actual_service_offers

Input components:
  GeoBase
  NordStream

Output tables:
  datacamp/united/routines/delivery_diff
