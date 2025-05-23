# Сработал алерт mds_storage_uac_namespace_free_space_alert

## Назначение алерта

Алерт контролирует объем свободной памяти, выделенной в аватарнице для uac'а, чтобы избежать проблем с созданием новых кампаний и загрузкой новых ассетов в случае ее нехватки.

В общем случае объем занимаемой памяти в аватарнице просто возрастает со временем. Немного нивелирует этот процесс [DeleteUnusedAssetsFromMDSJob](https://a.yandex-team.ru/arc_vcs/direct/jobs/src/main/java/ru/yandex/direct/jobs/uac/DeleteUnusedAssetsFromMDSJob.kt). 
Эта джоба удаляет из аватарницы ассеты, которые в течение заданного времени так и не были связаны ни с одной кампанией. Ее сбой или отключение может быть одной из причин в резком изменении скорости заполненеия выделенных для uac'а квот в Аватарнице.

## План действий

Сейчас запрос квот и выделение памяти в аватарнице находтся в полуручном режиме, поэтому типового флоу нет.
Если алерт сработал, требуется запросить повышение квоты в mds для uac-namespace, для этого нужно обратиться к руководителю группы/службы разработки Директа (например, [kuhtich@](https://staff.yandex-team.ru/kuhtich) или [bratgrim@](https://staff.yandex-team.ru/bratgrim)), они скоординируют дальнейшие действия.

## Полезные ссылки

[График связанный с алертом](https://yasm.yandex-team.ru/template/panel/mds-ns-space/ns=avatars-uac?range=2592000000)

[Дашборд аватарницы для  uac-namespace](https://avatars.chv.yandex-team.ru/projects/uac/projectDashboard)
