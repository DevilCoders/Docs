#
#
#

d2 -- is a control plane for dns configuration, monitoring and control. It 
controls clusters ns1+ns2, ns3+ns4, ns+dom0, ns-cache clusters, dns core [1],
dns guard control, see full command list and examples [2]. It collects and
sends graphics and monitoring states via solomon to [3] 

[1] https://st.yandex-team.ru/TRAFFIC-10736
[2] https://wiki.yandex-team.ru/dns/dnsguard/

* d2 core objects. Each d2 core node has objects methods to list current
  state of objects type: "zones", "robots", "userS", "groups". All these
  objects are used to make a master configuration and stored in zoo 
  cluster
 
         // Listing objects "zones" for "ns3+ns4" (dynamic)
         d2 master config objects --class="ns3+ns4" zones list --debug

         // Listing objects "robots", "users", "groups"
         d2 master config objects --class="ns3+ns4" robots list --debug
         d2 master config objects --class="ns3+ns4" users list --debug
         d2 master config objects --class="ns3+ns4" groups list --debug

* d2 master config update. A process to syncronize a configuration
  from master database and current files configurations. Should be 
  used (only) on active master?

         // Detecting configuration updates (w/o actually applying)
         d2 master config update --class="ns3+ns4" --dry-run
 
* d2 master managment (import). A process to get a snapshot from current
  master and import it to snapshot directory. A promote from passive master
  to active master could be done later from any snapshot imported.
 
         // Importing current master configuration+data tarball
         // from master of ns3+ns4 specfified directly cleaning
         // import file (could be treated as dry-run call)
         d2 master import --master="coldberry.yandex.ru" --class="ns3+ns4" --debug

         // Importing after detecting current active master
         d2 master import --class="ns3+ns4" --debug

         // Importing and making snapshot file
         d2 master import --master="coldberry.yandex.ru" --class="ns3+ns4" --snapshot --debug

         // All snapshots are stored as tarballs in /var/cache/snapshots
         2 13:23 1599042213499298160-69d7934b-c822-4749-a53f-b3ddd6766ec4.tar.gz
         2 12:51 1599040282829848758-b490e5ac-6da5-439d-a3df-7f132edc8e07.tar.gz
         2 12:21 1599038491450280770-2f8984c5-9e0d-4840-982e-70f33e66041f.tar.gz


* d2 master managment (promote). A process to make passive master be active master.
  It could be done from a snapshot or from current master (via snapshotting). 

        // Promoting a node (where command is executed) from passive
        // master to active. The following actions are executed:
        // (a) stopping bind
        // (b) installing data
        // (c) installing configuration, showing a diff
        // (d) starting bind
	snapshot="1599043584064969612-e1b0d1a9-e288-4a05-a236-a8cf87bc17f6.tar.gz"
        d2 master promote --class="ns3+ns4" --snapshot=$snapshot --debug


