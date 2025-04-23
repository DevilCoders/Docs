Что это?
========

Тут лежат основные представления для YT/YQL и утилита для обновления тела представления.

Выкладка
========

Сборка
------

```bash
$ cd deploy
$ ya make
```

Обновление тела представления
-----------------------------

```bash
$ ./deploy --yt-token=$YA_YT_TOKEN --view-name=v_refund --view-body=../v_refund.sql --ticket=DWH-683
Target view: hahn.//home/balance/dev/views/v_refund
Done.
```
