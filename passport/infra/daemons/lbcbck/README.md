lbcbck
==============

Logbroker-клиент переливает данные в динамические таблицы YT.

Сборка релиза
-------------
Через `ci changelog` + `ci release --no-issue`

Сборка устаревшая
------------
В [Sandbox](https://sandbox.yandex-team.ru/scheduler/15580)

Количественные мониторинги
-------------
1) [Основные панельки](https://yasm.yandex-team.ru/menu/passport/lbcbck/stable/)
2) [Время на запись в YT - глазами YT](https://solomon.yandex-team.ru/?project=yt&cluster=hahn&service=yt_node_tablet_profiling&l.host=s*%7Cn*&l.aggregation=avg&l.sensor=yt.hydra.mutation_wait_time&l.cell_id=-&graph=auto&checks=-Aggr%3BAggr_DC_Man%3BAggr_DC_Myt%3BAggr_DC_Sas&stack=false&filter=top&filterBy=max&filterLimit=10&l.tablet_cell_bundle=passport-rt&b=1d&e=)
3) [Скорость чтения из LB](https://solomon.yandex-team.ru/?b=1d&cluster=lbk&project=kikimr&service=pqproxy_readSession&graph=auto&Account=total&scale=1d&OriginDC=cluster&host=Iva%7CMan%7CMyt%7CSas%7CVla&sensor=BytesRead&TopicPath=total&ConsumerPath=blackbox%2Flbcbck&Client=%21total&Topic=total&Producer=total)
4) [Потребление дисковой квоты](https://solomon.yandex-team.ru/?project=yt&cluster=hahn&service=accounts&l.sensor=disk_space_*&l.account=passport-rt&medium=default&graph=auto&stack=false&min=0&max=100&norm=true&b=12h&e=)
5) [Дашборд акаунта в YT](https://solomon.yandex-team.ru/?cluster=hahn&project=yt&dashboard=yt-artemis-bundle&service=yt_node_tablet_profiling&b=1h&e=&l.tablet_cell_bundle=passport-rt)

Исходники панелек в Головане лежат [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/passport/infra/tools/scripts/yasm).

Качественные мониторинги
-------------
1) [Алерты в Solomon](https://solomon.yandex-team.ru/admin/projects/passport-rt/alerts)


Куда задавать вопросы
-------------
passport-dev@yandex-team.ru
