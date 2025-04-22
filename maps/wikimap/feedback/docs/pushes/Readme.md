## Задания и пуши 

Хотим активно собирать фидбек на карту. Для этого по логам метрики пользователя смотрим, где он провёл много времени. Если можем спросить у пользователя что-то полезное про это место, то создаём ему задание в личном кабинете и шлём пуш на задание.

Все задания относятся к какому-то месту на карте. Пользователь видит соответствующий кусок карты, когда смотрит на задание в ленте.

#### Типы заданий:

тип | смысл | исходники и доки | сборка в sandbox | рассылка в sandbox |
----|-------|------------------|------------------|--------------------|
адрес | просим добавить адрес здания | [addresses](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/addresses) | [MAKE_ADDRESS_AND_SETTLEMENTS_ASSIGNMENTS_PUSHES](https://sandbox.yandex-team.ru/scheduler/696783) | [MAPS_PREPARE_UGC_PUSHES_TASK](https://sandbox.yandex-team.ru/scheduler/696847)
схема СНТ  | просим добавить схему посёлка | [addresses](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/addresses) | [MAKE_ADDRESS_AND_SETTLEMENTS_ASSIGNMENTS_PUSHES](https://sandbox.yandex-team.ru/scheduler/696567) | [MAPS_PREPARE_UGC_PUSHES_TASK](https://sandbox.yandex-team.ru/scheduler/696849)
шлагбаумы | просим проверить, правильно ли размечены шлагбаумы | [barriers](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/barriers) | ~~[MAKE_BARRIERS_PUSHES](https://sandbox.yandex-team.ru/scheduler/256740)~~ | ~~[MAPS_PREPARE_UGC_PUSHES_TASK](https://sandbox.yandex-team.ru/scheduler/696935)~~ отключили в <https://st.yandex-team.ru/NMAPS-14943>
калитки | просим проверить, правильно ли размечены калитки | [barriers](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/barriers) | ~~[MAKE_BARRIERS_PUSHES](https://sandbox.yandex-team.ru/scheduler/328491)~~ | ~~[MAPS_PREPARE_UGC_PUSHES_TASK](https://sandbox.yandex-team.ru/scheduler/696936)~~ отключили в <https://st.yandex-team.ru/NMAPS-14943>
подъезды | просим проверить, правильно ли размечены подъезды и их названия | [entrances](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/entrances) | [MAKE_ENTRANCES_PUSHES](https://sandbox.yandex-team.ru/scheduler/696207) | [MAPS_PREPARE_UGC_PUSHES_TASK](https://sandbox.yandex-team.ru/scheduler/696532)

[Как добавить новый тип задания/пуша](https://a.yandex-team.ru/arc_vcs/maps/wikimap/feedback/pushes/AddNewAssignment.md)

Сейчас задания на калитки/шлгабаумы/подъезды не собираются, т.к. не хватает доступа к табличке `//home/user_identification/homework/prod`. При необходимости восстановить генерацию данных нужно перезапросить [доступ](https://idm.yandex-team.ru/system/yt-cluster-hahn#role=37702262,f-role-id=37702262).

## Этапы процесса

#### Подготовка данных
* По ymapsdf, dwellplaces и, возможно, каким-то ещё предподготовленным табличкам смотрим, в каких местах можем спросить пользователя. Ссылки на исходники в таблице выше. Для разных типов заданий может использоваться разный набор входных таблиц.
* По логам метрики ищем активных пользователей
* Объединяем пользователей с местами по геолокации
В итоге готовы пары (пользователь, задание), про которые можем спрашивать

#### Отправка заданий в личный кабинет

Данные из таблицы с заданиями и пользователями отправляем в [личный кабинет](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Readme.md). Код отправки в [create_ugc_account_tasks](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/notification/bin/create_ugc_account_tasks)

#### Фильтрация пушей

Пуши отправляем не на все сгенерированные задания: за 1 раз заданий можем сгенерировать много, а пуш отправляем только 1.

Также не хотим рассылать пуши, если:
* пользователь явно сказал, что ему этот тип пушей не интересен: признак `useless` в логах [SUP](https://yt.yandex-team.ru/hahn/navigation?path=//home/search-functionality/sup/push_stats)
* уже отсылали такой же по содержанию пуш
* пользователь уже сделал в личном кабинете задание, которому соответствует пуш

Код в [filter_pushes](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/filter_pushes).

### Рассылка пушей

[Скрипт](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/notification/bin/send_pushes) для отправки пушей. Скрипт берёт табличку на yt с данными для пушей, готовит правильный запрос в sup и логирует результат отправки пушей. Результат нужно сохранить для последующей фильтрации. Тип отправляемых пушей `geoplatform_address_request`.

## Релизный цикл

Настроен через [ci](https://a.yandex-team.ru/projects/maps-core-feedback-geodata-surveys/ci/releases/timeline).
Для скриптов сборки каждого типа заданий заведён отдельный релиз. И ещё один релиз заведён для всех общих скриптов: фильтрация, отправка заданий, отправка пушей.
Все скрипты запускаются из sandbox-а. Каждый тип заданий готовится раз в неделю, конкретные даты хранятся в scheduler-ах.

При обновлении кода надо перевести соответствующий релиз в stable, после этого обновление подтянется в scheduler

Отдельно происходит подготовка uuid-ов релевантных пользователей:
* планировщик: https://sandbox.yandex-team.ru/scheduler/45313
* нужный бинарник prepare_uuids: ресурс [MAPS_PREPARE_UUIDS_FOR_ADDRESS_PUSHES_BINARY][https://a.yandex-team.ru/arc_vcs/sandbox/projects/nmaps/ugc_assignments/common/resources.py?rev=b8341ce3e164b983969033ed17b71f37066f37d8#L13]
* итоговые данные: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/uuids_for_pushes

## Метрики
* [Дашборд](https://datalens.yandex-team.ru/ywy6v7i0ywjyr-feedback-metrics) метрик фидбека
* [Отчет](https://stat.yandex-team.ru/Yandex/Sup/navi/push_delivery?scale=d&push_type=geoplatform_address_request&app_id=_in_table_&app_version=all&platform=all&manufacturer=all&user_active_ttl=all&testid=all&personal=all&send_main_region=Earth+(id%3A10000)&receive_main_region=Earth+(id%3A10000)&_incl_fields=push_clicked&_incl_fields=push_clicked_rate&_incl_fields=push_clicked_ratio_corrected&_incl_fields=push_delivery_rate&_incl_fields=push_dismissed&_incl_fields=push_dismissed_rate&_incl_fields=push_received&_incl_fields=push_sent&_period_distance=30) отправки пушей в нави на стороне СУП
* [Отчет](https://stat.yandex-team.ru/Yandex/Sup/mobmaps/push_delivery?scale=d&push_type=geoplatform_address_request&app_id=_in_table_&app_version=all&platform=all&manufacturer=all&user_active_ttl=all&testid=all&personal=all&send_main_region=Earth+(id%3A10000)&receive_main_region=Earth+(id%3A10000)&_incl_fields=push_clicked&_incl_fields=push_clicked_rate&_incl_fields=push_clicked_ratio_corrected&_incl_fields=push_delivery_rate&_incl_fields=push_dismissed&_incl_fields=push_dismissed_rate&_incl_fields=push_received&_incl_fields=push_sent&_period_distance=30) отправки пушей в МЯК на стороне СУП

## Полезные ссылки

* [Архитектура пушей](https://wiki.yandex-team.ru/geo/quality/documentation/pushes/)
* [Документация](https://doc.yandex-team.ru/sup-overview/) СУП.
* [Тикет](https://st.yandex-team.ru/NMAPS-11746)
* [Документация](https://doc.yandex-team.ru/sup-overview/concepts/reports.html) по логам SUP.
* [Код и документация рассылки](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/notification/)

## Общий флоу
![](pipeline.png)
