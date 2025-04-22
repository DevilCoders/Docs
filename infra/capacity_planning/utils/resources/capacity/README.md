Ресурсы
===
##Capacity

Сбор данных по capacity облаков, данные собираются графом в нирване и кладутся в таблицу yt

###YP

Nirvana таск сбора capacity yp:
 - [Nirvana capacity yp](https://nirvana.yandex-team.ru/flow/4c0f2236-fcb8-4394-b07b-289bd645f172/048cf4cf-dfe1-4636-b45e-ed19afeea76c/graph)

Таблица в YT сбора capacity yp:
 - [Yt table capacity yp](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/reserves/capacity/yp/yp_add)

###GENCFG

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

###QLOUD

Nirvana таск сбора capacity qloud:
 - [Nirvana capacity qloud](https://nirvana.yandex-team.ru/flow/69be3ce9-7238-4642-bb67-79f5a2ba98c8/cb6688e0-ab95-4cba-b868-e92304e86320/graph)

Таблица в YT сбора capacity qloud:
 - [Yt table capacity qloud](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/reserves/capacity/qloud/qloud)
