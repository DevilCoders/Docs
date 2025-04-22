#
#
#

hx -- is a system to collect the following network and compute objects:
(a) prefixes (b) metrics. Prefixes are grouped by links/locations, metrics
are properties of links and containers (or dom0 hosts).

* hx keepalive subsystem. Containers fqdns (themselves of its interfaces) are
  managed conductor and organized in C-groups, e.g.

         // container strm-ufa01.strm.yandex.net belongs to
         // C-group: strm-stream-ufa. 
         strm-ufa01.strm.yandex.net

         // there is a strm-lost group that contains all
         // containers fqdns that are out of processing

  hx keepalive subsystem (hxss) is controlling if container/fqdn is alive
  and syncing this state with C-group. If ALIVE -> container fqdn should
  be in "strm-steam-$location" group, if DEAD -> container should be placed
  in "strm-lost". Periodically hx start keepalive check, it also could
  be run as:

         // Running keepalive check from command line (a)
         hx mgmt keepalive check --debug --dry-run (?)

         // Syncing current state with C-groups in dry-run
         // mode (such no any actions are taken, just
         // generated)
         hx mgmt keepalive sync --debug --dry-run (?)

   algorithm: each node from its own interval start check (a) and push
   results in global store (specfied by node fqdn). Please note that
   for some reason there could be no connectivity at all so all checks
   from one (spoil) node could mark all fqdns as "dead". Periodically,
   keepalive sync process is started - it fetches results and checks
   qorum and age of check - we need some anti-flap here.

* hx nodes are started in dry-run mode, they just calculate possible
  actions, log them and monitor them as

         // monrun -r core-mgmt-keepalive
         core-mgmt-keepalive: hosts:'true' c-groups:[9] hosts:[1088]
       
         // possible 2 flapping nodes are dom0 hosts of hx nodes  
         quorums:['UNKNOWN':'2','DOWN':'111','UP':'967']

         // actions generated
         actions:['up':'0','down':'1']

* hx keepalive processing (1) watching graphics, it some actions are
  generated, run

         // running in dry-run mode first in rdr01h or rdr01v
         hx mgmt keepalive sync --debug --dry-run 

         // running in force mode to apply actions
         hx mgmt keepalive sync --debug --force

* hx приложение имеет client-id: 72ac728602ee443aa1a7d61618b7515c

          // Получить токен для hx api
          https://oauth.yandex-team.ru/authorize?response_type=token&client_id=72ac728602ee443aa1a7d61618b7515c

* hx client connections should be also exported outside, we
  also have legacy overrides?

         (a) adding authorization OAUTH for current methods
             or for one more explicelty exported 
         (b) nginx configuration should allow PUT/POST
             methods for authorized methods

          // GET an object by :id, here could be
          // linkid, uniqid
	  GET /api/v4.0/connections
	  GET /api/v4.0/connections/:id
 
          {
          "connections": [
                {
                        "id": "fe268fd5-4bbc-4690-86b5-657b966f696a",
                        "link": "nnv1-rp1@vlan991",
                        "downstreams": [],
                        "upstreams": [],
                        "speed": 10000,
                        "load": 100,
                        "load_timestamp": "2020-05-06T20:49:39.463458958+03:00",
                        "enabled": true
                }
             ]
          }

          // http call request
          hx client connections list --json --debug  --http \
		--token="012345678012345678" \
		--id="fe268fd5-4bbc-4690-86b5-657b966f696a"

          // unix socket call request
          hx client connections list --json --debug \
                --id="fe268fd5-4bbc-4690-86b5-657b966f696a"

          (A) "id" could be one of several types:
              a) connection id as uuid: "fe268fd5-4bbc-4690-86b5-657b966f696a"
                 url:'https://rdr.alpha.tt.yandex.net/api/v4.0/connections/fe268fd5-4bbc-4690-86b5-657b966f696a
              b) link id as int: "1508"
                 url:'https://rdr.alpha.tt.yandex.net/api/v4.0/connections/1508
              c) link name: "jansson@et-2/0/5.0" (path encoded)
                 --id="marionetka@xe-11%2F1%2F2.0"
                 https://rdr.alpha.tt.yandex.net/api/v4.0/connections/marionetka@xe-11%252F1%252F2.0'

          // PUT a value for a list of attributes, connection object 
          PUT /api/v4.0/connections/:id

          (B) hx client connections attributes set --debug \
		 --id="marionetka@xe-11/1/2.0" --http \
                 --token="012345678012345678" \
		 --load=100 --speed=10000

          // DELETE an attribute for connection object
          DELETE /api/v4.0/connections/:id/attribute/:name

          (C) hx client connections attributes delete --debug \
                 --id="smr1-rp1@vlan991" --http \
                 --token="012345678012345678" \
                 --speed

          // PUT for exist connection, if a connection object
          // does not exist, PUT is transformed to POST (create) 
          // if connections requested to DELETE checking empty it or
          // not, if empty -> deleting the whole connection not only
          // attributes
          
           (F) checking load for different classes of links

