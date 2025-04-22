1. Меняем адреса igb в RT
2. Документируем изменения туннельных адресов в аннушку по [инструкции (п2-п7)](https://wiki.yandex-team.ru/noc/office/ОбщаяИнформация/#dokumentirovanietunnelja)
3. Заходим на рыбку и меняем в рантайме адрес на igb (можно через alias)`sudo ifconfig igbX inet <адрес>/<маска>`
4. Обновляем дерево конфигов`sudo -E make -C /usr/local/router update`
5. Обновляем rc.conf.local, предварительно посмотрев diff
   ```
   sudo -E make -C /usr/local/router/conffiles ifconfig
   sudo -E make -C /usr/local/router/conffiles ifconfig_diff
   sudo -E make -C /usr/local/router/conffiles install-ifconfig
   ```
6. Внимательно смотрим diff и обновляем конфиг bird
   ```
   sudo -E make -C /usr/local/router/conffiles/bird all bird-diff
   sudo -E make -C /usr/local/router/conffiles/bird all bird-check install loadrun
   ```
7. Обновляем внешний адрес на каждом gif интерфейсе со старым адресом`sudo ifconfig ipsecX inet tunnel <внешний адрес рыбки> <внешний адрес концентратора>`
8. Обновляем rc.conf, предварительно посмотрев diff
   ```
   sudo -E make -C /usr/local/router/conffiles rc.conf
   diff /etc/rc.conf /usr/local/router/conffiles/rc.conf
   sudo -E make -C /usr/local/router/conffiles install-rc-conf
   ```
9. Продуваем фаервол`sudo -E make -C /usr/local/router/fw restart`
10. Выполняем те же действия со стороны каждого vpn-концентратора: п4, п6, п7 (меняем адреса местами), п8, п9
11. На vpn-концентраторах подгружаем новый конфиг strongswan`sudo -E make -C /usr/local/router/strongswan/ reload`
12. Передергиваем ipsec
    ```
    sudo ipsec down <концентратор>-ipsecX
    sudo ipsec up <концентратор>-ipsecX
    ```
    После этого в выводе `ipsec statusall | grep ipsecX` должны увидеть новые адреса
    > Если это не помогло и мы все еще видим старые адреса в ipsec statusall и в /var/log/charon.log, то в ночное время рестартим strongswan на рыбках`sudo -E make -C /usr/local/router/strongswan/ -DJUST_DO_IT restart`
После этих действий BGP-сессии должны подняться: `birdc "sh proto"`