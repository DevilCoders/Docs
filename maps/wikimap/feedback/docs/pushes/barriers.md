## Задания на калитки/шлагбаумы

### Сейчас отключены: <https://st.yandex-team.ru/NMAPS-14943>

Хотим собрать с пользователей фидбек на последнюю милю. Будем спрашивать у пользователей про шлагбаумы и калитки возле их дома/работы.

### Подготовка данных

Входные данные:
* ymapsdf:
  * [данные](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/)
  * [документация](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/road_cond.html?lang=ru)
* регулярные координаты дом/работа:
  * [данные](https://yt.yandex-team.ru/hahn/#page=navigation&path=//home/user_identification/homework/v2/prod/homework_puid)
  * [документация](https://wiki.yandex-team.ru/geotargeting/regulargeo/)
* отфильтрованные из логов метрики uuid-ы активных пользователей:
  * [данные](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/uuids_for_pushes)
  * [планировщик](https://sandbox.yandex-team.ru/scheduler/45313) подготовки uuid-ов
  * [исходники](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/addresses/prepare_uuids/)
  * фильтруем пользователей:
    * которые заходили в МЯК/Навигатор iOS/Android
    * у которых русский язык установлен основным или с локалью `en_RU`.
* таблицы крипты:
  * [данные](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/public/matching/by_id)
  * [документация](https://wiki.yandex-team.ru/crypta/matching/consumers/yt/matchingdesc/)


Данные готовим так:
* из ymapsdf достаём шлагбаумы и калитки с координатами
  * шлагбаумы - объекты из табилицы cond с `cond_type=5` и в `access_id` есть `auto`
  * калитки - объекты из табилицы cond с `cond_type=5`, в `access_id` есть `pedestrian`, но нет `auto`
* для этих объектов считаем geohash (с `precision=6`)
* берём пользователей, для которых знаем дом/работу
  * для них изначально знаем uid
  * join-им их с таблицами криптами, чтобы получить их uuid-ы
  * join-им их с подготовленными данными про активных пользователей, чтобы отфильтровать неактивных
  * считаем для них geohash6
* join-им получившиеся данные по geohash6
  * здесь есть точка роста: при join-е по geohash теряются объекты из смежных квадратов. По-хорошему, надо для каждого пользователя брать 8 соседниих с ним geohash-ей и join-ить для них всех
* фильтруем полученные пары (пользователь, шлагбаум/калитка) по расстоянию: оставляем только пары, где расстояние между домом(работой) пользователя и шлагбаумом(калиткой) достаточно мало
* в итоговой таблице получаем набор (пользователь, координаты пользователя, координаты шлагбаума/калитки), этого достаточно для отправки задания.
* фильтруем данные, чтобы не слать пуш пользователю, который не захотел отвечать на предыдущий/не спамить пользователя одинаковыми заданиями

### Подготовка релевантных пользователей
Происходит отдельно:
* планировщик: https://sandbox.yandex-team.ru/scheduler/45313
* нужный бинарник prepare_uuids: ресурс [MAPS_PREPARE_UUIDS_FOR_ADDRESS_PUSHES_BINARY][MAPS_PREPARE_UUIDS_FOR_ADDRESS_PUSHES_BINARY]
* итоговые данные: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/uuids_for_pushes

### Как запустить локально

Результат сборки nile на yql-бекенде - не бинарник, а python udf. По факту это `.so` файл, для запуска которого надо использовать `ya nile` или [run_python_udf](https://a.yandex-team.ru/arc/trunk/arcadia/yql/tools/run_python_udf). [Документация](https://wiki.yandex-team.ru/users/sinister/posts/nile--python3/#sborkaizarkadii). Важно помнить, что всегда надо передавать абсолютный путь к собранному `.so`.

Пример запуска:
`/home/likynushka/.ya/build/symres/7707edafef00d7d689a695705c74fded/run_python_udf /home/likynushka/.ya/build/symres/c52e99ffc5ba09555cd1ef32168b82a6/libprepare_barriers.so --output "//home/maps/core/nmaps/analytics/junk/likynushka/barriers_experiments/gates_new" --type gates`

### Рассылка

Каждый из этапов подготовки данных - sandbox-таска, которая сохраняет результат в таблицу на yt. Всё это объединяет sandbox-таска [MAKE_BARRIERS_PUSHES][MAKE_BARRIERS_PUSHES].
Она запускает подтаски и управляется планировщиком. Планировщик настроен на запуск раз в неделю.
* ~~[Планировщик](https://sandbox.yandex-team.ru/scheduler/256740) для шлагбаумов~~ отключили в <https://st.yandex-team.ru/NMAPS-14943>
* ~~[Планировщик](https://sandbox.yandex-team.ru/scheduler/328491) для калиток~~ отключили в <https://st.yandex-team.ru/NMAPS-14943>

#### Таблицы с данными на yt:
* для шлагбаумов: [//home/maps/core/nmaps/analytics/barriers_assignments](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/core/nmaps/analytics/barriers_assignments)
* для калиток: [//home/maps/core/nmaps/analytics/gates_assignments](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/core/nmaps/analytics/gates_assignments)

#### Релизный цикл
Для деплоя скриптов в scheduler надо в [ci](https://a.yandex-team.ru/projects/maps-core-feedback-geodata-surveys/ci/releases/timeline?dir=maps%2Fwikimap%2Ffeedback%2Fpushes%2Fbarriers&id=barriers-release) зарелизить всё в стейбл: scheduler подт]гивает последнюю stable версию своих ресурсов. Доступы настраиваются через [abc](https://abc.yandex-team.ru/services/maps-core-feedback-geodata-surveys/)

#### Создание заданий и рассылка пушей
* ~~[Планировщик](https://sandbox.yandex-team.ru/scheduler/696935) для шлагбаумов~~ отключили в <https://st.yandex-team.ru/NMAPS-14943>
* ~~[Планировщик](https://sandbox.yandex-team.ru/scheduler/696936) для калиток~~ отключили в <https://st.yandex-team.ru/NMAPS-14943>


## Метрики
* [Дашборд](https://datalens.yandex-team.ru/ywy6v7i0ywjyr-feedback-metrics) метрик фидбека. Фильтровать надо по `client_context_id`:
  - `ugc.gate_edit.push_notifications`
  - `ugc.barrier_edit.push_notifications`
* [Отчет](https://stat.yandex-team.ru/Yandex/Sup/navi/push_delivery?scale=d&push_type=geoplatform_barrier_edit&app_id=_in_table_&app_version=all&platform=all&manufacturer=all&user_active_ttl=all&testid=all&personal=all&send_main_region=Earth+(id%3A10000)&receive_main_region=Earth+(id%3A10000)&_incl_fields=push_clicked&_incl_fields=push_clicked_rate&_incl_fields=push_clicked_ratio_corrected&_incl_fields=push_delivery_rate&_incl_fields=push_dismissed&_incl_fields=push_dismissed_rate&_incl_fields=push_received&_incl_fields=push_sent&_period_distance=30) отправки пушей в нави на стороне СУП. Надо выбирать `push_type`:
  - `geoplatform_barrier_edit` - для шлагбаумов
  - `geoplatform_gate_edit` - для калиток
* [Отчет](https://stat.yandex-team.ru/Yandex/Sup/mobmaps/push_delivery?scale=d&push_type=geoplatform_barrier_edit&app_id=_in_table_&app_version=all&platform=all&manufacturer=all&user_active_ttl=all&testid=all&personal=all&send_main_region=Earth+(id%3A10000)&receive_main_region=Earth+(id%3A10000)&_incl_fields=push_clicked&_incl_fields=push_clicked_rate&_incl_fields=push_clicked_ratio_corrected&_incl_fields=push_delivery_rate&_incl_fields=push_dismissed&_incl_fields=push_dismissed_rate&_incl_fields=push_received&_incl_fields=push_sent&_period_distance=30) отправки пушей в МЯК на стороне СУП. `push_type` выбирать аналогично.

[ymapsdf]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest
[MAKE_BARRIERS_PUSHES]: https://sandbox.yandex-team.ru/tasks?children=true&type=MAKE_BARRIERS_PUSHES
[MAPS_PREPARE_UUIDS_FOR_ADDRESS_PUSHES_BINARY]: https://sandbox.yandex-team.ru/resource/2413685106/view
