# logbroker_stages_getter

Получает все стейджи и под сеты, в которых используется заданный слой логброкера.

## Пример использования

Пример использования для получения всех stage с id и pod set id которые используют слой logbroker_tools_layer с url = 'rbtorrent:bd0daf64c77ac679845b99a6ae4b129f7253add7' на кластерe `sas-test`:

```
$ ./logbroker-stages-getter sas-test --logbroker-tools-layer 'rbtorrent:bd0daf64c77ac679845b99a6ae4b129f7253add7'
--------------------------------------------------
NUM MCRS 1
MCRS LIST:
test_stage-dkochetov-0102812.dkochetov-test-deploy-unit-2-0
--------------------------------------------------
NUM RS 1
RS LIST:
staroverovad-stage-aaaaa.deployUnit
--------------------------------------------------
NUM STAGES 2
STAGES LIST:
staroverovad-stage-aaaaa
test_stage-dkochetov-0102812
Press enter to continue
```