* d2 promote master tasks:

        (a) Makefile.nocvs + d2 slave config install. it is done on
            alpha-11i. Prerequsites (at each slave node)
            (1) (done) d2 deploy used for all nodes 
            (2) (done) Checking if all nodes are running on d2 last 
                       version or at least 08.08

                for all nodes per location: (ams)+(alpha)
            (3) (done) Makefile -> Makefile.nocvs
            (4) (done) Changing Makefile configuration in "coldberry"

            (5) (done) axfr/ixfr slaves + allow-notify() COLD -> CORE,
                might be some stranges as VS+RS(new) = COLD(legacy)

            (6) (done) Fixing Makefile on core nodes + alpha-30 to have control
                over each of them
   
            (7) (done) test case for dns-api-testing zone - to have
                (a) updates on core node (b) propagate updates 
                (c) checking data as resolving records (RR)

            (8) (done) switching API in zones/serial for monitoring to
                d2 native protocol https 6443: done for all except
                ns-infra, return to 80/tcp via nginx (socket leak)

            (9) (done) ns-cache d2 + ns-cache axfr/ixfr configuration 
  
                A question about possible allow-notify from
                several sources. Seems to be OK

                # coldberry (legacy)
                allow-notify: "2a02:6b8:0:1484::101"
                # dns-core01i.berry.yandex.net, dns-core01v.berry.yandex.net, dns-core01s.berry.yandex.net
                allow-notify: "2a02:6b8:c01:a5:0:433f:cc:11"
                allow-notify: "2a02:6b8:c0e:103:0:433f:cc:11"
                allow-notify: "2a02:6b8:c02:5f2:0:433f:cc:11"

            (A) (done) dns-core traefik v+s -> v stealths configuration, checking
                if only one node (active VLA) is capable to proxy all requests
                axfr/ixfr + updates.

            (B) making a call to promote command --last-snapshot, d2 calculates
                the last snapshot (by age) and promote from that file
                d2 master promote --class="ns3+ns4" --last-snapshot --debug

            (C) implement current generated d2 traefik config on
                dns-core to be sure that generated config is OK

            (D) checking NOTIFY passive/active master also produces notifyers 
                also-notify list is EMPTY for passive-masters

                Checking if we could use for outbound notifies
                IP address of IPV6 balancer to have this working.

            (E) implementing one more stage: activating also-nofity + 
                configuration origin (after promoting and reloading) via
                d2 ??... or could be set into promote stage (after reloading
                configuration on ACTIVE master). + A stage for PASSIVE master
                "demote" - disabling: SERVER_TYPE=PASSIVE-MASTER 
 
                TODO: logs via syslog for master transfer+update

            (F) d2 active-passive promotion algorithm and commands:
                
                0) selecting new active-master node (NAMN)
                   master="dns-core01s.berry.yandex.net"

                1) disabling VS L3 annonces:
                   d2.yaml: cluster.stealth-masters.stealth-masters: []

                   // (A) Per location commands
                   d2 slaves deploy --class="dns+core" --debug --location="vla"
                   d2 slaves deploy --class="dns+core" --debug --location="sas"
                   d2 slaves deploy --class="dns+core" --debug --location="man"

                   // (B) "All locations" command
                   [~] d2 slaves deploy --class="dns+core" --debug

                2) checking that all traefik level instances
                   have no request in processing logs
                   /var/log/traefik/traefik.log

                3) [d2] making a snapshot to choosen node [I]

                   // Importing and making snapshot file, possible
		   // errors of kind tmp-Ysd234fa from /etc/namedb/..

                   [~] d2 master import --master="coldberry.yandex.ru" --class="ns3+ns4" \
                          --snapshot --debug

                4) [d2] promoting master passive -> active
                   1.0 setting mode to PASSIVE (in any case) to eliminate
                       also-notify propagation upto 10-20 minutes
                   1.1 stop bind
                   1.2 installing the last snapshot, making configuration
                   1.3 restarting bind first time
                   1.4 start bind
                   1.5 making named-local.conf for ACTIVE mode
                   1.6 reloading bind
                       
                   [~] d2 master promote --class="ns3+ns4" --last-snapshot --debug
 
                5) [d2] switch traefik configuration via d2, first
                   run with dry-run, second w/o, for dns-core on each locally
       
                   [~] d2 master traefik --class="dns+core" --axfr --update
                         --master="$master" --debug [--dry-run]

                6) enabling VS L3 annonces:

                   # HEADSUP if master is unreachable bind back-off
                   # turns on for "10" minutes
 
	           d2.yaml: d2.yaml: cluster.dynamic.master: $master
                   d2.yaml: cluster.stealth-masters.stealth-masters: 
                            [ "dns-core01v.berry.yandex.net", "dns-core01s.berry.yandex.net" ]

                   // (B) "All locations" command "dns+core"
                   // actually L3 annonces online
                   d2 slaves deploy --class="dns+core" --debug

                   // (B)  "All locations" command "ns3+ns4"
                   // monitoring zones states
                   d2 slaves deploy --class="ns3+ns4" --debug

                   // (B)  "All locations" command "ns3+ns4"
                   // monitoring zones states
                   d2 slaves deploy --class="ns+cache" --debug

             (X) roll-back plan
                   
                   // switch L3 VS traefik back to coldberry.yandex.ru (force) 
                   [~] d2 master traefik --class="dns+core" --axfr --update --master="coldberry.yandex.ru" --debug

                   // switch L3 checks + monitoring
                   d2.yaml: d2.yaml: cluster.dynamic.master: "coldberry.yandex.ru"
                   d2.yaml: cluster.stealth-masters.stealth-masters:
                            [ "dns-core01v.berry.yandex.net", "dns-core01s.berry.yandex.net" ]
                  

             (L) прокачать изменения конфигурации в режиме: меняем через dns-mgmt.pl
                 смотрим что получается в dns-core via

                 // смотрим что получается на ACTIVE master, PASSIVE
                 // masters получат эти изменения как процесс promote
                 d2 master config update --class="ns3+ns4" --dry-run

             (F) algorithm version 2

                0) selecting new active-master node (ACTIVE)

                   master="dns-core01v.berry.yandex.net"

                1) disabling on dns-core nodes (on each from 3) updates

                   // for all nodes we need to turn off updates, for
                   // now on current ACTIVE master, first run --dry-run,
                   // second w/o [--dry-run]
                   [~] d2 master traefik --class="dns+core" --axfr \
                         --master="dns-core01v.berry.yandex.net" --debug

                   // checking if updates are turned off
                   // tail -f /var/log/named/named-dynamicupdates.log

                2) [d2] making a snapshot to choosen node [I]

                   // importing snapshot from current master and
                   // making a file snapshot (to promote later)
                   [~] d2 master import --master="dns-core01v.berry.yandex.net" \
                          --class="ns3+ns4" --snapshot --debug

                3) [d2] promoting master passive -> active
                   1.0 setting mode to PASSIVE (in any case) to eliminate
                       also-notify propagation upto 10-20 minutes
                   1.1 stop bind
                   1.2 installing the last snapshot, making configuration
                   1.3 restarting bind first time
                   1.4 start bind
                   1.5 making named-local.conf for ACTIVE mode
                   1.6 reloading bind

                   // on new master (or on all masters for backup)
                   [~] d2 master promote --class="ns3+ns4" --last-snapshot --debug

                4) [d2] switch traefik configuration via d2, first
                   run with dry-run, second w/o, for dns-core on 
                   each dns-core node [--dry-run]

                   # possible two phases - first only --axfr (just to
                   # switch transfers) second --axfr --update
                   [~] d2 master traefik --class="dns+core" --axfr --update \
                         --master="dns-core01v.berry.yandex.net" --debug

                5) enabling new ACTIVE master (for monitoring)

                   MAKE CHANGE in d2.yaml: 
                   d2.yaml: d2.yaml: cluster.dynamic.master: "dns-core01v.berry.yandex.net"

                   // (B) "All locations" command "dns+core"
                   // actually L3 annonces online
                   [~] d2 slaves deploy --class="dns+core" --debug

             (G) graphics for some actions on dns-core (bind) 
                 (traefik) + (updates)

             (K) making SAS -> VLA -> MAN -> SAS cyclic master
                 switching 
          -->
             (L) making F2 5 step to be done one each dns-core 
                 master server, now, it is possible only from
                 build-bionic-01i.cdn.yandex.net

             (H) delegation check in core servers uses coldberry+redberry
                 but should use current active masters?

             (Z) coldberry passive master is used also for (1) domain ownership
                 and monitoring (st+wiki) (2) static zones ip6/ip4 markup, so
                 we need at least from time to time syncronize either via
                 d2 config or (not tested yet) d2 snapshot + d2 promote

             (I) removing ns+infra class containers and all monitorings  

             (K) journal out of sync after snapshote promoting
                 06-Sep-2020 17:37:02.511 zoneload: zone beru.ru/IN/default: journal rollforward failed: journal out of sync with zone
                 06-Sep-2020 17:37:02.511 zoneload: zone beru.ru/IN/default: not loaded due to errors.
                 -rw-r--r-- 1 bind bind     3482 Aug 10 12:18 beru.ru
                 -rw-r--r-- 1 bind bind     8259 Jul 23 09:31 beru.ru.jnl

                 # possible if in active master there's no journal, but
                 # passive master has a journal (e.g. out of system edition via
                 # freeze sync thaw on active master

             (Y) some kind of garbage collecting: we need to
                 remove outdated files


