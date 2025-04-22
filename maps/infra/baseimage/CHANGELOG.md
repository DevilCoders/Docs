# Base image changelog
* * * * *
maps/core-base-trusty:8409768 | maps/core-base-bionic:8409768:

**r8409768** @khrolenko GEOINFRA-2652 fix nginx header name

* * * * *
maps/core-base-trusty:8402020 | maps/core-base-bionic:8402020:

**r8402020** @khrolenko GEOINFRA-2652 pass nginx $msec to yacare

**r8387131** @kmkolganov GEOINFRA-2710: allow to set logger params for push-client config in base image

**r8383603** @hattonuri Created external ping metric

**r8379640** @hattonuri Removed initializer

**r8349744** @hattonuri Improved lock place

**r8333721** @ar7is7 Move backtrace parsing to separate function

**r8333013** @hattonuri Remove .message that didn't exist

**r8324064** @vmazaev Yacare cleanup outdated junk

**r8315892** @khrolenko actualize readme

**r8276460** @alexey-savin yacare: canonical test for template_generator config

**r8276270** @hattonuri Removed status() from worker

**r8275257** @khrolenko CAPTCHA-2044 log X-Antirobot-Suspiciousness-Y for Geo

**r8273716** @nikitonsky Fix ecstatic worker tests

**r8273179** @alexey-savin yacare: fix ratelimiter auto-enabling in service docker configuration (via  template_generator)

**r8273104** @sobols [maps/common] Remove the use of boost::lexical_cast from exception.h

**r8269705** @alexey-savin yacare+quotateka: deliver service endpoints to the agent/access handle

**r8268699** @sobols [maps/common] Remove boost_test.h, migrate to BOOSTTEST_WITH_MAIN() macro

**r8267539** @khrolenko remove postinst and prerm support from environment_linker

* * * * *
maps/core-base-trusty:8256938 | maps/core-base-bionic:8256938:

**r8253324** @alexey-savin maps lua modules: use luajit2.1 instead of luajit2.0

**r8244181** @alexbobkov Change ecstatic error type to EcstaticError and add dataset URL MAPSGARDEN-20472

**r8229129** @hattonuri Create deadline for request

* * * * *
maps/core-base-trusty:8225711 | maps/core-base-bionic:8225711:

**r8225711** @nikitonsky Rm legacy symlink creation from baseimage

**r8225474** @nikitonsky Rm legacy detach_all symlink usages

**r8201255** @hattonuri Changed std::regex to re2

* * * * *
maps/core-base-trusty:8199753 | maps/core-base-bionic:8199753:

**r8199753** @khrolenko fix postbuild test

**r8199640** @khrolenko remove legacy push-cilent protocol support

**r8199418** @nikitonsky Move is_host_detached from pylibs/infrastructure_api to pylibs/utils

**r8195157** @gleb-kov IGNIETFERRO-1522 merge demangle.h and type_name.h into system/type_name.h

**r8180347** @alexey-savin yacare: dynamic quotateka resource with lua script

**r8176952** @unril Add [[maybe_unused]] to YCR_OPTIONS

**r8168749** @khrolenko python util to check if host is detached by ITS

**r8167974** @hattonuri Added thread pools count and size of listenFD backlog to config

**r8166328** @nikitonsky Rm boost::optional from maps/infra

**r8126010** @hattonuri Fixed thread_pool.h bug with universal references

**r8119504** @vmazaev Yacare process runner: fix process logging

**r8104290** @jemdo add metrics with generated names

**r8094040** @v-korovin DEVTOOLS-8344 Migration for maps

* * * * *
maps/core-base-trusty:8069555 | maps/core-base-bionic:8069555:

**r8069555** @alexey-savin quotateka-agent: allow use of default quota without project (by tvm)

**r8068326** @vmazaev Roquefort: add external metric

**r8066114** @vmazaev yacare-ctl: more logs

**r8063339** @mkrutyakov Change std::stoll to std::stoull in userId fetching method

* * * * *
maps/core-base-trusty:8061634 | maps/core-base-bionic:8061634:

**r8061634** @alexey-savin base image: update tvmtool to 1.3.7

**r8057846** @alexey-savin ratelimiter: fix v2 agent garbage collection

**r8051115** @alexey-savin quotateka: agent metrics for inventory_version and number of ratelimiter counters

* * * * *
maps/core-base-trusty:8049471 | maps/core-base-bionic:8049471:

**r8049471** @nikitonsky ecsttc worker: configure min work time

**r8045636** @alexey-savin ratelimiter: refactor number_of_counters metrics without YCR_CREATE_METRIC

**r8044231** @vmazaev quotateka: plugin dry run & tests

**r8043759** @k-tesker Mrc: add allowed user groups to ugc (MAPSMRC-2199)

**r8041575** @vmazaev ratelimiter: fix pkg.json

**r8041384** @nikitonsky Remove cpdef from ymtorrent

**r8040904** @alexey-savin quotateka+ratelimiter: agent monitorings

**r8037009** @alexey-savin ratelimiter v2: fix agent counters/limits serialization to proto

**r8035329** @vmazaev quotateka: fix integration with yacare

**r8029286** @imseleznev add logging of ja-3 header GEOINFRA-2530

**r7999325** @alexey-savin ratelimiter v2: agent shard id generation

