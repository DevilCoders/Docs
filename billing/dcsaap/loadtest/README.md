Нагрузочное тестирование
========================

Чтобы начать тестирование, необходимо рядом с нодами поднять образ танка:

- https://wiki.yandex-team.ru/load/howto/tankhowto/#kakpoluchitsvojjtankvqloud

Вот тут выбираем L7 балансер и прописываем его в lb_load.yaml:

- https://qloud-ext.yandex-team.ru/projects/paysys/slb/paysys-int-test?status=&component=balancer-l7&version=1585302929190

Заходим в него по ssh, в `ammo.txt` вставляем куку и запускаем тест:

```
$ ssh tank-1.tank.testing.balance-dcs.paysys.stable.qloud-d.yandex.net
[tank] balance-dcs.testing.tank.sas1-0559889ca353: /# cd ~
[tank] balance-dcs.testing.tank.sas1-0559889ca353: /root# 
[tank] balance-dcs.testing.tank.sas1-0559889ca353: /root# ls -l
total 40
-rw-rw-r-- 1 root root  1145 Mar 26 12:14 ammo.txt
-rw-rw-r-- 1 root root   676 Mar 26 12:54 lb_load.yaml
[tank] balance-dcs.testing.tank.sas1-0559889ca353: /root# yandex-tank -c lb_load.yaml
...
```

В конце появится ссылка на графический отчет, вида:

- https://lunapark.yandex-team.ru/2436786

Конфиг настроен, чтобы стрелять в тест:

- https://qloud-ext.yandex-team.ru/projects/paysys/balance-dcs/testing

