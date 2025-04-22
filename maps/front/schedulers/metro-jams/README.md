# Пробочный балл в метро
Service for generating and providing metro jams level

## General information

| Key | Value |
|---|---|
| ABC | https://abc.yandex-team.ru/services/maps-front-metro-jams/ |
| YDB | https://ydb.yandex-team.ru/db/ydb-ru/maps-front-metro/production/metro-jams/info |
| Reactor | https://reactor.yandex-team.ru/browse?selected=6864201 |
| Актуальные пороги в YT | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/analytics/data/metro-jams/thresholds/last |


## Monitorings

| Type | URL |
|---|---|
| Juggler | [Juggler](https://juggler.yandex-team.ru/check_details/?host=maps-front&service=%2Fmaps%2Ffront%2Fmaps%2Fmetro-jams%2Fmetro-jams-create_failure&query=&last=1DAY) |
| Solomon | [Solomon](https://solomon.yandex-team.ru/admin/projects/maps-front/alerts/_maps_front_maps_metro-jams_metro-jams-create_failure) |


## Dashboards

| Name | URL |
|---|---|
| YF | [Solomon](https://solomon.yandex-team.ru/?project=yf&service=yf+functions&cluster=prod_vla&host=cluster&dashboard=yf-function-dashboard&l.version=Total&l.jobSetPath=yql_metro-jams&b=1h&e=) |
| RTMR | [RTMR](https://rtmr.yandex-team.ru/production/accounts/maps-front-metro/overview?metricsFrom=1606307441724&locationFilter=vla&location=vla) |
| Время исполнения тасок | [Solomon](https://solomon.yandex-team.ru/?graph=auto&mode=usertime&cluster=prod&path=%2Fmaps%2Ffront%2Fmaps%2Fmetro-jams%2Fmetro-jams-create&service=prod_push&project=reactor&sensor=reaction1673247&attribute=status_running_sec) |
| Отставание сигналов в метрике | [Solomon](https://solomon.yandex-team.ru/?project=metrika&cluster=mobile-statbox-events-writer&service=core-events-writer&layer=total&metric=delay&graph=auto&queue=total&aggr=max&numberFormat=0%7C&downsamplingAggr=max&stack=true&overLinesTransform=WEIGHTED_PERCENTILE&percentiles=50,90,99,100&b=1d22h30m&e=) |
| In/Out потоки данных | [Solomon](https://solomon.yandex-team.ru/?graph=auto&project=rtmr&host=cluster&app=server&cluster=rtmr-vla&service=metrics_tasks&component=Task&sensor=*HostBytes&checks=-InputStateHostBytes%3BOutputStateHostBytes&stack=false&l.subcomponent=yql_metro-jams_reduce1&b=1d18h21m47s500ms&e=) |
| Дашборд Нирваны | [Nirvana](https://yasm.yandex-team.ru/panel/nirvana-kpi) |

## Documentation

https://a.yandex-team.ru/arc_vcs/maps/front/schedulers/metro-jams/DOC.md

## Known clients

[Веб-Метро](https://abc.yandex-team.ru/services/maps-front-metro/).
[Веб-Карты](https://abc.yandex-team.ru/services/maps-front-maps/).
[Мобильные Яндекс.Карты](https://abc.yandex-team.ru/services/mobilemaps/).

## What happens when service is down

В интерфейсе Яндекс.Карт и в мобильном приложении будет отображаться заглушка "Считаем загруженность станции" вместо пробочного балла.

## How to fix common problems

0) Поставить dt на алерт в juggler, написать, потом позвонить [дежурному](https://abc.yandex-team.ru/services/maps-front-metro-jams/duty/).

Если дежурный по какой-то причине недоступен:

1) Перейти в таску metro-jams-create в реакторе, посмотреть на последний [инстанс](https://jing.yandex-team.ru/files/astandrik/2020-11-26_02-30-46.png).
https://reactor.yandex-team.ru/browse?selected=6864201.
Если инстанс в состоянии [success](https://jing.yandex-team.ru/files/astandrik/2020-11-26_02-34-12.png), а в реакторе висит как running(или в каком-то другом статусе) - значит сломался реактор. Написать на рассылку Nirvana или в крайнем случае [дежурному по нирване]( https://abc.yandex-team.ru/services/Nirvana/duty/?role=1099).
Также можно попробовать просто поотменять долго выполняющиеся таски и посмотреть как выполняются новые.

2) Если с реактором всё ок, инстанс находится в статусе failed, покрашен в красный цвет и выглядит [как-то так](https://jing.yandex-team.ru/files/astandrik/2020-11-26_03-48-34.png)(извините, не нашёл реально упавшей таски), необходимо посмотреть что упало в самом инстансе.
В каждом блоке есть [логи ошибок](https://jing.yandex-team.ru/files/astandrik/2020-11-26_02-44-57.png)

3) Наибольшая вероятность того, что упал блок [Validate data freshness](https://jing.yandex-team.ru/files/astandrik/2020-11-26_02-49-11.png)
В таком случае необходимо посмотреть на файл в [Inputs блока во вкладке I/O](https://jing.yandex-team.ru/files/astandrik/2020-11-26_02-49-11.png).
Если данных нет или они старше 15 минут, то скорее всего что-то не так с RTMR.
Необходимо перейти на [страницу аккаунта в rtmr](https://rtmr.yandex-team.ru/production/accounts/maps-front-metro/overview?metricsFrom=1606261920746&locationFilter=sas&location=sas) и посмотреть на графики.
Если на них видны проседания Delivery time histogram или рост Discards выше нескольких сотен байт - значит сломался RTMR.
В этом случае необходимо написать в [чатик поддержки RTMR](https://t.me/joinchat/CmQ4RRRPWBrlfVgTCgb9fQ) или в крайнем случае [дежурному по сервису RTMR](https://abc.yandex-team.ru/services/RTMR/duty/).

4) Также можно зайти и посмотреть на [графики yf в соломоне](https://solomon.yandex-team.ru/?project=yf&service=yf+functions&cluster=prod_vla&host=cluster&dashboard=yf-function-dashboard&l.version=Total&l.jobSetPath=yql_metro-jams&b=1h&e=). Если там есть какие-то аномалии, то тоже написать в [чатик поддержки RTMR](https://t.me/joinchat/CmQ4RRRPWBrlfVgTCgb9fQ) или в крайнем случае [дежурному по сервису RTMR](https://abc.yandex-team.ru/services/RTMR/duty/).

5) Если с RTMR и YF всё ок и графики гладкие, возможно сломалась аппметрика.
Посмотреть, нет ли аномалий на [графиках rtmr для аппметрики](https://rtmr.yandex-team.ru/production/operations/create_logfeller_logs%3Aappmetrica_location_log/metrics?metricsFrom=1606345390645&locationFilter=vla&location=vla).
Если во всех ДЦ исчез или сильно просел трафик - написать в [чатик поддержки RTMR](https://t.me/joinchat/CmQ4RRRPWBrlfVgTCgb9fQ) или в крайнем случае [дежурному по сервису RTMR](https://abc.yandex-team.ru/services/RTMR/duty/).

6) Если с графиками аппметрики всё ок, посмотреть на графики [единого геолога](https://rtmr.yandex-team.ru/production/operations/united_geolog%3Amap_appmetrica/metrics?metricsFrom=1606345390645&locationFilter=sas&location=sas).
Если во всех ДЦ исчез или сильно просел трафик - писать в [чатик поддержки RTMR](https://t.me/joinchat/CmQ4RRRPWBrlfVgTCgb9fQ), [дежурному по сервису RTMR](https://abc.yandex-team.ru/services/RTMR/duty/) или одному из ответственных в списке "Кому писать" на [главной странице единого геолога](https://wiki.yandex-team.ru/geotargeting/geolocation-united-geolog/)

7) Если упал какой-то другой блок с какой-то странной ошибкой - написать на рассылку нирваны или в крайнем случае [дежурному по сервису NIRVANA](https://abc.yandex-team.ru/services/Nirvana/duty/?role=1099).


Полезные телеграм-чатики саппорта и ссылки на дежурства


| Key | Value | Description |
|---|---|---|
| Поддержка RTMR | https://t.me/joinchat/CmQ4RRRPWBrlfVgTCgb9fQ | Основной чатик поддержки RTMR |
| Hitman Support | https://telegram.me/joinchat/AAgzn0DGd1Qs7sX4ELiIdA | Не совсем про нирвану, но в случае массовых факапов туда часто пишут именно по нирване |
| YDB | https://t.me/joinchat/AqgqJEnmMtiBfXmAeu5HlQ | Писать по вопросам, связанным с YDB |
| Reactor | https://abc.yandex-team.ru/services/reactor/duty/ | Список дежурных по Реактору |
| Nirvana | https://abc.yandex-team.ru/services/Nirvana/duty/?role=1099 | Список дежурных по Нирване |


<details>
  <summary>Nirvana common problems</summary>
Как правило, проблемы здесь связаны с зависшими/упавшими блоками или зависшими инстансами в реакторами.

- Рассылка нирваны: nirvana@yandex-team.ru
- Главная страница нирваны: https://wiki.yandex-team.ru/nirvana/
- Дежурство по нирване: https://abc.yandex-team.ru/services/Nirvana/duty/?role=1099
- Очередь инцидентов нирваны: https://st.yandex-team.ru/NIRVANAINCIDENT
- Очередь реактора: https://st.yandex-team.ru/REACTOR
</details>

<details>
  <summary>RTMR common problems</summary>
yql over rtmr скрипты запущены от пользователя zomb-podrick@.
Для ручного оперирования ими необходимо под ним залогиниться.
Запущенные скрипты можно найти по фильтру RUNNING в [интерфейсе](https://yql.yandex-team.ru) YQL.
https://jing.yandex-team.ru/files/zomb-podrick/2020-11-25_01-38-30.png.

- Чатик поддержки в telegram: https://t.me/joinchat/CmQ4RRRPWBrlfVgTCgb9fQ
- Документация: https://docs.yandex-team.ru/rtmapreduce/yql_over_rtmr/
- ABC: https://abc.yandex-team.ru/services/RTMR/
- Главный по технологии RTMR over YQL: [slonn](https://staff.yandex-team.ru/slonnn)
- Главный по yf и сервису RTMR: [uzhas](https://staff.yandex-team.ru/uzhas)
</details>

<details>
  <summary>Примеры инцидентов</summary>
</details>
