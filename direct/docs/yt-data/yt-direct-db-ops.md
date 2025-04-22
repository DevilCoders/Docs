{% include [links](_includes/links.md) %}

# Выгрузка в YT, эксплуатация

## Графики { #graphs }
Возраст выгрузки рисуется на графиках: [ссылка](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs-push&service=push-monitoring&l.flow=yt_direct_db&l.env=production&l.sensor=new_export_age_seconds&l.yt_cluster=arnold%7Chahn&l.host=CLUSTER&graph=auto&stack=false&downsamplingFill=none&b=1w&e=).

## Алерты, мониторинги { #monitoring }
Алерт на возраст выгрузки: [ссылка](https://solomon.yandex-team.ru/admin/projects/direct/alerts/yt-home-direct-db-export-max-age).

Сырые juggler-события: [ссылка](https://juggler.yandex-team.ru/raw_events/?query=service%3Dyt-home-direct-db-export-max-age).

## Как починить { #how-to-fix }
Если загорелся мониторинг возраста выгрузки, значит хотя бы один YQL-запрос сломался.

### Поиск сломавшихся запросов { #search-broken-query }
Можно воспользоваться готовым [YQL-запросом](https://yql.yandex-team.ru/Operations/X7tvuxpqvyNgP-LCAcRuLqQk-nxeryQ9fDJHfdLkOJU=).
У упавших запросов в таблице `operations` выставляется статус `ERROR`
и количество попыток в поле `attempts` больше одной.

### Перезапуск запросов { #restart-queries }
После того как запросы починены и правки захотфикшены в релиз `java-jobs`, нужно эти запросы перезапустить.

Для этого надо в таблице `operations` у упавших запросов проставить значение количества попыток в поле `attempts` равное 1.
Если хочется перезапустить не упавший запрос, то надо еще выставить статус в поле `status` равный `ERROR`.


Пример миграции по перезапуску запросов:
```sh
# на кластере hahn
YT_TOKEN=`sudo cat /etc/direct-tokens/yt_robot-direct-yt` yt --proxy hahn select-rows "name, date, 'ERROR' as status, 1 as attempts from [//home/direct/db_new/operations] where date = '2020-10-09' and name IN ('campaigns.yql', 'autopay_settings.yql', 'bids_arc.yql', 'bids_base.yql', 'bids_dynamic.yql', 'bids_performance.yql', 'bids_retargeting.yql', 'bids.yql')" --format=json | YT_TOKEN=`sudo cat /etc/direct-tokens/yt_robot-direct-yt` yt insert-rows --proxy hahn --update --format json '//home/direct/db_new/operations'
# на кластере arnold
YT_TOKEN=`sudo cat /etc/direct-tokens/yt_robot-direct-yt` yt --proxy arnold select-rows "name, date, 'ERROR' as status, 1 as attempts from [//home/direct/db_new/operations] where date = '2020-10-09' and name IN ('campaigns.yql', 'autopay_settings.yql', 'bids_arc.yql', 'bids_base.yql', 'bids_dynamic.yql', 'bids_performance.yql', 'bids_retargeting.yql', 'bids.yql')" --format=json | YT_TOKEN=`sudo cat /etc/direct-tokens/yt_robot-direct-yt` yt insert-rows --proxy arnold --update --format json '//home/direct/db_new/operations'
```
