#
#
#

dns2-api -- new version of dns-api provided dns-api v2.3 methods.

* syncing data from zoo master database, forcing to list (and convert)
  objects from zoo. As from command line we do not have cache dns-api
  structures, the following command just retrieve data (zone) from zoo
  and list them

        dns2-api objects zones sync --debug --force
        dns2-api objects robots sync --debug --force
        dns2-api objects requests sync --debug --force

Commands above will fetch only objects specified 
but no any cache manipulations will be done

* syncing in the context of running service: push http
  request to server

        dns2-api objects zones sync --debug --server
        dns2-api objects robots sync --debug --server

* periodically run task have multiple jobs:

        case "objects-zones-sync":
                // Syncing zones means syncing all zoo objects:
                // zones, robots
                err = t.ExecObjectsZones(cache, "sync", nil)
                err = t.ExecObjectsRobots(cache, "sync", nil)
...   

* networks rt/xml parsing and caching, it has some 
  profit as networks are parsed, also some attributes
  be calculated:

        dns2-api objects networks sync --debug <--server>

* objects processes: syncing rotation dynamic (UA scheme)

        // https://st.yandex-team.ru/TRAFFIC-10738
        dns2-api sync objects --objects="rotation-dynamic" --debug

        // https://st.yandex-team.ru/TRAFFIC-10739
        dns2-api sync objects --objects="qloud-dynamic" --debug

        // https://st.yandex-team.ru/TRAFFIC-10858
        dns2-api sync objects --objects="ca-dynamic" --debug

* mgmt processing: pipeline

       // realm
       dns2-api mgmt pipeline show --debug --realm realm-vladimir

        // zone (arpa)
        dns2-api mgmt pipeline show --debug --zone 48.88.77.in-addr.arpa

       // markuping zone
       dns2-api mgmt pipeline markup --zone="136.108.95.in-addr.arpa" --debug --dry-run
       dns2-api mgmt pipeline markup --zone="136.108.95.in-addr.arpa" --debug --dry-run --update

       dns2-api mgmt pipeline markup --zone="c.0.8.b.6.0.2.0.a.2.ip6.arpa" --debug --dry-run
       dns2-api mgmt pipeline markup --zone="1.0.8.b.6.0.2.0.a.2.ip6.arpa" --debug --dry-run
       dns2-api mgmt pipeline markup --zone="0.0.d.f.0.1.0.0.2.6.2.ip6.arpa" --debug --dry-run
       dns2-api mgmt pipeline markup --zone="b.8.b.6.0.2.0.a.2.ip6.arpa" --debug --dry-run > /tmp/1
       dns2-api mgmt pipeline markup --zone="0.0.0.0.8.b.6.0.2.0.a.2.ip6.arpa" --debug --dry-run > /tmp/1

      // detecting delegation operations
      dns2-api mgmt pipeline markup --zone="b.8.b.6.0.2.0.a.2.ip6.arpa" --debug --dry-run --update > /tmp/1
      cat /tmp/1 | grep CREATE | grep realm

      dns2-api mgmt pipeline markup --zone="0.0.0.0.8.b.6.0.2.0.a.2.ip6.arpa" --debug --dry-run --update > /tmp/1

      // detecting zone create/remove opertions/delegations


* matching clients in dns2-api is done only for classical
  scheme in MatchObject()

       (A) we should also try matched to topology and return
           namespace+underlayer, at least for certificates (CA)
           sync objects [1]
       [1] https://st.yandex-team.ru/TRAFFIC-11011


