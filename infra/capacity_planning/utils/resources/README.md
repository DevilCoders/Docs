Ресурсы
===
##ALL RESOURCES

Таск должен зпускаться после всех таксов по ресурсам в Нирване, так как работает с данными из всех таблиц по ресурсам.<br />
Оптимизация сбора данных по всем ресурсам, а также вычисление разницы между capacity и quotas. Сделан для ускорения работы дашбордов.<br />
Данные собираются графом в нирване и кладутся в таблицу yt

Nirvana таск сбора данных по ресурсам:
 - [Nirvana all resources](https://nirvana.yandex-team.ru/flow/30470680-8707-4967-b6bb-410d67cc28b7/2f442358-5725-4b66-8f89-cf9abd7a4c2f/graph)

Таблица в YT сбора capacity yp:
 - [Yt table all resources](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/reserves/diff/all)

##Capacity

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

##Credits

Сбор данных по кредитам, данные собираются графом в нирване по тикетам с тегом rtc_credit и кладутся в таблицу yt

Nirvana таск сбора кредитов:
 - [Nirvana credits](https://nirvana.yandex-team.ru/flow/1c46aee9-e421-4666-a0b2-33980f5a22e4/8916f286-eda9-41a0-8b77-fdf1f0f0fcf2/graph)

Таблица в YT сбора кредитов:
 - [Yt table credits](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/reserves/credits/credits)

##Migrations

Сбор данных по миграциям, данные собираются графом в нирване и кладутся в таблицу yt<br />
Хранятся сведения о квотах, выданных через мигратор квот.

###GENCFG

Nirvana таск сбора данных по миграциям gencfg:
 - [Nirvana migrations gencfg](https://nirvana.yandex-team.ru/flow/89c78a4d-faa0-4683-9c1c-70cf6003d731/9c47e658-59fd-4816-9af5-c1c94b8a464e/graph)

Таблица в YT сбора данных по миграциям gencfg:
 - [Yt table migrations gencfg](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/reserves/migrations/gencfg)

###QLOUD

Nirvana таск сбора данных по миграциям qloud:
 - [Nirvana migrations qloud](https://nirvana.yandex-team.ru/flow/2a269492-a44c-4e64-af2e-853ea702d171/d605062e-1ce3-4953-9fae-2b7f2f95a068/graph)

Таблица в YT сбора данных по миграциям qloud:
 - [Yt table migrations qloud](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/reserves/migrations/qloud/qloud)

##Quotas

Сбор данных по квотам в облаках

###QLOUD

Сбор данных по квотам, данные собираются графом в нирване и кладутся в таблицу yt

Nirvana таск сбора quotas qloud:
 - [Nirvana quotas qloud](https://nirvana.yandex-team.ru/flow/fd3b1ab4-49b3-46f5-8f12-77e9b8c80bce/73254d28-8a4e-4634-bb6a-d3dd29adf23b/graph)

Таблица в YT сбора quotas qloud:
 - [Yt table quotas qloud](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/reserves/quotas/qloud/qloud)

###YP

Сбор данных по квотам yp, данные собираются графом в нирване и кладутся в таблицу yt

Nirvana таск сбора квот yp:
 - [Nirvana quotas yp](https://nirvana.yandex-team.ru/flow/9df7167a-09c2-4f83-96b2-a2cf9d466220/0c8a0d72-8792-430c-a43d-13495453f612/graph)

Таблица в YT сбора квот yp:
 - [Yt table quotas yp](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/reserves/quotas/yp/yp)

##Неиспользуемые GPU карты

###ABC сервисы

Сбор данных по неиспользуемым GPU картам в ABC сервисах, данные собираются графом в нирване и кладутся в таблицу yt

Nirvana таск сбора неиспользуемых карт:
 - [Nirvana abc unused gpu history](https://nirvana.yandex-team.ru/flow/461766ec-6851-41ad-a902-ae6c71bd5c59/509d11cf-f45c-4af0-9ca0-ab46a4928d0f/graph)

Таблица в YT сбора неиспользуемых карт с историей изменений:
 - [Yt table abc unused gpu history](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/gpu_idle/abc_history_dataset_cost)

Таблица в YT сбора неиспользуемых карт за один день в формате, удобном для SQL запроса:
 - [Yt table abc unused gpu day](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/gpu_idle/abc_day_cost)

##Walle проекты

Сбор данных по неиспользуемым GPU картам в Walle проектах, данные собираются графом в нирване и кладутся в таблицу yt

Nirvana таск сбора неиспользуемых карт:
 - [Nirvana walle unused gpu](https://nirvana.yandex-team.ru/flow/1159f661-5952-4bb7-9b67-56bbb8e9596b/33fd77dd-0c4b-4947-873e-4fc047b4c323/graph)

Таблица в YT сбора неиспользуемых карт:
 - [Yt table walle unused gpu](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/gpu_idle/walle_unused_weekly)

##Подсчет данных по вводимым/выводимым хостам в Walle проектах

Nirvana таски сбора неиспользуемых gpu карт:
 - [ABC history prices](https://nirvana.yandex-team.ru/flow/461766ec-6851-41ad-a902-ae6c71bd5c59/509d11cf-f45c-4af0-9ca0-ab46a4928d0f/graph)
 - [ABC unused gpu](https://nirvana.yandex-team.ru/flow/4f5476b3-4baf-4825-9faa-d9caec3eb507/e79748de-3947-4406-9ec2-ba16db38a7f8/graph)
 - [WALLE unused gpu](https://nirvana.yandex-team.ru/flow/1159f661-5952-4bb7-9b67-56bbb8e9596b/a4f7b747-c2f0-4b21-8fc7-746f195bff2d/graph)

Сбор данных по по вводимым/выводимым хостам в Walle проектах, данные собираются графом в нирване и кладутся в таблицу yt

Nirvana таск сбора данных по вводимым/выводимым хостам:
 - [Nirvana walle hosts](https://nirvana.yandex-team.ru/flow/5c66fc68-7970-44d9-ba62-d72526f5f13c/f422b2cc-3f5e-4227-bab5-897d7e8c58c5/graph)

Nirvana таски сбора ресурсов вводимых хостов walle:
 - [WALLE](https://nirvana.yandex-team.ru/flow/5c66fc68-7970-44d9-ba62-d72526f5f13c/f422b2cc-3f5e-4227-bab5-897d7e8c58c5/graph)

Таблица в YT сбора данных по вводимым/выводимым хостам:
 - [Yt table walle hosts](https://yt.yandex-team.ru/hahn/navigation?path=//home/capacity_planning/reserves/hosts)
