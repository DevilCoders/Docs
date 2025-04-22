# logbroker-custom-topic-stages-getter

Получает все стейджи и под сеты, в которых используется кастомный топик.

## Пример использования

Пример использования для получения всех stage с id и pod set id на кластерах `sas-test` и `man-pre`:

```
$ ./logbroker/custom-topic-stages-getter/logbroker-custom-topic-stages-getter --clusters sas-test man-pre
Use yp token from file /home/slamur/.yp/token
--------------------------------------------------
Processing cluster sas-test
--------------------------------------------------
Number of rs is 1:
slamur-stage-4010-local.custom-topic-du
--------------------------------------------------
Number of stages is 1:
slamur-stage-4010-local
--------------------------------------------------
Processing cluster man-pre
Press enter to continue

```