* client requests processing

       // Creating request by fqdn, type and data
       dns2-api client requests create --debug "create" "slayer.yastat.net" "A" "127.0.0.2" --service="alpha-31i.lxd.tt.yandex.net"
       '
                {"requests":[{"resource":{"fqdn":"slayer.yastat.net.","ttl":600,"type":"A","data":"127.0.0.1"},"operation":"create"}],
                "uuid":"cd3f148b-64ef-4848-afdb-482c9a6034f6","timestamp":"2020-08-31T18:44:55.708400217+03:00"}
                '
       // Listing requests from queue (first looking for
       // record in cache, second - in the storage)
       dns2-api client requests list --http --id="260e37b4-36b8-4e0a-88e7-129bb3f43c57"

       // Deleting request by its id
       dns2-api client requests delete --http --id="260e37b4-36b8-4e0a-88e7-129bb3f43c57"

        // Archiving request (also this transaction should
        // be done automatically for some aged request in terminated states:
        // done and error states)
        dns2-api client requests archive --http --id="260e37b4-36b8-4e0a-88e7-129bb3f43c57"

       // Listing "all requests" method w/o id it should return
       // all requests via api call
       dns2-api client requests list --debug
       dns2-api client requests list -H --debug

       // Listing requests in table mode?
       // TODO
       dns2-api client requests list -H -T --debug

       // processing should be done with token
       dns2-api client requests process --http --id="260e37b4-36b8-4e0a-88e7-129bb3f43c57" --service="alpha-31i.lxd.tt.yandex.net"
       #
       # dnl processing requests received via dns2-api methods
       # dnl dns2-api node: "alpha-31i.lxd.tt.yandex.net"
       # dnl current time: "2020-09-10 11:39:58.744615149 +0300 MSK m=+133.136695978"
       # dnl number of requests received: "1"
       #

       dnl; [0]/[1] uuid:'de9d0cab-542d-43a7-ac5b-b4cc2bb75bea'
       dnl; [0]/[1] age:'2m3.185422216s'
             dnl; *create the following records*'
             slayer.yastat.net.      IN      600     A       127.0.0.3

       dnl; [0]/[1] meta state:'new'
       dnl; [0]/[1] meta error:''

        (A) Добавить oauth авторизацию -> owner и добавить аттрибуты для
            requests (meta?)
        (B) Добавить метод получения requests по расширенному фильтру?
            Как формировать фильтр? GET /.../ или PUT "JSON"?

        (C) По-умолчанию отдавать requests привязанные к owner'у

           
        (Z) Добавлять --new --done --error поля для
            листинга по фильтру в методе GET? и в command line
            утилиты

            [~] dns2-api client requests list --debug --state="error"
            [~] dns2-api client requests list --debug --state="new"

        (1) syncing current requets objects and st
            dns2-api mgmt requests sync --debug

* auth mechs:

        (0) all keys for corresponding mechs:
            -rw-r--r--   1 root root   377 Oct  5 10:08 .dns2-api.serviceticket
            -rw-r--r--   1 root root   666 Oct  5 09:52 .dns2-api.sessionid
            -rw-r--r--   1 root root    40 Sep 25 10:51 .dns2-api.token

        (1) oauth token:
            # oauth via file (default: /etc/dns2-api/.dns2-api.token)
           dns2-api client requests list --http --debug \
                 --state=new --auth="oauth"

            # oauth via file + service-ticket 
            dns2-api client requests list --http --debug \
                 --state=new --auth="oauth" -Z

        (2) shared-key:
            dns2-api client requests list --http --debug --state=new \
                 --auth="shared-key"

        (4) user-ticket + service-ticket:
            dns2-api client requests list --http --debug --state=new \
                 --auth="user-ticket" -Z

        (5) session-id
            dns2-api client requests list --http --debug \
                 --state=new --auth="session-id"

* ссылки
        [1] https://st.yandex-team.ru/TRAFFIC-10736
        [2] https://wiki.yandex-team.ru/dns/dnsguard/

        (1) Проверяем полноту и правильность работы MatchObject
            dns2-api core.MatchObject()

        (2) Проверяем и делаем command line enabled cookie
            authorization

        (3) Добавляем tvmtool + конфигурацию для tvm демона +
            монитоииг со стороны dns2-api 
            (1) проверка существование нужного service ticket для
                пары dst src
            (2) валидация oauth токенов + service ticket
                относительно dst

        (4) Затаскиваем внутрь tvm для проверки oauth/sessionid
            на паспорте.

