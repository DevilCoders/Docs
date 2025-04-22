##yandex-vertis-parsing-old-holocron:0.0.20 (Tue, 12 Nov 2019 15:21:51 +0300)

  * old holocron: distribution name from zk
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * fixed logging duplication
  * fixed insert update results metrics: excluded dump_name, as it failed to get correct increase values for fresh dumps with it
  * changes
  * 'changes'
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * AUTORUAPI-6033 old data remover: updated worker: added checks to stop execution, added another feature for actual deletion
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * fixed ScrapinghubDromCarsParser.parsePrice
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.19...docker-yandex-vertis-parsing-old-holocron-0.0.20

##yandex-vertis-parsing-old-holocron:0.0.19 (Mon, 11 Nov 2019 14:35:30 +0300)

  * 'changes'
  * changes
  * changes
  * 'changes'
  * fixed compilation
  * AUTORUAPI-6033 old data remover: added feature, added to launcher, added logging
  * Merge pull request #81 from YandexClassifieds/AUTORUAPI-6033_remove_old_data
  * old holocron custom period from zookeeper
  * fixed vos2-autoru-diff-log processor: check offer is already published, updated logging
  * banned_phones from bunker: fixed test compilation
  * banned_phones from bunker: fixed test config
  * banned_phones from bunker
  * more strict bunker config format
  * fixed scraping hub am.ru: new parsed field listing_verified
  * todo
  * minor changes in logging
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * fixed (I hope) mdb unexpected master-replica switch
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * fixed filter reasons index tables
  * bizdev stats fix
  * minor changes
  * comments
  * fixed bizdev realty sender: distinct names
  * fixed bizdev realty sender: another url prefix
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * fixed bizdev realty sender: calculate workMoment for all callCenters before any send
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * fixed realty sender: calculate workMoment for all callCenters before any send
  * fixed features naming
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * scripts
  * REALTYBACK-1522 fixed api: obtain ids for hash via MailHashDao
  * REALTYBACK-1522 fixed bizdev checks in offers dao
  * 'changes'
  * REALTYBACK-1522 fixed features: added SendMailToBizdev to allFeatures
  * 'changes'
  * changes
  * Merge pull request #80 from YandexClassifieds/REALTYBACK-1827_realty_bizdev
  * 'changes'
  * changes
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * minor tests
  * added features to disable statistician and active count cache sync, to be able to remove load from database and perform heavy alter
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * improved index fields update: refactoring, added special check to PhonesWatcher
  * improved properties node serializer: check for empty string
  * cache sync: increased resync period: fixed tests
  * fixed improved index fields update (#TestsReallyHelped)
  * not published reason in proto model to make it possible to set it in NotPublishedReasonsWatcher.offerFields
  * improved index fields update: check for last diffs and update only watchers that really changed
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * cache sync: increased resync period
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.18...docker-yandex-vertis-parsing-old-holocron-0.0.19

##yandex-vertis-parsing-old-holocron:0.0.18 (Fri, 18 Oct 2019 18:13:42 +0300)

  * old holocron: check position.isDone every iteration
  * old holocron: position update fix
  * fixed parsers: price and mileage from scraping hub avito and drom
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * updated CarsParser: all return values are ParsedValue
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.17...docker-yandex-vertis-parsing-old-holocron-0.0.18

##yandex-vertis-parsing-old-holocron:0.0.17 (Thu, 17 Oct 2019 19:58:24 +0300)

  * scripts
  * scripts
  * refactoring
  * old holocron: fixed configurationId parsing
  * reverted: added order by id desc to send fresh offers to call centers first, unable to perform such queries with ONLY_FULL_GROUP_BY in sql_mode
  * old holocron: send certification in lower case
  * fixed compilation
  * global import progress counter
  * added order by id desc to send fresh offers to call centers first
  * Merge pull request #79 from YandexClassifieds/auto_all_parsed_value
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * realty: fixed tricky user names in letter
  * cache sync: reduced batch size for userId cache, trying to speed up
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * AUTORUAPI-6360 updated duplicates check: check for UNITY results, updated metrics, updated logging
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * scraping hub reactivator: getUnprocessedforReactivation, to speed up query
  * fixed test
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * scraping hub reactivator: fixed getUnprocessed: orderById
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * scraping hub reactivator: fixed cache name
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * scraping hub reactivator: fixed getUnprocessed
  * scraping hub reactivator: refactoring
  * fixed test
  * scraping hub reactivator: added to launcher
  * scraping hub reactivator, updated test
  * fixed test
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * scraping hub reactivator, not finished
  * fixed compilation
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * realty parsing: updated filtration: BannedPhone, ManyActiveByPhone, updated tests, added tests
  * fixed compilation
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * updated cache syncrhonizer: split on two, increased batch size
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.16...docker-yandex-vertis-parsing-old-holocron-0.0.17

##yandex-vertis-parsing-old-holocron:0.0.16 (Fri, 11 Oct 2019 10:47:55 +0300)

  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * AUTO-10615 old holocron: fixed nameplate set
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.15...docker-yandex-vertis-parsing-old-holocron-0.0.16

##yandex-vertis-parsing-old-holocron:0.0.15 (Thu, 10 Oct 2019 20:29:14 +0300)

  * AUTO-10615 old holocron: strict validation
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * AUTO-10615 old holocron: set discount, discount options, nameplate
  * old holocron: updated vas conversion, fixed configurationId/superGenerationId conversion
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.14...docker-yandex-vertis-parsing-old-holocron-0.0.15

##yandex-vertis-parsing-old-holocron:0.0.14 (Thu, 10 Oct 2019 09:43:28 +0300)

  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * old holocron: fixed configuration id parsing
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.13...docker-yandex-vertis-parsing-old-holocron-0.0.14

##yandex-vertis-parsing-old-holocron:0.0.13 (Wed, 09 Oct 2019 16:52:43 +0300)

  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * AUTO-10615 validation fixes and refactoring
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.12...docker-yandex-vertis-parsing-old-holocron-0.0.13

##yandex-vertis-parsing-old-holocron:0.0.12 (Wed, 09 Oct 2019 11:46:15 +0300)

  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * added timeout to verba
  * minor changes
  * realty: updated avito price parsing: 0 is NoValue, negative value is Unexpected
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * realty: fixed price parsing, 0 is unexpected
  * fixed compilation
  * parsing realty: import progress counter
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.11...docker-yandex-vertis-parsing-old-holocron-0.0.12

##yandex-vertis-parsing-old-holocron:0.0.11 (Tue, 08 Oct 2019 18:25:35 +0300)

  * old holocron: verba limiter: 1 rps
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.10...docker-yandex-vertis-parsing-old-holocron-0.0.11

##yandex-vertis-parsing-old-holocron:0.0.10 (Tue, 08 Oct 2019 17:08:04 +0300)

  * http client builder, refactoring, limited http client, updated verba client: made it limited and cached
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.9...docker-yandex-vertis-parsing-old-holocron-0.0.10

##yandex-vertis-parsing-old-holocron:0.0.9 (Tue, 08 Oct 2019 14:26:01 +0300)

  * old holocron: fixed HolocronSendData.key
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.8...docker-yandex-vertis-parsing-old-holocron-0.0.9

##yandex-vertis-parsing-old-holocron:0.0.8 (Tue, 08 Oct 2019 13:53:16 +0300)

  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * old holocron: updated queryAndImportDay: update positionNode
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * pealty parsing: fixed active count caches, trying to optimize queries
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.7...docker-yandex-vertis-parsing-old-holocron-0.0.8

##yandex-vertis-parsing-old-holocron:0.0.7 (Mon, 07 Oct 2019 18:07:53 +0300)

  * AUTO-10615 fixed old holocron sender
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.6...docker-yandex-vertis-parsing-old-holocron-0.0.7

##yandex-vertis-parsing-old-holocron:0.0.6 (Mon, 07 Oct 2019 18:02:04 +0300)

  * minor changes
  * AUTO-10615 fixed old holocron position isempty calculation
  * fixed zookeeper wrapper: remove node with children
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.5...docker-yandex-vertis-parsing-old-holocron-0.0.6

##yandex-vertis-parsing-old-holocron:0.0.5 (Mon, 07 Oct 2019 16:46:10 +0300)

  * AUTO-10615 decreased Xmx
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.4...docker-yandex-vertis-parsing-old-holocron-0.0.5

##yandex-vertis-parsing-old-holocron:0.0.4 (Mon, 07 Oct 2019 16:21:08 +0300)

  * AUTO-10615 added libticket parser
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.3...docker-yandex-vertis-parsing-old-holocron-0.0.4

##yandex-vertis-parsing-old-holocron:0.0.3 (Mon, 07 Oct 2019 14:48:49 +0300)

  * AUTO-10615 run launcher
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.2...docker-yandex-vertis-parsing-old-holocron-0.0.3

##yandex-vertis-parsing-old-holocron:0.0.2 (Mon, 07 Oct 2019 14:31:43 +0300)

  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * shrink, minor fixes
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * parsing realty: fixed active count for username caches (#TestsReallyHelped)
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * parsing realty: fixed active count for username caches, again
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * active count cache: refactoring, updated logging, added stats
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * cache synchronizer: added shouldWork check
  * fixed test
  * realty: normalize published phones
  * removed unused code
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * cache synchronizer, finished
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * parsing realty: fixed active count for username caches, added test, yes, again
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * parsing realty: active count caches: synchronizer, not finished
  * parsing realty: fixed active count for username caches, added test
  * parsing realty: fixed active count for username caches, added test
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * fixed next sync moment for active count for userId cache
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * parsing realty: fixed active count caches, added tests (#TestsReallyHelped)
  * parsing realty: updated active count caches
  * nameplate stats
  * realty validator refactoring
  * minor changes
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * realty: dao caches to speed up filtration, not finished
  * realty parsing: fixed many_active validation
  * search api: hashes
  * minor changes
  * AUTORUAPI-6184 big status history fix: refiltration fix, refactoring, added test
  * Merge branch 'master' of github.com:YandexClassifieds/parsing
  * hash resolver
  * fixed realty SendMail feature
  * realty migration api
  * AUTO-10615 fixed converter
  * https://github.com/YandexClassifieds/parsing/compare/docker-yandex-vertis-parsing-old-holocron-0.0.1...docker-yandex-vertis-parsing-old-holocron-0.0.2

##yandex-vertis-parsing-old-holocron:0.0.1 (Fri, 26 Sep 2019 18:00:00 +0300)

  * initial release
