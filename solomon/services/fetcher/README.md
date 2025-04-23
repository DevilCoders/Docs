### Project structure overview
- `api/` -- gRPC API specification. Corresponding implementation can be found in `lib/api` folder.
- `bin/` -- executable entry point and some code to wire things up on appliation startup in `bin/detail`. Also the HTTP API lives there in `bin/detail/http.cpp`
- `lib/` -- most of the application logic is located here
- `testlib/` -- mocks and other stuff that is reused in tests throughout the applicaction modules
- `ufetcher/` -- standalone binary that will fetch only a given set of URLs using the same logic main application uses. No dependencies on database, so can be used in tests
- `client/` -- client for fetcher gRPC API with very limited functionality. Is used only in tests
- `ut/` -- allows to run all project tests at once
- `config/` -- application config schema in protobuf format

##### `lib/` contents:
- `clients/` -- in fact only one actor-based client for c.y-t.ru
- `cluster/` -- extension of `solomon/libs/cpp/cluster_map`. Provides some info on current installation (datacenter, operation mode, the cluster map itself)
- `config_updater/` -- periodically reads tables for entities like projects, clusters, services and agents, and sends updates to subscribers. Also contains an actor that pulls shard locations from Coremon/Ingestor API
- `data_sink/` -- previously known as `coremon_sink` (hence some strange naming inside). Implements a wrapper around Coremon/Ingestor data processing APIs, request queueing, throttling and limits.
- `dns/` -- general DNS library has been moved to `solomon/libs/cpp/dns`, only the continiuous resolver actor lives here now. Basically this actor is a DNS cache with periodic refresh (~5 min for every hostname), which sends updates to interested parties on any record change
- `download/` -- actor-based wrapper around HTTP client
- `events.h` -- event slots
- `fetcher_shard/` -- implementation of a shard as it's used in fetcher. I.e. some settings like port, URL path, etc and a cluster interface which in turn can produce resolvers for host groups in a shard. Different implementations exist for classic Solomon shards (`TSimpleShard`) that consist of project, cluster and service, YASM agent shard and Solomon agent shard. *Limits for YASM and Solomon agent shards are currently hardcoded here*
- `fetcher_shard.h` -- common shard interface
- `host_groups/` -- implementation of different discovery methods 
- `host_list_cache/` -- cache for host groups that is stored in YDB. Currently unused. Probably can be dropped completely
- `id.h` -- composite IDs for entities like shard, services and shards
- `load_balancer/` -- contains code that interacts with `solomon/libs/cpp/coordination/load_balancer`. Basically it's an actor that subscribes for assignment updates from the load balancer actor at application startup. Theses assignments are later used to determine whether a URL should be fetched by this host. This type of balancing currently works only for agents
- `queue/` -- limited capacity queue class that is used in `data_sink` and `router`
- `racktables/` -- contains code that parses subnet tables we get from racktables so that we can match an IP address into a datacenter it belongs to
- `router` -- "knows" about the location of all Solomon shards in the processing cluster (Coremon/Ingestor), so after receiving a sample of data can route it to a proper send queue or put in a backlog if such shard is unknown/is not assigned anywhere. For an unknown shard also emits an event which currently results in the `CreateShard` call into Coremon/Ingestor API
- `shard_manager` -- manages shard actors (obviously) by creating new ones when a new shard config appears, killing actors that serve shards that have been gone and dispatching API requests to correct shard actors
- `sink` -- sink events and data types. Also contains a couple of test sink implementation (debug and devnull)
- `source_id` -- produces unique IDs for URLs within a shard so that Ingestor can properly aggregate metrics and calculate rates
- `tvm` -- wrapper around the TVM client. Holds tickets for known destination IDs and can request new ones
- `url` -- this is actually the _fetch_ part of the application. Contains an actor that issues an HTTP request to the specified URL with the specified interval. State and the logic on producing proper request, response parsing is implemented in non-actor class `TFetcherUrlBase` and its derivatives. Different implementations exist for simple URLs, agent multi-shard URLs and YASM agent URLs
- `yasm` -- YASM agent response parsing

##### Operation modes
`Local` -- fetch only URLs that are located in the same DC as the fetcher instance (configured in applicatino config)
`Global` -- fetch all URLs no matter what DC they are in
`LocalYasm` -- the same as `Local`, but fetch only YASM agent URLs


### HTTP API
`/shards/` -- show shards served by this host

`/shards/:shardStrId:` -- show information about a specific shard and list its URLs

`/urls/:url:?from_shard=:shardNumId:` -- show information about a specific url. Usually is accessed from a shard page

`/router/` -- dump router actor state, i.e. shard -> host mapping, known clients (Coremon/Ingestor) and backlog sizes

`/metrics/` -- dump fetcher metrics
POST `/logging/:component:/:level:/` -- allows to adjust logging level for a particular component on the fly

POST `/tracing/:shardId:` -- turn on verbose logging for a shard and all its URLs

DELETE `/tracing/:shardId:` -- turn off verbose logging for a shard and all its URLs

### Internals
Some charts:
[!Data flow chart] (https://jing.yandex-team.ru/files/msherbakov/data_flow.png)
[!Config flow chart] (https://jing.yandex-team.ru/files/msherbakov/conf_flow.png)

Photos from the meeting:
[!First] (https://jing.yandex-team.ru/files/msherbakov/photo_2020-02-07%2015.43.14.jpeg)
[!Second] (https://jing.yandex-team.ru/files/msherbakov/photo_2020-02-07%2015.43.29.jpeg)

##### Load balancing
Fetcher uses dead-simple load balancing implementation: leader of the cluster is elected by the acquisition of a distributed lock.
Leader is responsible for generating and sending assignments to other nodes. Assignment looks like several ranges within the ui64 space. All nodes then apply a hash function to URLs this way determining whether or not they whould handle this URL.

Nodes are connected via Interconnect and ping one another with some interval, so an unresponsive node is determined by an Interconnect disconnected/undelivered events, or by not responding to a few pings.
Pings can carry some additional info like machine load etc, but currently they are not. This is not an issue for URL balancing.

Code for load balancer, distributed lock over YDB and the related stuff is located in `solomon/libs/cpp/coordination`.

Application communicates with a load balancer actor by sending it a TEvSubscribe and then receiving back assignments when they change via TEvAssignments
