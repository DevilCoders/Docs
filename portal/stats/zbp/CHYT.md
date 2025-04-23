# CH over YT

Данные метрик могут храниться в YT на кластере Hahn по адресу [hahn://home/portal_zbp_and_stats/production/zbp](https://yt.yandex-team.ru/hahn/navigation?path=//home/portal_zbp_and_stats/production/zbp).

Для быстрой работы графиков лучше запустить [ClickHouse over YT](https://yt.yandex-team.ru/docs/description/chyt/about_chyt.html) или [Клику](https://yt.yandex-team.ru/hahn/operations?user=robot-portal-stats&state=running&type=vanilla).

Для запуска Клики нужно выполнить команду:
```sh
YT_TOKEN={robot-portal-stats yt_token} yt --proxy hahn start-clickhouse-clique --instance-count 18 --spec '{title="Clickhouse clique for portal_zbp_and_stats"; owners=[portal_zbp_and_stats]; alias="*portal_zbp_and_stats_clique"}'
```

**Важно**: alias должен быть именно `*portal_zbp_and_stats_clique`, он используется в настройках [коннекта](https://stat.yandex-team.ru/connections/6nhixy9h8mhu3).

Клика иногда может превратиться в тыкву или совсем умереть, например, при штатных работах YT. Об этом обязательно сообщат. Или не сообщат, но графики перестанут обновляться, потому что [коннект](https://stat.yandex-team.ru/connections/6nhixy9h8mhu3) в борде сделан до клики. Клику-тыкву нужно убить, нажав кнопку Abort в интерфейсе YT, и запустить новую.