* view sync:
       curl -L -v -k https://alpha-31i.lxd.tt.yandex.net/api/v3.0/view

* mgmt methods to retrieve user <-> groups from abc and staff
  fetching for current groups in zones (or full retrieval) and caching
  data (as json/memory <->).
 
  dns2-api subjects sync --debug --force --dry-run

* mgmt mtn networks: we need to get mtn, map it is cache objects
  (with some lookup later) and groups, user resync in  subjects sync.

  also we need to structure for ACL, lookup and so on

  dns2-api objects mtn sync --debug

* locking shared support
   dns2-api mgmt lock --debug --sleep=10

* legacy client method support: to have dns-client (v1.0) be compatible with 
  dns2-api methods

  (1) getting netinfo (network/zone information, zone content, some 
      auxiliary data) for dns-client (zone content and zone info 
      methods)

      dns2-api client legacy netinfo --json | --xml \
           --encoded(zlib+compression) \
           --zone "dns-api-testing.yandex.net"

      e.g.
      dns2-api client legacy netinfo --debug --json --zone="dns-api-testing.yandex.net" \
             --service="alpha-31i.lxd.tt.yandex.net" --encoded

* zones content methods support (1) archiving zones as command line command
     
      dns2-api mgmt zones archive --debug \
        --class="ns1+ns2" --type="all"

* dns2-api mgmt disable l3
     dns2-api mgmt l3 disable --debug
     dns2-api mgmt l3 enable --debug

* zones exported to YP 
     dns2-api mgmt zones export --debug

* acl0 DNS+ACL0 method sync data. Группы abc прорастают в течении 5 минут, 
     однако, есть startup timer в течении которого действуют группы из прикопанного
     acl.json (именно с него поднимается dns2-api и ждёт 10 минут чтобы его 
     обновить), так что тут есть два лага - startup lag (10 минут) update lag (5 минут)

     dns2-api objects acl sync --debug --dry-run

* importing impi objects, please note that process
  is started as external dns2-api process

     dns2-api import objects --class="ipmi-objects" --type="reverse" --debug --dry-run
     dns2-api import objects --class="zombie-objects" --type="reverse" --debug --dry-run
     dns2-api import objects --class="warehouses-objects" --type="reverse" --debug --dry-run --now --force > /tmp/1

*  ротация внешних источников в dns+core+static
        // ротируем Украину
        dns2-api sync objects --objects="rotation-static" --debug --dry-run

        // ротируем сертификаты
        dns2-api sync objects --objects="ca-static" --debug

        // ротируем racktables объекты (yandex.ru)
        dns2-api sync objects --objects="rt-static" --debug --dry-run --now

* dns2 meta objects and operations

     // Create and delete target meta for zone
     dns2-api meta create --dry-run --debug --backends "ns3+ns4" \
	--backends "ns1+ns2" --name "slayer.yandex.ru"

     dns2-api meta delete --uuid="c71a3bf0-7fb2-48a1-87a5-5ab4b7500465"

     // Listing current meta and states?
     dns2-api meta list --debug [--table]

     // Setting backends on meta name
     dns2-api meta set --debug --name="tt.yandex.net" --backends "ns3+ns4" --backends "ns+yp"

     // Setting frontends on meta name
     dns2-api meta set --debug --name="tt.yandex.net" --frontends "ns3+ns4" --dry-run
     dns2-api meta set --debug --name="tt.yandex.net" --activated "ns+yp" --dry-run

