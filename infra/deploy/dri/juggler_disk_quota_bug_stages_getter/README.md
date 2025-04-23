# logbroker_stages_getter

Получает все стейджи и под сеты, в которых есть бага с добавление дисковой квоты в случае использования джагглера. Квота для джагглера добавляется не в пользовательский диск, а в под агентский.

## Пример использования

Пример использования для получения всех stage с id и pod set id с вышеописанной багой на кластерe `sas-test`:

```
$ ./logbroker-stages-getter sas-test
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
