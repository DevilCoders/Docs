# Sandbox

Получение списка групп осуществляется по урлу API:

https://sandbox.yandex-team.ru/api/v1.0/group?limit=1200&offset=0

# Про поиск хостов по инвентарникам

## Wall-E

https://wall-e.yandex-team.ru/projects/hosts - можно вводить список инвентарников с любыми разделителями, дальше понятно что за проекты

Если нужна история - есть аудитный лог https://wall-e.yandex-team.ru/projects/log,
но к сожалению в wall-e не все хосты есть.

Чего нет в wall-e ищется тут: https://oops.yandex-team.ru

Например https://oops.yandex-team.ru/?q=electra
или https://oops.yandex-team.ru/?q=id+101461847

## GenCfg:

Просто получить данные о хосте
```
sereglond@electra:~/source/gencfg$ ./dump_hostsdata.sh -s electra
myt 101461847 electra.search.yandex.net unknown 752 2934 2784 myt-s101 myt-3 20
```

В /utils/common/dump_hostsdata.py на самом деле больше полей - даже есть данные о валли проектах

```
sereglond@electra:~/source/gencfg$ ./utils/common/dump_hostsdata.py
usage: dump_hostsdata.py [-h] [-s HOSTS] [-g GROUPS] [-i FIELDS] [-f FILTER]
                         [--group-filter GROUP_FILTER] [--iv] [--ing]
                         [-r {plain,json,detailed}]

Script to dump hardware_data hosts_data

optional arguments:
  -h, --help            show this help message and exit
  -s HOSTS, --hosts HOSTS
                        Optional. Comma-separated list of hosts
  -g GROUPS, --groups GROUPS
                        Optional. Comma-separated list of groups
  -i FIELDS, --fields FIELDS
                        Optional. List of fields to show: name,domain,model,po
                        wer,ncpu,disk,ssd,memory,switch,queue,dc,location,vlan
                        ,ipmi,os,n_disks,flags,rack,kernel,issue,invnum,raid,p
                        latform,netcard,ipv6addr,ipv4addr,botprj,botmem,botdis
                        k,botssd,vlan688ip,shelves,golemowners,ffactor,hwaddr,
                        lastupdate,unit,vmfor,l3enabled,vlans,walle_tags,stora
                        ges,ssd_models,ssd_size,ssd_count,hdd_models,hdd_size,
                        hdd_count,mtn_fqdn_version,net,gpu_count,gpu_models,ch
                        ange_time ('all' to show all)
  -f FILTER, --host-filter FILTER
                        Optional. Host filter
  --group-filter GROUP_FILTER
                        Optional. Group filter (check if any of host group
                        satisfy filter)
  --iv                  Optional. Ignore virtual machines
  --ing                 Optional. Ignore machines, which belongs to non-search
                        groups
  -r {plain,json,detailed}, --report-type {plain,json,detailed}
                        Report type. Show report type
```

Чтобы найти к каким группам принадлежат хосты делаем так:

```
sereglond@electra:~/source/gencfg$ ./utils/common/show_machine_types.py -ns "#0.txt"
ALL_OSOL_HEAD_COMPILATION ( 1 total of 2 ): electra.search.yandex.net
```

В 0.txt можно положить и fqdn и инвентарники

Можно напрямую передавать: `./utils/common/show_machine_types.py -ns electra`, разделив запятыми

P.S. Генерилка ставится так:
```
svn co svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/gencfg && cd gencfg && ./install.sh
```