* dns2 meta backend zone operations

     // Creating zone configuration in specific backend
     dns2-api meta operations backends --backend "ns3+ns4" \
         config create --uuid="c71a3bf0-7fb2-48a1-87a5-5ab4b7500465" \
         --zone "slayer.yandex.ru" --realm="realm-noc"

     // Listing a zone configuration from specific backend by its uuid
     dns2-api meta operations backends --backend "ns3+ns4" config list \
          --debug --uuid="69acf076-cb5c-11ea-8717-171e77bcdce8"

     // Listing YP zones exported by brige via dns-api
     dns2-api meta operations backends --backend "ns+yp" config list -T


     // Deleting a zone configuration by uuid
     dns2-api meta operations backends --backend "ns3+ns4" config delete \
           --uuid="8b62ddfc-1c4d-11ea-9279-c66776bcdce8" --debug

* dns2-api migration

     // Making call via api or direct as we do it in sync 
     // processing methods
     dns2-api zone migrate --zone="tt.yandex.net" --sync \
           --src-backend="ns3+ns4" \
           --dst-backend="ns+yp" \
           --debug --dry-run

     // Migrate/push zone from a file into backend (defaulting to YP)
     // file is validated to check if all RR are prefixed as zone name
     // in zone parameter. zone file should be in DIG AXFR format.
     dns2-api zone migrate --zone="tt.yandex.net" --sync \
          --file="/etc/dns2-api/zones/test.yandex.net" \
          --dst-backend="ns+yp" \
          --dry-run \
          --debug \

* dns2-api migration (sync)

     // For all zones that should be in sync between
     // ns3+ns4 and ns+YP we need validation/syncing
     // method to be sure that all data in sync state  
     dns2-api zone sync --migrate --dry-run --debug

* dns2-api configuration management show

      // Getting some kind of configuration (e.g. YP unbound
      // configuration) for UUID associated with YP
      dns2-api mgmt config show --debug --uuid="69acf076-cb5c-11ea-8717-171e77bcdce8"

* dns2-api migrate+meta 
      // Creating/syncing zone and setting meta in one operation
      // if meta switch is turned on

      # * "ns3+ns4" means that we activate
      #   data only from ns3+ns4 for reading

      # * "ns+yp" means that data read is activated
      #   from "ns+yp" unbound+yp module

      dns2-api zone migrate --zone="$zone" --sync --src-backend="ns3+ns4" \
	   --dst-backend="ns+yp" --debug --meta="ns3+ns4"

* dns2-api batch zone migration
      dns2-api zone migrate --zones="$zone" --sync --src-backend="ns3+ns4" \
           --dst-backend="ns+yp" --debug --meta="ns3+ns4" --parallels=16


* dns2-api rrset for bridge
       // removing data from YP bridge directly
       dns2-api rrset remove "0.0.0.0.4.0.c.0.8.b.6.0.2.0.a.2.ip6.arpa. 3600 IN NS ns3.yandex.ru." --yp --debug 

       // adding data to YP bridg
       dns2-api rrset add "0.0.1.0.3.0.c.0.8.b.6.0.2.0.a.2.ip6.arpa. 600 IN NS ns3.yandex.ru." --yp --debug

* dns2-api acl commands (managing acl2 entries as dynamic objects)

        // creating acl entry could be done via command line or via
        // yaml supplied or editor from yaml template
        dns2-api acl create --debug --dry-run --namespace "pattern://(.*)?infracc.taxi.yandex.net" \
             --subject "svc_dostavkatraffika_administration" \
             --subject "svc_taxiccinfra_administration" \
             --owner "realm-taxi"

        // creating zombies realm acl0
        dns2-api acl create --debug --namespace "network://172.28.68.0/24" \
            --subject "svc_dostavkatraffika_administration" --owner "realm-zombies"

        // dns2-api acl create --debug --dry-run --namespace "pattern://(.*)?infracc.tt.yandex.net" \
             --subject "svc_dostavkatraffika_administration" --subject "robot-dns" \
             --owner "realm-trafficteam" 

        // owner could be realm-taxi or by default dns-api
        // subject - array of subjects [svc_dostavkatraffika_administration,
        //     svc_taxiccinfra_administration]

        // listing and filtering ACL entries (owner filter)
        dns2-api acl list --debug --owner="realm-sandbox" --owner="realm-noc"

        // listing and filtering subjects filter
        dns2-api acl list --debug -T
        dns2-api acl list --debug --namespace="77.88.8.8" --namespace="1.1.1.1"

        // editing acl
        dns2-api acl edit --debug --uuid="0c1c8349-bd57-478b-b0a3-0643d43e4161"
        dns2-api acl edit --debug --uuid="47a64874-c345-4f8e-bb5b-4110495e32fa" --yaml
 
        // syncing acl w.r.t realms
        dns2-api acl sync --zone="77.88.49.0/24" --zone="77.88.50.0/24" --debug --dry-run

