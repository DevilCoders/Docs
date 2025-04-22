# Задания на подъезды

Хотим у пользователей спрашивать про подъезды возле мест, в которых они провели какое-то время.

## Подготовка данных

Во многом пересекается с [заданиями на шлагбаумы](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/barriers). [Подготовка пользователей](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/barriers/prepare_users) оттуда использована в неизменном виде.

### Подготовка подъездов и зданий

- Берём картографические объекты ([`ft`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/ft)) и оставляем из них только подъезды (`ft_type_id == 1904`).
- Список подъездов джоиним с [`ft_nm`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/ft_nm), [`ft_center`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/ft_center) и [`node`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/node). Так получаем подъезды с названиями (возможно отсутствующими) и координатами.
- Соединяем список подъездов с [`ft_addr`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/ft_addr) и [`bld_addr`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/bld_addr), таким образом сопоставляя подъезды и здания.
- Приджоиниваем [`bld_geom`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest/cis1/bld_geom) с координатами зданий.
- Соединяем всё вместе, сливая подъезды одного здания в один Yson и вычисляя geohash точности 6.

### Объединение зданий и пользователей

- Объединение делаем по geohash длины 6.
- Убираем пары (здание, пользователь), если между его dwellplace и зданием слишком большое расстояние (40 метров).
- Оставляем уникальные строки по ключу (здание, пользователь).
- Для таблицы с пушами для каждого пользователя берём ближайшее здание.
- Для таблицы с заданиями для каждого здания сливаем всех соответствующих ему пользователей в один список.

Итоговое использование состоит из трёх этапов:

- [prepare_entrances](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/entrances/prepare_entrances)
- [prepare_users](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/barriers/prepare_users)
- [join_users_with_entrances](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/entrances/join_users_with_entrances)

[Пример запуска](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/pushes/barriers#kak-zapustit-lokalno) одного этапа.

## Регулярный запуск

Подготовка данных запускается в sandbox:
* [Scheduler](https://sandbox.yandex-team.ru/scheduler/696207) сборки данных: запускается раз в неделю по вторникам
* Для деплоя скриптов в scheduler надо в [ci](https://a.yandex-team.ru/projects/maps-core-feedback-geodata-surveys/ci/releases/timeline?dir=maps%2Fwikimap%2Ffeedback%2Fpushes%2Fentrances&id=entrances-release) зарелизить всё в стейбл: scheduler подт]гивает последнюю stable версию своих ресурсов.
* [Результаты](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/entrances_assignments) сборок и рассылок на yt.
* [Scheduler](https://sandbox.yandex-team.ru/scheduler/696532) для рассылки заданий и пушей: запускается раз в неделю по средам. В нём сначала рассылаются задания в ugc account, потом из заданий отфильтровываются задания для пушей и результат рассылается в пушах.
* Релизится через тот же [ci](https://a.yandex-team.ru/projects/maps-core-feedback-geodata-surveys/ci/releases/timeline?dir=maps%2Fpoi%2Fnotification&id=send-ugc-notification-release).
* Доступы в ci настраиваются через abc [maps-core-feedback-geodata-surveys](https://abc.yandex-team.ru/services/maps-core-feedback-geodata-surveys)

## Метрики
* [Дашборд](https://datalens.yandex-team.ru/ywy6v7i0ywjyr-feedback-metrics) метрик фидбека. Фильтровать надо по `client_context_id`=`ugc.entrances_edit.push_notifications`
* [Отчет](https://stat.yandex-team.ru/Yandex/Sup/navi/push_delivery?scale=d&push_type=geoplatform_entrances_edit&app_id=_in_table_&app_version=all&platform=all&manufacturer=all&user_active_ttl=all&testid=all&personal=all&send_main_region=Earth+(id%3A10000)&receive_main_region=Earth+(id%3A10000)&_incl_fields=push_clicked&_incl_fields=push_clicked_rate&_incl_fields=push_clicked_ratio_corrected&_incl_fields=push_delivery_rate&_incl_fields=push_dismissed&_incl_fields=push_dismissed_rate&_incl_fields=push_received&_incl_fields=push_sent&_period_distance=30) отправки пушей в нави на стороне СУП.
* [Отчет](https://stat.yandex-team.ru/Yandex/Sup/mobmaps/push_delivery?scale=d&push_type=geoplatform_entrances_edit&app_id=_in_table_&app_version=all&platform=all&manufacturer=all&user_active_ttl=all&testid=all&personal=all&send_main_region=Earth+(id%3A10000)&receive_main_region=Earth+(id%3A10000)&_incl_fields=push_clicked&_incl_fields=push_clicked_rate&_incl_fields=push_clicked_ratio_corrected&_incl_fields=push_delivery_rate&_incl_fields=push_dismissed&_incl_fields=push_dismissed_rate&_incl_fields=push_received&_incl_fields=push_sent&_period_distance=30) отправки пушей в МЯК на стороне СУП.
