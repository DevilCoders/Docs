# Генератор конфигурации Guppy

Данный документ описывает логику работы генерации конфигурации Guppy для подключения устройств MacMini к сети ДЦ сети Яндекса.

Сам проект лежит в [arc](https://a.yandex-team.ru/arc_vcs/noc/office/guppy).

Настройка интерфейсов guppy (freebsd firewall) аля yandex-netconfig

Суть работы скрипта сводится к генерации содержимого к файлу конфигурации `/etc/rc.conf.local`.

Чтобы не править его из скрипта было решено:
- конфигурацию генерировать в `packages.cfg.PATH_INTERFACE_CONFIGURATION_FILE`
- и делать include `if [ -r /etc/rc.conf.guppynets ]; then . /etc/rc.conf.guppynets ; fi`

Вначале мы получаем словари с данными о link-local адресах и адресацию порта TOR через RT.

Bridge-domain в Racktables для MacMini: [235](https://racktables.yandex-team.ru/index.php?page=vlandomain&vdom_id=235)

@startuml
participant Guppy
participant RT
Guppy->>RT: Get HOST_64_IFNAMES file
Guppy->>RT: Get L3_TORS file
loop ParseLLDP:
    Guppy->>Guppy: Parsing LLDP data: Hostname and Port of TOR
    ToR->>Guppy: Hostname, Port via LLDP
end
Guppy->>RT: Get Bridge domain 235
RT->>Guppy: VLANs data
loop GenerateConfig:
    Guppy->>Guppy: Generate configuration for all VLANs more than 1200
    Guppy->>Guppy: Write network configuration
end
@enduml