* d2 deploy control plane

        // Checking versions of d2 installed
	d2 slaves deploy --class="ns3+ns4" --location="kiv" --dry-run --debug
 
        // Deploying d2 (with configuration) into host
        d2 slaves deploy --class="ns1+ns2" --host="dns01s.berry.yandex.net" --debug

        // Deploying d2 into location
        d2 slaves deploy --class="ns3+ns4" --location="ams" --debug

        // Deploying d2 info all nodes of class 
        d2 slaves deploy --class="ns3+ns4" --debug

* d2 traefik L3-underlayer balancer control

        // Enabling on specfic (locally run) core node traefik 
        // service for axfr and update balanced to master 
        // "dns-core01s.berry.yandex.net"
        d2 master traefik --class="dns+core"  --axfr --update --debug \
		 --master="dns-core01s.berry.yandex.net"

        // Dryrun commnd (just to show changes) to disable L3-underlayer 
        // traefik balancer. It shows a diff between configurations
        d2 master traefik --class="dns+core" --debug --dryrun \
		--master="dns-core01s.berry.yandex.net"


* d2 configurate levels
        // Level0 - configuration files (m4) defined core
        // configuration structures could be updated by, updates
        // Level0+Level1+Level2
        d2 master promote --class="ns3+ns4" --snapshot=$snapshot --debug 

        // Level1 - zone configuration files (could be created from
        // zoo configuration via (update only Level1)
        d2 master config update --class="ns3+ns4" --dry-run

        // Level2 - data files, see Level0

