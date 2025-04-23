
## Введение
Данное руководство описывает механизм ввода в работу сетевого оборудования в датацентрах Яндекса.

### Глоссарий

* *Наливка* - процесс доставки (через консольный порт либо ZTP) на новое сетевое устройство минимальной достаточной конфигурации для последующего ввода устройства в работу
* *Ввод в работу* - процесс доставки на новое сетевое устройство и его соседей необходимой конфигурации (в частности протоколов машрутизации), после чего устройство считается готовым к работу
* *Racktables, РТ* - наш основной инвентори для сетевых устройств и источник правды
* *Аннушка, ann* - наша утилита для генерации и деплоя конфигурации на сетевые устройства
* *Объект Racktables* - в контексте данного документа - сущность представляющая свитч внутри Racktables
* *Тег Racktables* - основной способ разметки метаинформации в Racktabes, обычно представляется в виде `{some text}`, например: `{серверный свитч}` или `{свитч для IPMI}`
* *Racktables Object-Id, object-id* - уникальный идетификатор объекта в Racktables
* *Мастер Racktables, мастер* - сервер Racktables на котором база доступна для записи (не в read-only) и на котором запускается логика наливки и ввода в работу. На данный момент один из двух серверов - `noc-myt` либо `noc-sas`. Определить который можно существованию файла `/home/racktables/master`.
* *PNS, ПНС, пункт наливки свитчей* - часть Racktables содержащая логику импортирования нового оборудования и создания новых объектов в Racktables, лежит в `plugins/pns.php`
* *mpdaemon, multiprotocol daemon, консольный демон, switchconf* - сервис который представляет для PNS интерфейс для консоляторов, через которые доставляется первоначальный конфиг когда свитч совершенно пустой
* *Метод, файл .php* - здесь и далее мы ссыемся на методы и файлы в коде Racktables

