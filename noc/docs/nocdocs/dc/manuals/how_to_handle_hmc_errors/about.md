# Введение

### Что есть HMC и что с ним не так?

HMC aka Hyper Memory Cube - это 3D-память, состоящая из кристаллов DRAM, собранных в стэк.Juniper решили использовать эту память в качестве off-chip памяти в своей линейке QFX10000.

{% cut "Тут картинка. Подробнее, как обычно, в ~~Гугле~~ Яндексе" %}

![](https://wiki.yandex-team.ru/users/vvenglovskii/how-to-handle-hmc-errors/.files/hmc2.jpg)

{% endcut %}

Подключается эта память к ASIC'у с помощью ++шести SerDes'ов++ с пропускной способностью в 15Gb/s каждый.Один ASIC aka PE, Packet Engine, aka PFE, Packet Forwarding Engine обслуживает ++пять 100Gb портов++ (*на нашей 30-портовой карте таких, соответственно, ++шесть штук++, PE
0-5*) и подключен к своему персональному HMC модулю размером 6GB, из которых 4GB выделено под буфер и 2GB для хранения необходимых структур данных (таблицы для lookup'ов, всякоразные счетчики и пр.).

{% cut "Вот схема от вендора," %}

![](https://wiki.yandex-team.ru/users/vvenglovskii/how-to-handle-hmc-errors/.files/screenshot2020-05-18at12.07.20.png)

{% endcut %}

{% cut "...а вот структура HMC" %}

![](./_images/img1.png)

{% endcut %}

Мэппинг портов в PFE можно глянуть fpc shell командой `show pepic 0 wanio-info` (см. раздел "*Как использовать cli в Juniper?*" если не умеешь использовать shell команды Джуна).

{% cut "Пример вывода show pepic 0 wanio-info" %}

```
---------------------------------------
bit-pos  asic-id     ifd         pe-intf
-------  -------  ------------  ---------
  0          0      et-1/0/0      0
 12          0      et-1/0/2      12
 24          0      et-1/0/4      24
 36          0      et-1/0/8      36
 48          0      et-1/0/6      47
  0          1      et-1/0/1      0
 12          1      et-1/0/3      12
 24          1      et-1/0/5      24
 36          1      et-1/0/9      36
 48          1      et-1/0/7      47
  0          2      et-1/0/10      0
 12          2      et-1/0/12      12
 24          2      et-1/0/14      24
 36          2      et-1/0/18      36
  0          3      et-1/0/11      0
 12          3      et-1/0/13      12
 24          3      et-1/0/15      24
 36          3      et-1/0/19      36
 48          3      et-1/0/17      47
  0          4      et-1/0/20      0
 12          4      et-1/0/22      12
 24          4      et-1/0/24      24
 36          4      et-1/0/28      36
 48          4      et-1/0/26      47
  0          5      et-1/0/21      0
 12          5      et-1/0/23      12
 24          5      et-1/0/25      24
 36          5      et-1/0/29      36
 48          5      et-1/0/27      47
```

{% endcut %}

Роль HMC-памяти заключается в хранении "тела" пакета, пока его заголовки парсятся (для  lookup'а, QoS'а, etc.), изменяются (уменьшение ttl, изменение QoS-маркировки, etc.) или вообще уничтожаются (Ethernet хэдер при маршрутизации, декапсуляция, etc.) и хранения счетчиков.

{% cut "Секретная схема, украденная шпионами КГБ из Бангалорской HQ Джуна" %}

![](./_images/img2.png)

{% endcut %}

Собственно, основная проблема, с которой мы сталкивались, сталкиваемся и будем сталкиваться, происходит в момент, когда судьба пакета уже определена, исходящий порт вычислен, все изменения заголовков подготовлены и пришла пора пришить к "телу" пакета новые хэдеры для последующей отправки в исходящий интерфейс, сериализации и пр.Иногда, но чаще, чем нам хотелось бы, при чтении пакета из HMC-памяти логика чипа понимает, что пакет был прочитан неверно: в некоторых местах "единички" и "нолики" перепутались и даже встроенный механизм ECC не может восстановить изначально записанный пакет.Такой пакет никуда отправлять нельзя и он тихо дропается, увеличив счетчик ошибок на единицу.

Чаще всего, такие события не случаются поодиночке, иными словами, дропаются десятки, сотни, тысячи пакетов.

### Как использовать cli в Juniper?

Информация с ASIC'а хранится и обрабатывается на самой карте, поэтому команды нужно выполнять на ней же (там есть свой CPU с микрокернелом).Существуют три способа выполнения задачи со своим плюсами и минусами. Разбор ниже:
- **Из cli утилиты Junos** `request pfe execute timeout 0 command "[command]" target fpc[fpc no.]`, e.g.
  ```
  vvenglovskii-nocauth@vla-6d1> request pfe execute command "bringup jspec read pechip[2] register hmcif link 0 hmc_err_log_0" target fpc1
  SENT: Ukern command: bringup jspec read pechip[2] register hmcif link 0 hmc_err_log_0
  
  0x01ee0060  pe.hmcif.link[0].hmc_err_log_0     3E10007F
                                                cmd[29:24] : 0x3e
                                                lng[23:20] : 0x1
                                                ltag[16:8] : 0x0
                                                 dinv[7:7] : 0x0
                                              errstat[6:0] : 0x7f
  ```
  `{green}(Плюсы:)` Не нужны спец.доступы 
  `{red}(Минусы:)` Нет интерактивных подсказок, нет доп. утилит, --самый медленный вариант--
- **Из shell'а FreeBSD, внутри которой крутится Junos, с помощью утилиты cattleprod** (`cli --> RE FreeBSD shell`)
  ```
  start shell
  cprod -A fpc[fpc no.] -c "[command]"
  ```

  , e.g.,
  ```
  vvenglovskii-nocauth@vla-6d1> start shell
  % cprod -A fpc1 -c "bringup jspec read pechip[2] register hmcif link 0 hmc_err_log_0"
  
  0x01ee0060  pe.hmcif.link[0].hmc_err_log_0     3E10007F
                                                cmd[29:24] : 0x3e
                                                lng[23:20] : 0x1
                                                ltag[16:8] : 0x0
                                                 dinv[7:7] : 0x0
                                              errstat[6:0] : 0x7f
  %
  ```
  `{green}(Плюсы:)` Можно использовать *nix утилиты: awk, xargs и т.п., быстрое выполнение `{red}(Минусы:) `Нет интерактивных подсказок, нужно разрешение на выполнение `start shell`
- Из shell'а ASIC'а на самой карте (`cli --> RE FreeBSD shell --> FPC ukern shell`)
  ```
  start shell
  vty fpc[fpc no.]
  [command]
  ```
  , e.g., 
  ```
  {master}
  vvenglovskii-nocauth@vla-6d1> start shell
  % vty fpc1
  
  Switching platform (1600 Mhz QorIQ P5020 processor, 3071MB memory, 8192KB flash)
  
  FPC1(vla1-2d1 vty)# ...ip[2] register hmcif link 0 hmc_err_log_0
  
  0x01ee0060  pe.hmcif.link[0].hmc_err_log_0     3E10007F
                                                cmd[29:24] : 0x3e
                                                lng[23:20] : 0x1
                                                ltag[16:8] : 0x0
                                                 dinv[7:7] : 0x0
                                              errstat[6:0] : 0x7f
  
  FPC1(vla1-2d1 vty)#
  ```
  {green}(Плюсы:) Интерактивные подсказки с помощью `?`, самый быстрый вариант{red}(Минусы:) нужно разрешение на выполнение `start shell`, нет доп.утилит
Весь сислог, относящийся к HMC, валится в дефолтный файл messages (и его 9 предыдущих gzip'нутых версий).Смотреть можно стандартной командой `show log messages` или `show log messages.[0-9].gz`, для фильтрации можно использовать `| match ""` (аналог *grep*), `| last ""` (аналог *tail*), `| except ""` (аналог *grep -Ev/egrep -v*) [и т.д.](https://www.juniper.net/documentation/en_US/junos/topics/reference/command-summary/pipe.html)Также Junos разрешает использовать `grep`, но без аргументов, e.g.,
```
{master}
vvenglovskii-nocauth@vla-6d1> show log messages | grep May | grep errstat | except "errstat:16"
May 17 10:21:55  vla-6d1 fpc1 Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link0: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000
May 17 10:21:55  vla-6d1 fpc1 Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link1: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000
May 17 10:21:55  vla-6d1 fpc1 Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link2: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000
May 17 10:21:55  vla-6d1 fpc1 fpc1 dcpfe: Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link0: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000#012
May 17 10:21:55  vla-6d1 fpc1 fpc1 dcpfe: Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link1: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000#012
May 17 10:21:55  vla-6d1 fpc1 fpc1 dcpfe: Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link2: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000#012
```

### Как правильно создать кейс в JTAC?

- Зайти в CaseManager ([http://casemanager.juniper.net/](http://casemanager.juniper.net/))

![](./_images/img3.png)

1. Кликнуть *Your Cases* (если по дефолту не в них, а в RMA)
2. Выбрать *+ Create Case*

- Заполнить форму (см. ниже):

![](./_images/img4.png)

3. В *Synopsis* написать `Yandex / QFX10016 / [хост] / [описание проблемы]`, это обговоренный формат, используйте именно его. К примеру, "Yandex / QFX10016 / sas2-x3 / HMC errstat:31 on FPC2"
4. *Этого шага нет, исправлять скрины неохота.*
5. Опишите проблему в двух словах (они и так уже понимают в чем дело, поэтому нет смысла растекаться мыслью по древу), запросите RMA и приложите базовые выводы из сислога/PFE shell'а об HMC-ошибке.

Базовые выводы соберите с помощью команд:
1. События из сислога - `show log messages | grep errstat`, применив нужные фильтры на ваше усмотрение
2. Лог ошибки из FPC - `bringup jspec read pechip[pechip no.] register hmcif link [link no] hmc_err_log_0`, где `pechip no.` узнайте из п.a (May 17 10:21:55  vla-6d1 fpc1 fpc1 dcpfe: Cmerror Op Set: PE Chip::FATAL ERROR!! ++**from PE2
   2**++: HMCIF: Link2: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000# 012),`link no.` узнайте из п.a (May 17 10:21:55  vla-6d1 fpc1 fpc1 dcpfe: Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2
   2
   : HMCIF: ++**Link2**++: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000# 012). Обычно ошибки появляются на трех линках из шести, выбирайте любой из трех.

{% cut "Вот пример письма" %}

```
Hello, TAC Team.

We've got errstat:127 HMC errors on a yet another ULC-30Q28 FPC accompanied by connectivity loss and PFE shutdown.
Please, initiate an RMA procedure as in cases # 2020-0406-0401, 2020-0420-0135, and 2020-0504-0366.

Here's the brief info.
Full logs/RSI are attached to the case files.

{master}
vvenglovskii-nocauth@vla-6d1> show log messages | grep May | grep errstat
May 17 10:21:55  vla-6d1 fpc1 Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link0: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000
May 17 10:21:55  vla-6d1 fpc1 Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link1: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000
May 17 10:21:55  vla-6d1 fpc1 Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link2: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000
May 17 10:21:55  vla-6d1 fpc1 fpc1 dcpfe: Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link0: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000#012
May 17 10:21:55  vla-6d1 fpc1 fpc1 dcpfe: Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link1: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000#012
May 17 10:21:55  vla-6d1 fpc1 fpc1 dcpfe: Cmerror Op Set: PE Chip::FATAL ERROR!! from PE2[2]: HMCIF: Link2: HMC Fatal Error cmd:62 lng:1 ltag:0 dinv:0 errstat:127 err_cnt:0x40000000#012

{master}
vvenglovskii-nocauth@vla-6d1> start shell
% vty fpc1


Switching platform (1600 Mhz QorIQ P5020 processor, 3071MB memory, 8192KB flash)

FPC1(vla1-2d1 vty)# bringup jspec read pe
^
'pe' is ambiguous.  Possible choices:

pechip[0]             jspec client for PECHIP[0] device
pechip[1]             jspec client for PECHIP[1] device
pechip[2]             jspec client for PECHIP[2] device
pechip[3]             jspec client for PECHIP[3] device
pechip[4]             jspec client for PECHIP[4] device
pechip[5]             jspec client for PECHIP[5] device

FPC1(vla1-2d1 vty)# ...ip[2] register hmcif link 0 hmc_err_l
^
'hmc_err_l' is ambiguous.  Possible choices:

hmc_err_log_0         HMC error log 0
hmc_err_log_1         HMC error log 1

FPC1(vla1-2d1 vty)# ...ip[2] register hmcif link 0 hmc_err_log_0

0x01ee0060  pe.hmcif.link[0].hmc_err_log_0     3E10007F
cmd[29:24] : 0x3e
lng[23:20] : 0x1
ltag[16:8] : 0x0
dinv[7:7] : 0x0
errstat[6:0] : 0x7f

FPC1(vla1-2d1 vty)#

All ports belonging to PE[2] aren't transmitting frames due to its auto-shutdown:

{master}
vvenglovskii-nocauth@vla-6d1> show interfaces et-1/0/1[02468] | grep "rate|Phy"
Physical interface: et-1/0/10, Enabled, Physical link is Up
Link-level type: Ethernet, MTU: 9216, LAN-PHY mode, Speed: 100Gbps, BPDU Error: None,
Input rate     : 1024 bps (1 pps)
Output rate    : 0 bps (0 pps)
FEC Corrected Errors Rate               0
FEC Uncorrected Errors Rate             0
Physical interface: et-1/0/12, Enabled, Physical link is Down
Link-level type: Ethernet, MTU: 9216, LAN-PHY mode, Speed: 100Gbps, BPDU Error: None,
Input rate     : 0 bps (0 pps)
Output rate    : 0 bps (0 pps)
FEC Corrected Errors Rate               0
FEC Uncorrected Errors Rate             0
Physical interface: et-1/0/14, Enabled, Physical link is Up
Link-level type: Ethernet, MTU: 9216, LAN-PHY mode, Speed: 100Gbps, BPDU Error: None,
Input rate     : 0 bps (0 pps)
Output rate    : 0 bps (0 pps)
FEC Corrected Errors Rate               0
FEC Uncorrected Errors Rate             0
Physical interface: et-1/0/18, Enabled, Physical link is Up
Link-level type: Ethernet, MTU: 9216, LAN-PHY mode, Speed: 100Gbps, BPDU Error: None,
Input rate     : 1024 bps (1 pps)
Output rate    : 0 bps (0 pps)
FEC Corrected Errors Rate               0
FEC Uncorrected Errors Rate             0


Regards,
Vitaly Venglovsky
Network Engineer
Yandex
```

{% endcut %}

6. В *Case Type* выберите Hardware
7. Выберите наш аккаунт (не облачный, который на Yandex NV)
8. Вставьте S/N карты, инфа по контракту будет добавлена автоматически.S/N можно посмотреть командой `show chassis hardware | grep "FPC [fpc no.]|Serial"`
9. Поле *Series:* заполнится само после п.8. В остальных напишите:Platform: **QFX10016**Version: **18.2**Release: **R2**
![](https://wiki.yandex-team.ru/users/vvenglovskii/how-to-handle-hmc-errors/.files/screenshot2020-05-18at14.04.28.png =1024x)
10. Приоритет на ваш вкус, я обычно выбираю *P3-Medium*
11. Добавьте *noc-tac@yandex-team.ru*
12. Выберите *No*, чтобы не добавлять лишних людей в переписку
13. Выберите *Full email update*, иначе начнут названивать.

- Нажмите *Save*![](https://wiki.yandex-team.ru/users/vvenglovskii/how-to-handle-hmc-errors/.files/screenshot2020-05-18at16.07.00.png =800x)

14. Нажмите *Yes*

- Соберите логи с железки командой `file archive compress source /var/log/* destination [путь к файлу, e.g., /var/tmp/[номер_кейса]_logs`, будет создан файл `/var/tmp/[номер_кейса]_logs.tgz`.Это займет пару секунд, скопируйте файл к себе.
- Соберите RSI с железки командой `request support information | save /var/tmp/[номер_кейса]_rsi`, будет создан файл `/var/tmp/[номер_кейса]_rsi`.Это займет пару (иногда десятков) минут, скопируйте файл к себе.![](https://wiki.yandex-team.ru/users/vvenglovskii/how-to-handle-hmc-errors/.files/screenshot2020-05-18at16.07.34.png =1024x)

15. На экране загрузки файлов из drop-down меню выберите *Syslog* и затем архив с логами
16. Нажмите *Attach a File*. Повторите пю.15, выбрав RSI из меню и сгенерированный ранее файл.

- Через какое-то время ответит инженер с запросом информации для RMA.Пришлите ему следующую инфу:
```
Shipping Customer E-Mail: vevstifeev@yandex-team.ru 
Ship to Contact Name: Vasiliy Evstifeev 
Ship to Contact Phone (Country + Number): +7 903 215-55-55 
Ship to Company Name: Yandex 
Address Line 1: UL Silikatnaya 19 
Address Line 2: 
City: Mytishchi 
State: 
Country: Russian Federation 
Postal Code: 141004 
Special Delivery Instructions (Include Data center ticket ID#, Security pass#, etc) for Courier (Max 255 characters):
```
Если он запросит серийный номер шасси, посмотрите командой `show chassis hardware | grep "Chassis|Serial"`
- После создания RMA технический кейс попросят закрыть. Делайте смело.

### errstat:16 (0x10)

### Что произошло?

На наше счастье, сила ECC смогла побороть космические лучи и  восстановить исходный пакет. Начиная с какой-то из свежих версий Junos, эти сообщения вообще не будут сыпаться в сислог.
### Что делать?

Ничего, игнорируем. Если таких сообщений сотни - сообщите кому-нибудь из галерных гребцов Группы эксплуатации (лучше, конечно, дежурному).
# errstat:31 (0x1f)

### Что произошло?

Самое серьезное по импакту на трафик событие: многочисленные ~~СОТНИ ИХ!!~~ невосстанавливаемые ошибки чтения из памяти, трафик льется на пол гигабитами, система в панике. На Нетмоне чаще всего весьма заметно.Или нет?Как и везде, есть некоторые исключения. Как я и писал выше, QFX хранит в HMC не только тело пакета, но и другие структуры: маршруты, некст-хопы, счетчики и пр.Если проблема возникла в "удачном" секторе памяти, то мы просто получим кривые счетчики или отъехавший маршрут, но не будем портить транзитный трафик, под катом выдержка из письма инженера Джунипер для любопытствующих.

{% cut "Выдержка из письма Йозеф Бухштайнера" %}

*The error reporting and detection is all performed inside HMC Firmware and the result is consumed by JunOS. So far we had never seen that result could be not trusted. The point is MUE ( Multi-bit Error) and the operational impact is the question. If there are parity errors then each read operation will fail and typically a write operation to this location will fix it. The key really is if the MUE event happen on static memory ( I would call a route or next-hop entry relative static) or if this is more dynamic/transactional ( which I would call packet data like packet het and tail-pointers). Usually if pointers are damages the impact is fatal and if you have static entries impacted then its often less impact from operational perspective. This sort of logic applies to all sort of Memory on-the-chop or of chip. That fact that you had no impact would indicate there was an impact on the more static aka route/nh entry portion of it. QFX/PTX is using HMC memory for both route/next-hop data as well for packet memory. MX platform have route-next-hop data on a different memory portion since the way or performing lookup is different.So in a sense as you said there is a version of errstat:31 lite version possible like in your case as it depends which memory location got affected.Those err cnt value you had read out manually is zero because those registers are clear-on-read and software is reading them out once an interrupt is raised. In the error log you see the err_cnt:0x40.*

{% endcut %}

### Что делать?

- Если все совсем плохо - отключить FPC самостоятельно (см. инструкцию в п."Приехали, замена"), если событие было краткосрочным и прошло - плывем дальше. Если самостоятельно отключать страшно и время позволяет - сообщите кому-нибудь из галерных гребцов Группы эксплуатации (лучше, конечно, дежурному).
- Создать кейс на замену карты в Джунипер по инструкции выше.
- Создать кейс на замену карты у ITDC, поставив в копию 
  
   и сообщив ему номер RMA и S/N карты на замену и дефектной карты.
- После доставки замены - заменить карту (см. инструкцию в п."Приехали, замена")

### errstat:127 (0x7f)

### Что произошло?

Среднее по импакту на трафик событие: многочисленные восстанавливаемые (вперемешку с несколькими невосстанавливаемыми) ошибки чтения из HMC. В 95% случаев система отключает ASIC и все его порты (упадут сессии с ТОРами, могут развалиться по min-links LAG'и), но в целом на Нетмоне несильно заметно.

### Что делать?

- Создать кейс на замену карты в Джунипер по инструкции выше.
- Создать кейс на замену карты у ITDC, поставив в копию 
  
   и сообщив ему номер RMA и S/N карты на замену и дефектной карты.
- Если отключившиеся порты мешают жить - перезагрузить карту (см. инструкцию в п."Приехали, ребут")
- После доставки замены - заменить карту (см. инструкцию в п."Приехали, замена")

### Приехали, ребут

- В случае "дэшки" или "икса" выводим коммутатор из прода с помощью навешивания тега "нагрузка снята автоматикой" в РТ и прогоном аннушки (теги аннушка обычно подтягивает через 3-5 мин.):
```
./ann deploy -g bgp,rpl <switch name> --recache
```
Аннушка выкатит **GSHUT_COMMUNITY** в политики анонсов BGP пирам и трафик начнет утекать с коммутатора.Мониторить можно с помощью `show interfaces ae* | grep "Phy|rate"`, обычно хуавеевские "дэшки" гонят через "икс" трафик примерно минуту, постепенно снижая bps.
- Перезагрузить карту с помощью `request chassis fpc slot [fpc no.] restart`
- Вернуть трафик после "взлёта" карты с помощью 
  ```
  rollback 1
  commit
  ```

### Приехали, замена

- В случае "дэшки" или "икса" выводим коммутатор из прода с помощью навешивания тега "нагрузка снята автоматикой" в РТ и прогоном аннушки (теги аннушка обычно подтягивает через 3-5 мин.):
```
./ann deploy -g bgp,rpl <switch name> --recache
```
Аннушка выкатит **GSHUT_COMMUNITY** в политики анонсов BGP пирам и трафик начнет утекать с коммутатора.Мониторить можно с помощью `show interfaces ae* | grep "Phy|rate"`, обычно хуавеевские "дэшки" гонят через "икс" трафик примерно минуту, постепенно снижая bps.
- Отключить карту с помощью `request chassis fpc slot [fpc no.] offline`
- Дождаться замены ITDC
- Вернуть трафик после "взлёта" карты с помощью 
  ```
  rollback 1
  commit
  ```

### Changelog

19.06.20 Добавил upd по errstat:31. Исправил опечатки и некоторые ошибки 21.12.2021, 

 - актуализировал инструкции по снятию трафика для ребута или замены карты.