* d2 changing configuration:

        // (1) CONFIG -> ACTIVE

        // Changing via dns-mgmt.pl + dns-client.pl properties:
        // adding/deleting zones, modifying acl and groups, adding
        // robots, coldberry.

	// Updating groups adding users, changing acl(s)
        // (to update local definitions and zoo objects)
        // dns-core uses zoo database in CONFIG node
	[~] /opt/dns-api/cron.d/dns-mgmt-external.sh

        // Detecting and looking at changes with dry-run
        // to apply execute command without --dry-run on ACTIVE 
        // master node
        [~] d2 master config update --class="ns3+ns4" \
		--debug [--dry-run]

        // Remote update all nodes
        [~] cd /etc/namedb && make remote-update-all

        // (2) ACTIVE -> PASSIVE(s) configuration propagation is done
        // via snapshot+promote

* d2 rtc specfic
        // (0) - logrotation, container mgmt generates
        // "/var/run/d2/d2-mgmt-logrotate.conf" file
        // with right permissions and owner to process
        // command

        [~] sudo -u loadbase d2 rtc logrotate --file=/var/run/d2/d2-mgmt-logrotate.conf \
               --state=/var/run/d2/d2-mgmt-logrotate.state \
               --debug --log=stdout


        // (1) updating rtc configuration
        [~] d2 rtc master config update --debug --dry-run
		[--cluster="rtc+dnscache" --location="sas"]

        // (2) monitoring rtc configuration
        [~] d2 monitor run --juggler d2-dns-rtc-config --debug

* d2 metrics
        //  gathering and sending metrics for unbound
        [~] d2 metrics send --class="unbound" --debug 

