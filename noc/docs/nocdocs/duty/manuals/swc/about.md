
# SWC

{% cut "Step-by-step с примерами" %}

0. Заказываем коммутацию.
1. Смотрим конфиг существующего интерфейса с каждой стороны:
```
myt-d1# sh run int e7/2/1

!Command: show running-config interface Ethernet7/2/1
!Time: Wed Jun 20 15:27:28 2018

version 6.2(12)

interface Ethernet7/2/1
  description myt-s238 10ge1/0/3
  switchport
  switchport mode trunk
  switchport trunk allowed vlan 521,542,578-581,583,628,639-640
  switchport trunk allowed vlan add 658,675,691,733,739-740,1300,1306
  switchport trunk allowed vlan add 1341-1342,1359-1362,1364,1366-1367
  switchport trunk allowed vlan add 1373,1376,1389,1392,1396,1400,1405-1406
  switchport trunk allowed vlan add 1413-1414,1417,1431-1433,1436,1442
  switchport trunk allowed vlan add 1444-1446,1451,1453,1456,1458,1461-1462
  switchport trunk allowed vlan add 1466,1476-1477,1480,1482,1484,1486-1487
  switchport trunk allowed vlan add 1489-1490,1493,1505,1510,1520,1577
  mtu 9000
  no shutdown
```