* MANAGING (dynamic) zones: creating, editing, deleting

* CREATE dynamic zone in realm

      // Create a zone "slayer.yandex.ru" at "ns3+ns4" backend
      // in realm "realm-trafficteam" with debug and dry-run
      // option set (for testing)
      dns2-api meta operations backends --backend "ns3+ns4" config create --zone "slayer.yandex.ru" --realm="realm-trafficteam" --debug --dry-run

      // Reverse zone should be in arpa notation
      dns2-api meta operations backends --backend "ns3+ns4" config create --zone "d.0.e.0.c.0.8.b.6.0.2.0.a.2.ip6.arpa" --realm="realm-vladimir" --debug --dry-run
      dns2-api meta operations backends --backend "ns3+ns4" config create --zone "e.0.e.0.c.0.8.b.6.0.2.0.a.2.ip6.arpa" --realm="realm-vladimir" --debug --dry-run

      // TODO: adding options to set meta for zone (by default ns3+ns4
      // and ns+yp for migration purposes), right now we should set meta
      // as follows:
      dns2-api meta create --debug --backends "ns3+ns4" --backends "ns+yp" --frontends "ns+yp" --frontends "ns+cache" --name "slayer.yandex.ru" --dry-run
      dns2-api meta create --debug --backends "ns3+ns4" --backends "ns+yp" --frontends "ns+yp" --frontends "ns+cache" --name "84.43.100.in-addr.arpa" --dry-run

* LIST dynamic zones

      // List all zones as table from backend "ns3+ns4"
      dns2-api meta operations backends --backend "ns3+ns4" config list -T

      // List a specific zone with UUID as table
      dns2-api meta operations backends --backend "ns3+ns4" config list -T --uuid="039ff206-205b-11e7-8488-456c5c05cc3d"

      // Listing zones w.r.t realm (as a table)
      dns2-api meta operations backends --backend "ns3+ns4" config list -T --realm="realm-pcidss"

* DELETE dynamic zones (by UUID)

      // Delete a zone by UUID (could be retrieved from LIST operations)
      // Also deletes a meta (if exists)
      dns2-api meta operations backends --backend "ns3+ns4" config delete --uuid="f1f81ab6-2a81-11e7-9ddb-d6925d05cc3d" --debug --dry-run

      dns2-api meta operations backends --backend "ns3+ns4" config delete --uuid="e79264b4-16e5-11ec-96f3-d9b277bcdce8" --debug --dry-run

* MANAGING (legacy) dynamic zones realms: creating, deleting, setting acl

      // Listing realms as table
      dns2-api realm list  -T --realm="realm-noc" --realm="realm-balance"

      // Setting acl for realm and realm zones
      dns2-api realm set acl --uuid="c1f802c6-8458-11e4-948e-afd65c05cc3d" --acl="ROBOT_KEY("l9y8-7wzc-hi9f-pzbt");GROUP_KEYS(svc_fintech_services_admin_administration);" --debug --dry-run

      // Creating realm:
      dns2-api realm create --realm="realm-test" --acl="ROBOT_KEY("l9y8-7wzc-hi9f-pzbt");GROUP_KEYS(svc_fintech_services_admin_administration);" --debug --dry-run
                --description="Test services" --zone test.slayer.yandex.ru --zone test2.yandex.net
      // Deleting realm:
      dns2-api realm remove --realm="realm-test" --debug --dry-run

      //
        #robot_id="l9y8-7wzc-hi9f-pzbt"
        #robot_create_enabled="no"
        ## config-apply after robot creation
        #robot_acl='GROUP_KEYS(dpt_yandex_mnt_dns_supporters);'

      dns2-api realm edit --realm="realm-test" --debug --dry-run