* d2 slave l3 checks

	// disabling slaves l3 nodes (as http
        // check by default) 
        [~] d2 slaves l3 disable --debug

        [~] d2 slaves l3 enable --debug

        // disabling http and tcp checks from
        // console command line (as command)
        [~] d2 slaves l3 disable --debug -http --tcp --console

	// disabling http and tcp from api call
        // please note that d2 is run under loadbase
        // user in rtc (need some permissions)
        [~] d2 slaves l3 disable --debug -http --tcp

        // all tcp and http configuration are set
        // in configuration file

* d2/l2 communications via api call
        [~] d2 slaves enable --debug --host="$host"
        [~] d2 slaves disable --debug

* d2/l2 host inforation via api call
        [~] d2 slaves info --debug --host="$host"

TODO:
* d2 zone management blocks:

* dns2-api zones managment
        // Creating zone configuration for fronted cluster
        // with a given backend selection. One zone could
        // exist in a number of configurations:
        // frontents: ns1+ns2, ns3+ns4, ns+yp, ns+cache?
        // backends: ns3+ns4, ns+yp.

        // all commands to create/edit/delete meta zones
        // should be executed via dns2-api command line
        // (or corresponding api calls)

        // I. Creating meta configuration for ns+yp zone
        // with activated on ns+cache, here we use this
        // zone as auth on ns1+yp, ns2+yp and as cache
        // on ns+cache

        [~] dns2-api meta create --backends "ns+yp" --frontends "ns+yp" \
               --frontends "ns+cache" --activated "ns+cache" \
               --name "test.qloud-d.yandex.net"

* d2 zone control plane configuration
        // Updating configuration  and making snapshots
        // to push it later on nodes (snapshot has all data
        // for all types of nodes. Each node of each type
        // knows itself which files are used to check
        // its state and updates

        [~] d2 master config update --class="ns3+ns4" --debug --dry-run

* d2 zone control slaves configuration update
        // Replicate bind, unbound and others files
        // to slave configurations to update
        // their config

        [~] d2 slaves config apply --debug --host="alpha-05i.lxd.tt.yandex.net"

* d2 scheduled configuration. we need some process to update
  configurations w.r.t snapshots recevied. Also as masters are switched 
  we need snaphots also be updated
        // Update on host configurations (if need) as schedule 
        // configured, including --now flag and --force to
        // update node even schedule is not turned on

        [~] d2 slaves schedule --debug --dry-run \
                  --now [--force]

TODO: -->
	alpha-05i.lxd:/etc/unbound# d2 slaves config apply --debug --dry-run --master=alpha-30i.lxd.tt.yandex.net --force

* d2 ns1+ns2 migration plan

        // getting last snaphot
	d2 master import --master="dns-core02s.berry.yandex.net" --class="ns1+ns2" --snapshot --debug

        // promote node to master
        d2 master promote --class="ns1+ns2" --last-snapshot --debug

        // set traefik to new ACTIVE-MASTER
        d2 master traefik --class="dns+core" --axfr --update --master="dns-core02v.berry.yandex.net" --debug --dry-run

        // changing master to /etc/d2/d2.yaml for static 
        // dns-core02s.berry.yandex.net -> dns-core02v.berry.yandex.net
        // and restarting d2
        systemctl restart d2

* d2 master zones configration showing the current sitation w.r.t to 
        (1) dynamic zones, (2) meta, (3) yp module

	// showing zones meta configuration plan for
        // zones that should be migrated 
	d2 master config plan --debug \
            --zones=reverse|direct|all*)
            --migration

* d2 master transfer zone (as a part of zone aggregation)

	// transferring zone and put data into zone corresponding to
        // cidr/arpa supplied as value for zone
	d2 master zone transfer --zone="77.88.49.0/24" --class="ns1+ns2" --debug --dry-run

* d2 master check zone content on slaves via native transfer methods, e.g.
  d2 master is on dns+core Z master and slave on unbound+YP replica as Y 
  
        // master version comparing zones slaves content for zones specified
        d2 slaves zone diff --zone="mail.yandex.kz" --debug --class="ns+cache" --location="alpha"

        // slave versioh of command
        d2 slaves zone diff --debug --zone='market.yandex.com'
