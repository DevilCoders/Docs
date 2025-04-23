---
title: Динамические Персонализированные PoI
---

## Что это?

В рамках совместной инициативы с Яндекс.Картами релизовано отображение динамических персонализированных points of interest (PoI) для отелей, в которых у пользователя есть активное бронирование.

Если пользователь совершил бронирование отеля, будучи залогиненым под яндексовым аккаунтом, то у него на мобильных яндексах картах будет подсвечен пинок этого отеля с указанием даты заезда:

![Скрин](https://jing.yandex-team.ru/files/tivelkov/dyn_poi.png)

Метка отображается, пока заказ не отменен или не прожит (т.е. метка пропадает в день выезда из отеля). 

Метки отображаются как для book-on-yandex, так и для click-out заказов (среди кликаут-партнеров на момент запуска поддержаны booking, hotelscombined, ostrovok и tvil).


## Как это устроено?

Из CPA платформы регулярно делается выгрузка активных (находящихся в статусах `pending` или `confirmed`, c датой выезда в будущем) заказов, для которых заполнено поле `label_passport_uid`, т.е. заказов, сделанных по клику авторизованного пользователя.

Для book-on-yandex-заказов для определения отеля, в который сделан заказ, используется поле `label_permalink`: для этих заказов невозможно изменение отеля на этапе бронирования, поэтому можно быть уверенным, что заказ сделан именно для того оффера, по которому кликнул пользователь (и именно пермалинк этого отеля зафиксирован в поле `label_permalink`).

Для click-out заказов возможна ситуация, при которой пользователь уходит к партнеру по одному офферу, а в итоге бронирует другой, в том числе и, возможно, в другом отеле. Для понимания, в каком отеле реально было совершено бронирование, используется поле `partner_hotel_id`, содержащее id фактически забронированного отеля в номенклатуре партнера. На этапе выгрузки активных партнеров этот id мапится в permalink с использованием таблицы `partnerid_originalid_to_cluster_permalink` из выгрузки Справочника.

Данные выгрузки регулярно строятся [sandbox_planner'ом](https://docs.yandex-team.ru/travel/services/hotels/sandbox_planner) посредством запуска планов [dynamic_poi_builder](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/sandbox_planner/plan/hotels.yaml?rev=r8437211#L726) (для BoY-заказов) и [dynamic_poi_builder_clickout](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/sandbox_planner/plan/hotels.yaml?rev=r8437211#L742) (для click-out заказов), каждый из которых запускает [run-yql утилиту](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/run_yql) с соответствующим YQL-запросом.

Результатом выгрузки являются две статических таблички YT: одна, содержащая [кликаут-заказы](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/general/dynamic_poi/active_clickout_orders), другая — [BoY-заказы](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/general/dynamic_poi/active_boy_orders). Схема обоих табличек одинаковая: каждая строка в ней соотвествует одному динамическому PoI, колонки задают его следующим образом:
  
  - `passport_uid` — паспортный идентификатор пользователя, для которого отображается poi;
  - `permalink` — пермалинк отеля;
  - `subscript` — словарь с текстами, отображаемых под PoI. Текст локализован для русского (RU) и английского (EN) языков интерфейса карт;
  - `travel_order_id` — id заказа Путешествий в нашей CPA платформы. Картами не используется, может быть использован для диагностики и ручного отключения отображения PoI на нашей стороне (см ниже).

Эти таблички зарегистрированы в конвейере Яндекс.Карт и регулярно собираются [соответствующим процессом](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/dynamic_poi/README.md).


## Operations и реагирование на жалобы пользователей

### Таблички должны генерироваться регулярно

У PoI нет никакого "времени жизни" на стороне карт. Для того, чтобы PoI по отмененному или "отжитому" заказу пропал у пользователя с карты, мы должны предоставить новую выгрузку, в которой этого PoI не будет, а значит таблички выгрузки должны генерироваться регулярно. Поэтому предполагается, что отельные дежурные будут реагировать на сообщения об ошибках запусков планов `dynamic_poi_builder` и `dynamic_poi_builder_clickout` в sandbox-planner'е (графики этих запусков в соломоне [тут](https://solomon.yandex-team.ru/?project=travel&cluster=push_prod&service=sandbox&graph=travel-sandbox-run-status&b=1d&l.plan_id=dynamic_poi_builder&checks=) и [тут](https://solomon.yandex-team.ru/?project=travel&cluster=push_prod&service=sandbox&graph=travel-sandbox-run-status&b=1d&l.plan_id=dynamic_poi_builder_clickout&checks=)) и восстанавливать процесс, если что-то сломалось в YQL-запросе или окрестностях.

### Точечное отключение PoI

Возможны сценарии, когда пользователи могут пожаловаться на отображение PoI по тем или иным причинам и захотеть, чтобы они были скрыты с карт. Для этого добавлен функционал черных списков, позволяющих:
  
  - спрятать динамические PoI во все отели для конкретного пользователя (если, например, пользователь жалуется и вообще не хочет этой фичи);
  - спрятать динамические PoI для всех пользователей для конкретного отеля (если, например, у отеля проблема с отображением локации на наших картах)
  - спрятать один конкретный динамический PoI, относящийся к конкретному заказу (если, например, случилась какая-то ошибка в CPA и пользователь жалуется, что у него заказ отображается неверно).

Для того, чтобы спрятать все PoI конкретного пользователя, необходимо добавить паспортный uid этого пользователя в табличку [blacklist_by_uid](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/general/dynamic_poi/blacklist_by_uid), выполнив (под production-токеном) следующий YQL:

    INSERT INTO hahn.`home/travel/prod/general/dynamic_poi/blacklist_by_uid`
    SELECT CAST(<паспортный id пользователя> AS uint64) AS passport_uid

Для того, чтобы спрятать все PoI в конкретный отель, необходимо добавить пермалинк этого отеля в табличку [blacklist_by_permalink](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/general/dynamic_poi/blacklist_by_permalink), выполнив (под production-токеном) следующий YQL:

    INSERT INTO hahn.`home/travel/prod/general/dynamic_poi/blacklist_by_permalink`
    SELECT CAST(<пермалинк отеля> AS uint64) AS permalink

Для того, чтобы спрятать конкретный PoI по конкретному заказу, необходимо добавить travel_order_id этого заказа в табличку [blacklist_by_order_id](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/general/dynamic_poi/blacklist_by_order_id), выполнив (под production-токеном) следующий YQL:

    INSERT INTO hahn.`home/travel/prod/general/dynamic_poi/blacklist_by_order_id`
    SELECT '<travel_order_id>' AS order_id

Значение travel_order_id можно взять или из таблички orders в CPA-платформе или выгрузки активных заказов для PoI.

### Полное отключение всех отельных PoI с карт

Если вдруг что-то идет совсем не так, то интеграцию можно быстро отключить целиком.
Для этого, в теории, можно очистить (именно очистить, а не удалить) текущие таблички активных выгрузок ([эту](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/general/dynamic_poi/active_clickout_orders), и [эту](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/general/dynamic_poi/active_boy_orders)) и остановить работу соответствующих sandbox-планнеров. Но лучше в этом случае отключать фичу целиком на уровне Яндекс.Карт. Для этого стоит обратиться к мейнтейнерам соответствующей фичи — [Maps.GeoQuality](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/).
