# Накатываение инстанса RackTables RO

Налить сервер через сетап. Задокументировать в RT хост. Добавить адрес в \_NOCRTSRV\_. Навесить теги {SNMP poller} и {сервер RT}. Добавить хост в кондуктор в группу noc_rt с тегами ipvs_tun, ipvs_tun_no_mtu, ipvs_tun_communal.
Добавить хость в RS pool racktables. После этого отансиблить хост ролью racktables:
```
FILTER="man1-rt1.yndx.net" ansible-playbook -f 1 -vvv playbooks/deploy-zabbix.yml
```

Сконфигурить сеть 
```
netconfig > /etc/network/interfaces
```
Разрешить новый хост как mysql slave на мастере RT. 
