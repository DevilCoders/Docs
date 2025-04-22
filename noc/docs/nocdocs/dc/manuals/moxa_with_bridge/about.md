### Настройка Bridge на консоляторе MOXA

В некоторых реализациях подключения МОХА к сети существует потребность в сборке bridge. Чтобы это сделать вам необходимо:
- налить флешку по пунктам [Этапа 2](https://docs.yandex-team.ru/nocdoc/office/ipmi/consoles/nalivka/about#etap-2-proshivka-flesh-karty)
- если вы не из NOC, то приквать дежурного NOC
- надо зайти под root на MOXA
- перевести флешку в режим rw
```
mount -o remount, rw /
```
- добавить конфигурацию в файл `/etc/config/network`: конфигурацию br0, rule и def2
```
config interface 'br0'         
        option type 'bridge'     
        option ifname 'lan2 lan3' 
        option proto 'static'         
        option ipaddr '195.208.26.52' 
        option netmask '29'           
        option gateway '195.208.26.49'
        option mtu '1450'             
config rule                           
        option src '195.208.26.52/32' 
        option lookup '200'           
config route def2                     
        option target '0.0.0.0'       
        option netmask '0.0.0.0'      
        option interface 'br0'        
        option gateway '195.208.26.49'
        option table '200' 
```
- Удалить блоки конфигурации интерфейсов и связанными с ними rule и def
```
config interface 'lan2'

config interface 'lan3'

```
- далее выполнить команды:
```
root@consoles-sas1-1:~# uci commit network
root@consoles-sas1-1:~# /etc/init.d/network restart
```
- можно проверить что получилось:
```
root@consoles-sas1-1:~# ifconfig 
br-br0    Link encap:Ethernet  HWaddr 02:78:00:10:03:01  
          inet addr:37.140.144.1  Bcast:37.140.147.255  Mask:255.255.252.0
          inet6 addr: fe80::78:ff:fe10:301/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1450  Metric:1
          RX packets:24 errors:0 dropped:0 overruns:0 frame:0
          TX packets:20 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:2202 (2.1 KiB)  TX bytes:2640 (2.5 KiB)

```