# Промо индексатор
Подсистема сбора и индексации промо-акций на маркете.

![image](https://arcanum.yandex-team.ru/api/v1/repos/arc_vcs/tree/blob/junk/eandreyf/drawio/AsyncPromo.png?commit_id=trunk)

Состоит из трёх утилит (`PromoReducer`, `PromoCollector` и `PromoMatcher`), запускающих периодические процессы сбора и преобразования информации в виде операций в системе [YT](https://yt.yandex-team.ru/docs/). Процесс запуска реализуется на основе "шедулеров" [SANDBOX](https://docs.yandex-team.ru/sandbox/), которые запускают бинарные задачи по заданному расписанию.

Выходные данные представлены в виде "вращающихся" таблиц в YT, когда название таблицы формируется на основе даты и времени запуска, при завершении операции на самую свежую таблицу ставится ссылка `recent`, а самые старые таблицы удаляются по истечению времени и/или количества таблиц.


## PromoReducer
Cобирает по-офферную информацию о промо из выгрузки офферного хранилища (например, цену по прямой скидке конкретного оффера). Для этого с помощью Map-операции сканируется офферная выгрузка из ОХ, откуда выбирается участие оффера в том или ином промо, после чего полученные данные комбинируются Reduce-ом по ключу `shop_promo_id` с "шапками" промо из выгрузки АХ. Результат - "сборные" промо-детали с длинными цепочками офферов, слишком длинные промо делятся на части, а промо не прошедшие проверку записываются в таблицу отбраковки.

[Ключи запуска](https://a.yandex-team.ru/arcadia/market/idx/promos/promo_reducer/bin/main.cpp?#L25)

[Расписания в SANDBOX](https://sandbox.yandex-team.ru/schedulers?tags=PROMO-REDUCER)

Входные таблицы (прод):
* [офферы из ОХ](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/export/filtered/recent/contract)
* [шапки промо из АХ](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/promo/backups/recent)
* [категории кэшбека](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/market-promo/partner_cashback/standard_promo_hids/current)
* [приоритеты кэшбека](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/market-promo/partner_cashback/standard_promo_properties/current)
* [группы кэшбека](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/market-promo/partner_cashback/properties/current)

Выход:
* [собранные промодетали](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/promos/datacamp_assembled_promo_details/recent)
* [отброшенные промо](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/promos/datacamp_assembled_promo_details/rejected/recent)

Мониторинги
* [[SB] Шедулеры индексатора](https://juggler.yandex-team.ru/dashboards/promo_meta_dashboard?project=market-promo)

Статистики:
* отсутствуют


## PromoCollector
Собирает готовые промо детали из множества входных таблиц одинакового формата. Применяет базовую логику ко всем деталям (контроль срока завершения, простановка автоматически генерируемых URL-ов акции). Отброшенные промо также записываются в отдельную таблицу.

[Ключи запуска](https://a.yandex-team.ru/arcadia/market/idx/promos/promo_collector/bin/main.cpp?#L25)

[Расписания в SANDBOX](https://sandbox.yandex-team.ru/schedulers?tags=PROMO-COLLECTOR)

Входные таблицы (прод):
* [промо-робот](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/gibson/promos/blue/in/recent)
* [кэшбеки](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/market-promo/market-promo/cashback/recent)
* [промокоды](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/market-promo/market-promo/promocode_coin/recent)
* [акции из АХ/ОХ](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/promos/datacamp_assembled_promo_details/recent) - от `PromoReducer`-а
* [персональные промо](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/monetize/dynamic_pricing/personal_promo/promo_for_index/latest)
* [персональные субсидии](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/monetize/dynamic_pricing/promo_subsidies_3p/promo_for_index/latest)
* [GUTGIN](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/promo/mbo_tmp)

Выход:
* [итоговые промодетали](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/promos/collected_promo_details/recent)
* [отброшенные промо](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/promos/collected_promo_details/rejected/recent) - должна быть пустой

Мониторинги
* [[SB] Шедулеры индексатора](https://juggler.yandex-team.ru/dashboards/promo_meta_dashboard?project=market-promo)
* [[IDX Promo] Здоровье промо на индексаторе](https://juggler.yandex-team.ru/dashboards/promo_meta_dashboard?project=market-promo)

Статистики:
* [тест](https://solomon.yandex-team.ru/?project=market-Promo&cluster=testing&service=promo_collector&graph=auto)
* [прод](https://solomon.yandex-team.ru/?project=market-Promo&cluster=stable&service=promo_collector&graph=auto)


## PromoMatcher
Решает задачу прямой индексации промо, т.е. для каждого оффера выдаёт список привязанных к нему акций. Для привязки использует правила описания ассортимента акции в виде набора `OffersMatchingRules`, а также вспомогательную информацию о категорийном дереве, экспресс-складах и магазинах.
Работает в двух режимах:
1. `mstat` - для аналитики, копирует офферную выгрузку, обогащая её списком привязанных промо, включая промо-фрагменты (конкретные детали участия оффера в заданном промо)
2. `idx` - для индексатора, формирует таблицу вида `offer -> [promo_keys]`, которая потом "приклеивается" к генлогам поколения индексатора - для построение `offer_promo.mmap` и промо-литералов; также формирует статистики с кол-во офферов в каждом промо

[Ключи запуска](https://a.yandex-team.ru/arcadia/market/idx/promos/promo_matcher/bin/main.cpp?#L24)

[Расписания в SANDBOX `mstat`](https://sandbox.yandex-team.ru/schedulers?tags=PROMO-ANALYST)

[Расписания в SANDBOX `idx`](https://sandbox.yandex-team.ru/schedulers?tags=PROMO-MATCHER)

Входные таблицы (прод), одинаковы для двух режимов:
* [дерево категорий](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/mbo/export/recent/tovar-tree)
* [экспресс склады](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/combinator/graph/yt_express_warehouse)
* [шопсдат](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/gibson/in/shopsdat/recent)
* [промо-детали](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/promos/collected_promo_details/recent) - от `PromoCollector`-а
* [офферы из ОХ](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/export/filtered/recent/contract)

Выход `mstat`:
* [офферы из ОХ с привязанными промо](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/mstat/dwh/staging)
* [копия промо-деталей](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/mstat/dwh/staging/stg_matching_promo_detail) - для консистентности

Выход `idx`:
* [id офферов из ОХ с привязанными промо](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/promos/offers_matched/recent)
* [копия промо-деталей](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/promos/offers_matched/promos/recent) - для консистентности
* [статистики](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/promos/offers_matched/stats) - статистики по кол-ву офферов в каждом промо

Мониторинги
* [[SB] Шедулеры индексатора](https://juggler.yandex-team.ru/dashboards/promo_meta_dashboard?project=market-promo)

Статистики:
* [тест](https://solomon.yandex-team.ru/?project=market-Promo&cluster=testing&service=promo_matcher&graph=auto)
* [прод](https://solomon.yandex-team.ru/?project=market-Promo&cluster=stable&service=promo_matcher&graph=auto)


## Исходный код и релизы
Все компоненты промо индексатора расположены в [аркадии](https://a.yandex-team.ru/arcadia/market/idx/promos) и собираются в отдельной [релизной машине](https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/market_indexer_promo).


## Аккаунты, квоты
Шедулеры в `SANDBOX` запускаются под [учётной записью робота](https://staff.yandex-team.ru/robot-promocoord).
Ключи доступа лежат в [секретнице](https://yav.yandex-team.ru/secret/sec-01fvz4v6e1zmp320f32dxpgs52/explore/versions).
Для запуска тяжёлых операций в YT используется выделенная [квота](https://abc.yandex-team.ru/services/marketpromo/folders/) гарантия на 256 ядер на каждом из продовых кластеров YT.


## Типовые проблемы и их решения
* сбой в работе шедулера
  * зайти в упавшую задачу, посмотреть логи
  * если используемый кластер YT недоступен - то ничего не делать
  * если сбой разовый/случайный, то запустить задачу заново или просто подождать
  * если не хватает памяти для YT операции - добавить в параметрах шедулера
  * пре-продовые шедулеры для `mstat` позволяют "поймать" проблему до запуска ночных задач
* если проблема требует правки кода, то после правки и коммита делается новый релиз
* если в таблице некорректные данные, то можно вручную изменить `recent` ссылку на корректную таблицу:
    * остановить шедулеры, иначе после завершения его работы ссылка снова изменится
    * изменить ссылку согласно [руководству](https://st.yandex-team.ru/PROMOGUIDE-65)
    * запустить шедулеры
    * убедиться что на выходе утилиты корректные данные
