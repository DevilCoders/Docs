# logbroker-custom-destroy-policy-stages-getter

Получает все стейджи и под сеты, в которых используется кастомные настройки destroy policy для бокса unified agent.

## Пример использования

Пример использования для получения всех stage с id и pod set id на кластерах `sas-test` и `man-pre`:

```
$ ./logbroker/custom-destroy-policy-stages-getter/logbroker-custom-destroy-policy-stages-getter --clusters sas-test man-pre
Use yp token from file /home/slamur/.yp/token
--------------------------------------------------
Processing cluster sas-test
--------------------------------------------------
Number of rs is 1:
mplbnv-stage-2.deployUnit
--------------------------------------------------
Number of stages is 1:
mplbnv-stage-2
--------------------------------------------------
Processing cluster man-pre
Press enter to continue
```