```
<myt-s238>disp cur int 10ge1/0/3
#
interface 10GE1/0/3
 description myt-d1 e7/2/1
 port link-type trunk
 undo port trunk allow-pass vlan 1
 port trunk allow-pass vlan 521 542 578 to 581 583 628 639 to 640 658 675 691 733
 port trunk allow-pass vlan 739 to 740 1300 1306 1341 to 1342 1359 to 1362 1364 1366 to 1367 1373 1376 1389
 port trunk allow-pass vlan 1392 1396 1400 1405 to 1406 1413 to 1414 1417 1431 to 1433 1436 1442 1444 to 1446
 port trunk allow-pass vlan 1451 1453 1456 1458 1461 to 1462 1466 1476 to 1477 1480 1482 1484
 port trunk allow-pass vlan 1486 to 1487 1489 to 1490 1493 1505 1510 1520 1577
 stp edged-port disable
 qos drr 0 to 5
 qos queue 0 drr weight 20
 qos queue 1 drr weight 75
 qos queue 2 drr weight 5
 jumboframe enable 9712
 device transceiver 10GBASE-FIBER
#
return
```
2. Создаём LACP-интерфейс с каждой стороны и настраиваем его, подобно старому:
На циске имя выбираем соответственно номеру свитча:
```
myt-d1# conf t
Enter configuration commands, one per line.  End with CNTL/Z.
myt-d1(config)# int po 238
myt-d1(config-if)# switchport 
myt-d1(config-if)#  switchport mode trunk
myt-d1(config-if)#   switchport trunk allowed vlan 521,542,578-581,583,628,639-640
myt-d1(config-if)#   switchport trunk allowed vlan add 658,675,691,733,739-740,1300,1306
myt-d1(config-if)#   switchport trunk allowed vlan add 1341-1342,1359-1362,1364,1366-1367
myt-d1(config-if)#   switchport trunk allowed vlan add 1373,1376,1389,1392,1396,1400,1405-1406
myt-d1(config-if)#   switchport trunk allowed vlan add 1413-1414,1417,1431-1433,1436,1442
myt-d1(config-if)#   switchport trunk allowed vlan add 1444-1446,1451,1453,1456,1458,1461-1462
myt-d1(config-if)#   switchport trunk allowed vlan add 1466,1476-1477,1480,1482,1484,1486-1487
myt-d1(config-if)#   switchport trunk allowed vlan add 1489-1490,1493,1505,1510,1520,1577
myt-d1(config-if)# mtu 9000
```
На свитче - нулевой:
```
<myt-s238>sys
Enter system view, return user view with return command.
[~myt-s238]int eth0
[*myt-s238-Eth-Trunk0]port link-type trunk
[*myt-s238-Eth-Trunk0] undo port trunk allow-pass vlan 1
[*myt-s238-Eth-Trunk0] port trunk allow-pass vlan 521 542 578 to 581 583 628 639 to 640 658 675 691 733
[*myt-s238-Eth-Trunk0] port trunk allow-pass vlan 739 to 740 1300 1306 1341 to 1342 1359 to 1362 1364 1366 to 1367 1373 1376 1389
[*myt-s238-Eth-Trunk0] port trunk allow-pass vlan 1392 1396 1400 1405 to 1406 1413 to 1414 1417 1431 to 1433 1436 1442 1444 to 1446
[*myt-s238-Eth-Trunk0] port trunk allow-pass vlan 1451 1453 1456 1458 1461 to 1462 1466 1476 to 1477 1480 1482 1484
[*myt-s238-Eth-Trunk0] port trunk allow-pass vlan 1486 to 1487 1489 to 1490 1493 1505 1510 1520 1577
```
На хуавее добавляем mode lacp-static и не забываем про коммит:
```
[*myt-s238-Eth-Trunk0]mode lacp-static 
[*myt-s238-Eth-Trunk0]commit
```
3. Когда коммутация готова, линкуем свитчи в рт через вкладку Live LLDP (с любой стороны).
4. Добавляем новые порты в LACP с обеих сторон:
```
myt-d1(config-if)# int e7/2/2
myt-d1(config-if)# channel-group 238 force mode active
```
На хуавее надо сначала зачистить конфиг:
```
[~myt-s238]clear conf int 10ge1/0/4
[~myt-s238]int 10ge1/0/4
[~myt-s238-10GE1/0/4]eth-trunk 0
[*myt-s238-10GE1/0/4]commit
```
5. Проверяем, что LACP заработал:
```
[~myt-s238-10GE1/0/4]disp int Eth-Trunk0
Eth-Trunk0 current state : UP (ifindex: 66)
Line protocol current state : UP 
Description: 
Switch Port, PVID :    1, TPID : 8100(Hex), Hash Arithmetic : profile default, Maximal BW : 10Gbps, Current BW : 10Gbps, The Maximum Frame Length is 9216
Internet protocol processing : disabled
IP Sending Frames' Format is PKTFMT_ETHNT_2, Hardware address is d4b1-10b0-73b1
Current system time: 2018-06-20 15:50:31+03:00
Physical is ETH_TRUNK
    Last 300 seconds input rate 35625189 bits/sec, 5346 packets/sec
    Last 300 seconds output rate 723 bits/sec, 0 packets/sec
    Input: 1533377 packets,1277257203 bytes
           1486922 unicast,4279 broadcast,3710 multicast
           0 errors,0 drops
    Output:167 packets,29264 bytes
           0 unicast,0 broadcast,167 multicast
           0 errors,0 drops
    Last 300 seconds input utility rate:  0.35%
    Last 300 seconds output utility rate: 0.01%
----------------------------------------------------------
PortName                      Status              Weight   
----------------------------------------------------------
10GE1/0/4                     UP                  1        
----------------------------------------------------------
The Number of Ports in Trunk : 1
The Number of Up Ports in Trunk : 1
```
6. Добавляем старые порты в LACP:
```
[~myt-s238]clear conf int 10GE1/0/3
[~myt-s238]int 10GE1/0/3
[~myt-s238-10GE1/0/3]eth-trunk 0
[*myt-s238-10GE1/0/3]commit
```

```
myt-d1(config-if)# interface Ethernet7/2/1
myt-d1(config-if)# channel-group 238 force mode active
```
7. Снова проверяем с обеих сторон:
```
myt-d1# sh int po 238
port-channel238 is up
admin state is up
  Hardware: Port-Channel, address: 64f6.9dc5.ec87 (bia 64f6.9dc5.ec87)
  MTU 9000 bytes, BW 20000000 Kbit, DLY 10 usec
  reliability 255/255, txload 151/255, rxload 62/255
  Encapsulation ARPA, medium is broadcast
  Port mode is trunk
  full-duplex, 10 Gb/s
  Input flow-control is off, output flow-control is off
  Auto-mdix is turned off
  Switchport monitor is off 
  EtherType is 0x8100 
  Members in this channel: Eth7/2/1, Eth7/2/2
```

