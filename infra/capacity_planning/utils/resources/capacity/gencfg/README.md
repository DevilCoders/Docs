Ресурсы
===
##Capacity

Сбор данных по ресурсам gencfg, данные собираются графом в нирване и кладутся в таблицу yt.

В capacity попадают данные из всех групп, в quota входят строки, которые не относятся к группам reserve_groups и dynamic_groups:

reserve_groups = ["MSK_RESERVED",
                  "VLA_RESERVED",
                  "SAS_RESERVED",
                  "MAN_RESERVED",
                  "RESERVE_SELECTED",
                  "RESERVE_UPDATE",
                  "RESERVE_BAD"]

dynamic_groups = ["ALL_DYNAMIC",
                  "ALL_PERSONAL",
                  "ALL_SOX"]

Nirvana таск сбора данных по gencfg:
 - [Nirvana gencfg](https://nirvana.yandex-team.ru/flow/3c9c2275-c885-45aa-8635-525819023f75/d5f16401-8556-4463-9a91-fccb5d02f22d/graph)

Таблица в YT сбора данных по gencfg:
 - [Yt table gencfg](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/reserves/gencfg/gencfg_add)
