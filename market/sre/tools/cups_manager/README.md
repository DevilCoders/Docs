HOW TO
===================================

Утилита `cups_manager` предназначена для добавления принтера в DNS, CUPS и WMS.

Для добавления принета в DNS требуется установленная утилита [dns-monkey](https://wiki.yandex-team.ru/dynamic-dns/dns-monkey-roadmap/).

# Как добавить новый принтер

0. Внимательно прочитать вывод встроенной помощи:

`     ./cups_manager add -h
     Add printer to CUPS server and WMS
     
     Usage:
       cups_manager add [wmsHost] [cupsPort] [printerName] [domain] [ipAddr] [printerLocation] [flags]
     
     Flags:
       -a, --addr string          Printer ip addres
       -c, --cupsHost string      Cups host (default "localhost")
       -p, --cupsPort int         Cups port (default 631)
       -h, --help                 help for add
       -s, --labelSize int        Printer label size.
                                  Допустимые значения для поля [labelSize]: {2, 7, 3, 5, 6, 8}
                                  LABEL_4x3 - 2
                                  LABEL_100x100 - 7, 3
                                  LABEL_43x25 - 5
                                  LABEL_58x40 - 6
                                  PAPER_A4 - 8
                                   (default 7)
       -l, --location string      Printer location (for WMS)
       -n, --printerName string   Printer Name (without domain!)
       -w, --wmsHost string       Wms host
       -t, --yandexteam           Printer in domain .yandex-team.ru
     
 `

1. Выбрать primary (либо 01) ноду WMS для нужной локации из [серверов](https://c.yandex-team.ru/groups/market_wms-app-stable) wms-app.

2. Пробросить CUPS с ноды WMS на localhost по ssh:

	`ssh  -N -L 1631:localhost:631 wms-app01sof.market.yandex.net`

3. Запустить `cups_manager` с нужными параметрами:

	`./cups_manager add -n tsc-tdp247.l1c-outsttn012sof -p 1631 -w wms-app01sof.market.yandex.net -a '2a02:6b8:0:5e0d:2c0:ebff:fe1a:b1fe' -s6`
	
	Особое внимание обратить, что имя принтера указываем без подчеркиваний, а только с тире. Кроме того, мы указываем его сокращенным: `tsc-tdp247.l1c-outsttn012sof`. Оставшийся `wh.market.yandex.net` зашит в коде и добавится автомагически. Второй момент: не забываем указывать размер этикеток, проставляется он через флак `-s` с цифрами 2, 7, 3, 5, 6 и 8. См. встроенную справку.

4. Добавить PTR-запись для принтера (эту функциональность вскоре должны допилить):

	`dns-monkey.pl --zone-update --expression 'add-ptr 2a02:6b8:0:5e0d:2c0:ebff:fe1a:b1fe tsc-tdp247.l1c-outsttn012sof.wh.market.yandex.net'`

## Как посмотреть все принтеры на CUPS:

Сначала нужно выбрать wms ноду и прокинуть ssh-тунель, аналогично инструкции про добавление принтера. А затем можно посмотреть список:

	`./cups_manager show -c wms-app01sof.market.yandex.net`
	
Человекочитайемый вывод может быть когда-нибудь будет позже.	

## Как удалить принтер из CUPS:

1. Сначала нужно выбрать wms ноду и прокинуть ssh-тунель, аналогично инструкции про добавление принтера. 

2. А затем можно удалить принтер по короткому имени:
 
 	`
 	$ ./cups_manager delete -n tsc_tdp247.l1c-outsttn012sof -p 1631 -a 2a02:6b8:0:5e0d:2c0:ebff:fe11:a7f0
 	Printer removed from cups tsc_tdp247.l1c-outsttn012sof
 	`
   Если не указать адрес, принтер удалится только из cups.

3. Удалить принтер из WMS должны сотрудники поддержки склада.
