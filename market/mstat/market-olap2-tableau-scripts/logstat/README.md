# Анализатор native логов vizql сервера табло

https://st.yandex-team.ru/MSTAT-9189

**view_stat_parser.py** принимает на stdin логи /var/opt/tableau/tableau_server/data/tabsvc/logs/vizqlserver/nativeapi_vizqlserver_*.txt
Результатом работы является json-файл со всеми открытиями вьюх в табло, которые удалось найти в логах. Парсит 95% открытий. По каждому открытию сохраняется много всякой статистики. Пока не все поля понятны.
Понятные поля:
название отчёта, воркбук, урл
elapsed —— время построения отчёта в секундах
request-info/mark-count —— количество точек (циферка слева внизу в десктопе)
request-info/width и height —— размер отчёта в пикселях

Не понятные:
десятки в request-info
какие-то циферки ресурсов в res/alloc и res/free
res/ucpu и kcpu —— то ли это просто текущие показатели по cpu на машине, то ли оно как-то считает, сколько потрачено на этот показ

**view_stat_analyzer.py** умеет анализировать этот json и конвертить его в csv. Смотри `./view_stat_analyzer.py -?`


Топ по времени построения:
```
ssh тачка-с-табло
cd /var/opt/tableau/tableau_server/data/tabsvc/logs/vizqlserver
cat nativeapi_vizqlserver_*2019_10_09*.txt | ./view_stat_parser.py reqs_2019_10_09.json
./view_stat_analyzer.py reqs_2019_10_09.json elapsed 10
```

Топ по количеству точек: 
```
./view_stat_analyzer.py reqs_2019_10_09.json request-info/mark-count 10
```

Сконвертировать в CSV:
```
./view_stat_analyzer.py reqs_2019_10_09.json convert_to_csv > reqs_2019_10_09.csv
```


## Планы
Понять поля. Можно подсмотреть в коде двух приложений:
https://github.com/thechosentom/LumberSnake/blob/master/README.md
https://tableau.github.io/Logshark/

Сделать в виде приложения. Собирать nativeapi_vizqlserver логи с кластера логброкером, анализировать на ыте (?), строить графики на графите.
