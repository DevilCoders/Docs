## Ввод в эксплуатацию "u-"коммутатора

### Действия и данные от HelpDesk'а, необходимые до ввода ТД в эксплуатацию:

1. Задача (тикет) на ввод в эксплуатацию, в котором есть таблица коммутаций.
### Ввод в эксплуатацию:

1. Настроить порты на uplink'ах  в сторону нового свитча. Uplink'и могут быть разные - для каждого варината свои настройки:  
   
   {% cut "Cisco" %}
   
   ```
   switchport mode trunk
    ip arp inspection trust
    spanning-tree cost 8192
    ip dhcp snooping trust
   ```
   **Никаких других команд (кроме description, который настраивается RackTables) быть не должно!**
   
   {% endcut %}
      
   
   {% cut "Cisco Nexus" %}
   
   ```
   switchport mode trunk
    speed 1000
   ```
   
   {% endcut %}
     
   
   {% cut "Huawei в роли u- коммутатора" %}
   
   ```
   port link-type trunk
      port trunk allow-pass vlan 2 to 998 1000 to 4094
      undo port trunk allow-pass vlan 1
      stp edged-port disable
      jumboframe enable 9200
      dhcp snooping trusted
   ```
   
   {% endcut %}
      
   
   {% cut "Huawei в роли a- коммутатора" %}
   
   ```
   port link-type trunk
      port trunk allow-pass vlan 2 to 998 1000 to 4094
      undo port trunk allow-pass vlan 1
      stp edged-port disable
      stp vlan 1 to 4094 cost 2000000
      jumboframe enable 9200
      dhcp snooping trusted
   ```
   
   {% endcut %}
2. В RackTables попытаться выполнить 
   SNMP sync
    по SNMPv2 с настройками по умолчанию. Если он не прошел - разбираться в причинах.
3. На вкладке LiveCDP для сisco и LiveLLDP для huawei выполнить линковку интерфейса. Убедиться, что действительность совпадает с таблицей коммутаций.
4. Снять теги 
   ещё не работает
    и 
   ожидает ввода в работу
   .
5. Подключиться к новому свитчу по telnet/ssh, убедиться, что конфигурация портов в сторону аплинков выглядит вот так:       
   
   {% cut "Cisco" %}
   
   ```
   switchport mode trunk
    ip dhcp snooping trust
   ```
   **Никаких других команд (кроме description, который настраивается RackTables) быть не должно!**
   
   {% endcut %}
          
   
   {% cut "Huawei" %}
   
   ```
   port link-type trunk
          port trunk allow-pass vlan 2 to 998 1000 to 4094
          undo port trunk allow-pass vlan 1
          stp edged-port disable
          jumboframe enable 9200
          dhcp snooping trusted
   ```
   
   {% endcut %}
6. Переключить в РТ  любой неактивный порт нового свитча в 999 vlan и синхронизировать кнопкой из 802.1q sync (push local changes out)Затем вернуть обратно в 13000 и снова синхронизировать.Это необходимо для раскатки на новый свитч всех vlan из домена 802.1q данной локации.
7. Отписаться о проделанной работе в тикет HelpDesk'а и закрыть его по необходимости.