# logbroker-throttling-stages-getter

Получает все стейджи и под сеты с заданными посекундными лимитами у unified agent.

## Пример использования

Пример использования для получения всех stage с id и pod set id на кластерах `sas-test` и `man-pre` c посекундными лимитами по объему сообщений `15 mb` и количеству сообщений `20000`:

```
$ ./logbroker/throttling-stages-getter/logbroker-throttling-stages-getter --rate 15mb --messages 20000 --clusters sas-test man-pre
Use yp token from file /home/slamur/.yp/token
--------------------------------------------------
Processing cluster sas-test
--------------------------------------------------
Number of rs is 1:
slamur-stage-4010-local.new-throttling-du
--------------------------------------------------
Number of stages is 1:
slamur-stage-4010-local
--------------------------------------------------
Processing cluster man-pre
--------------------------------------------------
Number of mcrs is 1:
security_features.security_features_deploy_unit
--------------------------------------------------
Number of stages is 1:
security_features
Press enter to continue
```