* setting load to a link
         (1) current state of overrides:
             [~] hx client connections list --json --debug --http \
                    --endpoint="https://rdr.alpha.tt.yandex.net" \
                    --id="m9mts@m9mts"

	"connections": [
		{
			"id": "8303c3ab-8fb0-469f-9fb9-1f89d71d05ee",
			"link": "m9mts@m9mts",
			"downstreams": [
				"m9-s115a@Eth-Trunk0/TX",
				"m9-s7@Eth-Trunk17/TX"
			],
			"upstreams": [
				"m9-s7@Eth-Trunk0/RX"
			],
			"load": 100,
			"load_timestamp": "2020-09-22T15:13:57.999926355+03:00",
			"enabled": true
		}

          (2) deleting a "load" override
              [~] hx client connections attributes delete --debug --http \
                     --endpoint="https://rdr.tt.yandex.net" \
                     --id="m9mts@m9mts" \
                     --load

          (3) setting a "load" override
              [~] hx client connections attributes set --debug --http \
                     --endpoint="https://rdr.tt.yandex.net" \
                     --id="m9mts@m9mts" \
                     --load=100
[1] https://wiki.yandex-team.ru/tt/hx/#linksconnections

* some more monitoring to establish hx-attributes, see [1]
         (1) validating servers metrics speed values
             [~] hx monitor-metrics run --juggler \
                    hx-core-attributes --debug

         (1) core-attributes = core-attributes: servers: speed: ['1056']/['0'] OK
         [1] https://st.yandex-team.ru/TRAFFIC-11056

* tvm monitoring
         (1) monitoring if all requested tvm tickets are avialble via tvm daemon
             [~] hx monitor-metrics run --juggler \
                    hx-core-tvm-servicetickets  --debug

* auth mech:
        (0) default files keys locations
           alpha-20i.lxd:/etc/hx# l
            -rw-r--r--   1 root root   377 Oct  5 10:55 .hx.serviceticket
            -rw-r--r--   1 root root   666 Oct  5 10:47 .hx.sessionid
            -rw-r--r--   1 root root    33 Oct  5 10:43 .hx.sharedkey
            -rw-r--r--   1 root root    40 Oct  5 10:45 .hx.token
            -rw-r--r--   1 root root  9481 Oct  4 14:42 hx.yaml

        # for user-ticket/service-ticket we need enable
        # tvm for oauth in configuration
        (1) oauth token:
            hx client connections list --json --debug --http \
               --id="c392f854-2e66-4b58-909c-65182f3c18d6"

        (2) shared-key:
	    hx client connections list --json --debug --http \
               --id="c392f854-2e66-4b58-909c-65182f3c18d6" \
               --auth="shared-key"

        (3) user-ticket:
            # user-tickets could be obtained by oauth method
            # it internally receives user-ticket (could be found
            # in log), user-ticket lives 5 minutes
            hx client connections list --json --debug --http \
               --id="c392f854-2e66-4b58-909c-65182f3c18d6" -Z \
               --auth="user-ticket"

        (4) oauth + service-ticket:
            hx client connections list --json --debug --http \
               --id="c392f854-2e66-4b58-909c-65182f3c18d6" -Z

        (5) session-id
            hx client connections list --json --debug --http \
               --id="c392f854-2e66-4b58-909c-65182f3c18d6" \
               --auth="session-id"

* adding one more property for connection: "available locations" [1]
       
	(1) установить available locations для id=1007 в значения "mskm9 mskstoredata"
            hx client connections attributes set --debug --http \
                     --endpoint="https://rdr.tt.yandex.net" \
                     --al="mskm9 mskstoredata" \
                     --id="1007"

        (2) посмотреть что получилось
            hx client connections list --debug --http \
                     --endpoint="https://rdr.tt.yandex.net" \
                     --id="1007"

		{
			"id": "b4a3ae90-c18a-4892-aa53-bff452348707",
			"link": "norilsk@norilsk",
			"speed": 3000,
			"load": 1,
			"load_timestamp": "2020-10-05T12:58:31.864205973+03:00",
			"enabled": true,
			"available-locations": [
				"mskm9",
				"mskstoredata"
			]
		}
         (3) удалить значения атрибута available locations:
            hx client connections attributes delete --debug --http \
                     --endpoint="https://rdr.tt.yandex.net" \
                     --id="1007" --al
 
        [1] https://st.yandex-team.ru/TRAFFIC-11001

* adding "drain" property for connection: "drain" "false/true", not defines [1]
        (1) установить drain в значение "true"/"false"

            hx client connections attributes set --debug --http \
                     --endpoint="https://rdr.tt.yandex.net" \
                     --drain="true" --id="1007"

            hx client connections attributes set --debug --http \
                     --endpoint="https://rdr.tt.yandex.net" \
                     --drain="false" --id="1007"

        (2) посмотреть что получилось
            hx client connections list --debug --http \
                     --endpoint="https://rdr.alpha.tt.yandex.net" \
                     --id="1007"

        (3) удалить значения атрибута drain:
            hx client connections attributes delete --debug --http \
                     --endpoint="https://rdr.tt.yandex.net" \
                     --id="1007" --drain

        [1] https://st.yandex-team.ru/TRAFFIC-11325


* monitoring hx links configuration [2]:

  (1) if link with the same Id has different configuration in HX and PEERS-REPORT
  (2) if link has routed=false and exist in PEERS-REPORT
      and prefixes in hx RIB more than 0 

  [2] https://st.yandex-team.ru/TRAFFIC-11231
         (1) validating hx links configuration
             [~] hx monitor-metrics run --juggler \
                    hx-core-links-configuration --debug
