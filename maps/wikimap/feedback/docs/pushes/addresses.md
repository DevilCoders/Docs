## Адресные пуши

Хотим активно добавлять новые адреса на карту. Для этого ищем пользователя, который много времени проводит неподалёку от здания без адреса, и отправляем ему пуш с предложением добавить адрес.
Кроме этого предлагаем пользователям добавить схему дачного посёлка, в котором пользователь проводил много времени.

## Подготовка данных

#### Подготовка зданий из ymapsdf.
Код в [prepare_buildings](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/addresses/prepare_buildings).
Из [ymapsdf][ymapsdf] для региона cis1 достаём здания. Сохраняем адресную точку для зданий, где адрес известен.

#### Отбор пользователей из логов метрики. 
Код в [prepare_uuids](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/addresses/prepare_uuids). Берём логи метрики: [общие](https://yt.yandex-team.ru/hahn/navigation?path=//logs/appmetrica-yandex-events/1d) и [навигатора](https://yt.yandex-team.ru/hahn/navigation?path=//logs/navi-metrika-mobile-log/1d) за последние 2 недели, из них оставляем уникальных пользователей:
* которые заходили в МЯК/Навигатор iOS/Android
* у которых русский язык установлен основным или с локалью "en_RU".

#### Вычисление dwellplaces.

Код в [prepare_dwellplaces](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/addresses/prepare_dwellplaces).
1. Из [ymapsdf][ymapsdf] выбираем [АТД](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/ad.html), у которых есть название, из них по названию фильтруем "не города" (СНТ/деревни и.т.п.)
2. Из табличек [dwellplaces](https://yt.yandex-team.ru/hahn/navigation?path=//home/user_identification/orgvisits/prod/state/dwellplaces/current) берём данные за последние 2 недели. Оставляем те dwellplace-ы, которые расположены на территории подходящих АТД и в которых пользователь провёл достаточно долгое время.

#### Мерж

Код в [make_pushes](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/addresses/make_pushes).
* По geohash для dwellplace-а находим расположенные рядом здания
* Для всех найденных пар с помощью данных крипты находим подходящих пользователей
* Для каждой пары __(пользователь, dwellplace)__ из списка зданий эвристиками выбираем наиболее релевантное здание без адреса.

### Фильтрация пушей

Код в [filter_pushes](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/filter_pushes).

Не хотим рассылать пуши, если пользователь явно сказал, что ему этот тип пушей не интересен (признак `useless` в логах [SUP](//home/search-functionality/sup/push_stats)). И не хотим регулярно отсылать одному и тому же пользователю пуш на одно и то же здание. Поэтому фильтруем подготовленные пуши по этим признакам.


### Подготовка релевантных пользователей
Происходит отдельно:
* планировщик: https://sandbox.yandex-team.ru/scheduler/45313
* нужный бинарник prepare_uuids: ресурс [MAPS_PREPARE_UUIDS_FOR_ADDRESS_PUSHES_BINARY][MAPS_PREPARE_UUIDS_FOR_ADDRESS_PUSHES_BINARY]
* итоговые данные: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/uuids_for_pushes

### Рассылка

Каждый из этапов подготовки данных - sandbox-таска, которая сохраняет результат в таблицу на yt. Всё это объединяет sandbox-таска [MAKE_ADDRESS_AND_SETTLEMENTS_ASSIGNMENTS_PUSHES](https://sandbox.yandex-team.ru/tasks?children=true&type=MAKE_ADDRESS_AND_SETTLEMENTS_ASSIGNMENTS_PUSHES&limit=20).
Она запускает подтаски и управляется планировщиком. Планировщик настроен на запуск раз в неделю.
* [Планировщик](https://sandbox.yandex-team.ru/scheduler/696783) для адресов
* [Планировщик](https://sandbox.yandex-team.ru/scheduler/696567) для СНТ

#### Таблицы с данными на yt:
* для адресов: [//home/maps/core/nmaps/analytics/address_pushes](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/core/nmaps/analytics/address_pushes)
* для схем СНТ: [//home/maps/core/nmaps/analytics/settlements_assignments](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/core/nmaps/analytics/settlements_assignments)

#### Релизный цикл
Для деплоя скриптов в scheduler надо в [ci](https://a.yandex-team.ru/projects/maps-core-feedback-geodata-surveys/ci/releases/timeline?dir=maps%2Fwikimap%2Ffeedback%2Fpushes%2Fentrances&id=entrances-release) зарелизить всё в стейбл: scheduler подтягивает последнюю stable версию своих ресурсов. Доступы настраиваются через [abc](https://abc.yandex-team.ru/services/maps-core-feedback-geodata-surveys/)

#### Создание заданий и рассылка пушей
* [Планировщик](https://sandbox.yandex-team.ru/scheduler/696847) для адресов
* [Планировщик](https://sandbox.yandex-team.ru/scheduler/696849) для СНТ


## Метрики
* [Дашборд](https://datalens.yandex-team.ru/ywy6v7i0ywjyr-feedback-metrics) метрик фидбека. Фильтровать надо по `client_context_id`:
  - `ugc.address_add.push_notifications`
  - `ugc.settlement_scheme.push_notifications`
* [Отчет](https://stat.yandex-team.ru/Yandex/Sup/navi/push_delivery?scale=d&push_type=geoplatform_address_request&app_id=_in_table_&app_version=all&platform=all&manufacturer=all&user_active_ttl=all&testid=all&personal=all&send_main_region=Earth+(id%3A10000)&receive_main_region=Earth+(id%3A10000)&_incl_fields=push_clicked&_incl_fields=push_clicked_rate&_incl_fields=push_clicked_ratio_corrected&_incl_fields=push_delivery_rate&_incl_fields=push_dismissed&_incl_fields=push_dismissed_rate&_incl_fields=push_received&_incl_fields=push_sent&_period_distance=30) отправки пушей в нави на стороне СУП. Надо выбирать `push_type`:
  - `geoplatform_address_request` - для пушей на адрес
  - `geoplatform_settlement_scheme` - для пушей на схему СНТ
* [Отчет](https://stat.yandex-team.ru/Yandex/Sup/mobmaps/push_delivery?scale=d&push_type=geoplatform_address_request&app_id=_in_table_&app_version=all&platform=all&manufacturer=all&user_active_ttl=all&testid=all&personal=all&send_main_region=Earth+(id%3A10000)&receive_main_region=Earth+(id%3A10000)&_incl_fields=push_clicked&_incl_fields=push_clicked_rate&_incl_fields=push_clicked_ratio_corrected&_incl_fields=push_delivery_rate&_incl_fields=push_dismissed&_incl_fields=push_dismissed_rate&_incl_fields=push_received&_incl_fields=push_sent&_period_distance=30) отправки пушей в МЯК на стороне СУП. `push_type` выбирать аналогично.

[ymapsdf]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest
[MAPS_PREPARE_UUIDS_FOR_ADDRESS_PUSHES_BINARY]: https://sandbox.yandex-team.ru/resource/2413685106/view
