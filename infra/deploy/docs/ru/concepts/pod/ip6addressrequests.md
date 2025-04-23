# IPv6 Address Requests / IPv4 туннель

IP6 Address Requests позволяют заказывать ipv6 адреса и ipv4 туннели для пода.

Представлен следующей [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/data_model.proto?rev=r8821812#L1401):

Выданные адреса можно узнать:

* в статусе пода `ya tool dctl status pod -c <cluster> <pod_id>`, см `ip6_address_allocations`
* в [env box/workload](box.md#systemenv)
* через [публичный api pod_agent](../../reference/api/pod-agent-public-api.md)

## Как заказать ipv4 туннель {#ipv4}

* Перед тем как заказывать ipv4, удостоверьтесь, что вам недостаточно NAT64 (IPv4 адресов немного - на них жесткие квоты.)

* IPv4 pool [выдают в службе NOC](https://wiki.yandex-team.ru/NOC/IPv6to4/#nalozhennajaipv4-setvvidetunnelejjakatun64). Через [форму.](https://wiki.yandex-team.ru/noc/ipreq/)

* Заведите тикет в очереди [YPSUPPORT](https://st.yandex-team.ru/createTicket?queue=YPSUPPORT) для импорта вашего пула в базу YP.

Укажите подсети для каждого YP кластера, например:

```yaml
VLA: 5.255.209.128/25
SAS: 37.9.118.128/25
MAN: 37.140.143.128/25
```

Дежурный настроит синхронизацию в YP объекта типа `ip4_address_pool`. Имя и ACL для пула будет синхронизироваться из [ручки racktables](https://racktables.yandex-team.ru/export/tun64-yp.php?yponly).
Указать человекочитаемый id для ipv4 пула нельзя. [Причины можно почитать вот тут](https://st.yandex-team.ru/NOCDEV-2416#5efddd16b9547a25f5eff736).

* Запросите квоту на IPv4 адреса через ABC.
Как посмотреть, сколько квоты использовано/доступно: [https://wiki.yandex-team.ru/yp/yp-cli/#uznatnachtotratitsjakvota](https://wiki.yandex-team.ru/yp/yp-cli/#uznatnachtotratitsjakvota)
Как запросить квоту [https://wiki.yandex-team.ru/yp/quotas/](https://wiki.yandex-team.ru/yp/quotas/). Пул стоит указать в комментарии и приложить тикет из YPSUPPORT, в котором импортировали. 

* Через UI ipv4 пока назначать нельзя DEPLOY-955
Через dctl надо указать свой ip4_address_pool_id для backbone в спеке stage (spec.deploy_units.<deploy_unit_id>.replica_set.replica_set_template.pod_template_spec.spec).

Например:
```yaml
ip6_address_requests: 
- 
  enable_dns: true
  ip4_address_pool_id: "1813:1457"
  network_id: "_TELEMOST_NETS_"
  vlan_id: "backbone"
- 
  enable_dns: true
  network_id: "_TELEMOST_NETS_"
  vlan_id: "fastbone"
```

* Проверьте, что всё импортировалось и в ручке RackTables есть новые пулы [https://racktables.yandex-team.ru/export/tun64-yp.php?yponly](https://racktables.yandex-team.ru/export/tun64-yp.php?yponly)
В случае проблем  необходимо обратиться к дежурному по racktables или завести тикет в st/NOCREQUESTS.

Свободные/занятые адреса на кластере можно узнать так:

```bash
yanddmi@yanddmi-dev[~]:ya tool yp select --address sas internet_address --filter '[/meta/ip4_address_pool_id]="1813:1457"' --selector /spec/ip4_address --selector /status/pod_id
+-------------------+--------------------+
| /spec/ip4_address |   /status/pod_id   |
+-------------------+--------------------+
|   "37.9.118.228"  |         #          |
|   "37.9.118.185"  |         #          |
|   "37.9.118.132"  |         #          |
|   "37.9.118.232"  | "nimfetdt5jqopt2s" |
|   "37.9.118.133"  | "6jnukb4q67uwqhkn" |
...
```

## Приоритет туннелей {#priority}

Можно настроить приоритет туннелей, для этого нужно заполнить поле priority:

```yaml
ip6_address_requests: 
- 
  enable_dns: true
  ip4_address_pool_id: "1813:1457"
  network_id: "_TELEMOST_NETS_"
  vlan_id: "backbone"
  priority: 1
- 
  enable_dns: true
  network_id: "_TELEMOST_NETS_"
  vlan_id: "fastbone"
```
В данном примере backbone сеть будет иметь более высокий приоритет и запросы будут идти в первую очередь через неё. То есть чем выше приоритет, тем выше будет туннель после сортировки. Незаполненное поле приоритета приравнивается к 0. Туннели с одинаковым приоритетом сортируются по положению в схеме: чем позже туннель описан, тем выше он будет стоять после сортировки. 


## Настройка балансировки L3-only {#l3-only}

После [создания](https://wiki.yandex-team.ru/awacs/tutorial/L3/) через AWACS балансера L3 можно приступить к настройке 

Для DeployUnit можно указать virtual_service_ids сервиса L3 
Представлен следующей [proto схемой](https://a.yandex-team.ru/arc_vcs/yp/yp_proto/yp/client/api/proto/stage.proto?rev=9709368976789150745deccc5fac0cc79f560ea9#L144):
Данная настройка доступна через UI ![NetworkDefaults](https://jing.yandex-team.ru/files/amich/ipvs.png)

Начиная с [Runtime version 11](https://deploy.yandex-team.ru/docs/reference/patchers-revision) туннель для балансировки создается только для backbone (до [Runtime version 11](https://deploy.yandex-team.ru/docs/reference/patchers-revision) для backbone и fastbone, что подходит далеко не всем)

Если необходимо более гибко настроить, например явно указать backbone или fastbone, можно задать настройки [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/data_model.proto?rev=r8821812#L1401) при этом удалив их из [TNetworkDefaults](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/data_model.proto?rev=r8821812#L1401):

```
 DeployUnit:
           
      multi_cluster_replica_set:	      
        ....            
          pod_template_spec:	          
            spec:	            
              .....                 
              ip6_address_requests:	              
                - enable_dns: true	                
                  network_id: "_CUSTOM_NETWORK_ID_"	                
                  virtual_service_ids:
                    - "my.fancy.domain.yandex.net"
                  vlan_id: "backbone"	                 

```