**r7999098** @alexey-savin ratelimiter v2: exception type for limit params validation fails

**r7994526** @alexey-savin ratelimiter: v2 agent

**r7989981** @vmazaev quotateka agent: many fixies

**r7989953** @alexey-savin ratelimiter: fix limits load on start

**r7986853** @nikitonsky ycr: faster ping while detached

**r7982623** @alexey-savin ratelimiter: v2 access limiter

**r7981272** @khrolenko GEOINFRA-2370 quotateka rps/quota metrics

**r7964036** @gotocoding [maps/libs/common] common_math.h -> math.h

**r7959631** @gotocoding [maps/*] [maps/libs/common] Use new correct header for `exception.h` in `maps/*`, review num. 12

**r7957414** @alexey-savin ratelimiter: LimitsCacheUpdater semantics

**r7954985** @alexey-savin ratelimiter: move yacare handles out of core library

**r7954449** @alexey-savin ratelimiter: delete SortedMap::erase methods for single entry

* * * * *
maps/core-base-trusty:7952664 | maps/core-base-bionic:7952664:

**r7952664** @axxeny Base image: Automatically set PUSH_CLIENT_TVM_SECRET if it is not set, but TVM_SECRET is. GEOINFRA-2558 GEOINFRA-2433

**r7952579** @khrolenko fix msan test

**r7950312** @ponomarev NMAPS-13269 added Request::getClientPort()

**r7948310** @alexey-savin yacare: fixed one more race on servant stop

**r7945697** @alexey-savin ratelimiter: Limit spaceship operator checks generation first

**r7942847** @alexey-savin ratelimiter: v2 limits & generations aggregation from multimaster response

**r7942612** @vmazaev CROWDFUNDING-3: fix parameters passing after click update

**r7942279** @neksard CROWDFUNDING-3 Update click from 6.7 to 7.1.2

**r7940990** @gotocoding `maps/libs/common`, move some headers out of `yandex/maps/common/`, review num. 2

**r7940670** @gotocoding `maps/libs/common`, move some headers out of `yandex/maps/common/`, review num. 1

**r7938589** @alexey-savin ratelimiter: improve convertLimits() semantics with pointer parameter

**r7933983** @vmazaev qttk: integration with yacare

**r7930155** @alexey-savin ratelimiter: v2 generations p2p

**r7924381** @nikitonsky Write upload error json in ecstatic tool

* * * * *
maps/core-base-trusty:7921791 | maps/core-base-bionic:7921791:

**r7921791** @alexey-savin ratelimiter: V2 generations draft

**r7921621** @vmazaev ycr: fix build after bad merge

**r7921594** @vmazaev ycr: fix nginx include

**r7921474** @vmazaev ycr: add exclude_ping_from_nginx option

**r7921329** @vmazaev ycr: use service requests for /stat & exclude /yacare/* from nginx

**r7921283** @nikitonsky ecsttc: Add locks test && bugfix

**r7913748** @vmazaev baseimage: split 01_infra.sh

**r7913246** @nikitonsky Bugfix experimental worker tests

**r7913017** @vmazaev ycr: remove legacy stats

**r7910240** @nikitonsky Fix NoDeployListsException

**r7910162** @nikitonsky Fix not awaiting lock.release()

**r7910059** @vmazaev ycr: fix build

**r7909923** @vmazaev ycr: remove separate alerts checking binary

**r7909912** @nikitonsky Ecsttc worker: init async managers

* * * * *
maps/core-base-trusty:7909416 | maps/core-base-bionic:7909416:

**r7909416** @vmazaev ycr: force yacare-light in make_configs

**r7908114** @khrolenko GEOINFRA-2500 GEOINFRA-2516 keep permissions when linking logs volume and link push-client state to logs persistent volume

**r7905692** @vmazaev ycr: no more heavy

**r7902942** @imseleznev use by default X_FORWARDED_FOR_Y for ip detection GEOINFRA-2097

**r7897762** @chikunov maps-yacare: add nginx server config for default vhost GEOINFRA-845

**r7886607** @muzykantov yacare: fix LimitRate::authTypes documentation comment

**r7863268** @muzykantov yacare: add Response::setHeader(pair)

**r7860274** @shalyga Better ratelimiter logic

**r7858029** @imseleznev GEOINFRA-2401 add predicate for being detached by ITS & make predicates public. Do not CRIT in ratelimiter-proxy if detached by ITS

* * * * *
maps/core-base-trusty:7847239 | maps/core-base-bionic:7847239:

**r7847239** @nikitonsky Kill hooks with sudo in worker

**r7847220** @khrolenko enable stable debian repo only (bionic fix)

**r7846881** @vmazaev yacare-ctl: copy logs to syslog

**r7846759** @ponomarev NMAPS-13060 reusing BlackboxAPI in yacare app

**r7833805** @nikitonsky Decrease min_announce_interval from 5 minutes to 1

**r7825756** @nikitonsky ecsttc worker: make hook_contoller async

**r7823453** @alexey-savin ratelimiter: separate proto messages for V2 protocol

**r7817722** @alexey-savin ratelimiter: V2 protocol counters new data structure

* * * * *
maps/core-base-trusty:7788225 | maps/core-base-bionic:7788225:

**r7788225** @nikitonsky Add DeduceTeasetResource tasklet

**r7783935** @muzykantov staticapi: add api_key, add signature validation MAPSPRINTER-86

**r7780272** @vmazaev Yacare ctl: force flush after every line

**r7773445** @alexey-savin ratelimiter: separate limits updater from jobs engine

**r7770587** @alexey-savin ratelimiter: move upstreams discovery from proxy/bin into the core lib

**r7769518** @khrolenko package build fix

**r7767925** @khrolenko GEOINFRA-1408 capture stderr in juggler_check_wrapper

**r7763156** @khrolenko migrate from ticket_parser2 to tvmauth

**r7762304** @alexey-savin ratelimiter: moved metrics generators and sync timestamps into Core/CoreNova

**r7757360** @alexey-savin yacare: maybeUserId param supresses 403 on failed scopes validation

* * * * *
maps/core-base-trusty:7744262 | maps/core-base-bionic:7744262:

**r7744262** @nikitonsky Fix ecsttc worker preserved data

**r7741395** @khrolenko run push-client under statbox user

**r7741392** @khrolenko log local hostname

**r7726962** @alexey-savin ratelimiter: renamed agent -> plugin

**r7712366** @nikitonsky Add ecsttk tool docs

**r7708825** @vmazaev Yacare nginx config tests: disable sanitizers

**r7676196** @shalyga Introduce v2/matrix handler

**r7672268** @alexey-savin auth_agent:  use yacare builtin auth  instead of copy-pasted code

**r7665934** @cerevra [tvmauth/cpp] Rename ticket_parser2 (PASSP-30788)

**r7665744** @cerevra [ticket_parser2/cpp] Renaming: status.h -> ticket_status.h (PASSP-30788)

**r7664870** @cerevra [tvmauth/cpp] Renaming: TUserTicket -> TCheckedUserTicket. Part1 (PASSP-30788)

**r7662308** @cerevra [tvmauth/cpp] Renaming: EStatus -> ETicketStatus. Part 1 (PASSP-30788)

* * * * *
maps/core-base-trusty:7661836 | maps/core-base-bionic:7661836:

**r7661836** @cerevra [ticket_parser2/cpp] Renaming: NTicketParser2 -> NTvmAuth (PASSP-30788)

**r7659884** @alexey-savin ratelimiter: v2 peers sync monitoring on server

**r7657509** @alexey-savin ratelimiter: v2 protocol server side (handles and jobs)

**r7657233** @nikitonsky Generate changelog in sandbox

**r7656055** @khrolenko get back forgotten methods in ecstatic client

**r7643518** @robot-maps-sandbox Update base image version: stable to 7640337

* * * * *
maps/core-base-trusty:7640337 | maps/core-base-bionic:7640337 (Release V34.1):

**r7640337** @alexey-savin ratelimiter: refactoring before V2 handles implementation

**r7639281** @nikitonsky Remove custom datatesting environment logic from baseimage

* * * * *
maps/core-base-trusty:7613926 | maps/core-base-bionic:7613926 (Release V32.1):

**r7613926** @khrolenko GEOINFRA-2425 ecstatic upload inactivity limit

**r7613895** @khrolenko add ending slashes to destination dir path

**r7613648** @khrolenko GEOINFRA-2432 recommended push-client checks

* * * * *
maps/core-base-trusty:7580788 | maps/core-base-bionic:7580788 (Release V30.1):

**r7580788** @khrolenko more robust push-client tvm id check

**r7579334** @nikitonsky Ignore tcp ping in agent under flag

**r7551614** @vmazaev Yacare: fix quoting regexp for yasm signal names

**r7543948** @nikitonsky Add ecstatic integration tests

**r7540354** @khrolenko GEOINFRA-2396 tracker events logging

**r7535980** @prettyboy [pytest/plugins/ya] Mark test as failed if it uses fork() without os._exit()

**r7525167** @vmazaev Yacare: YCR_NGINX_INCLUDE -> YCR_NGINX_LOCATION

**r7522980** @alexey-savin ratelimiter: v2 protocol server side (limit encoded into resource_id)

**r7520877** @robot-maps-sandbox Update base image version: stable to 7490807

* * * * *
maps/core-base-trusty:7490807 | maps/core-base-bionic:7490807 (Release V29.1):

**r7490196** @khrolenko fix bracket

**r7490064** @khrolenko nginx-depent push-client configs

**r7488227** @vmazaev Pycare: enable metrics

* * * * *
maps/core-base-trusty:7476588 | maps/core-base-bionic:7476588 (Release V27.1):

**r7476588** @khrolenko GEOINFRA-2377 RestrictToLocal for /yasm_stats with baseimage check

**r7473493** @khrolenko make bash as default shell for bionic

* * * * *
maps/core-base-trusty:7415115 | maps/core-base-bionic:7415115 (Release V22.1):

**r7414211** @nikitonsky Add datatesting{prestable,validation} to baseimage

**r7413997** @nikitonsky Return 100 from ecstataic_api when data already uploaded

**r7413045** @robot-maps-sandbox Update base image version: stable to 7369614

**r7409277** @svidyuk Enable GO_PROTO by default

**r7406442** @nikitonsky Remove tar from worker

* * * * *
maps/core-base-trusty:7369614 | maps/core-base-bionic:7369614 (Release V21.1):

**r7364034** @nikitonsky Fix ecstatic download deadlock

**r7362648** @imseleznev add x_source_port_y logging GEOINFRA-2257

**r7360861** @imseleznev if detached by ITS do not CRIT for tvmtool check  GEOINFRA-2169

**r7360718** @alexey-savin tvmtool-health-check CRIT threshold is 1 host

**r7360669** @nikitonsky Move ecstatic & garden to py3-only

**r7360229** @nikitonsky Log not avaliable required datasets in baseimage

* * * * *
maps/core-base-trusty:7327547 | maps/core-base-bionic:7327547 (Release V17.1):

**r7327547** @nikitonsky Poll avaliable switches in worker

**r7324943** @khrolenko update changelog

**r7319290** @khrolenko GEOINFRA-1410: skip removed datasets when download

**r7318309** @imseleznev bugfix metric collector

* * * * *
maps/core-base-trusty:7210239 | maps/core-base-bionic:7210239 (Release V15.1):

**r7208009** @vmazaev Yacare: fix vhost regexp

**r7207815** @nikitonsky Refactor ecstatic tool

**r7180376** @thegeorg Remove some proxies for google/protobuf/*.h

**r7177662** @vmazaev Baseimage: do not symlink detach_all to ~/controls in development

**r7169528** @imseleznev update warn for base_image_revision monitoring

**r7164973** @robot-maps-sandbox Update base image version: stable to 7160262

* * * * *
maps/core-base-trusty:7160262 | maps/core-base-bionic:7160262 (Release V14.1):

**r7160262** @nikitonsky Suspend ecstatic-client before stopping yacare app

**r7158980** @nikitonsky Add suspend mode to ecstatic-agent

**r7155675** @nikitonsky Retry get requests in ecstatic coordinator

**r7153473** @nikitonsky Run worker/ymtorrent from agent without a subshell

**r7152989** @nikitonsky Remove unneeded log

**r7150200** @alexey-savin yacare: avoid exception for optional user when no credentials in the request

**r7147584** @alexey-savin yacare: legalize explicit 0 weight for ratelimiter

**r7143312** @alexey-savin Adjusted ratelimiter chapter in yacare/readme

**r7142424** @vmazaev Yacare vhost regexp: remove qloud support

**r7140526** @vmazaev Yacare: clean up vhost regexp

**r7139468** @nikitonsky Update unstable coordinator fqdn

**r7139165** @nikitonsky Add retries on read errors in ecstatic lib

**r7139153** @nikitonsky Rerun hook using ecstatic user

**r7136966** @alexey-savin yacare: readme markup adjusted

**r7130214** @robot-maps-sandbox Update base image version: stable to 7120231

**r7130042** @alexey-savin yacare: throw away ratelimiter weights for params feature

**r7121217** @quoter fix several YCR_NGINX_INCLUDEs

* * * * *
maps/core-base-trusty:7120231 | maps/core-base-bionic:7120231 (Release V13.1):

**r7120231** @alexey-savin yacare: dynamic ratelimiter params with lua script

**r7115677** @nikitonsky Configure roquefort totals

**r7104811** @alexey-savin ratelimiter: billion in the constant for limit not found

**r7099200** @vmazaev Roquefort: better error message

**r7089420** @robot-maps-sandbox Update base image version: stable to 7088877

* * * * *
maps/core-base-trusty:7088877 | maps/core-base-bionic:7088877 (Release V12.1):

**r7088877** @nikitonsky Fix ecstatic in unstable environment

**r7088580** @nikitonsky Remove ecstatic config files from baseimage

**r7081724** @alexey-savin Remove custom MDB alerts overrides for ratelimiter & coordinator

**r7069208** @robot-maps-sandbox Update base image version: stable to 7040096, prestable to 7040096

**r7069129** @imseleznev release baseimage 7040096

**r7068892** @nikitonsky Use tvm in stable backups

**r7068228** @nikitonsky Ecstatic reconfigurer r6980172 in stable

**r7050961** @nikitonsky Release ecstatic tool to package and sandbox

**r7040096** @imseleznev bugfix ln to ITS flag files

**r7038739** @alexey-savin ratelimiter: disable averaging window for mdb monitorings, enable flap detector

**r7037106** @nikitonsky Remove all tags in coordinator /remove handle when tag is not specified

**r7035060** @eak1mov Fix ecstatic outside of RTC

**r7030359** @vmazaev Introducing pycare

**r7008708** @imseleznev add symlinks from /usr/lib/y/m/yacare/detach_all -> controls/maps_detach_all GEOINFRA-2071

**r7004224** @imseleznev add warm up of locale before starting serving requests

**r6989795** @nikitonsky Allow wildcard upload using tvm in ecstatic coordinator

**r6988737** @nikitonsky Release ecstatic tool package r6988187

**r6988187** @nikitonsky Write warning when using auth cookie

**r6985330** @nikitonsky Use tvm in MAPS_PARTIAL_RESTORE sandbox task except stable

**r6984076** @nikitonsky Ecstatic reconfigurer r6980172 in unstable/testing/datatestnig

**r6983736** @robot-maps-sandbox Update base image version: stable to 6974818, prestable to 6974818

**r6983633** @nikitonsky Release baseimage r6974818

* * * * *
maps/core-base-trusty:7040096 | maps/core-base-bionic:7040096:

(GEOINFRA-2071) yacare/baseimage: bugfix ln to ITS flag files

(GEOINFRA-775) ecstatic/baseimage: Remove all tags in coordinator /remove handle when tag is not specified

(MAPSRENDERER-2770) baseimage: removed default dump.json to fix ecstatic outside of RTC  

(GEOINFRA-2071) yacare/baseimage: add symlinks from /usr/lib/y/m/yacare/detach_all -> controls/maps_detach_all
 
(GEOINFRA-935) yacare/baseimage: add warm up of locale before starting serving requests (will be applied to auth_agent & ratelimiter_proxy)

ecstatic/baseimage: Write warning when using auth cookie

(GEOINFRA-1998) yacare: add persistent detach_all via file

* * * * *
maps/core-base-trusty:6974818 | maps/core-base-bionic:6974818:

(GEOINFRA-2065) baseimage: make all config files with +x attribute to hack distbuild inconsistency

baseimage: dont restart push-client on nginx logrotate
           
(GEOINFRA-2065) yacare: check config file access before starting app

(GEOINFRA-2065) yacare/baseimage: add postbuild checks for yacare conf permissions

(GEOINFRA-2065) yacare: fix yacare-heavy stub failures

(GEOINFRA-2065) yacare: Possibility to skip config check

(GEOINFRA-2018) ecstatic: Realtime write hooks output to logs 

(GEOINFRA-851) yacare: permit yacare backend to respond to datatesting service balancer requests
                       
(GEOINFRA-2081) ecstatic/baseimage: Add required preserved datasets to baseimage config 

(GEOINFRA-2052) baseimage: Check network availabiltity on build time 

(GEOINFRA-1986) baseimage: add /etc/yandex/environment.type to whitelist

(GEOINFRA-2084) baseimage: make sure auth_agent starts before nginx

* * * * *
maps/core-base-trusty:6876809 | maps/core-base-bionic:6876809:

(GEOINFRA-1986) add test.sh to baseimage + add option for template_generator to fail on overwrites

Move environment_linker to maps/infra

* * * * *
maps/core-base-trusty:6861868 | maps/core-base-bionic:6861868:

(GEOINFRA-2006) ecstatic: fix worker deadlocks

(GEOINFRA-1672) roquefort: filter out Molly requests

(GEOINFRA-1988) template_generator and base image moved to infra

(GEOINFRA-1924) Use contrib/libs/luajit for building and testing of lua modules

(GEOINFRA-1874) yacare-light: remove retries on startup & more tests

(GEOINFRA-1828) base image: default app.name value

ecstatic: pass ECSTATIC_VERSIONED_DATA_PATH while rerun hook 

(GEOINFRA-1919) yacare-light: dont cut environ off 

(GEOINFRA-1523) ratelimiter: remove deltas heuristic

(GEOINFRA-1943) ymtorrent: Use libtorrent from contrib

* * * * *
maps/core-base-trusty:6675461 | maps/core-base-bionic:6675461:

(GEOINFRA-1957) ratelimiter: renaming folowup

(GEOINFRA-1962) ecstatic: Use maps/pylibs/cython_tools in ymtorrent cython binding  

* * * * *
maps/core-base-trusty:6590805 | maps/core-base-bionic:6590805:

maps-yacare-check: properly split alarm output

(GEOINFRA-1816) ecstatic: Fix hooks timeouts

(GEOINFRA-1815) ecstatic: Add local lock for switch

(GEOINFRA-1869) yacare: handle SIGABRT and std::terminate 

* * * * *
maps/core-base-trusty:6536554 | maps/core-base-bionic:6536554:

base-image: Add preserved data support to switchlib

ecstatic: Refactor preserved data support. Add hardlinks right after enabling

ecstatic: Fix --check params validation

* * * * *
maps/core-base-trusty:6500968 | maps/core-base-bionic:6500968:

(GEOINFRA-1799) Upgrade nginx to 1.14.2

* * * * *
maps/core-base-trusty:6498559 | maps/core-base-bionic:6498559:

(GEOINFRA-1814) Rotate atop log during start of container

(GEOINFRA-1751) ecstatic: add retry_switch command

(GEOINFRA-1729) push-client: support for datavalidation/dataprestable environments in config

(GEOINFRA-735) ecstatic: Add hardlinks support for activated datasets

* * * * *
maps/core-base-trusty:6443667 | maps/core-base-bionic:6443667:

(GEOINFRA-1772) Add cron support

Bring missing telnet back

(GEOINFRA-1674) Record system state every 5 sec with atop

(GEOINFRA-1755) Fix bionic sources list & apt update for both base images

(GEOINFRA-1775) template generator: Copy file mode to generated files

(GEOINFRA-1685) template generator: Support for datavalidation/dataprestable env

(GEOINFRA-1713) tvm2lua: Reject requests with 403 instead of 401

(GEOINFRA-1722) ratelimiter: Fix 5xx on ratelimiter-agent start

(GEOINFRA-1691) supervisord: Switch to arcadia version

(GEOINFRA-1481) ecstatic: Migrate worker to python 3

* * * * *
maps/core-base-trusty:6350958 | maps/core-base-bionic:6350958:

yacare: deterministic order of executing scripts in yacare/lua/init.d

ecstatic-tool: Fix crash caused by None sys.stdin

* * * * *
maps/core-base-trusty:6326782 | maps/core-base-bionic:6326782:

ecstatic: Fix xtlock for groups with dead hosts

yacare-light: Allow "all" for all commands

* * * * *
maps/core-base-trusty:6261122 | maps/core-base-bionic:6261122:

Fix Moscow timezone setting in bionic base image

Fix logrotate in bionic base image

(RTCSUPPORT-5383) Resolve localhost with /etc/hosts

(GEOINFRA-1554) ratelimiter: Avoid garbage collecting on multiple workers simultaneously

(GEOINFRA-1391) yasm: Yasm subagent in base image (for metrics pushing)

* * * * *
maps/core-base-trusty:6236302 | maps/core-base-bionic:6236302:

New image "core-base-bionic" based Ubuntu Bionic Beaver (18.04)

(GEOINFRA-1427) yacare: pythonized some bash scripts

(GEOINFRA-1462) yacare-light: fix non-root invocation / (re)start all

(GEOINFRA-1589) ecstatic: remove ecstatic config package

(GEOINFRA-1494) ecstatic: descrease disk cache buffer size

ecstatic: Add custom host in juggler monitorings

* * * * *
maps/core-base-trusty:6217080:

New image name "core-base-trusty" for future bionic migration

ecstatic: fixed problem with obsolete items in /torrents

(GEOINFRA-1578) ratelimiter: add session id to shard id

(GEOINFRA-1577) yacare-light: fix ctl behavior for nonexistent services

(GEOINRFA-1611) yacare-light: fix collision on parallel start/restart,
                              fix status atomicity, new pythonized ctl

(GEOINFRA-1060) ecstatic tool: datatesting coordinator

* * * * *
maps/core-base:6045805:

ecstatic: fixed problem working without syslog

(GEOINFRA-1105) ecstatic: custom timeouts for ecstatic hooks

(GEOINFRA-1501) ecstatic: reannounce until seeding to at least 2 peers

(GEOINFRA-1501) ymtorrent: 1mb socket buffer and 4 peers reannounce limit

(GEOINFRA-1438) ratelimiter: added timings metrics

(GEOINFRA-1512) ratelimiter: lamport timestamp in proto message

(GEOINFRA-1586) ratelimiter fix

(MAPSRENDER-2319) ymtorrent: maps/libs/common ported to Windows

(MAPSGARDEN-15911) ecstatic-client package rearranged to comply with the style guide

* * * * *
maps/core-base:5985356:

apt-get autoremove in dockerfile

(GEOINFRA-1526) ratelimiter: limits version in proto message

(GEOINFRA-1347) ecstatic: remove hook while purging datasets

* * * * *
maps/core-base:5926772:

GEOINFRA-1345: short-live tvm client for crash fix

GEOINFRA-1489: Base Image - Enable cores aggregator

GEOINFRA-1501: ymtorrent socket buffer 256kb

Remove .torrent files support

GEOINFRA-1538: fix yacare segfault

Introduce yacare UserInfoFixture

Base Image version monitoring setup

GEOINFRA-1488: Default segfault logger in yacare

GEOINFRA-1289: Fix ymtorrent with no space on disk

Remove yandex-maps-xpath from dockerfile (it is not used)

GEOINFRA-1520: Fix ymtorrent.status

GEOINFRA-1345: Remove check_cookie monitoring

GEOINFRA-1356: Yacare: fix handling consequent SIGTERMs

Don't write torrent files in download and upload

Add ecstatic worker gRPC timeout

GEOINFRA-1503: Ratelimiter hotfix for incorrect counters sync

GEOINFRA-1410: ecstatic download fix part 1: add probe_torrents to ymtorrent

GEOINFRA-1510: Fix ecstatic worker

GEOINFRA-1501: pass through libtorrent options

GEOINFRA-1484: properly terminate upload_finished_check_thread if an exception was raised

GEOINFRA-1477: Use curl instead of yacare/request

Light yacare: fix commands exit codes & streams to write

GEOINFRA-1462: Yacare-light: monitor starting service

GEOINFRA-1337: Ratelimiter: force 0 grace period for proxy servant

GEOINFRA-1462: Fixies in yacare before announcing light version

GEOINFRA-1481: Move ecstatic tool to py3

GEOINFRA-1404: Remove legacy network code from ecstatic client

GEOINFRA-1471: yacare/request: ability to set custom timeout

GEOINFRA-887: Add torrent priorities in ecstatic

* * * * *
maps/core-base:5781489:

GEOINFRA-1382: Fix ecstatic crashes on start

Fix roquefort crashes caused by exception in main thread

Fix ymtorrent subcontainer monitoring because of new instancectl

GEOINFRA-1429: Fix yacare/request usage according to new qargs format

GEOINFRA-1429: Yacare request.py: fix empty path handling

GEOINFRA-1415: docker:core-base make nginx, roquefort, push_client optional

GEOINFRA-1371: 403 code for incorrect tvm2 service-ticket destination

MAPSMOBCORE-9767: Run ecstatic hooks in lexicographic order

GEOINFRA-1013: Force reannounce in ymtorrent uploads

GEOINFRA-1013: ymtorrent2 hash doesn't depend on data dir name

GEOINFRA-1345: ecstatic tool crashes fix

* * * * *
maps/core-base:5702729:

GEOINFRA-1433: tvmtool updated to v1.3.3

GEOINFRA-1429: Fixed yacare detach freezing

GEOINFRA-1398: "Light" yacare (disabled by default)

GEOINFRA-1216: Fixed roquefort configuration parsing

* * * * *
maps/core-base:5649667:

GEOINFRA-1397: Yacare: Force connection release when socket is closing

GEOINFRA-1337: Yacare: Set yacare grace period to 10s by default

GEOINFRA-1343: Ecstatic: ymtorrent as a lib

GEOINFRA-887:  Ecstatic: Added priorities support to ymtorrent

GEOINFRA-1255: Ecstatic: ymtorrent status write speedup

GEOINFRA-721:  Yacare: Supervised yacare v3

GEOINFRA-1380: Logrotate: Fix postrotate for nginx

GEOINFRA-1350: Ecstatic: take into account daemon-mode ymtorrent invocations only

GEOINFRA-1216: Roquefort: per-config enabled signals about nginx caches

GEOINFRA-1298: Base: run.sh and supervisord falures/restarts

GEOINFRA-1330: TVM: Tvm id in nginx access_tskv.log

GEOINFRA-914:  Ecstatic: Add gRPC support for communication between ymtorrent and ecstatic worker

GEOINFRA-1329: Ecstatic: ecstatic worker fix logs duplication

GEOINFRA-1101: TVM: Base image support for running tvmtool in 'development' environment

* * * * *
maps/core-base:5419259:

GEOINFRA-1278: ecstatic_worker: clean up torrent content if it is in inconsistent state

GEOINFRA-1160: use tvmtool auth

MAPSMOBCORE-9530: Make nginx error.log logrotate configurable

Reduce time between tvmtool-health-checks on runlast.d

fix fatal-programs check after update to latest supervisord

update ecstatic subcontainer name to comply with new instancectl (>=187)

* * * * *
maps/core-base:5298046:

GEOINFRA-1160: Ecstatic tool: support of tvm authentication

GEOINFRA-1146: Ecstatic tool: Removed ecstatic datasets command

GEOINFRA-1160: Tvm2 nginx plugin: fix bug, that allowed to pass tvm src id in plain header

GEOINFRA-1260: metric_collector: Add yasm signal with base docker image revision and juggler warning alert for too old revisions

GEOINFRA-1188: Logrotate: make logrotate period adjustable

GEOINFRA-1188: supervisor updated to 4.0.3

GEOINFRA-1255: ymtorrent monitoring fix

GEOINFRA-1184: Ecstatic: Prevent ecstatic deleting datasets when host dropped out from deploy group

GEOINFRA-1053: Nginx: 'service_name' assign unknown as default value

GEOINFRA-1013: Ecstatic: Support ecstatic datasets backup and restore

MAPSMOBCORE-9362: template_generator: Add hostname retrieval with `HOSTNAME` template variable

* * * * *
maps/core-base:5174261:

GEOINFRA-1194 Ecstatic tool refactoring around handling cookies

Add support for custom libtorrent options in ymtorrent

GEOINFRA-1045 Build roquefort with musl

GEOINFRA-1126 Ecstatic-agent tries to restart ymtorrent subcontainer in case it fails to attach ymtorrent to it

GEOINFRA-1126 Monitoring of ymtorrent subcontainer

GEOINFRA-1126 Fix new attempts to create existing subcontainer when start script is rerun after failure
* * * * *
maps/core-base:5144032:

GEOINFRA-1213: tvmtool-health-check monitoring refactored as shell script

GEOINFRA-1209: template_generator rounds up number of CPU cores
* * * * *
5127792:
GEOINFRA-1140: speedup roquefort

GEOINFRA-1045: build ecstatic tool and ymtorrent with musl

GEOINFRA-1188: handle all levels in syslog

GEOINFRA-1163: Set Europe/Moscow timezone in container
* * * * *
r5095535: add fsync option to ymtorrent2 by scanning /proc/self/fd GEOINFRA-1126

r5090807: Add TVM_SECRET variable in load if no secret was deployed

r5087477: GEOINFRA-1126 add option to run ymtorrent in separate porto subcontainer with custom memory
* * * * *
5084409:

GEOINFRA-1159: tvm2: support for tvmId yacare parameter

GEOINFRA-1126: ymtorrent: change minimum piece size to 1mb & increase buffer sizes to 512mb

GEOINFRA-1013: add to /torrents a mode which returns all the available torrents
* * * * *
5070381:
GEOINFRA-1165: fixed ymtorrent crash on broken resume and torrent files
* * * * *
5065894:
GEOINFRA-1053: Distinguish services in roquefort
GEOINFRA-1007: Supress CRIT in ecstatic on startup
GEOINFRA-1125: libtorrent-1.2.1
* * * * *
5002780:
GEOINFRA-1071 almost disable writing nginx error logs directly on disk
5002081:
GEOINFRA-1124 remove $args from tskv log
4970664:
Add nocompress support to nginx logrotate in yacare.
* * * * *
4965914:
(GEOINFRA-953) Ecstatic check hooks support
* * * * *
4956886:
Bugfix: revert back applying custom configs for ecstatic.
* * * * *
4946106:
Push client updated.
* * * * *
4943544:
(GEOINFRA-1072) Better handling for long request bodies in nginx + ability to configure it.
* * * * *
4941290:
(GEOINFRA-1071, GEOINFRA-1027) upgrade to new nginx 1.12, added buffering to syslog-ng config,
nginx logs are written through syslog-ng, fix syslog-ng reloads on logrotate.
(GEOINFRA-956) Fix rerunHooks script to run any type of hooks.
* * * * *
4932952:
(GEOINFRA-1072) Increase default memory buffer sizes for request bodies, add buffering to tskv_log
* * * * *
4932860:
(GEOINFRA-1066) Save fastresume files and the data on the same storage
(GEOINFRA-996) Initialize ecstatic file structure in the right way
Remove temporary files created during ecstatic upload
* * * * *
4700121:
(GEOINFRA-1056) Updated libtorrent to version 1.1.12
(GEOINFRA-1044) ratelimiter: correct vhost by adding slb host name in requests to ratelimiter server to speed up SLA calculation
(GEOINFRA-690) yacare: auto enable tvmtool and ratelimiter agent based on yacare options being used (no need to explicitly enable in config anymore)
* * * * *
4660472:
(GEOINFRA-996) Fix ecstatic ymtorrent-fresh monitoring
* * * * *
4622179:
(GEOMONITORINGS-6023) Bugfix overriding logrotate state on container start
(GEOINFRA-996) Ecstatic-client creates its subdirs, if necessary
(GEOINFRA-999) Port ecstatic-client to xenial
Bugfix syslog-ng-include-tpl3.5 broken dependency => apt-get install was not working
* * * * *
4602511:
(GEOINFRA-1026) tvm2: running tvmtool in unittest mode now is based on env:TVM_SECRET instead of template_generator config
(GEOINFRA-1002) ratelimiter: 'anonym' quota for unidentified clients
(GEOINFRA-700) ratelimiter: no client_id/resource_id in reject responses
(r4572967) ratelimiter: agent killswitch script refactored
* * * * *
4503382:
(GEOINFRA-1006) template_generator: fix cpu_guarantee detection in YP pods
(GEOINFRA-974) tvm2: nginx master configuration check
(GEOINFRA-973) tvm2: use mock keys/tickets in load staging (load uses tvmtool 'unittest' mode by default)
* * * * *
4486244:
(GEOINFRA-957) ecstatic: removed a file which was committed too early
(GEOINFRA-980) ratelimiter: ratelimiter weights by request parameters in yacare
(GEOINFRA-1003) Fix bug in lua check for ngx.var.*
4479361:
(GEOINFRA-991) ratelimiter: removed softtesting configuration
(GEOINFRA-905) ymtorrent2: rolled back changes
(GEOINFRA-901) ymtorrent2: support for multiple torrent downloads
* * * * *
4452019:
(GEOINFRA-991) ratelimiter: configuration for softtesting
(GEOINFRA-978) ecstatic: fix symlinks creating during switch
(GEOINFRA-905) ymtorrent: fix issue when ymtorrent hangs if there is no space left on device
* * * * *
4436229:
(GEOINFRA-977) ymtorrent2: Fixed race condition during status file creation in daemon mode
(GEOINFRA-901) ymtorrent2: Added retries as a workaround for the bind() race condition
(GEOINFRA-709) ecstatic: client monitorings redesigned to just 3 checks 'ecstatic-worker', 'ecstatic-ymtorrent' and 'ecstatic-client-config'
(GEOINFRA-776) tvm2: added nginx plugin to support tickets check for yacare
(GEOINFRA-974) tvm2: nginx plugin worker init retries
tvmtool v1.2.15 (PASSP-20927)
* * * * *
4384002:
Fix logging non-ascii hooks output in ecstatic worker (https://a.yandex-team.ru/arc/commit/4379989)
* * * * *
Fix minor bug in ecstatic worker (https://a.yandex-team.ru/arc/review/688427/details)
Templating template_generator config (https://a.yandex-team.ru/review/685935/details)
* * * * *
4370464
disable os disk write cache option for ymtorrent MAPSNAVI-5071
* * * * *
4361353:
Python ecstatic worker (GEOINFRA-589)
Fix supervisor fatal programs monitoring
* * * * *
4335455:
Custom log parsing in Roquefort (GEOINFRA-850)
Save base image revision in /etc/base_image_revision
Start yacare servant after superevisor tasks
Added tvmtool (GEOINFRA-780)
Added ncdu and openssh-client (GEOINFRA-857)
* * * * *
4288822:
Fix memory storage dir creation in ecstatic client
* * * * *
4234155:
Fix race in ymtorrent (GEOMONITORINGS-4638)
* * * * *
4230444:
Ratelimiter-agent:
Add roquefort in ratelimiter package config (GEOINFRA-813)
Add template file for yacare to detect cpu_limit (GEOINFRA-472)
* * * * *
4162690:
Ratelimiter-agent:
Upstreams discovery through balancer (GEOINFRA-710)
Fixed broken limits update on workers (GEOINFRA-795)
* * * * *
3999321:
Logrotate лимит для yacare_app уменьшен по умолчанию до 10G
В рокфоре убраны ненужные сигрналы от внутренних ручек якара
* * * * *
3961283:
Улучшены ретраи в воркере экстатика
В рокфоре добавился сигнал для ping
Во всем logrotate базовых компонент заменен size на maxsize, дефолтное ограничение для yacare_app 100G
Добавлена возможность настраивать параметры logrotate для nginx-access-tskv.log
Добавлена поддержка ratelimiter2
* * * * *