```
<myt-s238>disp int Eth-Trunk0
Eth-Trunk0 current state : UP (ifindex: 66)
Line protocol current state : UP 
Description: 
Switch Port, PVID :    1, TPID : 8100(Hex), Hash Arithmetic : profile default, Maximal BW : 20Gbps, Current BW : 20Gbps, The Maximum Frame Length is 9216
Internet protocol processing : disabled
IP Sending Frames' Format is PKTFMT_ETHNT_2, Hardware address is d4b1-10b0-73b1
Current system time: 2018-06-20 15:51:41+03:00
Physical is ETH_TRUNK
    Last 300 seconds input rate 4736551868 bits/sec, 474307 packets/sec
    Last 300 seconds output rate 1543965481 bits/sec, 270840 packets/sec
    Input: 31645469 packets,37987803446 bytes
           30898980 unicast,7634 broadcast,7400 multicast
           0 errors,0 drops
    Output:21011201 packets,13343903562 bytes
           20813884 unicast,0 broadcast,195 multicast
           0 errors,0 drops
    Last 300 seconds input utility rate:  23.68%
    Last 300 seconds output utility rate: 7.71%
----------------------------------------------------------
PortName                      Status              Weight   
----------------------------------------------------------
10GE1/0/3                     UP                  1        
10GE1/0/4                     UP                  1        
----------------------------------------------------------
The Number of Ports in Trunk : 2
The Number of Up Ports in Trunk : 2
```
8. Выходим из режима конфигурации и сохраняем успехи:
```
<myt-s238>save
Warning: The current configuration will be written to the device. Continue? [Y/N]:Y
Now saving the current configuration to the slot 1 ..
Info: Save the configuration successfully.
```

```
myt-d1# copy run start
[########################################] 100%
Copy complete.
```
9. В рт идём во вкладку Ports и нажимаем syncronize port list с обеих сторон. Проверяем, что LACP-интерфейсы приехали, линкуем их между собой. Убеждаемся, что портам добавились правильные комментарии, и в списке портов в Browse они отображаются под LACP-интерфейсом. Если этого не произошло, добавляем комментарий руками.
10. Идём во вкладку 802.1Q sync, разрешаем получившийся конфликт, синкаем. повторяем для обеих сторон.
11. Готово. Можно подождать минут 15 и посмотреть в графики - трафик должен раскладываться на оба порта (не обязательно равномерно).

{% endcut %}

Порядок действий при расширении аплинка стоечному свитчу (с помощью etherchannel):
1. Проверить занятость порта перед фастбонным аплинком (gi0/46 при 48-портовом свитче). Если занят попросить отвественных за влан, который настроен на порту его освободить (переехать в соседний порт/свитч);
2. Сконфигурить порт из П.1 (gi0/46) так же как FB аплинк (gi0/47).
3. Написать на helpdc для организации кабсоеда и перемещения FB аплинка в порт из П.1. Желательно второй линк приводить на другую карточку аплинкового свитча, и чтобы номера портов совпадали (например gi2/35 и gi3/35). Вновь выбранный  порт (gi3/35) зашатдаунить.
4. Настроить etherchannel на портах gi0/47 -- gi3/35. На сторне аплинкового свитча выбрать номер для порта etherchannel, он выбирается исходя из номера свитча в идеале (если свитч s3241, то 41). Расшатдаунить на стороне аплинкового свитча порт gi3/35, он станет STP Altn на расширяемом свитче.
5. Погасить на стороне аплинкового свитча gi2/35. Настроить etherchannel между gi0/48 -- gi2/35. Теперь должно стать по два порта в etherchannel'е.
6. включить алгоритм хеширования на основе L4-полей пакета
7. Добавить в RackTables порты po и Eth-Trunk на оба свитча(магистральный и стоечный). Тип порта - LACP. Слинковать их.
8. Затянуть конфигурацию обоих свитчей в базу на странице 802.1Q sync,разрешить конфликты
9. Отредактировать или сменить шаблоны на обоих свитчах таким образом,чтобы на магистральном po-порт был в роли downlink, а на стоечном -в uplink.
10. На странице 802.1Q Ports на обоих свитчах новые po-порты не должнысветиться красным, на них должен отображаться линк во второй коммутатор.
Если порты серверные
1. балансировка src-ip
2. Создать агрегированный порт в РТ
3. В комменте к порту указать fqdn сервера