* NAMESPACES commands

        // Lookup namespaces
        dns2-api namespaces lookup --namespace "pattern://(.*)?mail.yandex.ru" --namespace "network://172.26.209.64/26" --debug

        // Simplifyed version
        dns2-api namespaces lookup --namespace "77.88.50.0/29" --debug 

* IMPORT OBJECTS
       // Importing objects (syncing)
        dns2-api import objects --class="zombie-objects" --type="reverse" --debug  --dry-run  --force

        // Setting correct ACL for?
        // 172.28.128.0/24
        dns2-api acl sync --zone="172.28.128.0/24" --debug --dry-run

        // Syncing private zones for printers and zombies
        dns2-api acl sync --zone="172.24.0.0/13" --zone="10.208.0.0/12" --realm="realm-printers" --debug --dry-run

        dns2-api acl sync --zone="172.24.0.0/13" --zone="10.208.0.0/12" --zone="213.180.192.0/19" --zone="5.45.192.0/18" --zone="5.255.192.0/18" --zone="37.9.64.0/18" --zone="37.140.128.0/18" --zone="45.87.132.0/22" --zone="77.88.0.0/18" --zone="87.250.224.0/19" --zone="93.158.128.0/18" --zone="95.108.128.0/17" --zone="100.43.64.0/19" --zone="141.8.128.0/18" --zone="178.154.128.0/19" --zone="178.154.160.0/19" --zone="199.21.96.0/22" --zone="199.36.240.0/22" --realm="realm-noc" --debug --dry-run

* MERGE zones as aggregates (from dynamic to static, e.g)

        // Merging 77.88.49.0/24 into file for static
        dns2-api zone merge --zone="77.88.49.0/24" --dry-run
        dns2-api zone merge --zone="77.88.50.0/24" --dry-run

        // Merging ip6 zone 1.0.8.b.6.0.2.0.a.2.ip6.arpa -> 2a02:6b8:100::/40
        dns2-api zone merge --zone="1.0.8.b.6.0.2.0.a.2.ip6.arpa" --dry-run

* ACL SYNC + ZONE CONFIGURATION 
        dns2-api acl sync --zone="172.24.0.0/13" --zone="10.208.0.0/12" --zone="213.180.192.0/19" --zone="5.45.192.0/18" --zone="5.255.192.0/18" --zone="37.9.64.0/18" --zone="37.140.128.0/18" --zone="45.87.132.0/22" --zone="77.88.0.0/18" --zone="87.250.224.0/19" --zone="93.158.128.0/18" --zone="95.108.128.0/17" --zone="100.43.64.0/19" --zone="141.8.128.0/18" --zone="178.154.128.0/19" --zone="178.154.160.0/19" --zone="199.21.96.0/22" --zone="199.36.240.0/22" --zone="2a02:6b8::/29" --zone="2620:10f:d000::/44" --acl="pattern://(.*)?wh.market.yandex.net" --realm="realm-warehouses" --debug --dry-run


* CONVERTING zone realm acl into namespace acl 

        // merging acl realm zone into namespace notation
        dns2-api acl merge --realm="realm-tanks" --debug --dry-run
        dns2-api acl merge --realm="realm-corpservices" --debug --dry-run

        // simplified form for acl sync (networks w.r.t acl are set from configuration)
        dns2-api acl sync --realm="realm-corpservices" --debug --dry-run
