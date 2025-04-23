1. Вносим изменения в RT: снимаем сеть vlan401 из IP и добавляем с новым адресом
2. Ждем 5 минут, чтобы сгенерировался racktables.m4
3. Если IPMI живет на адресах ISP, то выполняем проливку фаервола согласно [инструкции](https://wiki.yandex-team.ru/noc/OOBM/#ipmivregionax) с учетом производителя сервера. Это требуется, чтобы исключить вероятность присутствия новых адресов vlan401 в файле ipmi-static-routes (iptables для ipmi).
4. Меняем адрес вручную`sudo ifconfig vlan401 inet (inet6) <новый адрес>/<маска> alias`
5. Обновляем дерево конфигов`sudo -E make -C /usr/local/router update`
6. Обновляем rc.conf.local
   ```
   sudo -E make -C /usr/local/router/conffiles ifconfig
   sudo -E make -C /usr/local/router/conffiles ifconfig_diff
   sudo -E make -C /usr/local/router/conffiles install-ifconfig
   ```
7. Продуваем фаервол`sudo -E make -C /usr/local/router/fw restart`
8. Делаем предыдущие шаги на другой рыбке и обновляем конфиги bird
   ```
   sudo -E make -C /usr/local/router/conffiles/bird clean
   sudo -E make -C /usr/local/router/conffiles/bird all bird-diff
   sudo -E make -C /usr/local/router/conffiles/bird all bird-check install loadrun
   ```
9. Удаляем старые адреса: `ifconfig vlan401 inet (inet6) <старый адрес>/<маска> delete`
10. Перезапускаем dhcprelay (обязательно!) `sudo -E make -C  /usr/local/router/conffiles/dhcprelya all install restart`
11. Удаляем старую сеть из RT