### Ссылки
* [Racktables web](https://racktables.yandex-team.ru),  [Racktables git](https://noc-gitlab.yandex-team.ru/nocdev/racktables)
* [Ann git](https://noc-gitlab.yandex-team.ru/nocdev/annushka)
* [PNS web](https://racktables.yandex-team.ru/index.php?page=switchgen), [PNS git](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/blob/master/plugins/pns.php)
* [ mpdaemon git](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/tree/master/switchconf)

### Видео с рассказом про устройство
<video src="https://wiki.yandex-team.ru/azryve/nalivka-debug/.files/pns.mp4?download=1"
width="640" height="480" controls="controls">Печалька :(
<a href="https://wiki.yandex-team.ru/azryve/nalivka-debug/.files/pns.mp4?download=1"
target="_blank">Скачайте видео</a></video>

если видео не проигрывается - [на диске](https://disk.yandex.ru/public/nda/?hash=EE6zbt7TxpuFhtfUkh0jTAYFLIgn4XMkdBR%2BwD9B9Ih%2B9zXeZi1Pe3%2B%2BbHBpWNw7q/J6bpmRyOJonT3VoXnDag%3D%3D)

### Целевая аудитория
* Инженеры NOC, ответственные за пуско-наладку и эксплуатацию сетевого оборудования
* Инженеры службы сетевой разработки NocDev

#### Схемы

{% cut "Диаграмма логики" %}

![](_images/nalivka/img1.png)

{% endcut %}  

{% cut "Диаграмма данных" %}

![](_images/nalivka/img2.png)

{% endcut %}  

#### Наливка
У нас есть два типа наливок для линуксовых свичей: для Cumulus и для Switchdev.  
Если есть необходимость переключить наливку, то нужно сделать следующее:
1) Проверить текущий [статус](http://sas1-cumulus-zeroconf.yndx.net/status) переключателя наливки
2) Проверить что в [ПНС](https://racktables.yandex-team.ru/index.php?page=switchgen) сейчас ничего не льется из текущей настройки (в противном случае они повиснут и потребуется их ребут, не считая того что можете расстроить автора задания на наливку)
3) Зайти на <sas1-cumulus-zeroconf.yndx.net> и сначала погасить текущую и включить нужную наливку:

{% cut "- Нам нужен Cumulus:" %}

```
sudo systemctl stop ztpd
sudo systemctl start cumulus-zeroconf.service
sudo systemctl status cumulus-zeroconf.service
```

{% endcut %}  

{% cut "- Нам нужен Switchdev:" %}

```
sudo systemctl stop cumulus-zeroconf.service
sudo systemctl start ztpd
sudo systemctl status ztpd
```

{% endcut %}  

Логи наливки Switchdev следует смотреть в `sudo journalctl -fu ztpd`

```
azryve@sas1-cumulus-zeroconf ~ $ sudo journalctl -fu ztpd
-- Logs begin at Tue 2022-06-28 12:11:13 MSK. --
Jun 28 13:33:26 sas1-cumulus-zeroconf.yndx.net ztpd[29270]: 2022-06-28T13:33:26.752+0300        INFO        plugins/ztp        ztp/ztp.go:54        ZTP switch mac: b4:2e:99:5b:7d:e6, vendor class id: PXEClient:Arch:00000:UNDI:002001, relay ip: 172.24.207.254
Jun 28 13:33:26 sas1-cumulus-zeroconf.yndx.net ztpd[29270]: 2022-06-28T13:33:26.752+0300        INFO        server        server/handle.go:183        MainHandler4: dropping request because response is nil
Jun 28 13:33:27 sas1-cumulus-zeroconf.yndx.net ztpd[29270]: 2022-06-28T13:33:27.868+0300        INFO        plugins/ztp        ztp/ztp.go:54        ZTP switch mac: 0c:c4:7a:dd:8b:dc, vendor class id: udhcp 1.23.1, relay ip: 172.24.207.254
Jun 28 13:33:27 sas1-cumulus-zeroconf.yndx.net ztpd[29270]: 2022-06-28T13:33:27.868+0300        INFO        server        server/handle.
```

#### Ввод в работу

Под вводом в работу свитча (далее `инициализация`) понимается доставка(`выкатка`) на него полного набора настроечных параметров (`конфигурации | конфига`).  
Данный процесс происходит после, строго после, наливки свитча, когда на нем уже имеется минимальная конфигурация, достаточная для того, чтобы Racktables доступ к свичу.

Этапы инициализации:

* Получение списка портов со свитча и их настройка
* Аллокация пользовательских сетей
* Настройки bgp и все, что с ними связано (в т.ч. пиры и политики)
* Настройка нового bgp-пира на смежных устройства

В зависимости от локации и типа вводимого в работу устройства данные шаги могут пропускаться. Ниже мы подробнее рассмотрим окружение при начале наливки и шаги на примере условного тора.

#### Начальное окружение
При вводе в работу объект свитча уже создан в Racktables с минимальным необходимым набором атрибутов и на свитч выкачен PNS'ом через консоль минимальный конфиг. Наиболее важные атрибуты включают в себя 

* Имя устройства, хостнейм
* На устройство повешен mgmt адрес из управляющей сети с тегом `{управляющая сеть}`
* Теги типа устройства - например `{серверный свитч}` либо `{spine1}`
* Теги `{ещё не работает}` `{ожидает ввода в работу}`

{% cut "Скриншот объекта готового к вводу в работу" %}

![](_images/nalivka/img3.png)

{% endcut %}  

На тег `{ожидает ввода в работу}` как раз завязана логика вкладки "Ввести в работу" через которую можно запустить процесс ввода в работу свитча. Подробнее в разделе ниже.

На свитче минимальный конфиг включает в себя

* Обновленный до целевой версии софт
* Рабочий и доступный mgmt интерфейс
* Добавлен локальный пользователь racktables
* Настройки управляющих протоколов ssh, lldp, snmp, etc.
* Порты рассплитованы в нужную конфигурацию

Данный конфиг генерируется вообще говоря двумя возможными способами: через копию аннушки на сервере Racktables, либо через генерацию m4 шаблона. Способ выбирается на предыдущем шаге согласно логике указанной в pns.php структуре. В случае если для устройства указано `use_annushka: true` - мы используем первый способ, в обратном случае - второй.


#### Запуск ввода в работу
Ввод в работу может быть инициирован двумя способами - вручную и автоматически.

Ручной способ предполагает то что инженер noc заходит на вкладку "Ввести в работу" на объекте Racktables и нажимает кнопку "Начать".

{% cut "Скриншот вкладки Ввод в работу" %}

![](_images/nalivka/img4.png)

{% endcut %} 

При нажатии кнопки начать форма тут же пытается зайти на свитч и начать процесс распознания. После чего пользователь переправляется на главную страницу устройства на которой отображаются успешные и не успешные шаги выполненные Racktables. Не все шаги выполняются в контексте формы, так называемая L3-инициализация ставится в очередь в виде отложенной задачи в случае успешного распознания и выполняется асинхронно. Более подробно о шагах процесса смотри ниже.

Автоматический способ запуска включается до того как свитч переходит в готовое для ввода в работу состояние, через форму постановки свитча в наливку чекбоксом "Try to auto init". Чекбокс включен по-умолчанию. Данный флаг добавляет на объект в Racktables тег `{автоматически ввести в работу}`. Когда устройство готово к наливке при наличии данного тега на объекте Racktables ставит в очередь процесс запуска ввода в работу. Описание выполненных шагов отправляется письмом на почту выбранную в форме постановки свитча в наливку параметром Ticket assignee. В данный момент это рассылки hdmon@ либо itdc@ - офисные и датацентровые хелпы соотвественно.

{% cut "Скриншот формы постановки свитча в наливку" %}

![](_images/nalivka/img9.png)

{% endcut %} 


#### Ввод в работу
Сам процесс ввода в работу разделен на первый и второй этапы.

1) Распознание (дискавери) - импортирование и валидация данных в Racktables
2) L3-инициализация - Аллокация подсетей (если требуется) и выкатка конфигурации на свитч и его соседей

Первый шаг предполагает исключительно получение информации от свитча и модификацию объекта в Racktables согласно полученным данным. Второй шаг же - выкатка и применение конфигурации получившейся на основе созданного в Racktables объекта. Обе части логики располагаются в init-switch.php в методах `do_initSwitchStage1` и `do_initSwitchStage2` соответсвенно.

#### Распознание
При распознании устройства выполняются следующие шаги

* SNMP синхронизация
* LLDP синхронизация
* Валидация аплинков
* Импорт 8021Q конфигурации


Логика лежит в методе `do_initSwitchStage1`.

#### SNMP синхронизация
Логика расположена в методе `doSNMPmining`. Со свитча стягиваются при помощи snmpwalk несколько MIB'ов. Через `sysObjectID.0` проставляется тип софта на устройстве согласно словарю `$known_switches` в snmp.php.

{% cut "Пример маппинга в $known_switches" %}

```
$known_switches['30065.1.3011.7260.2733.3.64'] = [
	'dict_key'   => 83814,
	'text'       => 'Arista 7260CX3-64-F',
	'processors' => ['arista-any-QSFP28', 'arista-any-SFP+', 'arista-management'],
];
```

{% endcut %} 

Через ifDescr, ifPhysAddress получается список физических портов. Полученные имена преобразуются в сокращенные наименования согласно методам указанным в словаре `$iftable_processors`, ключи которых указываются в поле `processors` словаря `$known_switches`. Пример метода `arista-management` который сокращает именование Mgmt-порта вида `Management0` на свитчах Arista в `ma0`

{% cut "Пример метода arista-management" %}

```
$iftable_processors['arista-management'] = [
	'pattern'       => '@^Management([[:digit:]](/[[:digit:]])?)$@',
	'replacement'   => 'ma\1',
	'dict_key'      => '1-24',
	'try_next_proc' => FALSE,
];
```

{% endcut %} 

#### LLDP синхронизация
LLDP синхронизация предполагает получение актуальной информации о текущих соседях наливаемого устройства. В частности это:

* IPMI-свитч в который коммутируется MGMT-порт
* Вышестоящие свитчи в которые коммутируются аплинки

Логика LLDP синхронизации доступна для любого устройства на его вкладке Live LLDP, логика ввода в работу просто ее переиспользует. При запуске LLDP синхронизации (как и при клике на вкладку) Racktables

* Идет на устройство и стягивает через cli текущий список LLDP соседей
* По имени соседа пытается найти его среди устройств существующих в Racktables, а так же порт которым сосед скоммутирован
* Строит diff по тому состоянию коммутаций которое существует для устройства в данный момент и тому которое показывает LLDP

В рамках данной логики, возможны конфликты, которые механизм LLDP синхронизации не знает как разрешить. 
В случае возникновения любого конфликта, шаг LLDP синхронизации потребует вмешательства инженера для решения конфликта. Для примера скриншот вкладки Live LLDP который показывает 3 порта с разным возможным состоянием в диффе:

{% cut "Скриншот" %}

![](_images/nalivka/img5.png)

{% endcut %} 

Зеленым помечены консистентные коммутации, отсутствующие в данный момент коммутации, но готовые к импорту. Красным помечены конфликты.

* **me0/0/0** (зеленый) текущая коммутация и показания LLDP совпадают
* **100ge1/0/2** (желтый) текущая коммутация отсутсвует, но LLDP указывает на свободный порт
* **100ge1/0/2** (красный) текущая коммутация не совпадает, а удаленный порт занят другой коммутацией


#### L3-инициализация
L3-инициализация последний шаг ввода свитча в работу после ее удачного выполнения свитч помечается как рабочий и с него снимаются оффлайновые теги. В отличии от распознания она выполняется только для L3-свитчей которым для работы нужна конфигурация BGP-протокола. На текущий момент это ToR'ы и spine1, spine2.

При этом она, в отличии от распознания, всегда происходит асинхронно и вызывается через контекст отложенной задачи в Racktables. Механизм отложенных задач (aka Task, TaskQueue), является частью Racktables и не привязан конкретно к вводу в работу. Отложенная задача представляет собой имя метода который будет вызван и аргументов которые будут ему переданы. Добавление задачи в очередь осуществляется через метод `registerTask`. Разбор очереди запускается cron'ом на мастер-сервере Racktables.

В L3-инициализации можно выделить три шага, превый из которых вообще выполняется только для ToR-свитчей

* Аллокация пользовательский ipv6-сетей для ToR
* Выкатка конфигурации на вводимый в работу свитч
* Выкатка конфигурации на вышестоящие свитчи

Логика целиком лежит в методе `do_initSwitchStage2`. При ошибке выполнения любого из шагов процесс фейлится и откладывается на перезапуск. Перезапуск происходит через `N*15` минут, где N - порядковый номер попытки. Таким образом, чем больше раз процесс завершается неудачей, тем реже мы пытаемся его перезапустить. Максимальное количество повторов - 5.

#### Аллокация пользовательский ipv6-сетей для ToR
TODO

#### Выкатка конфигурации на вводимый в работу свитч

Выкатка конфигурации на ToR происходит через запуск аннушки - `ann deploy`. На каждом Racktables-сервере есть локальный так называемый "наливочный" репозиторий аннушки в `~racktables/gitworkdir/annushka-production/ann`. Вокруг него написано чуть-чуть логики Racktables в `annushka.php`.

После того как устройство было слинковано по LLDP и на него аллоцированы сети annushka должна на основе это информации сгенерировать всю релевантную L3-конфигурацию. Точные аргументы передаваемые `ann.py` можно изучить в методе `execTorJob`, при этом каждый запуск логируется во временные файлы `/var/tmp/rt-ann-deploy.*`. Пример таких файлов для свитча sas2-12s17:

{% cut "Файлы выкатки" %}

```
[azryve@noc-myt ~]$ ls -lct /var/tmp/rt-ann-deploy.sas2-12s17*
-rw-r--r--  1 gondar  wheel  5165 Aug  5 16:48 /var/tmp/rt-ann-deploy.sas2-12s17.AtkdL7
-rw-r--r--  1 gondar  wheel  2375 Aug  5 15:57 /var/tmp/rt-ann-deploy.sas2-12s17.pR1FVu
-rw-r--r--  1 gondar  wheel  2375 Aug  5 15:50 /var/tmp/rt-ann-deploy.sas2-12s17.KiB7cx
```

{% endcut %} 

{% cut "Лог успешной выкатки" %}

```
[azryve@noc-myt ~]$ cat /var/tmp/rt-ann-deploy.sas2-12s17.AtkdL7 
Calling annushka: --filter-acl /var/tmp/rt-ann-acl.sas2-12s17.zOT0bZ --cache - -Gqos sas2-12s17

# -------------------- sas2-12s17.yndx.net --------------------

exception:


commands:
system-view
undo bgp
commit
interface 100GE1/0/1
undo ipv6 address FE80::E89:D1 link-local
ipv6 address FE80::E17:D1 link-local
description sas-90d1 100ge4/0/10
quit
interface 100GE1/0/2
undo ipv6 address FE80::E89:D2 link-local
ipv6 address FE80::E17:D2 link-local
description sas-90d2 100ge4/0/10
quit
interface 100GE1/0/3
undo ipv6 address FE80::E89:D3 link-local
ipv6 address FE80::E17:D3 link-local
description sas-90d3 100ge4/0/10
quit
interface 100GE1/0/4
undo ipv6 address FE80::E89:D4 link-local
ipv6 address FE80::E17:D4 link-local
description sas-90d4 100ge4/0/10
quit
bgp 65002.12017
router-id 178.154.177.72
ipv4-family unicast
quit
ipv6-family vpn-instance Hbf
load-balancing as-path-relax
import-route direct route-policy IMPORT_DIRECT
maximum load-balancing 16
group S1 external
peer FE80::90:C1 as-number 65002.65090
peer FE80::90:C2 as-number 65002.65090
peer FE80::90:C3 as-number 65002.65090
peer FE80::90:C4 as-number 65002.65090
peer FE80::90:C1 group S1
peer FE80::90:C1 connect-interface 100GE1/0/1
peer S1 advertise-community
peer S1 route-policy TOR_IMPORT_S1 import
peer S1 route-policy TOR_EXPORT_S1 export
peer FE80::90:C2 group S1
peer FE80::90:C2 connect-interface 100GE1/0/2
peer FE80::90:C3 group S1
peer FE80::90:C3 connect-interface 100GE1/0/3
peer FE80::90:C4 group S1
peer FE80::90:C4 connect-interface 100GE1/0/4
peer S1 bfd min-tx-interval 500 min-rx-interval 500 detect-multiplier 4
peer S1 bfd enable
quit
quit
commit
q
save

trace:

Info: The max number of VTY users is 8, the number of current VTY users online is 5, and total number of terminal users online is 5.
      The current login time is 2021-08-05 16:48:27+03:00.
      The last login time is 2021-08-05 16:47:54+03:00 from 77.88.1.117 through SSH.
<sas2-92s89>screen-length 0 temporary
Info: The configuration takes effect on the current user terminal interface only.
<sas2-92s89>system-view
Enter system view, return user view with return command.
[~sas2-92s89]undo bgp
Warning: The BGP process will be deleted. Continue? [Y/N]:Y
[*sas2-92s89]commit
[~sas2-92s89]interface 100GE1/0/1
[~sas2-92s89-100GE1/0/1]undo ipv6 address FE80::E89:D1 link-local
[*sas2-92s89-100GE1/0/1]ipv6 address FE80::E17:D1 link-local
[*sas2-92s89-100GE1/0/1]description sas-90d1 100ge4/0/10
[*sas2-92s89-100GE1/0/1]quit
[*sas2-92s89]interface 100GE1/0/2
[*sas2-92s89-100GE1/0/2]undo ipv6 address FE80::E89:D2 link-local
[*sas2-92s89-100GE1/0/2]ipv6 address FE80::E17:D2 link-local
[*sas2-92s89-100GE1/0/2]description sas-90d2 100ge4/0/10
[*sas2-92s89-100GE1/0/2]quit
[*sas2-92s89]interface 100GE1/0/3
[*sas2-92s89-100GE1/0/3]undo ipv6 address FE80::E89:D3 link-local
[*sas2-92s89-100GE1/0/3]ipv6 address FE80::E17:D3 link-local
[*sas2-92s89-100GE1/0/3]description sas-90d3 100ge4/0/10
[*sas2-92s89-100GE1/0/3]quit
[*sas2-92s89]interface 100GE1/0/4
[*sas2-92s89-100GE1/0/4]undo ipv6 address FE80::E89:D4 link-local
[*sas2-92s89-100GE1/0/4]ipv6 address FE80::E17:D4 link-local
[*sas2-92s89-100GE1/0/4]description sas-90d4 100ge4/0/10
[*sas2-92s89-100GE1/0/4]quit
[*sas2-92s89]bgp 65002.12017
[*sas2-92s89-bgp]router-id 178.154.177.72
[*sas2-92s89-bgp]ipv4-family unicast
[*sas2-92s89-bgp-af-ipv4]quit
[*sas2-92s89-bgp]ipv6-family vpn-instance Hbf
[*sas2-92s89-bgp-6-Hbf]load-balancing as-path-relax
[*sas2-92s89-bgp-6-Hbf]import-route direct route-policy IMPORT_DIRECT
[*sas2-92s89-bgp-6-Hbf]maximum load-balancing 16
[*sas2-92s89-bgp-6-Hbf]group S1 external
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C1 as-number 65002.65090
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C2 as-number 65002.65090
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C3 as-number 65002.65090
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C4 as-number 65002.65090
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C1 group S1
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C1 connect-interface 100GE1/0/1
[*sas2-92s89-bgp-6-Hbf]peer S1 advertise-community
[*sas2-92s89-bgp-6-Hbf]peer S1 route-policy TOR_IMPORT_S1 import
[*sas2-92s89-bgp-6-Hbf]peer S1 route-policy TOR_EXPORT_S1 export
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C2 group S1
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C2 connect-interface 100GE1/0/2
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C3 group S1
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C3 connect-interface 100GE1/0/3
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C4 group S1
[*sas2-92s89-bgp-6-Hbf]peer FE80::90:C4 connect-interface 100GE1/0/4
[*sas2-92s89-bgp-6-Hbf]peer S1 bfd min-tx-interval 500 min-rx-interval 500 detect-multiplier 4
[*sas2-92s89-bgp-6-Hbf]peer S1 bfd enable
[*sas2-92s89-bgp-6-Hbf]quit
[*sas2-92s89-bgp]quit
[*sas2-92s89]commit
Committing....done.
[~sas2-92s89]q
<sas2-92s89>save
Warning: The current configuration will be written to the device. Continue? [Y/N]:Y
Now saving the current configuration to the slot 1 ..........
Info: Save the configuration successfully.
<sas2-92s89>

####  bulk deploy report
Done :   1 of 1   25.6/25.6/25.6/-  (min/max/avg/stdev)
  sas2-12s17.yndx.net
```

{% endcut %} 

{% cut "Лог неуспешной выкатки - свитч еще не пророс в DNS" %}

```
[azryve@noc-myt ~]$ cat /var/tmp/rt-ann-deploy.sas2-12s17.pR1FVu
Calling annushka: --filter-acl /var/tmp/rt-ann-acl.sas2-12s17.HlrwNc --cache - -Gqos sas2-12s17

[15:57:38]   ERROR MainProcess - deploy.py:269 - sas2-12s17.yndx.net ConnectionException(args=("unable to connect. errors=[gaierror(8, 'Name does not resolve')],
conn_fabric=[ConnFabric[functools.partial(<class 'comocutor.streamer.NocauthSshStream'>, host='sas2-12s17.yndx.net',
ssh_opts={'kex_algs': ['diffie-hellman-group1-sha1', 'diffie-hellman-group-exchange-sha1'], 'encryption_algs': ['aes128-cbc', '3des-cbc']}), None],
ConnFabric[functools.partial(<class 'comocutor.streamer.TelnetStream'>, host='sas2-12s17.yndx.net'), None]]",),auxiliary=None) -- 
```

{% endcut %} 


#### Выкатка конфигурации на вышестоящие свитчи
В зависимости от того какую роль занимает наливаемый свитч нам может быть необходимо выкатить конфигурацию нового пира на вышестоящий свитч. Для ToR'а вышестоящим свитчем является spine1. Для spine1 - spine2. Для spine2 данный шаг не выполняется.

Для определения какие именно свитчи являются вышестоящими используется выгрузка из аннушки - `ann x-show-mesh <device>`. Она выводит набор сессий которые поднимались на целевом устройстве. Пример вызова для ToR'a sas2-12s17:

{% cut "ann x-mesh-show sas2-12s17" %}

```(yaml)
# -------------------- sas2-12s17 --------------------
sessions:
-   local:
        asnum: '65002.12017'
        bfd: true
        device: sas2-12s17
        export_policy: TOR_EXPORT_S1
        ifname: 100GE1/0/1
        import_policy: TOR_IMPORT_S1
        ll: fe80::e17:d1
        name: TOR
        parallel_count: 1
        peers_min: 4
        portname: 100GE1/0/1
        router_id: 178.154.177.72
        send_community: true
        vrf: Hbf
    remote:
        advertise_inactive: true
        asnum: '65002.65090'
        bfd: true
        device: sas-90d1
        export_policy: S1_EXPORT_TOR
        ifname: 100GE4/0/10
        import_policy: S1_IMPORT_TOR
        ll: fe80::90:c1
        multipath: 32
        name: S1
        parallel_count: 1
        passive: true
        portname: 100GE4/0/10
        router_id: 1.80.90.1
        send_community: true
        vrf: ''
-   local:
        asnum: '65002.12017'
        bfd: true
        device: sas2-12s17
        export_policy: TOR_EXPORT_S1
        ifname: 100GE1/0/2
        import_policy: TOR_IMPORT_S1
        ll: fe80::e17:d2
        name: TOR
        parallel_count: 1
        peers_min: 4
        portname: 100GE1/0/2
        router_id: 178.154.177.72
        send_community: true
        vrf: Hbf
    remote:
        advertise_inactive: true
        asnum: '65002.65090'
        bfd: true
        device: sas-90d2
        export_policy: S1_EXPORT_TOR
        ifname: 100GE4/0/10
        import_policy: S1_IMPORT_TOR
        ll: fe80::90:c2
        multipath: 32
        name: S1
        parallel_count: 1
        passive: true
        portname: 100GE4/0/10
        router_id: 1.80.90.2
        send_community: true
        vrf: ''
-   local:
        asnum: '65002.12017'
        bfd: true
        device: sas2-12s17
        export_policy: TOR_EXPORT_S1
        ifname: 100GE1/0/3
        import_policy: TOR_IMPORT_S1
        ll: fe80::e17:d3
        name: TOR
        parallel_count: 1
        peers_min: 4
        portname: 100GE1/0/3
        router_id: 178.154.177.72
        send_community: true
        vrf: Hbf
    remote:
        advertise_inactive: true
        asnum: '65002.65090'
        bfd: true
        device: sas-90d3
        export_policy: S1_EXPORT_TOR
        ifname: 100GE4/0/10
        import_policy: S1_IMPORT_TOR
        ll: fe80::90:c3
        multipath: 32
        name: S1
        parallel_count: 1
        passive: true
        portname: 100GE4/0/10
        router_id: 1.80.90.3
        send_community: true
        vrf: ''
-   local:
        asnum: '65002.12017'
        bfd: true
        device: sas2-12s17
        export_policy: TOR_EXPORT_S1
        ifname: 100GE1/0/4
        import_policy: TOR_IMPORT_S1
        ll: fe80::e17:d4
        name: TOR
        parallel_count: 1
        peers_min: 4
        portname: 100GE1/0/4
        router_id: 178.154.177.72
        send_community: true
        vrf: Hbf
    remote:
        advertise_inactive: true
        asnum: '65002.65090'
        bfd: true
        device: sas-90d4
        export_policy: S1_EXPORT_TOR
        ifname: 100GE4/0/10
        import_policy: S1_IMPORT_TOR
        ll: fe80::90:c4
        multipath: 32
        name: S1
        parallel_count: 1
        passive: true
        portname: 100GE4/0/10
        router_id: 1.80.90.4
        send_community: true
        vrf: ''
```

{% endcut %} 

Из данной выгрузки мы получаем имена устройств на которые мы будем выкатывать настройки нового пира. Данный набор фильтруется чтобы оставить только вышестоящие свитчи по уже упомянутой схеме. Конкретные методы для каждого из типов инициализируемых устройств описаны в `init-switch.php`

{% cut "$actions_init_stage2" %}

```(php)
$actions_init_stage2 = [
	# Должен быть выше чем {серверный свитч}
	# Поскольку это его подтип
	'{ToR-агрегатор slave}' => [
		'fn' => 'do_initSwitchStage2TorAggSlave',
	],
	'{серверный свитч}' => [
		'fn' => 'do_initSwitchStage2',
	],
	'{spine1}' => [
		'fn' => 'do_initSwitchStage2Spine1',
	],
];
```

{% endcut %} 

Выкатка конфигурации так же генерит файл с логом в `/var/tmp/` как на предыдущем шаге. Примеры выкатки на один из спайнов для sas2-12s17:

{% cut "Лог выкатки на spine1 sas-90d4" %}

```
azryve@noc-myt /var/tmp]$ cat rt-ann-deploy.sas-90d4.PUrruN 
Calling annushka: --filter-acl /var/tmp/rt-ann-acl.sas-90d4.JpOsmK --cache - -Gqos --filter-peer sas2-12s17 sas-90d4

# -------------------- sas-90d4.yndx.net --------------------

exception:


commands:
system-view
interface 100GE4/0/10
ipv6 enable
ipv6 mtu 9000
ipv6 address FE80::90:C4 link-local
mtu 9000
quit
bgp 65002.65090
peer FE80::E17:D4 as-number 65002.12017
ipv6-family unicast
peer FE80::E17:D4 enable
peer FE80::E17:D4 group TOR
quit
peer FE80::E17:D4 group TOR
peer FE80::E17:D4 connect-interface 100GE4/0/10
quit
commit
q
save

trace:

Info: The max number of VTY users is 8, the number of current VTY users online is 4, and total number of terminal users online is 4.
      The current login time is 2021-08-05 16:52:52+03:00.
      The last login time is 2021-08-05 16:52:31+03:00 from 2A02:6B8:0:1482::100 through SSH.
<sas-90d4>screen-length 0 temporary
Info: The configuration takes effect on the current user terminal interface only.
<sas-90d4>system-view
Enter system view, return user view with return command.
[~sas-90d4]interface 100GE4/0/10
[~sas-90d4-100GE4/0/10]ipv6 enable
[*sas-90d4-100GE4/0/10]ipv6 mtu 9000
[*sas-90d4-100GE4/0/10]ipv6 address FE80::90:C4 link-local
[*sas-90d4-100GE4/0/10]mtu 9000
[*sas-90d4-100GE4/0/10]quit
[*sas-90d4]bgp 65002.65090
[*sas-90d4-bgp]peer FE80::E17:D4 as-number 65002.12017
[*sas-90d4-bgp]ipv6-family unicast
[*sas-90d4-bgp-af-ipv6]peer FE80::E17:D4 enable
Warning: This operation will reset the peer session. Continue? [Y/N]:Y
[*sas-90d4-bgp-af-ipv6]peer FE80::E17:D4 group TOR
[*sas-90d4-bgp-af-ipv6]quit
[*sas-90d4-bgp]peer FE80::E17:D4 group TOR
[*sas-90d4-bgp]peer FE80::E17:D4 connect-interface 100GE4/0/10
[*sas-90d4-bgp]quit
[*sas-90d4]commit
[~sas-90d4]q
<sas-90d4>save
Warning: The current configuration will be written to the device. Continue? [Y/N]:Y
Now saving the current configuration to the slot 13 ...
Info: Save the configuration successfully.
Now saving the current configuration to the slot 14 .......
Info: Save the configuration successfully.
<sas-90d4>

####  bulk deploy report
Done :   1 of 1   14.1/14.1/14.1/-  (min/max/avg/stdev)
  sas-90d4.yndx.net
```

{% endcut %} 

Ограничения скоупа выкатки одним только пирингом задаются через опцию `--filter-peer sas2-12s17` в отличие от инициализации ToR'ов. Посмотреть какой именно конфиг генерируется для данного тора можно локально вызвав ann gen:

{% cut "Пример конфига для sas-90d4 касающегося sas2-12s17" %}

```(shell)
$ ann gen --filter-peer=sas2-12s17 sas-90d4
# -------------------- sas-90d4.cfg --------------------
ip community-filter basic DONT_ANNOUNCE_COMMUNITY index 10 permit 13238:999
ip community-filter basic GSHUT_COMMUNITY index 10 permit 65535:0
interface 100GE4/0/10
  undo portswitch
  ipv6 enable
  ipv6 address FE80::90:C4 link-local
  ipv6 mtu 9000
  qos wfq 0 to 7
  qos queue 0 wfq weight 30
  qos queue 1 wfq weight 20
  qos queue 2 wfq weight 20
  qos queue 3 wfq weight 30
  qos queue 4 wfq weight 30
  qos queue 5 wfq weight 3
  qos queue 6 wfq weight 5
  qos queue 4 ecn ECN
  description sas2-12s17 100ge1/0/4
  mtu 9000
  traffic-policy RETRANSMIT_RX_sas2-12s17 inbound
route-policy S1_EXPORT_TOR permit node 10
  apply community 13238:999 additive
route-policy S1_IMPORT_TOR deny node 10
  if-match community-filter DONT_ANNOUNCE_COMMUNITY
route-policy S1_IMPORT_TOR permit node 20
  if-match community-filter GSHUT_COMMUNITY
  apply local-preference 0
route-policy S1_IMPORT_TOR permit node 30
  apply local-preference 100
bgp 65002.65090
  group TOR external
  peer FE80::E17:D4 as-number 65002.12017
  ipv6-family unicast
    peer TOR enable
    peer FE80::E17:D4 enable
    peer TOR advertise-community
    peer TOR route-policy S1_IMPORT_TOR import
    peer TOR route-policy S1_EXPORT_TOR export
    peer FE80::E17:D4 group TOR
  peer TOR bfd enable
  peer TOR bfd min-tx-interval 500 min-rx-interval 500 detect-multiplier 4
  peer TOR listen-only
  peer FE80::E17:D4 group TOR
  peer FE80::E17:D4 connect-interface 100GE4/0/10
bfd
```

{% endcut %} 

#### Логи ввода в работу
Следует упомянуть что файл лога именуется по имени свитча `на который выкатывают`. Таким лог выкатки на вышестоящие свитчи будет содержать имя спайна, а не вводимого в работу тора.

Однако в самом тексте лога имя вводимого в работу свитча указывается агрументом для аннушки. Таким образом искать можно по имени вводимого в работу свитча, но уже в тексте самого файла. Вот пример команды который логи за последние семь дней (`-ctime 7`) которые имеют отношение к вводу в работу свитча `sas2-12s13`

{% cut "find /var/tmp -maxdepth 1 -ctime 7 -name rt-ann-deploy\* | xargs fgrep -l sas2-12s13" %}

```
[azryve@noc-myt /var/tmp]$ sudo find /var/tmp -maxdepth 1 -ctime 7 -name rt-ann-deploy\* | xargs fgrep -l sas2-12s13
/var/tmp/rt-ann-deploy.sas-90d4.QLd5Xt
/var/tmp/rt-ann-deploy.sas-90d1.z1QQ4V
/var/tmp/rt-ann-deploy.sas-90d3.npzicz
/var/tmp/rt-ann-deploy.sas2-12s13.bQ2Voc
/var/tmp/rt-ann-deploy.sas-90d2.wWxk9W
```

{% endcut %} 

### Известные проблемы и способы их расследования

#### Наливка
TODO

#### Ввод в работу

Как уже было указано выше ввод в работу разделен на два этапа: распознание и L3-инициализация. Поскольку запуск первого этапа можно произвести вручную (см. (Запуск ввода в работу)[#zapuskvvodavrabotu]) любые ошибки на этом этапе достаточно легко диагностируются.

После нажатия на форму пользователя переводит на главную страницу наливаемого объекта, а сверху указывается набор успешных шагов (зеленым) либо не успешных шагов (красным).

{% cut "Скриншот с примером успешного распознания свитча" %}

![](_images/nalivka/img6.png)

{% endcut %} 

Последний пункт: `L3 init will happen at ...` указывает на то что была создана отложенная задача L3-инициализации.

Второй этап происходит асинхронно (см. [L3-инициализация](#l3-inicializacija)) и гораздо менее прозрачен. Касательно него cуществует несколько методов обратной связи:

**Серая плашка `L3 init will happen at ...`** - висит на главной странице устройства если для него существует задача на L3-инициализациию.

{% cut "Скриншот" %}

![](_images/nalivka/img7.png)

{% endcut %} 

**Оранжевая плашка `L3 init failed, will be retried at ...`** - висит на главной странице устройства если для него существует задача на инициализацию, но уже не первая (т.e. были предыдущие не успешные попытки)

{% cut "Скриншот" %}

![](_images/nalivka/img8.png)

{% endcut %} 

**Файлы логами выкатки** - Логи лежат на мастере Racktables `/var/tmp/rt-ann-deploy-*`. Подробнее структуру и содержание см. в [Выкатка конфигурации на вводимый в работу свитч](#vykatkakonfiguraciinavvodimyjjvrabotusvitch)

После успешной L3-инициализации с устройства снимаются теги `{еще не работает}` и `{ожидает ввода в работу}`.

#### Типичные проблемы

{% cut "Шаблон" %}

#### Краткое описание
**Симптомы**:  
**Вероятные причины**:  
**Способы дебага**:  
**Способы решения**:  

{% endcut %} 

#### На устройстве выключен автоматический ввод в работу

**Симптомы**: Устройство налилось по консоли, но объект в РТ пустой, отсутствуют физические порты. На устройстве висит тег `{ожидает ввода в работу}`, но тега `{автоматически ввести в работу}` нет  

**Вероятные причины**: На устройстве не был включен автоматический ввод в работу при постановке в наливку (см. [Запуск ввода в работу](#zapusk-vvoda-v-rabotu))  

**Способы решения**: Открыть вкладку "Ввести в работу" и нажать "Начать" вручную  

#### Устройство не синхронизируется по SNMP

**Симптомы**: На объекте отсутствуют физические порты, при нажатии на "Ввести в работу" появляется красная плашка `Fatal SNMP failure`  

**Вероятные причины**: MGMT свитча не доступен  

**Способы дебага**: `ping`, `snmpget`  

Способы воспроизведения: `./scripts/rt-exec do_initSwitchStage1 <object-id>`  

Решение: Чиним доступность  

#### Устройство не синхронизируется по LLDP

**Симптомы**: На устройстве есть порты но ни один не не скоммутирован, показывается красная плашка `No LLDP neighbors found`, `LLDP query failed`

**Вероятные причины**: Свитч не доступен, на свитче не включен LLDP, у свитча нет ни одного LLDP нейбора (как минимум ожидается IPMI свитч для MGMT-интрефейса)

**Способы дебага**: `ping`, `snmpget`, проверить статус lldp нейборов на свитче  

Способы воспроизведения: `./scripts/rt-exec <object-id> getlldpstatus`  

Решение: Чиним доступность, ищем почему не видно соседей  

#### Устройство не может слинковать некоторые порты полученные по LLDP

**Симптомы**: Выводится красная плашка `There are unrecoverable LLDP errors above`  

**Вероятные причины**: Порт с которым мы пытаемся добавить линк уже привязан к чему-то еще. Обычно это происходит если старые линки не были зачищены, либо если свитч переехал.  

**Способы дебага**: На вкладке "Live LLDP" все не валидные линки будут помечены красным. По ним можно найти конкретных нейборов с которыми возникли проблемы  

**Способы решения**: Удалить не валидный линк  

#### На устройстве не нашлось нужных l3-аплинков согласно аннушке

**Симптомы**: На устройстве созданы порты, но появляется оранжевая плашка `Error calling ann mesh-validate` 

**Вероятные причины**: Обычно это ошибки коммутации  

**Способы дебага**: Проверить что все LLDP нейборы были импортированы. Руками запустить `./scripts/rt-exec checkMeshValidate <object-name>`. 

**Способы решения**: Подключать инженеров ITDC и просить их проверить почему не загорелись аплинки  

#### На устройство не приехали пользователи либо настройки tacacs

**Симптомы**: Устройство уже вводится в работу, но попасть на него по ssh не выходит - устройство не принимает пароль либо ключ

**Вероятные причины**: Ошибки выкатки пользователей, либо они не успели доехать.
 
**Способы дебага**: Попытаться выкатить пользователей руками через `php ./scripts/localuser-db/localuser-db.php <object-fqdn>`. Попытаться зайти на устройство с локальной учетки пользователя `racktables@`.
 


#### На устройство не выходит выкатить L3-конфигурацию

**Симптомы**: На устройстве висит оранжевая плашка `L3 init failed, will be retried at`, сети аллоцированы, на устройстве нет релевантной конфигурации  

**Вероятные причины**: Ошибка при вызове ann deploy на целевой свитч  

**Способы дебага**: Найти по хостнейму лог выкатки (см. [Логи ввода в работу](#logi-vvoda-v-rabotu)) и посмотреть в чем ошибка  

**Способы решения**: Проблемы бывают с не доступностью железки. В таком случае их нужно разбирать совместно с инженерами ITDC. Так же они бывают с самой аннушкой. Их можно обойти руками в зависимости от степени их серьезности и срочности наливки (иногда достаточно добавить несколько строк на коммутатор вручную), но обязательно стоит донести о проблеме дежурного [NOCDEVDUTY](https://st.yandex-team.ru/NOCDEVDUTY)


#### На вышестоящие устройства не выходит выкатить L3-конфигурацию

**Симптомы**: На устройстве висит оранжевая плашка `L3 init failed, will be retried at`, сети аллоцированы, на устройстве есть конфигурация, но одна или несколько сессиий не горят  

**Вероятные причины**: Ошибка при вызове ann deploy на один из вышестоящих свитчей  

**Способы дебага**: Найти по хостнейму лог выкатки (см. [Логи ввода в работу](#logi-vvoda-v-rabotu)) и посмотреть в чем ошибка  

**Способы решения**: Тут так же бывает достаточно добавить либо удалить несколько команд на устройстве, например зачистить старую конфигурацию аплинке, но опять же, обязательно стоит донести о проблеме дежурного [NOCDEVDUTY](https://st.yandex-team.ru/NOCDEVDUTY)


#### Не генерируется L3 конфигурация из-за `rtapi.RtApiExecException: Undefined offset`

**Симптомы**: На устройстве висит оранжевая плашка `L3 init failed, will be retried at`, сети аллоцированы, в логе длинный трейсбек аннушки вроде 

{% cut "такого" %}

  ```
  [azryve@noc-sas /var/tmp]$ cat rt-ann-deploy.sas2-12s27.M7cdJK
  Calling annushka: --filter-acl /var/tmp/rt-ann-acl.sas2-12s27.KSgEyH --cache - -Gqos sas2-12s27

  [12:33:38]   ERROR MainProcess - __init__.py:318 - Generator error in file '<generator object Bgp.run_huawei at 0x805f1ead0>:-1' -- host='sas2-12s27' generator='bgp.[Bgp]'
  Traceback (most recent call last):
    File "/usr/home/racktables/gitworkdir/annushka-production/annushka/generators/__init__.py", line 312, in _run_partial_generator
      output = gen(device, run_args.annotate)
    File "/usr/home/racktables/gitworkdir/annushka-production/annushka/generators/__init__.py", line 621, in __call__
      for text in self._running_gen:
    File "/usr/home/racktables/gitworkdir/annushka-production/annushka/generators/bgp.py", line 95, in run_huawei
      if (_is_bgp_device(device)):
    File "/usr/home/racktables/gitworkdir/annushka-production/annushka/generators/bgp.py", line 1071, in _is_bgp_device
      device_devmodel = generate_devmodel(device)
    File "/usr/home/racktables/gitworkdir/annushka-production/devmodel/annushka_helpers.py", line 13, in generate_devmodel
      return DeviceModel(device).build_device_model(vrf=None)
    File "/usr/home/racktables/gitworkdir/annushka-production/devmodel/device_model.py", line 343, in build_device_model
      children = [cl(self) for cl in devmodel.models.models_classes()]
    File "/usr/home/racktables/gitworkdir/annushka-production/devmodel/device_model.py", line 343, in <listcomp>
      children = [cl(self) for cl in devmodel.models.models_classes()]
    File "/usr/home/racktables/gitworkdir/annushka-production/devmodel/models/routing_protocols.py", line 16, in __init__
      self._handle_protos(cfg_role['protocols'], self, None)
    File "/usr/home/racktables/gitworkdir/annushka-production/devmodel/models/routing_protocols.py", line 227, in _handle_protos
      for pname, proto in protocols.items()]
    File "/usr/home/racktables/gitworkdir/annushka-production/devmodel/models/routing_protocols.py", line 227, in <listcomp>
      for pname, proto in protocols.items()]
    File "/usr/home/racktables/gitworkdir/annushka-production/devmodel/models/_proto_bgp.py", line 22, in __init__
      self.generate_base_groups()
    File "/usr/home/racktables/gitworkdir/annushka-production/devmodel/models/_proto_bgp.py", line 45, in generate_base_groups
      self._generate_global_opts()
    File "/usr/home/racktables/gitworkdir/annushka-production/devmodel/models/_proto_bgp.py", line 29, in _generate_global_opts
      asnum = helpers.process_asnum(bgp_defs['autonomous_system'], device=self.base.netdev)
    File "/usr/home/racktables/gitworkdir/annushka-production/devmodel/router_helpers.py", line 429, in process_asnum
      return annushka.model.bgp.tor_as_number(device)
    File "/usr/home/racktables/gitworkdir/annushka-production/annushka/model/bgp.py", line 70, in tor_as_number
      if router.non_vrf_device(device) and not device.tags["Сасово"]:
    File "/usr/home/racktables/gitworkdir/annushka-production/annushka/model/router.py", line 311, in non_vrf_device
      ids = device.rt.resolve_objects("[non-vrf ToR]")
    File "/usr/home/racktables/gitworkdir/annushka-production/netdev/racktables.py", line 136, in resolve_objects
      return self.resolve_objects_fqdns(query).keys()
    File "/usr/home/racktables/gitworkdir/annushka-production/netdev/cache.py", line 83, in wrap
      retval = freeze_data(method(self, *args, **kwargs))
    File "/usr/home/racktables/gitworkdir/annushka-production/netdev/racktables.py", line 147, in resolve_objects_fqdns
      self._rtapi.call.findObjectsByRackCode(query, True).items()}
    File "/home/racktables/gitworkdir/annushka-production/.venv/lib/python3.7/site-packages/rtapi.py", line 454, in __call__
      return self._caller(self._method_name, args, kwargs)
    File "/home/racktables/gitworkdir/annushka-production/.venv/lib/python3.7/site-packages/rtapi.py", line 336, in _call
      return self._check_ret(ret)
    File "/home/racktables/gitworkdir/annushka-production/.venv/lib/python3.7/site-packages/rtapi.py", line 314, in _check_ret
      raise RtApiExecException(exc_cls, fn_name, exc_msg)
  rtapi.RtApiExecException: ('NoticeException', 'findObjectsByRackCode', 'Undefined offset: 2118')

  Locals at innermost frame:

  {'_': 'Exception',
  'data': {'error': {'code': 0,
                      'message': 'Exception,findObjectsByRackCode,NoticeException,Undefined '
                                'offset: 2118'},
            'id': 38,
            'jsonrpc': '2.0'},
  'exc_cls': 'NoticeException',
  'exc_msg': 'Undefined offset: 2118',
  'fn_name': 'findObjectsByRackCode'}
  ```

{% endcut %} 

**Вероятные причины**: RTAPI сервер в который ходит наливочная аннушка залип с невалидным кешом
**Способы дебага**: Посмотреть [Логи ввода в работу](#logi-vvoda-v-rabotu) на предмет ошибок RTAPI
**Способы решения**: Достаточно порестартить локальный rtapi-сервер и попробовать запустить инициализацию еще раз

{% cut "/usr/local/etc/rc.d/rtapi-local-server restart" %}

  ```
  [root@noc-sas ~]# /usr/local/etc/rc.d/rtapi-local-server restart
  Stopping rtapid_local.
  Waiting for PIDS: 35955, 35955.
  starting rtapid_local.
  ```

{% endcut %} 



#### Устройство не может обновить ПО из-за проблем с сетевой связностью
**Симптомы**: наливка обрывается после лога "Default gw reachability test..." и проваленного ping. Примеры: [NOCREQUESTS-30145](https://st.yandex-team.ru/OCREQUESTS-30145), [NOCREQUESTS-33998](https://st.yandex-team.ru/NOCREQUESTS-33998)

**Вероятные причины**: устройство скомутированно правильно, но на Рыбке не прописан default-gw для этой подсети или vlan отсутствует в trunk по пути к рыбке. 

На всех рыбках c наливочным vlan прописаны сети: 172.20.0.0/17 или 172.20.128.0/17, из них есть доступ до 77.88.1.117 (noc-myt tftp). Данный GW должен быть доступен.

**Способы дебага**: 
* Проверить наличие интерфейса наливочного vlan на рыбке
* Проверить arp-таблицу наливаемого устройства на наличие mac-адреса рыбки
* Проверить наличие vlan в trunk-интерфейсах на промежуточных коммутаторах. Проверить записи mac-address-table на наличие адресов (наливаемого устройства и рыбки) в наливочном vlan. 
* Проверить состояние и статусы портов у STP-like протоколов для наливочного vlan

**Способы решения**: Обеспечить сетевую связность до GW. 
