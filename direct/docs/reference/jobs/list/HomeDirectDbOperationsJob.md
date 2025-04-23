## HomeDirectDbOperationsJob

### Продукт/подсистема

Выгрузка базы данных Директа в YT для внешних потребителей внутри Яндекса.


### Роль в работе продукта/подсистемы

Представляет собой набор YQL-запросов, которые берут подневные снапшоты из директории [//home/direct/mysql-sync/current](https://yt.yandex-team.ru/arnold/navigation?path=//home/direct/mysql-sync/current) в YT, производят нужные произвольные преобразования и кладут в статичные таблицы в YT, на которые смотрят внешние потребители.


### Датафлоу

- Выполняется для двух YT кластеров - `Arnold` и `Hahn`, чтобы при даунтайме одного из них, данные все равно были актуальными. Запросы в YT выполняются асинхронно - джоба не ждет их завершения, только запускает и позже проверяет результат.
- Данные читаются из таблиц подневных снепшотов в YT в директории: [//home/direct/mysql-sync](https://yt.yandex-team.ru/hahn/navigation?path//home/direct/mysql-sync).
- Данные преобразовываются в YQL-запросах.
- Затем сохраняются в директории [//home/direct/db-archive](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db-archive) (симлинк на последнюю дату - [//home/direct/db](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db).

Статусы запуска YQL-запросов по датам хранятся в таблице [//home/direct/db-archive/operations](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/direct/db-archive/operations).

Дополнительное описание есть в коде [HomeDirectDbOperationsJob.java](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/java/ru/yandex/direct/jobs/directdb/HomeDirectDbOperationsJob.java).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка на возраст выгрузки](https://juggler.yandex-team.ru/raw_events/?query=service%3Dyt-home-direct-db-export-max-age)
- [Ручной алерт в Соломоне](https://solomon.yandex-team.ru/admin/projects/direct/alerts/yt-home-direct-db-export-max-age)
- [График в Соломоне](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs-push&service=push-monitoring&l.flow=yt_direct_db&l.env=production&l.sensor=new_export_age_seconds&l.yt_cluster=arnold%7Chahn&l.host=CLUSTER&graph=auto&stack=false&downsamplingFill=none&b=1w&e=)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.HomeDirectDbOperationsJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'directdb.HomeDirectDbOperationsJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Внешние потребители перестанут получать актуальные данные от Директа.


### Как пользователи (или команда) заметят проблему и через какое время

По мониторингам свежести данных. У Директа он свой, у потребителей могут быть свои, с которыми они придут.


### Контакты разработчиков и менеджеров

Разработчики: [Максим Серебряков](https://staff.yandex-team.ru/palasonic), [Олег Юрьев](https://staff.yandex-team.ru/santama)


### Желательное время исправления в случае поломки

В течение суток.


### Способы регулирования работы джобы

- Поиск сломавшихся YQL-запросов:
  - Можно воспользоваться готовым [YQL-запросом](https://yql.yandex-team.ru/Operations/X7tvuxpqvyNgP-LCAcRuLqQk-nxeryQ9fDJHfdLkOJU=?editor_page=main) - у упавших запросов в таблице [//home/direct/db-archive/operations](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/direct/db-archive/operations) выставляется статус `ERROR` и количество попыток в поле `attempts` больше одной.

- Перезапуск запросов:
  - После того как запросы починены и правки захотфикшены в релиз java-jobs, нужно эти запросы перезапустить.
  - Для этого надо в таблице `operations` у упавших запросов проставить значение количества попыток в поле `attempts` равное 1. Если хочется перезапустить не упавший запрос, то надо еще выставить статус в поле status равный `ERROR`.
  - Пример миграции по перезапуску запросов

```
YT_TOKEN=`sudo cat /etc/direct-tokens/yt_robot-direct-yt` yt --proxy hahn select-rows "name, date, 'ERROR' as status, 1 as attempts from [//home/direct/db_new/operations] where date = '2020-10-09' and name IN ('campaigns.yql', 'autopay_settings.yql', 'bids_arc.yql', 'bids_base.yql', 'bids_dynamic.yql', 'bids_performance.yql', 'bids_retargeting.yql', 'bids.yql')" --format=json | YT_TOKEN=`sudo cat /etc/direct-tokens/yt_robot-direct-yt` yt insert-rows --proxy hahn --update --format json '//home/direct/db_new/operations'
```

```
YT_TOKEN=`sudo cat /etc/direct-tokens/yt_robot-direct-yt` yt --proxy arnold select-rows "name, date, 'ERROR' as status, 1 as attempts from [//home/direct/db_new/operations] where date = '2020-10-09' and name IN ('campaigns.yql', 'autopay_settings.yql', 'bids_arc.yql', 'bids_base.yql', 'bids_dynamic.yql', 'bids_performance.yql', 'bids_retargeting.yql', 'bids.yql')" --format=json | YT_TOKEN=`sudo cat /etc/direct-tokens/yt_robot-direct-yt` yt insert-rows --proxy arnold --update --format json '//home/direct/db_new/operations'
```

- Ppc-property `HOME_DIRECT_DB_DATE` - дата за которую будет запускаться джоб. От нее зависит какой снепшот будет выбран для запуска операций, если они еще не запущены, остальные части джобы от даты не зависят (трекинг статусов, перезапуск).
- Ppc-property `HOME_DIRECT_DB_INCLUDE` - только запросы, которые находятся в этом множестве будут запущены на новом снепшоте. Если параметр не задан или список пустой, то будут запускаться все запросы, кроме тех, которые указаны в параметре ниже.
- Ppc-property `HOME_DIRECT_DB_EXCLUDE` - эти запросы будут исключены из списка запуска.

### Известные причины поломок

Неправильный запрос.


### Дополнительно: тонкости и подводные камни
