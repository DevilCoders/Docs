common
===========

Common models and code for RASP family of services

Here belong:
- mysql_switcher (including connectdb)
- stripped models
- distributed cache methods
- common global settings (local settings should be handled by yandex-rasp-common package)
- ... (to be continued)
- initially specific modules (form parser/search/station schedule) will be here


## MySQLdb dependency

Каждый проект, использующий common, должен выбрать библиотеку для взаимодействия с mysql.

Есть два варианта библиотек:
1. MySQL-python - deprecated, давно не обновляется, только python2
2. mysqlclient-python - форк варианта 1., поддерживает python3

Нужно перейти с варианта 1. на вариант 2., чтобы это сделать,
нужно дать возможность проектам самим выбирать библиотеку.
Одновременно указывать обе зависимости не получится.

Поэтому зависимость на переходный период убрана из common.
И теперь каждый проект должен прописать у себя одну или другую зависимость.

