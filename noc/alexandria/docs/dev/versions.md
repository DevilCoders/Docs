### Раздельные спецификации swagger
[Спецификации Caesar и Marcus](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/api/alexandria)  
Генерация swagger в [Makefile](https://a.yandex-team.ru/arc/trunk/arcadia/noc/alexandria/Makefile) на основе _swaggo_

### Alexandria APIv2 (Draft)
Порт по-умолчанию 9998.

http handlers обозначены как "v2" в названии, а типы переменных, функции и mux носят приставку Marcus.

### Alexandria APIv1 (Legacy)
Сервис, в виде API, запущен на серверах Racktables:
* http://noc-myt.yndx.net:9999 (FreeBSD)
* http://noc-sas.yndx.net:9999 (FreeBSD)
* http://man1-rt1.yndx.net:9999 (Ubuntu)

А также в тестовом режиме на Racktables prestable:
* sas-rt-prestable1.net.yandex.net (FreeBSD)

http handlers обозначены как "v1" в названии, а типы переменных, функции и mux носят приставку Caesar.

