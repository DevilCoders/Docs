# Основное

## Полезные ссылки
* [RackTablesUserGuide](https://wiki.racktables.org/index.php/RackTablesUserGuide)
* [RackTablesDevelGuide](https://wiki.racktables.org/index.php/RackTablesDevelGuide)
* [RT в Яндекс](https://wiki.yandex-team.ru/noc/racktables/)
* [Новая дока Racktables](https://docs.yandex-team.ru/racktables/)

## Source code:
* [rt-yandex](https://noc-gitlab.yandex-team.ru/nocdev/racktables)
* [rt-upstream](https://noc-gitlab.yandex-team.ru/nocdev/racktables-upstream)



## set-up
[set-up](https://racktables.yandex-team.ru/index.php?page=switchgen&tab=manage)
Если не указать FQDN, то pns будет пытаться найти свободный для этого варианта наливки.

Правильный формат ввода - `107688133 ektserov-u1201.yndx.net`

Имя оборудования должно удовлетворять правилам именования в [pns.php](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/blob/master/plugins/pns.php)


## permissions
[RT Permission configuration](https://wiki.racktables.org/index.php/RackTablesAdminGuide#Permission_configuration)


Права хелпдеску на просмотр логов консолятора
```
RCS file: /opt/CVSROOT/noc/routers/salamander-data/RackTables-permissions.txt,v
diff -u -b -r1.3410 -r1.3412
@@ -2572,7 +2572,8 @@
  or {сервер консольного доступа} and {$op_conport} # включать/выключать наливку
 )

-allow {helpdesker} and {сервер консольного доступа} and ({router for office} or {Красная Роза} or {офис Минск}) and {$op_conport}  # включать/выключать наливку
+# $loc_Office появился из NOCREQUESTS-26908
+allow {helpdesker} and {сервер консольного доступа} and ({router for office} or {Красная Роза} or ([$loc_Office] and not [$loc_DC])) and {$op_conport}  # включать/выключать наливку
 allow {helpdesker} and {юзерский свитч} and {$tab_ports}
 allow {helpdesker} and {$tab_poepanel} and not {$any_op}
 allow {helpdesker} and {$tab_fw} and not {$any_op}
```

## Доступ к ssh help@noc-myt,noc-sas
```
[root@noc-myt /usr/home/racktables/.ssh]# grep help /etc/ssh/sshd_config
Match User help
        AuthorizedKeysCommand /root/proxy-authorized_keys-for-help.sh
        AuthorizedKeysCommandUser help

[root@noc-myt /usr/home/racktables/.ssh]# cat /root/proxy-authorized_keys-for-help.sh
#!/bin/sh

cat /usr/home/racktables/.ssh/authorized_keys.for.help
```

Файл с ключами `authorized_keys.for.help` синкается функцией `updateStaffSSHKeysForConsoleAccess` в [plugins/staff.php](https://noc-gitlab.yandex-team.ru/nocdev/racktables/-/blob/master/plugins/staff.php)

## Добавление локальных учеток на сервера noc-sas/myt
[Инструкция в доке](https://docs.yandex-team.ru/racktables/scripts/add-freebsd-user)

## Кроны

Большинство кронов отправляют свой выхлоп в рассылку [noc-cronjobs@](https://ml.yandex-team.ru/noc-cronjobs/)

----

```
[ -e ~/nocron -o  -e ~/noslb ] || lockf -s -t0 /tmp/slb-check-update.lock slb-check-update.sh
```
Используется в slb-check.php для ответа балансеру

----

```
[ -e ~/nocron -o ! -e ~/master ] || for q in balancer:10 regoffice:5 core:10 tun64:5; do  lockf -s -t0 /tmp/restart-firewalls-$q.lock php ~/rt-yandex.git/scripts/restart-firewalls.php ${q\%\%:*} ${q##*:} | mail -E -s "Racktables $q fw restart softerror" lytboris@yandex-team.ru,artem@yandex-team.ru & done
[ -e ~/nocron -o ! -e ~/master ] || lockf -s -t30 /tmp/check-firewalls.lock rt-exec checkFwRestarts
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/fw-restart.php --tun64
```
Рестарт FW [topka](../firewall/topka)

----

```
[ -e ~/nocron ] || save-export hbf-drills.json -- rt-exec exportHbfTrainingsJson
[ -e ~/nocron ] || save-export hbf-drills_v2.json -- rt-exec exportHbfTrainingsJsonV2
```
Учения [topka](../firewall/topka)

----

```
[ -e ~/nocron -o -e ~/master -o ! "`uname -s`" = "FreeBSD" ] || lockf -s -t0 /tmp/populate-logexport.lock /bin/sh ~/rt-yandex.git/scripts/populate-logexport.sh
[ -e ~/nocron -o -e ~/master -o ! "`uname -s`" = "FreeBSD" ] || lockf -s -t0 /tmp/upload-logexport.lock /bin/sh ~/rt-yandex.git/scripts/upload-logexport.sh
[ -e ~/nocron -o -e ~/master -o ! "`uname -s`" = "FreeBSD" ] || lockf -s -t0 /tmp/populate-logexport.lock /bin/sh ~/rt-yandex.git/scripts/populate-logexport.sh
[ -e ~/nocron -o -e ~/master -o ! "`uname -s`" = "FreeBSD" ] || lockf -s -t0 /tmp/upload-logexport.lock /bin/sh ~/rt-yandex.git/scripts/upload-logexport.sh
```
какое-то управление логами

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/cronPushProjectIdAcl.lock rt-exec cronPushProjectIdAcl >> /var/log/cronPushProjectIdAcl.log
```
???

----

```
[ -e ~/nocron ] || lockf -s -t0 /tmp/update_mondata_export.lock bash -c 'sleep $(( RANDOM \% 15 )); update_mondata_export.sh'
```
выгрузки мондаты

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/fetch-lb-status.lock rt-exec fetchLbStatus 2>&1 | mail -Es "CRON: rt-exec fetchLbStatus" noc-cronjobs@yandex-team.ru,neverov@yandex-team.ru,ezhichek@yandex-team.ru,junk@yandex-team.ru
```
таскаются файлики с балансеров

----

```
[ -e ~/nocron -o ! -e ~/master ] || staffnets-by-POI.sh >/dev/null
```
выгрузка списка девайсов в файлик, зачем надо неясно

----

```
[ -e ~/nocron ] || lockf -t0 /tmp/networklist.lock php ~/rt-yandex.git/export/networklist.php --warm-cache
```
подогрев кеша ручки

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/update_dnscache.lock rt-exec commitDnsCache
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec rotateSlbIps
```

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec capwap2ndStageDeploy 2>&1 | mail-utf8 -Es "capwap2ndStageDeploy errors" lytboris@yandex-team.ru
[ -e ~/nocron -o ! -e ~/master ] || rt-exec capwap2ndStageDeploy TRUE 2>&1 | mail-utf8 -Es "capwap2ndStageDeploy errors" lytboris@yandex-team.ru
```
new pns

----

```
[ -e ~/nocron ] || lockf -s -t60 /tmp/pull-gitworkdir.lock pull-gitworkdir.sh -q
```
стягивает свежие comocutor/ann etc

----

```
[ -e ~/nocron -o ! -e ~/master ] || save-export decap-monitoring-info.json -- php ~/rt-yandex.git/scripts/decap-monitoring-info.php
```
очередная выгрузка для мониторинга декапов

----

```
[ -e ~/nocron ] || save-export macro-to-projectid.json -- ~/rt-yandex.git/scripts/macro-to-projectid.py
```
уже rtapi?

----

```
[ -e ~/nocron -o -e ~/netmap-master ] || (cd /netmap && lockf -s -t0 /tmp/netmap-slave.lock src/DO_netmap_slave.sh)
[ -e ~/nocron -o ! -e ~/netmap-master ] || (cd /netmap && lockf -t 0 /tmp/netmap-lock src/DO_netmap.sh)
```
new netmap

----

```
[ -e ~/nocron ] || save-export l3-tors.txt -- rt-exec printL3TorNets
[ -e ~/nocron ] || save-export l3-tors.json -- rt-exec printL3TorNetsJson
```
выгрузка сетей торов текстом и json

----

```
[ -e ~/nocron -o ! -e ~/master ] || ( cd ~/cvsworkdir/routers/scripts/syncers/ && ./export_hostgroups.sh )
```
коммит хостов в cvs, использование неясно

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec commitRTDynfwInjectors
```
[topka](../firewall/topka)/`puncher`

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec syncFWSections
```
[topka](../firewall/topka)

----

```
[ -e ~/nocron ] || [ ! -x /usr/local/conserver/conserver/racktables-update.sh ] || /usr/local/conserver/conserver/racktables-update.sh >/dev/null 2>&1
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/racktables-update-MobTest-ACL.php
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/racktables-set-wifi-password.php Guests
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/racktables-set-wifi-password.php MobCert
[ -e ~/nocron -o ! -e ~/master ] || [ `date \+\%-e` -gt 7 ] || php ~/rt-yandex.git/scripts/racktables-set-wifi-password.php MobTest
[ -e ~/nocron -o ! -e ~/master ] || [ `date \+\%-e` -gt 7 ] || php ~/rt-yandex.git/scripts/racktables-set-wifi-password.php MobDevInternet
[ -e ~/nocron -o ! -e ~/master ] || [ `date \+\%-e` -gt 7 ] || php ~/rt-yandex.git/scripts/racktables-set-wifi-password.php MobDevHotSpot
[ -e ~/nocron -o ! -e ~/master ] || [ `date \+\%-e` -gt 7 ] || php ~/rt-yandex.git/scripts/racktables-set-wifi-password.php MobTestContractors
```
[Документация по обновлению SSID паролей](https://docs.yandex-team.ru/racktables/scripts/set-wifi-passwords)

----
```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/check-8021q-vtp.lock php ~/rt-yandex.git/scripts/check-8021q-vtp.php
```
[Документация по выкатке вланов](https://docs.yandex-team.ru/racktables/plugins/pseudo-vtp)

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/racktables.bgppl.lock php -d memory_limit=1G -r '$script_mode=TRUE; require "./racktables-production/wwwroot/inc/init.php"; bgpPLQueueMaker();bgpPLQueueExec();'
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/check-inner-pls.lock rt-exec checkInnerPLs
```
[Документация по првоерке и выкатке prefix-list'ов](https://docs.yandex-team.ru/racktables/plugins/bgp-filters)

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec pruneOncePns
```
pns

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/sync_flow_label.lock php ~/rt-yandex.git/scripts/fl_label.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/syncdescr.lock php ~/rt-yandex.git/scripts/racktables-port-descriptions.php | sendmail -t >/dev/null
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/annsyncdescr.lock php ~/rt-yandex.git/scripts/ann-deploy.php -gdescriptions "[работает ann-port-descriptions]" | mail -E -s "A description sync" noc-robots.racktables@yandex.net
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/import-conductor-macros.lock php ~/rt-yandex.git/scripts/import-conductor-macros.php
```
[topka](../firewall/topka)

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/gen-fwmacros.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/set-tacacs-enabled.php
```
tacacs

----

```
[ -e ~/nocron -o ! -e ~/master ] || copy-running-startup.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/syncdomain.pullall.lock syncdomain.php --stderr --nolock --mode=pullall >> ~/syncdomain.log
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/racktables-delete-old-huawei-files.php
```
???

----

```
[ -e ~/master ] || ~/rt-yandex.git/scripts/backup-rt-db.sh
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec checkDomainAggSwitches fix show_path | mail-utf8 -E -s "checkDomainAggSwitches" "noc-cronjobs@yandex-team.ru"
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/racktables-clear-5300-macs.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/auto-park.lock php ~/rt-yandex.git/scripts/autoparking.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/set-vrf-on-routed-networks.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || ~/rt-yandex.git/scripts/link_errors_export.py | mail-utf8 -E -s "link_errors_export" "adess@yandex-team.ru"
```
???

----

```
[ -e ~/nocron ] || rt-exec updateStaffSSHKeysForConsoleAccess
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || ~/gitworkdir/comocutor-contrib/utils/inventory.py --update_inv_file /usr/local/racktables-export/inventory.json
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/generate-fw-infra-events.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || ( set -e; cd ~/cvsworkdir/balancers/iptables; cvs -Q up -ACd >/dev/null; cd ~/cvsworkdir/routers/fw; cvs -Q up -ACd >/dev/null; ./sections-review.pl ) | mail-utf8 -E -s "Racktables FW commits" firewall@yandex-team.ru
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || syncdomain.php --stderr --mode=push >> ~/syncdomain.log
```
Обновляет вланы на оборудовании -> rtapi/ck

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -s -t0 /tmp/sync_downtimes.lock ~/rt-yandex.git/scripts/sync_downtimes.py 2>&1
```

----

```
[ -e ~/nocron ] || php ~/rt-yandex.git/scripts/make-unrdup-cfg.php > /tmp/unrdup.cfg cat /tmp/unrdup.cfg > /usr/local/racktables-export/unrdup.cfg
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec commitConserverConfig
```
управление консоляторами

----

```
[ -e ~/nocron ] || lockf -s -t0 /tmp/nat64-mapping.lock rt-exec publishNat64
```
фактически неиспользуется -> ipv4mgr

----

```
[ -e ~/nocron ] || lockf -s -t0 /tmp/cron_sh.lock cron_sh.py
[ -e ~/nocron ] || lockf -s -t60 /tmp/cron_sh.lock cron_sh.py --clean
```
отправка алертов кронджоб

----

```
[ -e ~/nocron ] || save-export map64.json -- rt-exec export64MappingJson
[ -e ~/nocron ] || save-export tun64_yponly.json -- rt-exec exportTun64PoolsYPOnly
[ -e ~/nocron ] || save-export map64_rndsrc.json -- rt-exec export64MappingJsonWithRandomization
[ -e ~/nocron ] || save-export map64.txt -- rt-exec export64Mapping
```


----

```
[ -e ~/nocron ] || lockf -s -t0 /tmp/arb-disp.lock save-export arb-disp.json -- php ~/rt-yandex.git/scripts/arb-confgen.php --kind=disp
[ -e ~/nocron ] || lockf -s -t0 /tmp/arb-agent.lock save-export arb-agent.json -- php ~/rt-yandex.git/scripts/arb-confgen.php --kind=agent
```
запчасти от арбитра

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec checkTorAllocsMissingTagJuggler
[ -e ~/nocron -o ! -e ~/master ] || rt-exec checkTorAllocsDuplicatedJuggler
[ -e ~/nocron -o ! -e ~/master ] || rt-exec checkTorL3VlanWithoutPrefixJuggler
[ -e ~/nocron -o ! -e ~/master ] || rt-exec checkTorProjectIdPushStaleJuggler
```
???

----

```
[ -e ~/nocron ] || save-export fw-sections.json -- rt-exec printSectionOwners
```
выгрузка для панчера

----

```
[ -e ~/nocron ] || save-export owners.json -- rt-exec printOwnersJson
```
очередная выгрузка ответственных

----

```
[ -e ~/nocron ] || save-export port-vlans.json -- rt-exec printPortVlans
```
частная выгрузка для решения [NOCDEV-689](http://st.yandex-team.ru/NOCDEV-689)

----

```
[ -e ~/nocron ] || lockf -s -t0 /tmp/magistral-links.lock save-export magistral-links.json -- rt-exec printMagistralLinks
```
используется где-то в мониторинге, надо бы поменять на хождение в api в том месте

----

```
[ -e ~/nocron ] || save-export l3-segments2.xml -- php ~/rt-yandex.git/scripts/l3_segments2.php xml
[ -e ~/nocron ] || save-export l3-segments2.json -- php ~/rt-yandex.git/scripts/l3_segments2.php json
```
???

----

```
[ -e ~/nocron ] || save-export fastbone-vlan-map.json -- rt-exec exportFastboneVlanMap
```
еще одна выгрузка

----

```
[ -e ~/master ] || pull-rt-code.sh
```
Деплой

----

```
[ -e ~/master ] || tar-all-repos.sh
```
Бэкап

----

```
[ -e ~/nocron ] || save-export noc-ips.txt -- rt-exec printNOCIPs
```
похоже вообще не используется

----

```
[ -e ~/nocron ] || save-export net-layout.xml -- rt-exec printNetLayoutXml
```
опять частная выгрузка

----

```
[ -e ~/nocron -o ! -e ~/master ] || (rt-exec updateNetworkSectionMap && php ~/rt-yandex.git/scripts/racktables-macro2section.php)
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec backupIPLayoutCron
```
выгрузка в cvs сетей

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/commit-allow-global-rules sh ~/rt-yandex.git/scripts/commit-allow-global-rules.sh
```
??? (уже сделано в панчере для dynfw)

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/add-ipv6-search-tag.php
```
добавляет забытые теги

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/racktables.hbf-client-log.lock ~/rt-yandex.git/scripts/hbf-client-log/collect-hbf-log.sh
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec fillDynamicZones
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/set-wifi-breed.php
```
добавляет sw type

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/racktables-fetch-qos.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/mac-learning-handler.php check
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || racktables-hostinfo-hub.php
```
собиралка данных

----

```
[ -e ~/nocron -o ! -e ~/master ] || pending-dyn-nets.sh | mail-utf8 -E -s "pending-dyn-nets.sh" "noc-cronjobs@yandex-team.ru"
```
мониторилка отрезания в динамику сетей

----

```
[ -e ~/nocron ] || refresh-hostkeys.pl -P1 -i -n 20 >/dev/null
```
чистка known hosts

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/update_snmpports.php
```
обновляет данные по snmp

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/export/gen_prefix_lists.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec updateStaffSSHKeysOnTunnelers
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec dispatchTasksQueue 2>&1 | filter-pq-dispatcher.php
```
отложенные задания, в том числе внутри РТ штуки

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -s -t5 /tmp/ipv4mgr_import.lock rt-exec importFromIpv4MgrNat64 https://ipv4.yandex-team.ru/v0/export
```
???

----

```
[ -e ~/nocron ] || rt-exec updateFWCVS routers/fw/macros-inc.m4
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/deploy-dhcp.lock rt-exec checkDeployRegDhcp
```
части управления офисными роутерами

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/cache-macros-list.lock rt-exec cacheMacrosList
```
используется при создании pid

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec databaseGarbageCollect
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || ( rt-exec recalcPerDTorTags ; rt-exec recalcGreyNetTags ; rt-exec recalcTorSlaveTags ; rt-exec recalcGeoTagsByRacks ; rt-exec recalcDynFWNetTags )
```
актуальность РТ

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/localuser-db/localuser-db.php -S2 noc-gitlab
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || a-robots-svnup.sh
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/auto-tags.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/plugins/scripts/racktables-sw-versions.php | mail -E -s "SW versions sync" noc-robots.racktables@yandex.net
```

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/racktables-re-authenticate-dc.php
```
802.1x запчасти

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec applyAlienNetTag
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec fixLaggLinks
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec fixFastboneMistaggedNets
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec clearPermsForRemovedVs
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/localuser-db.lock ~/rt-yandex.git/scripts/localuser-db/deploy/deploy-localuser-db.sh
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/sync-staff.lock rt-exec updateStaffCache
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec warmDNSCacheOwners
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec reloadBot >/dev/null 2>&1
[ -e ~/nocron -o ! -e ~/master ] || rt-exec reloadBot 10 2>&1 | mail -Es "bot import errors" noc-cronjobs@yandex-team.ru,lytboris@yandex-team.ru
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec fetchStaffDptTree
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec rotateLogTables
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec renderYandexToolsRIPEDiffReport | mail -E -s 'RIPE discrepancies' noc-robots.racktables@yandex.net,karyakin@yandex-team.ru
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/importumka.php >/dev/null
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec clearUnusedL3Nets
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/deploy-dhcp.lock rt-exec deployRegDhcp
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/sync-dynrows.lock rt-exec syncDynamicRows
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec relinkAllMgmtPorts
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/check-subj-type-consistency.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/updateJuniperRETags.php
```
???

----

```
[ -e ~/nocron ] || ( sudo chown -R racktables:racktables /var/tmp/rt-gw-log && php ~/rt-yandex.git/scripts/daily-cleanup.php )
```
???

----

```
[ -e ~/nocron ] || save-export networklist-perdc.txt -- php ~/rt-yandex.git/export/networklist.php --report=perdc
```
???

----

```
[ -e ~/nocron ] || lockf -t0 /tmp/zones-xml.lock save-export zones.xml -- rt-exec echoReverseZonesXML
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || save-export conductor-map.json -- rt-exec exportConductorMapJson
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || save-export fullview/m9-rr1.v4.json -- ~/rt-yandex.git/scripts/rr-dump.py m9-rr1.yndx.net
```
???

----

```
[ -e ~/nocron ] || save-export switchports.txt -- rt-exec echoPortRoles
```
???

----

```
[ -e ~/nocron ] || save-export dns-walle-nets.txt -- rt-exec printDnsNetsWalle
```
???

----

```
[ -e ~/nocron ] || save-export slb-map.json.gz -- rt-exec printSlbRecords gzip
```
???

----

```
[ -e ~/nocron -o ] || save-export topo-links.json -- rt-exec printTopologyJson
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || save-export l3tor-pod-nums.json -- ~/rt-yandex.git/scripts/l3tor-pod-nums.php
```
???

----

```
[ -e ~/nocron ] || save-export asn_names.txt -- ~/rt-yandex.git/scripts/as_name_export.py
```
???

----

```
[ -e ~/nocron ] || save-export ports.json -- rt-exec printAllLinks
```
???

----

```
[ -e ~/nocron ] || save-export vm-projects2.txt -- rt-exec updateVmFw2
```
выгрузка pid

----

```
[ -e ~/nocron ] || save-export vm-projects.txt -- rt-exec updateVmFw
```
выгрузка pid в другом формате

----

```
[ -e ~/nocron ] || save-export vm-projects-puncher.txt -- rt-exec updateVmFw_puncher
```
еще одна выгрузка pid

----

```
[ -e ~/nocron -o  -e ~/stopzk ] || lockf -s -t0 /tmp/zk-mysql.lock zk-mysql.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || ~/gitworkdir/automation/datasync/export_rt_data.py -d ~/gitworkdir/nocdata -c
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || ( cd ~/gitworkdir/automation/datasync && ./sync_wiki_grids.sh dccodes ctagmap )
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || (export LANG="ru_RU.UTF-8"; save-export dccodes.json -- get_wiki_grid.py dccodes )
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || ( cd ~/gitworkdir/automation/datasync && ./export_macro_inc.sh )
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || save-export bgp-macros-inc.json -- get-bgp-macros-inc-json.sh
```
???

----

```
racktables-nocron-alerts
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || save-export fullview/m9-6pe.v6.json -- ~/rt-yandex.git/scripts/rr-dump.py --ipv6 m9-6pe.yndx.net
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || php ~/rt-yandex.git/scripts/deploy-vlan-policies.php
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || lockf -t0 /tmp/prefix-list.lock ~/rt-yandex.git/scripts/prefix-list-generator.sh
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || rt-exec 'RT\Yandex\Plugin\Cloud\netbox_import' 2>&1 | mail-utf8 -E -s "cloud netbox_import" "noc-cronjobs@yandex-team.ru"
[ -e ~/nocron -o ! -e ~/master ] || rt-exec 'RT\Yandex\Plugin\Cloud\netbox_sync' 2>&1 | mail-utf8 -E -s "cloud netbox_sync" "noc-cronjobs@yandex-team.ru"
```
???

----

```
[ -e ~/nocron ] || ~/rt-yandex.git/scripts/security-fw-svn-cleanup.sh
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || ipmi_agg.php
```
???

----

```
[ -e ~/nocron ] || save-export IB-sw-to-host-link.txt -- rt-exec mellanox_ufm_export_links_to_servers
```
???

----

```
[ -e ~/nocron -o ! -e ~/master ] || (audit-netdev-configs.php --task=orangelamp | tee /home/racktables/audit-netdev-configs-orangelamp.txt | mail -E -s "netdev audit orangelamp" noc-robots.racktables@yandex.net)
```
???
