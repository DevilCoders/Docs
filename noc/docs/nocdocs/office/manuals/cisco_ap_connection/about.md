### {red}(В Яндексе используются как контроллерные, так и stand alone решения от cisco. Приступая к вводу в работу, сначала необходимо определить в каком из режимов будет работать ТД, а затем переходить к соответствующей инструкции:)

I.[Stand alone режим](https://wiki.yandex-team.ru/noc/office/wifi/cisco-wds/#vvodvjekspluatacijudljastandalone)II.[Контроллерный режим](https://wiki.yandex-team.ru/noc/office/wifi/cisco-wds/#vvodvjekspluatacijudljakontrollernyx) (Преимущественно КР)
### Действия и данные от HelpDesk'а, необходимые до ввода ТД в эксплуатацию:

1. Задача (тикет) на ввод в эксплуатацию, в котором есть таблица коммутаций.
2. ТД должна быть отмечена на карте офиса
### Ввод в эксплуатацию для **stand alone**:

1. Настроить порт на коммутаторе, куда подключена точка:
   ```
   switchport trunk native vlan <mgmt vlan>
    switchport trunk allowed vlan <пользовательские WiFi-вланы офиса + управляющий + vlan441>
    switchport mode trunk
    switchport nonegotiate
    spanning-tree portfast trunk
    spanning-tree bpduguard enable
   ```
    Если не добавить "пользовательские Wi-Fi vlan"- точка введется в эксплуатацию, но  Wi-Fi пользователь окажется в тупиковом  vlan без сервисов и доступа. **Никаких других команд (кроме description, который настраивается RackTables) быть не должно!**
2. Подключиться к ТД по telnet/ssh
3. Убедиться, что точка подцепилась к WDS, в логе должна быть следующая строчка:
   ```
   #sh logg | i WLCCP
   Nov 22 16:11:22 MSK: %WLCCP_AP-6-INFRA: WLCCP Infrastructure Authenticated
   ```
   Кроме этого, ТД должна встать в BACKUP WDS'а:
   ```
   #sh wlccp wds
         MAC: 0035.1aaf.1d44, IP-ADDR: 37.9.66.26     , IPV6-ADDR: ::         , Priority: 1
         Interface BVI1, State: BACKUP
   Currently ACTIVE WDS - MAC: 30e4.db7e.c4a0, Priority: 100, IP-ADDR: 37.9.66.7
   ```
4. При сомнениях - в отдельном окне подключиться к WDS-мастеру (в примере выше - к 
   37.9.66.7
   ) и убедиться, что ТД есть в списке ТД в корректном статусе REGISTERED:
   ```
   rplaza-w1#sh wlccp wds ap
     HOSTNAME                           MAC-ADDR      IP-ADDR          STATE
    rplaza-w8                        4c00.82ad.7929  37.9.66.15      REGISTERED
    rplaza-w7                        4c00.82ad.7866  37.9.66.13      REGISTERED
    rplaza-w2                        6073.5ca8.886a  37.9.66.8       REGISTERED
    rplaza-16w1                      4c00.82df.970e  37.9.66.18      REGISTERED
    rplaza-w1                        30e4.db7e.c4a0  37.9.66.7       REGISTERED
    rplaza-23w4                      4c00.82ad.797f  37.9.66.16      REGISTERED
    rplaza-15w1                      0035.1aaf.1d44  37.9.66.26      REGISTERED
    rplaza-17w1                      4c00.82df.96ee  37.9.66.11      REGISTERED
    rplaza-17w2                      f872.ea76.dfed  37.9.66.10      REGISTERED
    rplaza-15w2                      0035.1a32.256c  37.9.66.27      REGISTERED
    rplaza-16w2                      4c00.8277.3af5  37.9.66.12      REGISTERED
   ```
5. Поднять радиоинтерфейсы: 
   ```
   rplaza-15w1#conf t
   Enter configuration commands, one per line.  End with CNTL/Z.
   rplaza-15w1(config)#int do0
   rplaza-15w1(config-if)#no shut
   rplaza-15w1(config-if)#int do1
   rplaza-15w1(config-if)#no shut
   rplaza-15w1(config-if)#
   ```
6. Убедится, что все необходимые BSSID включены
   ```
   rostof-w4#show dot11 bssid
   Interface      BSSID         Guest  SSID
   Dot11Radio0   d0c7.8967.c2b0  Yes  Guests
   Dot11Radio0   d0c7.8967.c2b1  Yes  MobCert
   Dot11Radio0   d0c7.8967.c2b2  Yes  PDAS
   Dot11Radio0   d0c7.8967.c2b3  Yes  Yandex
   Dot11Radio1   d0c7.8969.c250  Yes  Guests
   Dot11Radio1   d0c7.8969.c251  Yes  MobCert
   Dot11Radio1   d0c7.8969.c252  Yes  PDAS
   Dot11Radio1   d0c7.8969.c253  Yes  Yandex
   ```
7. Добавить недостающие в списке выше BSSID и выкатить актуальные пароли (взять отсюда для [Guests](https://wiki.yandex-team.ru/diy/wifi/guestpass/) и [MobCert](https://wiki.yandex-team.ru/diy/wifi/mobcertpass) )
   ```
   ben-31w1(config)#dot11 ssid Guests
   ben-31w1(config-ssid)#wpa-psk ascii 0 <пароль plain-текстом>
   ben-31w1(config-ssid)#int do0
   ben-31w1(config-if)#ssid Guests
   ben-31w1(config-if)#int do1
   ben-31w1(config-if)#ssid Guests
   ```
8. Содать в RackTables у ТД порт gi0 (fa0 для старых моделей), после чего в LiveCDP выполнить линковку интерфейса. Убедиться, что действительность совпадает с таблицей коммутаций.
9. Снять теги 
   ещё не работает
    и 
   ожидает ввода в работу
    и проставить для всех запрошенных HD-ом SSID тэги вида 
   ssid MobCert
    исключая 
   запароленный ssid Guests
   .
10. Отписаться о проделанной работе в тикет HelpDesk'а и закрыть его по необходимости.
### Ввод в эксплуатацию для **контроллерных**:

1. Настроить порт на коммутаторе, куда подключена точка:
   ```
   switchport access <mgmt vlan>
    switchport mode access
    spanning-tree portfast
    spanning-tree bpduguard enable
   ```
2. Выставить в РТ "CAPWAP AP group name" и "CAPWAP data encryption" как у соседних точек или уточнить у офисной группы
3. Кликунть в РТ "ввести в работу"
### CAPWAP профили в РТ

**CAPWAP data encryption** используется в случаях, когда трасса от точки выходит за границы арендуемой нами территории с пропускным режимом.Другими словами, мы шифруем всё, что за границами турникетов.

Вот основные варианты:
- RedRose.Morozov (Yandex, PDAS, Guests, MobCert)
- RedRose.Morozov.DTC (Yandex, PDAS, Guests, MobCert, MobTest, MobDevInternet)
- RedRose.Mamontov (Yandex, PDAS, Guests, MobCert)
- RedRose.Mamontov.pDTC (Yandex, PDAS, Guests, MobCert, MobTest, MobDevInternet)
- RedRose.Stroganoff (Yandex, PDAS, Guests, MobCert)
- RedRose.Stroganoff.pDTC (Yandex, PDAS, Guests, MobCert, MobTest, MobDevInternet)
Соответственно, для включения MobDevInternet нужно выбрать в RT группу *DTC.И проставить тег "ssid MobDevInternet".Дальше всё сделает автоматика. С перерывом сервиса на 5-10 минут.

**И еще про теги:**Теги обязательно нужны для сетей MobDevInternet, MobTest:
- тег ssid MobDevInternet
- тег ssid MobTest
Есть ещё несколько специфичных сетей, которые подняты на небольшом количестве точек. Например:
- тег ssid MobDevHotSpot
- тег ssid Yandex_Free