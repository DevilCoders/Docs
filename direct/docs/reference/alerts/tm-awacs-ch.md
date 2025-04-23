# tm-dtt49untf48po1s3ki1f-awacs-to-ch-*

## Описание { #description }
Трансфер для записи логов с аваксововых балансеров, льющихся в логброкер в кликхаус с логцами через логфеллер.
Сам трансфер https://yc.yandex-team.ru/folders/fooa07bcrr7souccreru/data-transfer/transfer/dtt49untf48po1s3ki1f/view

Есть два алерта (скопированы из [рекомендаций по алертам](https://wiki.yandex-team.ru/transfer-manager/replication/monitoring/alerts/) от команды ТМ ):
- [про живость](https://solomon.yandex-team.ru/admin/projects/direct/alerts/tm-dtt49untf48po1s3ki1f-awacs-to-ch-active)
- [про запись](https://solomon.yandex-team.ru/admin/projects/direct/alerts/tm-dtt49untf48po1s3ki1f-awacs-to-ch-write)

## Диагностика
При зажигании алерта стоит перейти на страницу трансфера и посмотреть его статус, логи, а также действия(там бывает пишется причина остановки).
Может ломаться из-за:
 - того, что в принимающем кликхаусе(ppchouse) не хватает хостов в шардах для кворума записи.
 - работ на логброкере
 - работ в YT
 - кончившемся месте

Если по логам ничего не понятно, то попробовать [диагностику от команды ТМ](https://wiki.yandex-team.ru/transfer-manager/replication/monitoring/Alerts/#chtodelatprisrabatyvaniialerta)

