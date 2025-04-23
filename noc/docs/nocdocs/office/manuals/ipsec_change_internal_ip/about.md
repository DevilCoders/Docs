Последовательность действий:
1. При замене IPv4 выделяем /31 сеть под туннель, либо /64 для IPv6:

- Name: IPsec peer to peer
- Tags: IPSEC VPN, <локация>
- FW-macro: 
  IPSECTUNNELENDPOINTS
  Альтернативно: удалить туннель с рыбки и концентратора, и создать новый с тем же номером на ![https://racktables.yandex-team.ru/index.php?page=staffonly&tab=regoffice](https://racktables.yandex-team.ru/index.php?page=staffonly&tab=regoffice), в таком случае пункт 3 можно пропустить.

2. Необходимо убедиться, что агрегат новой сети входит в noc/routers/global-routers-inc.m4
3. Меняем IP-адреса ipsec-интерфейса на рыбке и VPN-концентраторе (удаляем в RT старый и добавляем новый с тем же именем, но с другим адресом). На рыбку вешается второй адрес из /31, на VPN-концентратор первый. Тип аллокации во всех случаях - Point-to-point.
4. Ждем 5 минут, чтобы сгенерировался файл racktables.m4 с измененными внутренними адресами gif-интерфейсов
5. Меняем адреса вручную на рыбке и VPN-концентраторах  
   ```
   IPv4
   sudo ifconfig ipsecXXX <ip рыбки> <ip концентратора> netmask 255.255.255.255 #это для рыбки
   sudo ifconfig ipsecXXX <ip концентратора> <ip рыбки> netmask 255.255.255.255 #это для концентратора
   IPv6
   sudo ifconfig ipsecXXX <new ipv6 концентратора> <ipv6 рыбки> prefixlen 128 
   sudo ifconfig ipsecXXX <new ipv6 рыбки> <ipv6 концентратора> prefixlen 128
   sudo ifconfig ipsecXXX <old ipv6 концентратора> <ipv6 рыбки> prefixlen 128 delete
   sudo ifconfig ipsecXXX <old ipv6 рыбки> <ipv6 концентратора> prefixlen 128 delete
   ```
6. Проверяем маршрут для локального адреса:на рыбке 
   ```
   route -n get <ip рыбки>
   если видим PROTO (должно быть STATIC), делаем еще раз:
   ifconfig ipsecXXX inet <ip рыбки>/32 <ip сети>
   ```
7. На обоих сторонах туннеля обновляем дерево конфигов:  `sudo -E make -C /usr/local/router update`
8. продуваем файрволы: `sudo -E make -C /usr/local/router/fw restart`
9. Обновляем и конфигурируем rc.conf
   ```
   sudo -E make -C /usr/local/router/conffiles rc.conf 
   diff /etc/rc.conf /usr/local/router/conffiles/rc.conf
   sudo -E make -C /usr/local/router/conffiles install-rc-conf
   ```
10. Обновляем конфиги bird на обоих сторонах туннеля:
    ```
    sudo -E make -C /usr/local/router/conffiles/bird clean
    sudo -E make -C /usr/local/router/conffiles/bird all bird-check install loadrun
    ```