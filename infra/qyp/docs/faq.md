# FAQ

## Можно ли использовать Intel vtune гипервизор для виртуальной машины? {#intel-vtune}

Для получения доступа ко всем возможностям V-tune требуется выполнение на хосте – используются аппаратные и невиртуализируемые facilities CPU Intel – PEBS (processor event based sampler), BTS (Branch trace store), LBR (Last branch interrupt/exception) + требуется загрузка на хосте специального модуля ядра, поставляющегося вместе с vTune.
Детали: <https://software.intel.com/en-us/vtune-amplifier-help-on-virtual-machine>

Таким образом, V-tune, работающий внутри виртуальной машины, функционирует в ограниченном режиме, то есть по сути почти эквивалентен Linux perf. Драйверов v-tune/спец.модуля ядра в RTC на машинах нет, поэтому на хосте выполнение на данный момент невозможно.


## Осуществляется ли поддержка Windows образов? {#windows}

В QYP возможен запуск виртуальных машин с Windows, но официально мы осуществляем поддержку только [Linux-образов](images-set.md).
[Готовые образы](https://wiki.yandex-team.ru/browser/dev/dev-vm/) можно взять у коллег из Браузера (в наличии есть образ для windows server 2016). При старте вируталки потребуется задать пароль для дальнейшего доступа до неё.


## Как пересоздать виртуальную машину с сохранением данных? {#vm-recreate}

1. Запустить бэкап через UI или vmctl.

   {% note warning %}

   До завершения бэкапа виртуальную машину нельзя включать. Включение приведет к поломке бэкапа.

   {% endnote %}

1. Дождаться завершения бэкапа. Следить за выполнением можно в UI или через команду `vmctl list-backup`.
1. Удалить ВМ.
1. На вкладке **Backups** из UI найти нужный бэкап и создать из него новую ВМ (кнопка **Create VM from Backup**).
1. Если требуется изменить ресурсы ВМ, скопировать ссылку на бэкап (например, `qdm:f0341e1ddbe0b09af2335870a7dbf5c39b74c33c`) и подставить ее в поле образа при создании новой ВМ.

## Что такое QDM и как долго хранятся бекапы? {#qdm-backup}

Про QDM подробнее тут: <https://wiki.yandex-team.ru/qyp/qdm/#chtotakoeqdmzachemonnuzhen>

Бекапы хранятся год (но не более 3х).


## Можно ли создать несколько дисков в виртуальной машине с precise/trusty версией ОС? {#precise-trusty-images}

precise и trusty [объявлены deprecated версиями ОС](https://clubs.at.yandex-team.ru/infra-cloud/709), создать виртуальную машину с несколькими дисками/стораджами можно на основе следующих воркараундов, но в этом случае мы не гарантируем работоспособность ВМ:

1. precise / precise-dev добавление дополнительного диска:

    {% note warning %}

    Если не выполнить эти действия, vm переходит в нерабочее состояние! 
   
    {% endnote %}
    
    Перед добавлением диска на vm необходимо выполнить следующий набор команд:
      * `sudo apt-get update`
      * `sudo apt-get install --only-upgrade cloud-init=0.6.3-0ubuntu1.26`
1. trusty / trusty-dev добавление дополнительного диска:
    Перед добавлением диска на vm необходимо выполнить следующий набор команд:
      * `sudo apt-get update`
      * `sudo apt-get install --only-upgrade cloud-init=0.7.5-0ubuntu1.24`
1. Удаление дополнительного диска из vm c OS precise или trusty
   
    {% note warning %}

    Если не выполнить эти действия, vm переходит в нерабочее состояние! 
   
    {% endnote %}

    Перед удалением диска через UI, необходимо выполнить следующие действия:
      * `sudo unmount /extra_{disk_name}`
      * `sudo vim /etc/fstab` -> удалить строку с указанием дополнительного диска
1. precise / precise-dev расширение основного раздела диска до указанных в квоте
    * `sudo apt-get update`
    * `sudo apt-get install --only-upgrade cloud-utils=0.25-1ubuntu5.2`
    * `sudo apt-get install gdisk`
    * `sudo growpart /dev/vda 1`
    * `sudo sgdisk /dev/vda --attributes=1:set:2`
    * `sudo reboot`



## Настройка сети в докере внутри ВМ {#docker-inside-vm}

1. Учим докер выделять контейнерам адреса из приватного диапазона ipv6 и делаем NAT:
   
    ```
    # cat > /etc/docker/daemon.json <<-EOF
    {
        "iptables": false,
        "ip-forward": false,
        "ipv6": true,
        "dns": [
            "2a02:6b8:0:3400::1023",
            "2a02:6b8:0:3400::5005"
        ],
        "fixed-cidr": "",
        "fixed-cidr-v6": "fd00::/8"
    }
    EOF
    ```

    {% cut "Вариант для Ubuntu 14" %}

    ```
    # cat > /etc/default/docker <<-EOF
    DOCKER_OPTS="--ipv6 --fixed-cidr-v6 fd00::/8 --dns 2a02:6b8:0:3400::1023"
    EOF
    ```

    {% endcut %}

    ```
    # service docker stop && ip link del docker0 && service docker start
    # ip6tables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
    # sysctl -w net.ipv6.conf.all.forwarding=1
    ```

    {% cut "Проверяем что контейнеры получают адреса из указанной сети и NAT работает" %}
    
    ```
    $ docker run -it --rm registry.yandex.net/maps/yacare bash
    root@e78ed0816983:/# ip a
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host 
           valid_lft forever preferred_lft forever
    45: eth0@if46: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
        link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff
        inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
           valid_lft forever preferred_lft forever
        inet6 fd00::242:ac11:2/8 scope global nodad 
           valid_lft forever preferred_lft forever
        inet6 fe80::42:acff:fe11:2/64 scope link tentative 
           valid_lft forever preferred_lft forever
    
    root@e78ed0816983:/# ping6 ya.ru -c5
    PING ya.ru(ya.ru) 56 data bytes
    64 bytes from ya.ru: icmp_seq=1 ttl=56 time=0.243 ms
    64 bytes from ya.ru: icmp_seq=2 ttl=56 time=0.367 ms
    64 bytes from ya.ru: icmp_seq=3 ttl=56 time=0.362 ms
    64 bytes from ya.ru: icmp_seq=4 ttl=56 time=0.364 ms
    64 bytes from ya.ru: icmp_seq=5 ttl=56 time=0.281 ms
    
    --- ya.ru ping statistics ---
    5 packets transmitted, 5 received, 0% packet loss, time 4000ms
    rtt min/avg/max/mdev = 0.243/0.323/0.367/0.054 ms
    ```
    
    {% endcut %}

2. Для сохранения настроек после перезапуска ВМ:
    * ставим пакет `iptables-persistent`, при установке сохраняем только ipv6-правила: `# ip6tables -t nat -A POSTROUTING \! -o docker0 -j MASQUERADE`
    * прописываем настройки systctl в файл `/etc/sysctl.d/local.conf`

Источники:
* <https://wiki.yandex-team.ru/users/vmazaev/docker-v-QYP/>
* <https://wiki.yandex-team.ru/users/bgleb/docker-ipv6/>
