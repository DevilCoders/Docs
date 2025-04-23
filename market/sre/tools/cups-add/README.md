## **Тулза для добавления принтеров**
Тулза для добавления принтеров на складе, для работы необходимо наличие dns-monkey.pl в PATH, а так же необходимо прокинуть тунель до нужного cups мастера (01 нода wma-app на нужном складе, так как нас сетап cups позволяет добавлять принтеры только локально.
####**Пример форварда:**
```shell
ssh  -N -L 1631:localhost:631 wms-app01sof.market.yandex.net
```
Тулза принимает на вход хост, порт капс сервера, путь до файла со списком принтеров, а так же опциональный флаг валидации --validate, при котором не выполняется никаких изменеий. Список принтеров состоит из строчек содержащих ip принтера и его имя через пробел, имя принтера задется **без** домена
####**Пример списка принтеров:**
```shell
2a02:6b8:0:5409:2c0:ebff:fe11:a805 tsc_tdp247.l5-outsttn001sof
2a02:6b8:0:5409:2c0:ebff:fe11:a801 tsc_tdp247.l5-outsttn002sof
2a02:6b8:0:5409:2c0:ebff:fe11:a80f tsc_tdp247.l5-outsttn003sof
2a02:6b8:0:5409:2c0:ebff:fe11:a7f2 tsc_tdp247.l5-outsttn004sof
```
####**Пример строки запуска:**
```shell
cmd/cups-add/cups-add localhost 1631 /Users/isonami/printers.txt --validate
```
####**Пример строки запуска для yandex-team принтера:**
```shell
cmd/cups-add/cups-add localhost 1631 /Users/isonami/printers.txt --validate --yandex-team
```
