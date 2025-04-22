#  Актуализированная процедура смены мастера RT

> TODO: Уточнить перечень сервисов зависимых от роли мастера, и сервисов, обслуживаемых на резервных серверах.

---
## Назначение
Данное руководство разработано с целью структурировать и описать основные шаги по изменению сервера, на котором расположен мастер Racktables (далее RT).

Основная сложность процедуры состоит в том, что от статуса мастера Racktables зависит целый ряд сервисов.  
При изменениях в подсистемах данных сервисов, таких как обновление ПО, или изменение скриптов, сценарий переезда может изменяться.  
Предполагается, что упрощение процедуры или повторяющиеся проблемы будут отражены в данном руководстве инженерами, ответственными за последний переезд.

Если процедура станет достаточно предсказуемой, она должна быть автоматизирована(заскриптована) или превращена в регламент.

---
## Ограничения и область применения
* В текущей редакции процедуры смена мастера RT происходит только между *noc-sas.yndx.net* и *noc-myt.yndx.net*
* На текущий момент *man1-rt1.yndx.net* не поддерживает все сервисы мастера
* Мастер netmap может переноситься отдельно от мастера RT без дополнительных известных рисков
* Сервер мастера MySQL mysync должен соответствовать мастеру RT, в противном случае нельзя гарантировать скорость работы и стабильность ряда сервисов
---
## Подготовка и планирование работ {#prepare}
Переезд мастера RT должен предваряться созданием [запроса на изменение NOCRFCS](https://forms.yandex-team.ru/surveys/21525/).
[Пример запроса](https://st.yandex-team.ru/NOCRFCS-7922). 
Инженер, ответственный за выполнение работ(далее *инженер*), перед исполнением должен убедиться в следующем:
* Запрос на изменение согласован
* Время работ не пересекается с другими важными работами в NOC, где задействуются сервисы Racktables
* Время работ не пересекается с важными мероприятиями компании с участием сетевой инфраструктуры (например Хурал)
* Инженер может авторизоваться по ssh-ключам на серверах RT и имеет sudo.
* У инженера есть доступ в [permissions](https://racktables.yandex-team.ru/index.php?page=perms)
* Посмотреть текущие события в [heatmap](https://heat.yandex-team.ru/#/nocdev)
* Старый и новый мастер присутствуют в active nodes статуса mysync (`mysync info -s`)
* Сервера RT должны иметь одинаковые версии коммитов в локальных репозиториях RT. 
  Если изменения вносились в обход gitlab - уточнить их статус у коллег. 
  - `/home/racktables/rt-yandex.git`
  - `/usr/local/rt-yandex.git`
Перед началом работ желательно кинуть клич в чаты (и убедиться в участии в этих группах на случай проблем)
* "[NOCDEV Support](https://t.me/joinchat/BKHmxB0PGFLM1FyunrOV3w)"
* "NOC координация"
>Если смена мастера происходит в аварийном, а не плановом режиме, текущие риски могут перевешивать риски от игнорирования подготовительных процедур. 
---
## Высокоуровневое описание процедуры
Новый мастер (далее ***NEW***) - сервер RT, который примет роль мастера после проведения работ.  
Старый мастер (далее ***OLD***) - сервер RT, который имеет действующую роль мастера до активной фазы работ. В рамках процедуры сервер сохраняет название ***OLD*** до самого конца работ.

0. Снять RO с ***NEW*** (если ещё по каким-то причинам не снят) и ***OLD***
1. Остановить CRON на ***NEW*** и ***OLD***
2. Запустить предварительную синхронизацию
3. Дождаться завершения CRON задач или остановить текущие
4. Остановить RT master на ***OLD***
    * Остановить mpdaemon
    * Остановить rtapi-rw
    * Остановить netmap master
    * Остановить RT master
5. Переключить MySQL-мастер для узлов с установленным stopzk (noc-myt, noc-sas)
6. Запустить master на ***NEW***
    * Переключить MySQL-мастер
    * Повторить синхронизацию
    * Запустить RT master
    * Запустить netmap master
    * Запустить rtapi-rw
    * Запустить mpdaemon
8. Финальные изменения
    * Запустить CRON
    * Установить новый мастер в permissions

<table style="border-left:4px solid #ffde40; margin:20px; width:90%; background-color:#f1f1e1">
<tr valign="middle" style="vertical-align: middle;"><td style="vertical-align: middle; padding:20px; 20px 0 0px; text-align:left;">
Перевозить мастера netmap можно отдельно от мастера RT. 
</td></tr></table>
<table style="border-left:4px solid #e45d50; margin:20px; width:90%; background-color:#fbe8e6">
<tr valign="middle" style="vertical-align: middle;"><td style="vertical-align: middle; padding:20px; 20px 0 0px; text-align:left;">
TODO: Уточнить. Согласно коментариям скрипта по синхронизации, необходимо останавливать и запускать: сервисы rtapi(sudo service -l | grep rtapi), nginx, php-fpm.
</td></tr></table>

**Переключение мастера MySQL**  
[Подробнее про резервирование mysql и mysync](https://wiki.yandex-team.ru/noc/racktables/mysqlsetup/)  
В стандартном случае, мастер RT и мастер MySQL должны совпадать. Это важно для скорости работы.  
Переключать можно с любого узла кластера.  

В прикреплённых командах будут встречаться переменные окружения, которые можно установить перед выполенением процедур для возможности использовать copy-paste:
```bash
export NEW_MASTER=***NEW_FQDN***
export OLD_MASTER=***OLD_FQDN***
export NEW_MASTER_IP=`host $NEW_MASTER | grep IPv6 | cut -d ' ' -f 5`
```
---
## Снять RO с ***NEW*** (если ещё по каким-то причинам не снят) и ***OLD***
На текущий момент noc-сервера не обслуживают RO нагрузку, поэтому стоит убедиться, что RO-адреса с них сняты.
Формально выполнение работ, согласованных в NOCRFCS, начинается с этого этапа.
```bash
sudo ifconfig gif255 inet 93.158.157.117 127.0.0.117 netmask 255.255.255.255 -alias
sudo ifconfig gif254 inet6 2a02:6b8:0:3400::117/128 -alias
```
---
## Остановить CRON на ***NEW*** и ***OLD***
Crontab опирается на наличие или отсутствие файла "nocron" (`/home/racktables/nocron`).

Установка nocron останавливает запуск новых задач, но не останавливает выполнение уже запущенных. При этом, уже запущенные задачи могут иметь установленные подключения к MySQL-master'у и продолжать производить записи в БД. При переключении MySQL-мастера через mysync на старом мастере переменная read_only будет установлена в значение 1 и задача остановится с ошибкой при следующей попытке записать в БД. Лучше такой ситуации избежать дождавшись завершения всех CRON-задач.

С другой стороны, продолжительная работа с установленным nocron может вызвать слишком большое устаревание экспортов для потребителей использующих RW домен. Поэтому наилучший результат можно достичь правильно подгадав время остановки кронов, когда долго выполняемые задачи уже остановились.

Наиболее безопасным будет установка nocron как на ***OLD**, так и на ***NEW*** до полного переключения мастера.
```bash
sudo touch /home/racktables/nocron
```

>TODO: разделить CRON задачи на RO и RW
>TODO: уточнить текущее состояние редиректов для экспортов с RW домена на RO домен
---
## Запустить предварительную синхронизацию
***NEW*** и ***OLD*** необходимо синхронизировать на уровне ряда директорий.  
Для этого есть [скрипт](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/blob/master/once-scripts/sync_from_master.sh)    
Как и весь репозиторий rt-yandex, скрипт располагается в домашней директории пользователя racktables:   
`/home/racktables/rt-yandex.git/once-scripts/sync_from_master.sh`  

Скрипт будет необходимо запускать на ***NEW***, изменив значение переменной "OLD_MASTER" на FQDN-имя ***OLD***. Если переменная экспортирована в окружение, то переписывать в файле её не нужно.
Скрипт активно использует ssh для доступа к ***OLD***. Не забудьте про "ssh agent forwarding" при заходе на ***NEW***. (`ssh -A $fqdn`)  
Для синхронизации netmap можно воспользоваться DO_netmap_slave.sh
```bash
cd /home/racktables/rt-yandex.git/once-scripts  
sudo -H -u racktables OLD_MASTER=$OLD_MASTER ./sync_from_master.sh
sudo -H -u racktables bash -c 'cd /netmap && lockf -s -t0 /tmp/netmap-slave.lock src/DO_netmap_slave.sh'
```
>TODO: автоматизировать синхронизацию /www/export  
>`#rsync error: some files/attrs were not transferred (see previous errors) (code 23) at main.c(1837) [generator=3.2.3]`  
---
## Дождаться завершения CRON задач или остановить текущие
Контроллировать текущее состояние можно при помощи
```bash
ps auxwwwf | grep -E "cron|php" | grep -v -E "php-fpm|rtapi2rr|graphql|API_server"
```
и
```bash
sudo -H -u racktables rtcronsh --show
```
Если какие-то задачи не могут завершиться слишком продолжительное время в большинстве случаев лучшем решением будет их остановить при помощи `kill`.
>TODO: Определить список задач, которые безопасно останавливать
---
## Остановить RT master на OLD
Роль мастера определяется наличием файлов `/home/racktables/netmap-master` и `/home/racktables/master` соответственноо.
```bash
sudo service mpdaemon stop && \
sudo sysrc mpdaemon_enable=NO && \
sudo service rtapi-rw-server stop && \
sudo rm -v /home/racktables/netmap-master && \
sudo rm -v /home/racktables/master
```
---
## Переключить MySQL-мастер для узлов с установленным stopzk (noc-myt, noc-sas)
zk-mysql обновляет файлы mysql_master, mysql_ro, mysql_ips.php в /home/racktables/ . На них ссылаются различные воркеры, чтобы подключаться к MySQL. mysql_master и mysql_ro - старая схема переключения и в текущий момент не должна использоваться. На смену ей пришёл mysql_ips.php. Но пока желательно обновлять мастера в обеих схемах.
>Требуется дополнительное тестирование этих команд... Всякие тесты они проходят, но при переключениях у меня пока ни разу нормально не отработали(возможно слишком сильно задумываются над ssh'ем) и приходилось править в полуручном режиме...
```bash
ssh $OLD_MASTER "sudo -H -u racktables bash -c 'echo [$NEW_MASTER_IP] > /home/racktables/mysql_master'"
ssh $OLD_MASTER "sudo -H -u racktables sed -e \"s/mysql_master=.*$/mysql_master='[${NEW_MASTER_IP}]';/\" -i .bak /home/racktables/mysql_ips.php"
ssh $NEW_MASTER "sudo -H -u racktables bash -c 'echo localhost > /home/racktables/mysql_master'"
ssh $NEW_MASTER "sudo -H -u racktables sed -e \"s/mysql_master=.*$/mysql_master='localhost';/\" -i .bak /home/racktables/mysql_ips.php"
```
>TODO: Подумать над тем, чтобы снять stopzk в том числе на мастерах или перебраться на схему с MySQL Proxy, чтобы отпилить выбор MySQL из кода RT.
---
## Запустить master на NEW
```bash
sudo mysync switch --to $NEW_MASTER && \
sudo bash -c 'echo localhost > /home/racktables/mysql_master' && \
sudo -H -u racktables OLD_MASTER=$OLD_MASTER /home/racktables/rt-yandex.git/once-scripts/sync_from_master.sh && \
sudo -H -u racktables bash -c 'cd /netmap && lockf -s -t0 /tmp/netmap-slave.lock src/DO_netmap_slave.sh' && \
sudo touch /home/racktables/master && \
sudo touch /home/racktables/netmap-master && \
sudo sysrc mpdaemon_enable=YES && \
sudo service rtapi-rw-server start && \
sudo service mpdaemon start
```

## Финальные изменения
**Если NEW стартовал успешно:**
```bash
sudo rm -v /home/racktables/nocron
```
Поменять предикат [мастер RT]  в [permissions](https://racktables.yandex-team.ru/index.php?page=perms).

Раньше на backup_master возвращали RO нагрукзу (сейчас это не делается):
```bash
sudo ifconfig gif255 inet 93.158.157.117 127.0.0.117 netmask 255.255.255.255 alias
sudo ifconfig gif254 inet6 2a02:6b8:0:3400::117/128 alias
ifconfig | egrep '93.158.157.117|2a02:6b8:0:3400::117'
```
[Статус балансировщиков](https://racktables.yandex-team.ru/index.php?page=ipvs&tab=default&vs_id=46)
---
## Проверки
<table style="border-left:4px solid #e45d50; margin:20px; width:90%; background-color:#fbe8e6">
<tr valign="middle" style="vertical-align: middle;"><td style="vertical-align: middle; padding:20px; 20px 0 0px; text-align:left;">
TODO: Составить каталог сервисов RT и проверки для них.
</td></tr></table>

* При попытке доступа по https, в ответных заголовках будут поля ***X-RT-Server*** и ***X-RT-RW***, содержащие FQDN нового мастера(NEW)  
* Проверить текущие события в [heatmap](https://heat.yandex-team.ru/#/nocdev).
* Проверить на ***OLD***, что mpdaemon и rtapi-rw-server полностью потушились (NOCDEVDUTY-744) и добить по необходимости.
```bash
ps auxwww | grep -E "rtapi-rw-server|multiport"
```
