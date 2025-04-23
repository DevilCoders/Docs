# Полезные ссылки

[Замена и совместимость](http://wiki.yandex-team.ru/DC/ipmicompatible)

# Как пользоваться

## Как найти

FQDN'ы для BMC генерятся автоматически в зависимости от FQDN'а сервера. Если сервер находится в зоне yandex.net будет сгенерена запись вида "$HOST.mgmt.yandex.net", если в зоне yndx.net то "$SERVER.ipmi.yndx.net".

## Web-сервер

Требует только браузер. Оттуда можно почитать лог событий, потыкать в кнопку питания или reset, поменять настройки RAC/BMC. Прямо из этого же интерфейса можно бывает запустить KVM-клиент, для которого нужна Java.При возникновении ошибки Java - "Unable to launch the application", нужно открыть скаченный jnlp в редакторе, заменить 443 на 80 и https на http, и открыть сохраненный файл.

## KVM-клиент

Софт на многоплатформенном языке Java. При отсуствии Java-машины можно зайти на kraken и запустить браузер (и софт) оттуда. Например, вот так: 

rdesktop -r clipboard:PRIMARYCLIPBOARD -k en-us -g 1024x768 kraken

## Управление питанием

Протокол IPMI также позволяет потыкать в кнопку питания или reset. Например, reset:
```
ipmitool -I lanplus -H $HOST.mgmt.yandex.net -U $USER -P $PASSWORD chassis power reset
```
## SOL (serial over LAN)

Если BMC сервера поддерживает протокол IPMI версии 2.0, то можно воспользоваться SOL. Для этого нужно включить в настройках IPMI over LAN (у DRAC это делается в меню "Remote access -> Network/Security"), заиметь IPMI-клиент на своём десктопе и воспользоваться им. Вот пример того, как это сделать с помощью линуксового пакета OpenIPMI:`solterm lan -U $USER -P $PASSWORD $HOST.mgmt.yandex.net -bitrate 115200`Или с помощью ipmitool:
```
ipmitool -I lanplus -H $HOST.mgmt.yandex.net -U $USER -P $PASSWORD sol activate
```
Чтобы выйти надо нажать комбинацию ENTER + TILDA + DOT

# Стандартный ipmi

Скрипты для массового апдейта, добавления пользователей лежат в git: ![http://noc-gitlab.yandex-team.ru/nocdev/racktables/tree/master/scripts/ipmi-mgmt](http://noc-gitlab.yandex-team.ru/nocdev/racktables/tree/master/scripts/ipmi-mgmt)ipmi-add.sh - добавление нового пользователя. ipmi-change.sh - изменение пароля для существующего ipmi-ipaddr.sh - сброс настроек lan на 0.0.0.0 и статические адреса

login: ADMINpass: Lah8ohshдефолтный пароль на ipmi на новых платформах: Yand3xBmc

## как сбросить пароль

```
# (без последнего параметра почему-то не работает)
$ ipmitool user list 1
ID  Name	     Callin  Link Auth	IPMI Msg   Channel Priv Limit
2   root             true    true       true       ADMINISTRATOR
$ ipmitool user set password 2 NEWPASSWORD
# если нужно сделать по сети:
ipmitool -U LOGIN -P PASSWORD -H HOST user set password 2 NEWPASSWORD
```
## как сбросить зависший BMC

Стандартное решение этой задачи сводится к выполнению команды:
```
ipmitool mc reset cold
```
Если залип модуль системы отвечающий за работу с IPMI, то выполняем то-же самое, но по сети:
```
ipmitool -H HOST -U LOGIN -P PASSWORD bmc reset cold
```
Но будь осторожен с выполнением это команды - есть информации о негативном влиянии на основную систему. Особенно там где запущен watchdogd.

В совсем запущенных случаях необходима перезагрузка сервера с помощью выдергивания кабеля питания.

Если совсем всё плохо, то могут помочь хелпы, перепрошив IPMI. Потребуется выключить сервер. [Чуть подробнее.](http://wiki.yandex-team.ru/andrejjvorfolomeev/IPMIneotvechaet)

В некоторых случаях случаях может помочь заход по SSH'у на BMC и выполнение команды
```
/etc/init.d/webgo restart
```
Еще один кейс, когда IPMI на все попытки его сконфигурить отвечал 
LAN Parameter Data does not match!  Write may have failed.
 решился отключением IPMIOverLAN и перещелкиванием интерфейса на LANFailOver (в примере для X9 платформы Supermicro). 
mc reset cold
 при этом не помогал.
```
ipmitool lan set 1 access off
ipmitool raw 0x30 0x70 0x0c 1 2
make -C /usr/local/router/conffiles update install-ipmi-lancfg
ipmitool lan set 1 access on
```
## Переключение сети IPMI между интерфейсами

| X8 | X9,X10 |
| - | - |
| ```sh
# get lan mode
ipmitool raw 0x30 0x70 0xc 0 0 0
# Default (failover):  00 00 
# Dedicated LAN:  01 00 
# Onboard LAN:  01 01

# Set Dedicated LAN
ipmitool raw 0x30 0x70 0xc 1 1 0
# Set Onboard LAN1
ipmitool raw 0x30 0x70 0xc 1 1 1
# Set Failover(default setting)
ipmitool raw 0x30 0x70 0xc 1 0 0
``` | ```sh
# get lan mode
ipmitool raw 0x30 0x70 0x0c 0
# Dedicated: 00
# Share: 01
# Failover (default): 02

# set to dedicated
ipmitool raw 0x30 0x70 0x0c 1 0
# set to share
ipmitool raw 0x30 0x70 0x0c 1 1
# set to failover (default)
ipmitool raw 0x30 0x70 0x0c 1 2
``` |

## посмотреть версию BIOS из shell

```
dmidecode --type BIOS
```
# о прошивках

Восстановим пароль после сброса настроек:
```
ipmitool user list 1 | awk '$2 ~ /ADMIN/{print $1}' | read id; [ -n "$id" ] && ipmitool user set password $id PASSWORD
```
Настроим сеть:
```
make -C /usr/local/balancers/conffiles update install-ipmi-lancfg
make -C /usr/local/router/conffiles update install-ipmi-lancfg
```
Сеть можно настроить и вручную:
```
ipmitool lan set 1 ipsrc static
ipmitool lan set 1 ipaddr HOST
ipmitool lan set 1 netmask NETMASK
ipmitool lan set 1 defgw ipaddr DEFGW
```
## DRAC - Dell Remote Access Control (v5,v6)

[Немного документации по iDRAC CLI](http://stuff.mit.edu/afs/athena/dept/cron/documentation/dell-server-admin/en/idrac1/chap10.htm). Этим можно воспользоваться для выполнения команды 
racadm racreset
, если вдруг HTTP-морда сошла с ума.

У Dell есть две прошивки, одна для DRAC, другая для BMC. Внутри они дополнительно делятся по DRAC5 и DRAC6.
- DRAC-прошивку можно загрузить, поискав "drac 5 firmware" на support.dell.com (последняя версия 1.51, 22MB, приаттачена к этой странице). Использовать можно, положив на TFTP-сервер, либо прямо через HTTP (Remote access -> Update). Процесс занимает время и меняет SSH host key.
- BMC-прошивка находится в разделе "embedded server management", который можно увидеть, зайдя на ![http://support.dell.com](http://support.dell.com) с серийным номером сервера Dell (записан в RackTables как OEM S/N 1). Последняя версия BMC для 1950 -- 2.37, 500КБ, приаттачена. Как прикладывать, пока непонятно.
Обновление DRAC через TFTP можно выполнить показанным ниже способом. Особенность RACADM в том, что он всегда запрашивает одно и то же имя файла в рамках своей major-версии (5/6). Поэтому на TFTP-сервере установлен symlink.
```
$ racadm fwupdate -s
Firmware update is not currently in progress
$ racadm fwupdate -g -u -a 93.158.158.93 -d /Dell
Preparing for firmware update. Please wait...
```
{red}(Ввиду тормознутости TFTP эта операция не удаётся.)

О решении проблем с биндингом онбордного интерфейса можно почитать [тут](http://wiki.yandex-team.ru/ipmi).
## Supermicro

**Vendor:10876**
| Название | Стоковая прошивка | Прошивка для регионов (IPMI на чужих адресах) | Диагноз |
| - | - | - | - |
| X9DRW-3F, X9DRW-iF | [2.59](http://www.supermicro.nl/support/resources/getfile.aspx?ID=2959) [2.49](https://yadi.sk/d/Gg5uEY2_wHF4B) [2.19](https://yadi.sk/d/Z_5bMxEC38ATTy) | [Огонь-прошивка на основе 2.59](file:NOC_X9_2_59.4.ima) |  |
| X8DTU | [3.13](https://www.supermicro.com/about/policies/disclaimer.cfm?SoftwareItemID=3242) | [Огонь-прошивка на основе 3.10](file:NOC-X8DTU310.ima) |  |

Для Х9 2.49 более стабильная

{% cut "Старая версия таблички" %}

| Название | Прошивка | Диагноз |
| - | - | - |
| X9DRW Материнские платы: X9DRW-3F,X9DRW-iF | [Старая патченная прошивка](file:x9drw-bmc-2.14.1.ima)[Огонь-прошивка на основе 2.59](file:NOC_X9_2_59.4.ima) |  |
| X8DTU | [Патченная прошивка](file:x8dtunew.ima)[Патченная прошивка 2.20, патч добавляет возможность прописывать статик роуты](file:x8dtu220.ima)Огонь-прошивка на основе 3.10](file:NOC-X8DTU310.ima) | На стоковой прошивке залипает WEB-интерфейс |

{% endcut %}

{% cut "Как обновить прошивку BMC Supermicro не перезагружая рыбку" %}

Внимание: все настройки на BMC будут сброшены.
- Скачиваем [прошивку для BMC](https://wiki.yandex-team.ru/noc/oobm/) (огонь-прошивку на основе 2.59, по состоянию на август 2021)
- Переводим порт на свитче в VLAN 412 или 2612
- На рыбке выполняем `ipmitool lan set 1 ipsrc dhcp`, чтобы получить DHCP-адрес для дальнейшей работы с IPMI
- Рыбка станет доступна по адресу вида `${MAC через дефисы}.ipmi.yandex.net`
- Идём в вебинтерфейс BMC (например, ![https://0c-c4-7a-5b-13-be.ipmi.yandex.net](https://0c-c4-7a-5b-13-be.ipmi.yandex.net)) **chrome-based** браузером
- {red}(Открываем консоль разработчика (F12), таб Application: Storage -> Cookies, выбираем домен (например, ![https://0c-c4-7a-5b-13-be.ipmi.yandex.net](https://0c-c4-7a-5b-13-be.ipmi.yandex.net)), и добавляем новую куку с именем "WebServer" и любым значением. **Если этого не сделать, следующие два шага сломаются.**) Хак стырен [отсюда](https://www.truenas.com/community/threads/ipmi-update.73437/) 
  
  > 1. Log in to BMC
  > 2. Open Chrome Dev Tools
  > 3. Switch to Application tab. Expand "Cookies" and click the appropriate domain name for your server.
  > 4. At the end of the existing cookie list, double click the empty spot. Enter "WebServer" under name.
  > 5. Should be good to go now.
  
- Maintenance - BMC Firmware Update - Enter Update Mode (галочка preserve all configuration не нужна)
- На этапе Uploading firmware image всплывёт окошко - подсовываем прошивку
- Не отключаемся - через некоторое время система попросит подтвердить намерения
BMC перезагрузится с новой прошивкой и сброшенными настройками.
- Через веб-интерфейс (Configuration - Users) выставляем актуальный пароль для ADMIN
- Выставляем сетевые настройки IPMI: логинимся на рыбку, выполняем `sudo -Es make -C /usr/local/router/conffiles install-ipmi-lancfg`
- Переводим VLAN на порту коммутатора в целевое значение
С этого момента BMC становится доступен извне, поэтому все остальные этапы должны быть пройдены незамедлительно.
- Прольём правила FW: запускаем с noc (из своего репозитория router/conffiles) таргет `make install-ipmi-static-routes IPMISSHUSERNAME=sysadmin IPMIDSTADDR=<ipmi_address>`
- Система спросит пароль для sysadmin - он тот же, что мы ранее настроили для ADMIN
- Хладнокровно перезагрузим BMC, запустив с рыбки: `sudo ipmitool mc reset cold`
- Проверим, что BMC пингуется только с адресов, входящих в перечисленные в файле static-routes сети (пингуется, например, с noc-myt и не пингуется с sas1-grad1)

{% endcut %}

### Огонь-ISOшка

[ISO-образ, который **автоматически** прошивает BMC и BIOS до правильных версий](file:/NOC/OOBM/nocx8x9biosbmcreflash.iso.bz2)ISO умеет обновлять BMC и BIOS X8DTU и X9DRW. При обновлении BMC восстанавливает настройки сети.Этап BMC может пропущен, либо BMC будет прошит или стоковой, или огонь- прошивками. Для управления этим процессом требуется создание псевдопользователей. Пользователя нужно создавать с уровнем доступа "No Access":
- nobmc - пропустить этап прошивки BMC, пользователя нужно удалить вручную после завершения процесса обновления BIOS
- stockbmc - прошить стоковую версию BMC, пользователь будет удален автоматически
- нет ни одного из вышеперечисленных - прошить огонь-прошивку BMCПользователей добавлять можно вот так:
```sh
ipmitool user list 1 # выводим список пользователей
ipmitool user set name 4 nobmc # используем свободный слот
```
**Работа с Огонь-ISO**
- Загружаемся с Огонь-ISO
  - Надо подмонтировать ISO в виртуальный cdrom. Это удобно делать через iKVM, т.к. isoшник уже лежит на VNC сервере:Ractables -> iKVM -> Значок диска -> CD/DVD Media -> Browse -> /home/vnc/iso/noc/noc_X8_X9_bios_bmc_reflash.iso
  - Перезагрузить сервер
  - Долбить F11, чтобы открыть Boot menu, и загрузиться с cdrom
  - Спустя 2-3 минуты после загрузки iKVM отвалится. Сервер вернется с обновленными BIOS и BMC через ~15-30 минут.
- Меняем пароль на пользователе ADMIN на стандартный, т.к. после обновления стал ADMIN/ADMIN, [воспользовавшись этим разделом](https://wiki.yandex-team.ru/noc/OOBM/#kaksbrositparol)
- Проливаем firewall
  - Проблема: BMC не пускает по SSHЗато пускает по порту 80 с noc-*. Делаем SSH туннель `ssh -L 9999:<IPMI-IP>:80 -N -T <username>@noc-myt`, заходим на `http://localhost:9999`, в WEB находим Services и для SSH делаем disable/enable, после чего IPMI станет доступен по SSH, и можно проливать firewall.

{% cut "Как собирать" %}

[Окружение для сборки этой ISOшки](file:/NOC/OOBM/bootiso.tar.bz2):
```
apt-get install mtools genisoimage qemu-system-x86
make clean
make noc_X8_X9_bios_bmc_reflash.iso
```

{% endcut %}

## Asus

**Vendor:4163**
| Device ID | Название | Прошивки | Диагноз |
| - | - | - | - |
| 2098 | ASMB3-iKVM |  |
| 2371 | ASMB4-iKVM | [прошивка](file:z8nr0212.ima) от мауса с возможностью залогиниться под рутом. При обновлении убрать галку "Preserve Configuration". | IPMI(авторизация через WEB) залипает с вероятностью 100%. Проверено на прошивках 2.05, 2.12, 2.14, 2.15. |
| 3171 | ASMB6-iKVM | Последняя прошивка: 1.16. Скачать ![file:zpe1g116.ima](file:zpe1g116.ima) |  |

Внимание! При обновлении могут возникнуть следующие проблемы:
- Передергивание онбордных интерфейсов
- Сбрасывание настроек сети в шаред режим
## Hewlett-Packard

**Vendor:11**
| Device ID | Название | Прошивки | Диагноз |
| - | - | - | - |
| 8192 | iLO 2 | ![file:ilo2215.bin](file:ilo2215.bin) | Похоже что ок |
| 0 | Lights-Out 100i (LO100i) |  | Похоже что ок |

# IPMI в регионах

Процедура настройки для региональных машин:
## SM и ASUS

1. Обновляем IPMI до актуального состояния
2. Настраиваем учетные данные и сеть.
3. (этот пункт в огонь-прошивках уже сделан) меняем хеш у юзера sysadmin на `$1$FtlOXO9V$OBwQgPpRN.qq4T9vb6evc0` (это хеш "стандартного" IPMI пароля) и выключаем anonymous в файлике  /conf/shadow. Хеш можно сгенерить на какой нибудь linux машинке `mkpasswd -m md5`.
4. Обновляем файл static-routes до актуального состояния:
   - Стянуть cvs репозиторий в /home/$USER на noc-*
   - Выполнить выполнить на noc-* make-таргет 
     install-ipmi-static-routes
      в routers/conffiles, указав ему параметры 
     IPMISSHUSERNAME
      и 
     IPMIDSTADDR
      (просто вызов 
     make install-ipmi-static-routes
      покажет маленькую памятку, ориентируйтесь по ней).
5. Делаем 
   ipmitool mc reset cold
6. Проверить с любой машины, кроме входящих в перечисленные в файле static-routes сети. BMC не должен отвечать на пинги и веб-интерфейс.
На Supermicro X10 в BMC есть фича "IP Access control" - фаервол на BMC. Он позволяет средствами штатной прошивки добиться нужного уровня защиты. Для этого включаем "IP access control", добавляем сети/хосты из файла ipmi-static-routes с действием ALLOW, последним добавляем 0.0.0.0/0 с действием DENY.

{% cut "Результат выглядит примерно вот так:" %}

![file:ip-access-control.png](file:ip-access-control.png)

{% endcut %}

Правил там, увы, всего лишь 10, так что в фильтр вписывайте админскую сеть в КР, noc-myt, noc-sas, zabbix, 3 сети из HAASNETS (93.158.168.136/29, 77.88.57.176/29, 5.45.214.80/29) и подсеть, где живет этот IPMI.
## Gigabyte

1. Обновляем IPMI до актуального состояния. Через веб-интерфейс, меню Update. Актуальная прошивка [gigabyte-small-server-v606.img](file:/noc/oobm/gigabyte-small-server-v606.img).
2. Настраиваем учетные данные и сеть. У BMC 2 админских учётки: ADMIN и admin. У первой меняем пароль, вторую выключаем.
3. Обновляем файл ipmi-gigabyte до актуального состояния:
   - Стянуть cvs репозиторий в /home/$USER на noc-*
   - Выполнить на noc-* make-таргет 
     install-ipmi-gigabyte
      в routers/conffiles, указав ему параметры 
     IPMISSHUSERNAME
      и 
     IPMIDSTADDR
      (просто вызов 
     make install-ipmi-gigabyte
      покажет маленькую памятку, ориентируйтесь по ней). Пароль от непрошитой учетки пользователя avct 
     
     avctr00t
     
     . У прошитой разрешены все ssh-ключи NOC (username тем не менее используем avct), + стандартный IPMI пароль
4. Делаем 
   ipmitool mc reset cold
5. Проверить с любой машины, кроме входящих в перечисленные в файле 
   ipmi-gigabyte
    сети. BMC не должен отвечать на пинги и веб-интерфейс.
# OOB в Москве

TBDВ [тикете](https://st.yandex-team.ru/NOC-337/files) есть немного картинок с рассуждениями.
# Тушим все сервера в ДЦ по IPMI

```sh
arp -an -ivlan2612 | awk -F '[ ()]' '/expires/ {print "ipmitool -U ADMIN -P ADMIN -H " $3 " chassis power soft &"} NR % 1000 == 0 {print "sleep 1"}' > shutdown-soft.sh
arp -an -ivlan2612 | awk -F '[ ()]' '/expires/ {print "ipmitool -U ADMIN -P ADMIN -H " $3 " chassis power off &"} NR % 1000 == 0 {print "sleep 1"}' > shutdown-off.sh
arp -an -ivlan2612 | awk -F '[ ()]' '/expires/ {print "ipmitool -U ADMIN -P ADMIN -H " $3 " chassis power status &"} NR % 1000 == 0 {print "sleep 1"}' > shutdown-status.sh
```
На выходе получаем 3 файла. Первый отправляет "добрую" команду отключения, второй - "жесткую", третий опрашивает статус.Статус удобнее всего обрабатывать так:
```sh
sh shutdown-status.sh 2>&1 >status
# дожидаемся отработки скрипта, после чего смотрим агрегированную статистику
sort status | uniq -c
```