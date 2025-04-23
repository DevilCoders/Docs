# Скрипты подсчета статистики использования пушки Pandora

Скрипт psql.sh достает из постгресовой базы номер стрельбы(n) и конфиг стрельбы(configinfo)
```bash
sh psql.sh <password> > configinfo.data
```

Далее скрипт stat.py принимает на вход configinfo.data и ищет в yaml-ах использование Pandora и подсчитывает статистику:
```bash
cat configinfo.data | python stat.py
All:277568, Pandora true:21204, Pandora false:253150, Yaml:177134, INI:100433
```
Где: 
  All - всего стрельб
  Pandora true - стрельбы пушкой Pandorа
  Pandora false - стрельбы не Pandorа
  Yaml - кол-во стрельб с конфигами с yaml-формате
  INI - кол-во стрельб с конфигами в ini-формате

Тикет с результатами последнего подсчета: https://st.yandex-team.ru/LOAD-1030
