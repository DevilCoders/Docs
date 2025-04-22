## vos2-autoru-ydb-workers:0.93.51 (Thu, 14 Apr 2022 15:48:22 +0300)

  *  AUTORUBACK-3168 Offer recheck  notification (#1353)
     

  *  AUTORUBACK-3054 add StoryAuctionPhotoWorkerYdb (#1326)
     
     * AUTORUBACK-3054 add StoryAuctionPhotoWorkerYdb
     
     * AUTORUBACK-3054 add StoryAuctionPhotoWorkerYdb
     
     * AUTORUBACK-3054 add StoryAuctionPhotoWorkerYdb
     
     * AUTORUBACK-3054 add StoryAuctionPhotoWorkerYdb
     
     * AUTORUBACK-3054 fix is_valid_for_c2b_auction
     
     * AUTORUBACK-3054 fix is_valid_for_c2b_auction
     
     * AUTORUBACK-3054 fix is_valid_for_c2b_auction
     
     * AUTORUBACK-3054 fix fmt
     
     * AUTORUBACK-3054 fix fmt
     
     * AUTORUBACK-3054 fix after review
     
     * AUTORUBACK-3054 fix after review
     
     * AUTORUBACK-3054 fix after review
     
     * AUTORUBACK-3054 fix after review
     
     * AUTORUBACK-3054 fix after review
     
     * AUTORUBACK-3054 fix after review
     
     * AUTORUBACK-3054 fix after review
     
     * AUTORUBACK-3054 fix after review
     
     * AUTORUBACK-3054 add test
     
     * AUTORUBACK-3054 add test
     
     * AUTORUBACK-3054 add isPrivate
     
     * AUTORUBACK-3054 fix shouldProcess
     
     * AUTORUBACK-3054 fix shouldProcess
     
     * AUTORUBACK-3054 fix shouldProcess
     
     * AUTORUBACK-3054 fix shouldProcess
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-3196 (#1356)
     

  *  AUTORUBACK-3052 (#1347)
     

  *  #AUTORUBACK-3189 BrandCertificationUpdateWorkerYdb update (#1352)
     

  *  AUTORUBACK-3173 (#1351)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata (#1350)
     
     * AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata
     
     * AUTORUBACK-3141 Clean up duplicated logic
  *  AUTORUBACK-3089_new_zookeeper_hosts (#1349)
     

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3175_cert_fix (#1345)
     
     * AUTORUBACK-3175_cert_fix
     
     * AUTORUBACK-3175_cert_fix: added and updated tests, fixed compilation
  *  AUTORUBACK-3171 Move NO_PTS converting under feature (#1344)
     

  *  AUTORUBACK-3163 Filter by calls auction bid presence (#1342)
     
     * Revert "AUTORUBACK-3086 add filter not in auction (#1338)"
     
     This reverts commit 4ff24a21908729d00d2a15198c93e52ca2931ecf.
     
     * AUTORUBACK-3163 Filter by calls auction bid presence
     
     * AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * fixup! AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * AUTORUBACK-3163 Add a test for has_calls_auction_bid filter
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 14 Apr 2022 15:48:22 +0300

## vos2-autoru-ydb-workers:0.93.50 (Thu, 14 Apr 2022 09:39:17 +0300)

  *  AUTORUBACK-3196 (#1356)
     

  *  AUTORUBACK-3052 (#1347)
     

  *  #AUTORUBACK-3189 BrandCertificationUpdateWorkerYdb update (#1352)
     

  *  AUTORUBACK-3173 (#1351)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata (#1350)
     
     * AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata
     
     * AUTORUBACK-3141 Clean up duplicated logic
  *  AUTORUBACK-3089_new_zookeeper_hosts (#1349)
     

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3175_cert_fix (#1345)
     
     * AUTORUBACK-3175_cert_fix
     
     * AUTORUBACK-3175_cert_fix: added and updated tests, fixed compilation
  *  AUTORUBACK-3171 Move NO_PTS converting under feature (#1344)
     

  *  AUTORUBACK-3163 Filter by calls auction bid presence (#1342)
     
     * Revert "AUTORUBACK-3086 add filter not in auction (#1338)"
     
     This reverts commit 4ff24a21908729d00d2a15198c93e52ca2931ecf.
     
     * AUTORUBACK-3163 Filter by calls auction bid presence
     
     * AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * fixup! AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * AUTORUBACK-3163 Add a test for has_calls_auction_bid filter
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 14 Apr 2022 09:39:17 +0300

## vos2-autoru-ydb-workers:0.93.49 (Wed, 13 Apr 2022 15:47:43 +0300)

  *  AUTORUBACK-3052 (#1347)
     

  *  #AUTORUBACK-3189 BrandCertificationUpdateWorkerYdb update (#1352)
     

  *  AUTORUBACK-3173 (#1351)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata (#1350)
     
     * AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata
     
     * AUTORUBACK-3141 Clean up duplicated logic
  *  AUTORUBACK-3089_new_zookeeper_hosts (#1349)
     

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3175_cert_fix (#1345)
     
     * AUTORUBACK-3175_cert_fix
     
     * AUTORUBACK-3175_cert_fix: added and updated tests, fixed compilation
  *  AUTORUBACK-3171 Move NO_PTS converting under feature (#1344)
     

  *  AUTORUBACK-3163 Filter by calls auction bid presence (#1342)
     
     * Revert "AUTORUBACK-3086 add filter not in auction (#1338)"
     
     This reverts commit 4ff24a21908729d00d2a15198c93e52ca2931ecf.
     
     * AUTORUBACK-3163 Filter by calls auction bid presence
     
     * AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * fixup! AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * AUTORUBACK-3163 Add a test for has_calls_auction_bid filter
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 13 Apr 2022 15:47:43 +0300

## vos2-autoru-ydb-workers:0.93.48 (Mon, 11 Apr 2022 17:39:15 +0300)

  *  #AUTORUBACK-3189 BrandCertificationUpdateWorkerYdb update (#1352)
     

  *  AUTORUBACK-3173 (#1351)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata (#1350)
     
     * AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata
     
     * AUTORUBACK-3141 Clean up duplicated logic
  *  AUTORUBACK-3089_new_zookeeper_hosts (#1349)
     

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3175_cert_fix (#1345)
     
     * AUTORUBACK-3175_cert_fix
     
     * AUTORUBACK-3175_cert_fix: added and updated tests, fixed compilation
  *  AUTORUBACK-3171 Move NO_PTS converting under feature (#1344)
     

  *  AUTORUBACK-3163 Filter by calls auction bid presence (#1342)
     
     * Revert "AUTORUBACK-3086 add filter not in auction (#1338)"
     
     This reverts commit 4ff24a21908729d00d2a15198c93e52ca2931ecf.
     
     * AUTORUBACK-3163 Filter by calls auction bid presence
     
     * AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * fixup! AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * AUTORUBACK-3163 Add a test for has_calls_auction_bid filter
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 11 Apr 2022 17:39:15 +0300

## vos2-autoru-ydb-workers:0.93.47 (Mon, 11 Apr 2022 15:23:23 +0300)

  *  AUTORUBACK-3173 (#1351)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata (#1350)
     
     * AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata
     
     * AUTORUBACK-3141 Clean up duplicated logic
  *  AUTORUBACK-3089_new_zookeeper_hosts (#1349)
     

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3175_cert_fix (#1345)
     
     * AUTORUBACK-3175_cert_fix
     
     * AUTORUBACK-3175_cert_fix: added and updated tests, fixed compilation
  *  AUTORUBACK-3171 Move NO_PTS converting under feature (#1344)
     

  *  AUTORUBACK-3163 Filter by calls auction bid presence (#1342)
     
     * Revert "AUTORUBACK-3086 add filter not in auction (#1338)"
     
     This reverts commit 4ff24a21908729d00d2a15198c93e52ca2931ecf.
     
     * AUTORUBACK-3163 Filter by calls auction bid presence
     
     * AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * fixup! AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * AUTORUBACK-3163 Add a test for has_calls_auction_bid filter
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 11 Apr 2022 15:23:23 +0300

## vos2-autoru-ydb-workers:0.93.46 (Fri, 08 Apr 2022 13:48:35 +0300)

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3175_cert_fix (#1345)
     
     * AUTORUBACK-3175_cert_fix
     
     * AUTORUBACK-3175_cert_fix: added and updated tests, fixed compilation
  *  AUTORUBACK-3171 Move NO_PTS converting under feature (#1344)
     

  *  AUTORUBACK-3163 Filter by calls auction bid presence (#1342)
     
     * Revert "AUTORUBACK-3086 add filter not in auction (#1338)"
     
     This reverts commit 4ff24a21908729d00d2a15198c93e52ca2931ecf.
     
     * AUTORUBACK-3163 Filter by calls auction bid presence
     
     * AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * fixup! AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * AUTORUBACK-3163 Add a test for has_calls_auction_bid filter
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 08 Apr 2022 13:48:35 +0300

## vos2-autoru-ydb-workers:0.93.45 (Fri, 08 Apr 2022 13:31:18 +0300)

  *  AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3175_cert_fix (#1345)
     
     * AUTORUBACK-3175_cert_fix
     
     * AUTORUBACK-3175_cert_fix: added and updated tests, fixed compilation
  *  AUTORUBACK-3171 Move NO_PTS converting under feature (#1344)
     

  *  AUTORUBACK-3163 Filter by calls auction bid presence (#1342)
     
     * Revert "AUTORUBACK-3086 add filter not in auction (#1338)"
     
     This reverts commit 4ff24a21908729d00d2a15198c93e52ca2931ecf.
     
     * AUTORUBACK-3163 Filter by calls auction bid presence
     
     * AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * fixup! AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * AUTORUBACK-3163 Add a test for has_calls_auction_bid filter
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 08 Apr 2022 13:31:18 +0300

## vos2-autoru-ydb-workers:0.93.44 (Fri, 08 Apr 2022 13:08:00 +0300)

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3175_cert_fix (#1345)
     
     * AUTORUBACK-3175_cert_fix
     
     * AUTORUBACK-3175_cert_fix: added and updated tests, fixed compilation
  *  AUTORUBACK-3171 Move NO_PTS converting under feature (#1344)
     

  *  AUTORUBACK-3163 Filter by calls auction bid presence (#1342)
     
     * Revert "AUTORUBACK-3086 add filter not in auction (#1338)"
     
     This reverts commit 4ff24a21908729d00d2a15198c93e52ca2931ecf.
     
     * AUTORUBACK-3163 Filter by calls auction bid presence
     
     * AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * fixup! AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * AUTORUBACK-3163 Add a test for has_calls_auction_bid filter
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 08 Apr 2022 13:08:00 +0300

## vos2-autoru-ydb-workers:0.93.43 (Fri, 08 Apr 2022 09:04:28 +0300)

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3175_cert_fix (#1345)
     
     * AUTORUBACK-3175_cert_fix
     
     * AUTORUBACK-3175_cert_fix: added and updated tests, fixed compilation
  *  AUTORUBACK-3171 Move NO_PTS converting under feature (#1344)
     

  *  AUTORUBACK-3163 Filter by calls auction bid presence (#1342)
     
     * Revert "AUTORUBACK-3086 add filter not in auction (#1338)"
     
     This reverts commit 4ff24a21908729d00d2a15198c93e52ca2931ecf.
     
     * AUTORUBACK-3163 Filter by calls auction bid presence
     
     * AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * fixup! AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * AUTORUBACK-3163 Add a test for has_calls_auction_bid filter
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 08 Apr 2022 09:04:28 +0300

## vos2-autoru-ydb-workers:0.93.42 (Thu, 07 Apr 2022 16:46:45 +0300)

  *  AUTORUBACK-3175_cert_fix (#1345)
     
     * AUTORUBACK-3175_cert_fix
     
     * AUTORUBACK-3175_cert_fix: added and updated tests, fixed compilation
  *  AUTORUBACK-3171 Move NO_PTS converting under feature (#1344)
     

  *  AUTORUBACK-3163 Filter by calls auction bid presence (#1342)
     
     * Revert "AUTORUBACK-3086 add filter not in auction (#1338)"
     
     This reverts commit 4ff24a21908729d00d2a15198c93e52ca2931ecf.
     
     * AUTORUBACK-3163 Filter by calls auction bid presence
     
     * AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * fixup! AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * AUTORUBACK-3163 Add a test for has_calls_auction_bid filter
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 07 Apr 2022 16:46:45 +0300

## vos2-autoru-ydb-workers:0.93.41 (Thu, 07 Apr 2022 11:52:51 +0300)

  *  AUTORUBACK-3171 Move NO_PTS converting under feature (#1344)
     

  *  AUTORUBACK-3163 Filter by calls auction bid presence (#1342)
     
     * Revert "AUTORUBACK-3086 add filter not in auction (#1338)"
     
     This reverts commit 4ff24a21908729d00d2a15198c93e52ca2931ecf.
     
     * AUTORUBACK-3163 Filter by calls auction bid presence
     
     * AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * fixup! AUTORUBACK-3163 Fix Swagger for has_calls_auction_bid
     
     * AUTORUBACK-3163 Add a test for has_calls_auction_bid filter
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 07 Apr 2022 11:52:51 +0300

## vos2-autoru-ydb-workers:0.93.40 (Wed, 06 Apr 2022 09:38:43 +0300)

  *  AUTORUBACK-3161 (#1339)
     
     AUTORUBACK-3161
  *  AUTORUBACK-3164 (#1341)
     
     * AUTORUBACK-3164

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 06 Apr 2022 09:38:43 +0300

## vos2-autoru-ydb-workers:0.93.39 (Tue, 05 Apr 2022 18:37:55 +0300)

  *  AUTORUBACK-3133: Remove palma catalog (#1340)
     

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 05 Apr 2022 18:37:55 +0300

## vos2-autoru-ydb-workers:0.93.38 (Mon, 04 Apr 2022 21:35:30 +0300)

  *  AUTORUBACK-3086 add filter not in auction (#1338)
     
     * AUTORUBACK-3086 add filter not in auction
     
     * AUTORUBACK-3086 fix type
  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 04 Apr 2022 21:35:30 +0300

## vos2-autoru-ydb-workers:0.93.37 (Mon, 04 Apr 2022 15:30:07 +0300)

  *  AUTORUBACK-3090 Support NO_PTS enum (#1332)
     

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 04 Apr 2022 15:30:07 +0300

## vos2-autoru-ydb-workers:0.93.36 (Fri, 01 Apr 2022 11:46:55 +0300)

  *  AUTORUBACK-3144 (#1337)
     

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 01 Apr 2022 11:46:55 +0300

## vos2-autoru-ydb-workers:0.93.35 (Fri, 01 Apr 2022 11:07:55 +0300)

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 01 Apr 2022 11:07:55 +0300

## vos2-autoru-ydb-workers:0.93.34 (Thu, 31 Mar 2022 10:34:38 +0300)

  *  AUTORUBACK-3086 Fix Kafka config for calls auction bids log consumer (#1336)
     
     * AUTORUBACK-3086 Untangle KafkaConfig parsing
     
     * AUTORUBACK-3086 Add SASL support to KafkaUtils
     
     * AUTORUBACK-3086 Use separate config variables for calls auction bids log consumer
     
     * AUTORUBACK-3086 Tweak config property priorities
     
     * AUTORUBACK-3086 Add a hack to fix the tests without adding junk to datasources
     
     * AUTORUBACK-3086 Add workaround for broken Properties overload
     
     * AUTORUBACK-3086 Fix logging when initializing consumers and mirror
     
     * AUTORUBACK-3086 Make Kafka config parsing more robust
     
     * Revert "AUTORUBACK-3086 Fix logging when initializing consumers and mirror"
     
     This reverts commit 1579d59e8936fb1658cddceff0ba96a6b4126895.
  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 31 Mar 2022 10:34:38 +0300

## vos2-autoru-ydb-workers:0.93.33 (Wed, 30 Mar 2022 15:07:52 +0300)

  *  AUTORUBACK-3136 (#1335)
     

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 30 Mar 2022 15:07:52 +0300

## vos2-autoru-ydb-workers:0.93.32 (Mon, 28 Mar 2022 09:49:19 +0300)

  *  AUTORUBACK-3086 Фильтрация объявлений по ставке аукциона (#1329)
     
     * AUTORUBACK-3086 Add an index table for offer auction bids
     
     * AUTORUBACK-3086 Add a consumer for auction bids log
     
     * AUTORUBACK-3086 Filter offers by auction bid
     
     * AUTORUBACK-3086 Check auction bid index in AutoruOfferDaoImplTest
     
     * AUTORUBACK-3086 Fix a test
     
     * AUTORUBACK-3086 Fix auction handling in OfferConverterCommon
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Use proto macro to avoid repetition
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * fixup! AUTORUBACK-3086 Replace "auction" with "calls auction" everywhere
     
     * AUTORUBACK-3086 Rename config branch and Kafka consumer group
     
     * AUTORUBACK-3086 Clean up following PR discussion
     
     * AUTORUBACK-3086 Fix auction bid event parsing
  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 28 Mar 2022 09:49:19 +0300

## vos2-autoru-ydb-workers:0.93.31 (Fri, 25 Mar 2022 16:19:10 +0300)

  *  AUTORUBACK-3108 (#1334)
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
     
     * AUTORUBACK-3108
  *  AUTORUBACK-3052 (#1333)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 25 Mar 2022 16:19:10 +0300

## vos2-autoru-ydb-workers:0.93.30 (Wed, 23 Mar 2022 15:57:07 +0300)

  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 23 Mar 2022 15:57:07 +0300

## vos2-autoru-ydb-workers:0.93.29 (Wed, 23 Mar 2022 15:18:04 +0300)

  *  AUTORUBACK-3052 (#1330)
     

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 23 Mar 2022 15:18:04 +0300

## vos2-autoru-ydb-workers:0.93.28 (Wed, 23 Mar 2022 11:40:50 +0300)

  *  AUTORUBACK-3073 (#1309)
     
     * AUTORUBACK-3073

  *  AUTORUBACK-1219_vin_in_description (#1327)
     

  *  AUTORUBACK-3077 General search endpoint for autocenter (#1321)
     
     * AUTORUBACK-3077 Add a general search endpoint for autocenter
     
     * AUTORUBACK-3077 Remove getOffersByVins etc.
     
     * AUTORUBACK-3077 Fix tests after rebase
     
     * release 0.265.14
     
     * AUTORUBACK-3077 Remove incorrect default value in API doc
     
     * AUTORUBACK-3077 Fix shard handling
     
     * AUTORUBACK-3077 Avoid a naked Int
     
     * AUTORUBACK-3077 Test the license plate filter condition
     
     * AUTORUBACK-3077 Use JSON body instead of query parameters
     
     * AUTORUBACK-3077 Fix request method
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Rename the endpoint and related methods
     
     * AUTORUBACK-3077 Update schema-registry
     
     * AUTORUBACK-3077 Set global pageSize restriction in OffersHandler
     
     * AUTORUBACK-3077 Test YDB offer DAO
     
     * AUTORUBACK-3077 Fix trace label
     
     * AUTORUBACK-3077 Set maxPageSize to 1000 by default
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 23 Mar 2022 11:40:50 +0300

## vos2-autoru-ydb-workers:0.93.27 (Mon, 21 Mar 2022 13:57:08 +0300)

  *  AUTORUBACK-3052 (#1324)
     
     * AUTORUBACK-3052
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 21 Mar 2022 13:57:08 +0300

## vos2-autoru-ydb-workers:0.93.26 (Mon, 21 Mar 2022 12:25:16 +0300)

  *  AUTORUBACK-3092

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 21 Mar 2022 12:25:16 +0300

## vos2-autoru-ydb-workers:0.93.25 (Fri, 18 Mar 2022 17:30:10 +0300)

  *  AUTORUBACK-3107 (#1323)
     

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 18 Mar 2022 17:30:10 +0300

## vos2-autoru-ydb-workers:0.93.24 (Thu, 17 Mar 2022 16:49:03 +0300)

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Mar 2022 16:49:03 +0300

## vos2-autoru-ydb-workers:0.93.23 (Thu, 17 Mar 2022 16:12:28 +0300)

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Mar 2022 16:12:28 +0300

## vos2-autoru-ydb-workers:0.93.22 (Thu, 17 Mar 2022 14:45:29 +0300)

  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Mar 2022 14:45:29 +0300

## vos2-autoru-ydb-workers:0.93.21 (Thu, 17 Mar 2022 11:32:42 +0300)

  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Mar 2022 11:32:42 +0300

## vos2-autoru-ydb-workers:0.93.20 (Wed, 16 Mar 2022 16:29:32 +0300)

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 16 Mar 2022 16:29:32 +0300

## vos2-autoru-ydb-workers:0.93.19 (Wed, 16 Mar 2022 16:18:56 +0300)

  *  AUTORUBACK-3091 Fix hash field (#1318)
     

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 16 Mar 2022 16:18:56 +0300

## vos2-autoru-ydb-workers:0.93.18 (Wed, 16 Mar 2022 14:40:35 +0300)

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 16 Mar 2022 14:40:35 +0300

## vos2-autoru-ydb-workers:0.93.17 (Tue, 15 Mar 2022 16:19:16 +0300)

  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 15 Mar 2022 16:19:16 +0300

## vos2-autoru-ydb-workers:0.93.16 (Tue, 15 Mar 2022 14:57:36 +0300)

  *  fix

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 15 Mar 2022 14:57:36 +0300

## vos2-autoru-ydb-workers:0.93.15 (Tue, 15 Mar 2022 14:34:59 +0300)

  *  fix

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 15 Mar 2022 14:34:59 +0300

## vos2-autoru-ydb-workers:0.93.14 (Tue, 15 Mar 2022 13:20:25 +0300)

  *  AUTORUBACK-3062 (#1314)
     
     * AUTORUBACK-3062
     
     * AUTORUBACK-3062
  *  recall reason fix

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 15 Mar 2022 13:20:25 +0300

## vos2-autoru-ydb-workers:0.93.13 (Mon, 14 Mar 2022 12:20:16 +0300)

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 14 Mar 2022 12:20:16 +0300

## vos2-autoru-ydb-workers:0.93.12 (Fri, 11 Mar 2022 09:20:50 +0300)

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 11 Mar 2022 09:20:50 +0300

## vos2-autoru-ydb-workers:0.93.11 (Thu, 10 Mar 2022 14:01:44 +0300)

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 10 Mar 2022 14:01:44 +0300

## vos2-autoru-ydb-workers:0.93.10 (Sat, 05 Mar 2022 14:54:30 +0300)

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 05 Mar 2022 14:54:30 +0300

## vos2-autoru-ydb-workers:0.93.9 (Sat, 05 Mar 2022 11:46:36 +0300)

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 05 Mar 2022 11:46:36 +0300

## vos2-autoru-ydb-workers:0.93.8 (Sat, 05 Mar 2022 10:03:51 +0300)

  *  increased blur rate limit

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 05 Mar 2022 10:03:51 +0300

## vos2-autoru-ydb-workers:0.93.7 (Fri, 04 Mar 2022 17:09:35 +0300)

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3035 (#1305)
     

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 04 Mar 2022 17:09:35 +0300

## vos2-autoru-ydb-workers:0.93.6 (Fri, 04 Mar 2022 13:40:31 +0300)

  *  AUTORUBACK-3035 (#1304)
     

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 04 Mar 2022 13:40:31 +0300

## vos2-autoru-ydb-workers:0.93.5 (Thu, 03 Mar 2022 18:24:50 +0300)

  *  AUTORUBACK-3001

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 03 Mar 2022 18:24:50 +0300

## vos2-autoru-ydb-workers:0.93.4 (Thu, 03 Mar 2022 16:55:58 +0300)

  *  AUTORUBACK-3042 allowed_user_offers_show tag (#1301)
     

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 03 Mar 2022 16:55:58 +0300

## vos2-autoru-ydb-workers:0.93.3 (Thu, 03 Mar 2022 15:50:27 +0300)

  *  AUTORUBACK-3047 (#1300)
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
     
     * AUTORUBACK-3047
  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 03 Mar 2022 15:50:27 +0300

## vos2-autoru-ydb-workers:0.93.2 (Thu, 03 Mar 2022 13:56:18 +0300)

  *  VSDEALERS-1902 remove legacy redirect conf (#1299)
     
     * VSDEALERS-1902 remove legacy redirect conf
     
     * VSDEALERS-1902 redundant feature
     
     * VSDEALERS-1902 drop feature
     
     * VSDEALERS-1902 drop feature
  *  AUTORUBACK-2854 Up schema (#1298)
     

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 03 Mar 2022 13:56:18 +0300

## vos2-autoru-ydb-workers:0.93.1 (Tue, 01 Mar 2022 17:47:29 +0300)

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 01 Mar 2022 17:47:29 +0300

## vos2-autoru-ydb-workers:0.93.0 (Mon, 28 Feb 2022 16:52:11 +0300)

## yandex-vos2-autoru-ydb-workers:0.92.6 (Mon, 28 Feb 2022 16:52:11 +0300)

  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 
  *  AUTORUBACK-3023 clear empty ecredit_precondition (#1288)
     
     * AUTORUBACK-3023 clear empty ecredit_precondition
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-3001-3 (#1287)
     
     * AUTORUBACK-3001
     
     * AUTORUBACK-3001
  *  AUTORUBACK-2965

  *  AUTORUBACK-3012 send orig sizes to searcher (#1284)
     
     * AUTORUBACK-3012 send orig sizes to searcher
     
     * AUTORUBACK-3012 send original sizes to searcher
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-3001 (#1282)
     
     * AUTORUBACK-3001
  *  AUTORUBACK-3006 (#1283)
     
     * AUTORUBACK-3006
     
     * AUTORUBACK-3006
  *  AUTORUBACK-2963_cv_hash_missing_fix (#1278)
     
     * AUTORUBACK-2963_cv_hash_missing_fix
     
     * AUTORUBACK-2963_cv_hash_missing_fix: updated rescheduling
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed picapica client metrics
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed verba and auto-von-decoder client metrics
     
     * CV-2646: xYandexReqId
  *  AUTORUBACK-2965 (#1279)
     
     * AUTORUBACK-2965

  *  AUTORUBACK-2994 (#1276)
     
     * AUTORUBACK-2994

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 28 Feb 2022 16:52:11 +0300

## yandex-vos2-autoru-ydb-workers:0.92.5 (Mon, 21 Feb 2022 15:58:47 +0300)

  *  AUTORUBACK-3023 clear empty ecredit_precondition (#1288)
     
     * AUTORUBACK-3023 clear empty ecredit_precondition
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-3001-3 (#1287)
     
     * AUTORUBACK-3001
     
     * AUTORUBACK-3001
  *  AUTORUBACK-2965

  *  AUTORUBACK-3012 send orig sizes to searcher (#1284)
     
     * AUTORUBACK-3012 send orig sizes to searcher
     
     * AUTORUBACK-3012 send original sizes to searcher
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-3001 (#1282)
     
     * AUTORUBACK-3001
  *  AUTORUBACK-3006 (#1283)
     
     * AUTORUBACK-3006
     
     * AUTORUBACK-3006
  *  AUTORUBACK-2963_cv_hash_missing_fix (#1278)
     
     * AUTORUBACK-2963_cv_hash_missing_fix
     
     * AUTORUBACK-2963_cv_hash_missing_fix: updated rescheduling
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed picapica client metrics
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed verba and auto-von-decoder client metrics
     
     * CV-2646: xYandexReqId
  *  AUTORUBACK-2965 (#1279)
     
     * AUTORUBACK-2965

  *  AUTORUBACK-2994 (#1276)
     
     * AUTORUBACK-2994

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 21 Feb 2022 15:58:47 +0300

## yandex-vos2-autoru-ydb-workers:0.92.4 (Fri, 18 Feb 2022 16:35:06 +0300)

  *  AUTORUBACK-3001-3 (#1287)
     
     * AUTORUBACK-3001
     
     * AUTORUBACK-3001
  *  AUTORUBACK-2965

  *  AUTORUBACK-3012 send orig sizes to searcher (#1284)
     
     * AUTORUBACK-3012 send orig sizes to searcher
     
     * AUTORUBACK-3012 send original sizes to searcher
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-3001 (#1282)
     
     * AUTORUBACK-3001
  *  AUTORUBACK-3006 (#1283)
     
     * AUTORUBACK-3006
     
     * AUTORUBACK-3006
  *  AUTORUBACK-2963_cv_hash_missing_fix (#1278)
     
     * AUTORUBACK-2963_cv_hash_missing_fix
     
     * AUTORUBACK-2963_cv_hash_missing_fix: updated rescheduling
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed picapica client metrics
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed verba and auto-von-decoder client metrics
     
     * CV-2646: xYandexReqId
  *  AUTORUBACK-2965 (#1279)
     
     * AUTORUBACK-2965

  *  AUTORUBACK-2994 (#1276)
     
     * AUTORUBACK-2994

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 18 Feb 2022 16:35:06 +0300

## yandex-vos2-autoru-ydb-workers:0.92.3 (Fri, 18 Feb 2022 12:43:07 +0300)

  *  AUTORUBACK-2965

  *  AUTORUBACK-3012 send orig sizes to searcher (#1284)
     
     * AUTORUBACK-3012 send orig sizes to searcher
     
     * AUTORUBACK-3012 send original sizes to searcher
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-3001 (#1282)
     
     * AUTORUBACK-3001
  *  AUTORUBACK-3006 (#1283)
     
     * AUTORUBACK-3006
     
     * AUTORUBACK-3006
  *  AUTORUBACK-2963_cv_hash_missing_fix (#1278)
     
     * AUTORUBACK-2963_cv_hash_missing_fix
     
     * AUTORUBACK-2963_cv_hash_missing_fix: updated rescheduling
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed picapica client metrics
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed verba and auto-von-decoder client metrics
     
     * CV-2646: xYandexReqId
  *  AUTORUBACK-2965 (#1279)
     
     * AUTORUBACK-2965

  *  AUTORUBACK-2994 (#1276)
     
     * AUTORUBACK-2994

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 18 Feb 2022 12:43:07 +0300

## yandex-vos2-autoru-ydb-workers:0.92.2 (Thu, 17 Feb 2022 16:02:37 +0300)

  *  AUTORUBACK-3012 send orig sizes to searcher (#1284)
     
     * AUTORUBACK-3012 send orig sizes to searcher
     
     * AUTORUBACK-3012 send original sizes to searcher
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-3001 (#1282)
     
     * AUTORUBACK-3001
  *  AUTORUBACK-3006 (#1283)
     
     * AUTORUBACK-3006
     
     * AUTORUBACK-3006
  *  AUTORUBACK-2963_cv_hash_missing_fix (#1278)
     
     * AUTORUBACK-2963_cv_hash_missing_fix
     
     * AUTORUBACK-2963_cv_hash_missing_fix: updated rescheduling
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed picapica client metrics
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed verba and auto-von-decoder client metrics
     
     * CV-2646: xYandexReqId
  *  AUTORUBACK-2965 (#1279)
     
     * AUTORUBACK-2965

  *  AUTORUBACK-2994 (#1276)
     
     * AUTORUBACK-2994

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Feb 2022 16:02:37 +0300

## yandex-vos2-autoru-ydb-workers:0.92.1 (Thu, 17 Feb 2022 15:38:54 +0300)

  *  AUTORUBACK-3001 (#1282)
     
     * AUTORUBACK-3001
  *  AUTORUBACK-3006 (#1283)
     
     * AUTORUBACK-3006
     
     * AUTORUBACK-3006
  *  AUTORUBACK-2963_cv_hash_missing_fix (#1278)
     
     * AUTORUBACK-2963_cv_hash_missing_fix
     
     * AUTORUBACK-2963_cv_hash_missing_fix: updated rescheduling
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed picapica client metrics
     
     * AUTORUBACK-2963_cv_hash_missing_fix: fixed verba and auto-von-decoder client metrics
     
     * CV-2646: xYandexReqId
  *  AUTORUBACK-2965 (#1279)
     
     * AUTORUBACK-2965

  *  AUTORUBACK-2994 (#1276)
     
     * AUTORUBACK-2994

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Feb 2022 15:38:54 +0300

## yandex-vos2-autoru-ydb-workers:0.92.0 (Mon, 14 Feb 2022 19:09:46 +0300)

  *  AUTORUBACK-2963_cv_hash_missing: updated logging (#1277)
     
     * AUTORUBACK-2963_cv_hash_missing: updated logging
     
     * AUTORUBACK-2963_cv_hash_missing: format
  *  AUTORUBACK-2936 use PriceHistory (#1275)
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 14 Feb 2022 19:09:46 +0300

## yandex-vos2-autoru-ydb-workers:0.91.3 (Fri, 11 Feb 2022 11:26:41 +0300)

  *  AUTORUBACK-2936 use PriceHistory (#1275)
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2940 Clean up following (merged) PR discussion (#1274)
     

  *  AUTORUBACK-2936 don't use empty ecredit_precondition (#1273)
     
     * AUTORUBACK-2936 don't use empty precondition
     
     * AUTORUBACK-2936 check precondition existence
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2940 Уведомление о провале повторной валидации оффера (#1271)
     
     * AUTORUBACK-2940 Parse banned revalidation settings from Bunker
     
     * AUTORUBACK-2940 Add BannedRevalidationRenderer
     
     * AUTORUBACK-2940 Convert COMPLETE_CHECK_FAILED opinions into notifications
     
     * AUTORUBACK-2940 Change message template to match templates in other renderers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 11 Feb 2022 11:26:41 +0300

## yandex-vos2-autoru-ydb-workers:0.91.2 (Fri, 11 Feb 2022 10:57:29 +0300)

  *  AUTORUBACK-2940 Clean up following (merged) PR discussion (#1274)
     

  *  AUTORUBACK-2936 don't use empty ecredit_precondition (#1273)
     
     * AUTORUBACK-2936 don't use empty precondition
     
     * AUTORUBACK-2936 check precondition existence
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2940 Уведомление о провале повторной валидации оффера (#1271)
     
     * AUTORUBACK-2940 Parse banned revalidation settings from Bunker
     
     * AUTORUBACK-2940 Add BannedRevalidationRenderer
     
     * AUTORUBACK-2940 Convert COMPLETE_CHECK_FAILED opinions into notifications
     
     * AUTORUBACK-2940 Change message template to match templates in other renderers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 11 Feb 2022 10:57:29 +0300

## yandex-vos2-autoru-ydb-workers:0.91.1 (Fri, 11 Feb 2022 10:07:29 +0300)

  *  AUTORUBACK-2936 don't use empty ecredit_precondition (#1273)
     
     * AUTORUBACK-2936 don't use empty precondition
     
     * AUTORUBACK-2936 check precondition existence
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2940 Уведомление о провале повторной валидации оффера (#1271)
     
     * AUTORUBACK-2940 Parse banned revalidation settings from Bunker
     
     * AUTORUBACK-2940 Add BannedRevalidationRenderer
     
     * AUTORUBACK-2940 Convert COMPLETE_CHECK_FAILED opinions into notifications
     
     * AUTORUBACK-2940 Change message template to match templates in other renderers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 11 Feb 2022 10:07:29 +0300

## yandex-vos2-autoru-ydb-workers:0.91.0 (Thu, 10 Feb 2022 14:55:06 +0300)

  *  AUTORUBACK-2940 Уведомление о провале повторной валидации оффера (#1271)
     
     * AUTORUBACK-2940 Parse banned revalidation settings from Bunker
     
     * AUTORUBACK-2940 Add BannedRevalidationRenderer
     
     * AUTORUBACK-2940 Convert COMPLETE_CHECK_FAILED opinions into notifications
     
     * AUTORUBACK-2940 Change message template to match templates in other renderers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 10 Feb 2022 14:55:06 +0300

## yandex-vos2-autoru-ydb-workers:0.90.3 (Thu, 10 Feb 2022 00:03:18 +0300)

  *  AUTORUBACK-2936 byOfferId -> byParams (#1272)
     
     * AUTORUBACK-2936 byOfferId -> byParams
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2917 (#1270)
     
     * AUTORUBACK-2917

  *  AUTORUBACK-1506 Allow moderators to override the autoru exclusive flag (#1266)
     
     * AUTORUBACK-1506 Allow moderators to override the autoru exclusive flag
     
     * AUTORUBACK-1506 Add tests for updating autoru_exclusive_manual_update
     
     * AUTORUBACK-1506 Bump schema-registry
  *  AUTORUBACK-2936 eCredit worker (#1265)
     
     * AUTORUBACK-2936 eCredit worker
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2973

  *  Autoruback-2973 2 (#1269)
     
     * AUTORUBACK-2973
     
     * AUTORUBACK-2973
  *  AUTORUBACK-2973 (#1268)
     
     * AUTORUBACK-2973

  *  AUTORUBACK-2923 Secure video field (#1263)
     
     * AUTORUBACK-2923 Secure video field
     
     * AUTORUBACK-2923 Fix tests
     
     * AUTORUBACK-2923 Add test
     
     * AUTORUBACK-2923 Add test
  *  AUTORUBACK-2864 (#1267)
     

  *  AUTORUBACK-2876: Set offer inactivated timestamp (#1264)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 10 Feb 2022 00:03:18 +0300

## yandex-vos2-autoru-ydb-workers:0.90.2 (Wed, 09 Feb 2022 17:06:04 +0300)

  *  AUTORUBACK-2917 (#1270)
     
     * AUTORUBACK-2917

  *  AUTORUBACK-1506 Allow moderators to override the autoru exclusive flag (#1266)
     
     * AUTORUBACK-1506 Allow moderators to override the autoru exclusive flag
     
     * AUTORUBACK-1506 Add tests for updating autoru_exclusive_manual_update
     
     * AUTORUBACK-1506 Bump schema-registry
  *  AUTORUBACK-2936 eCredit worker (#1265)
     
     * AUTORUBACK-2936 eCredit worker
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2973

  *  Autoruback-2973 2 (#1269)
     
     * AUTORUBACK-2973
     
     * AUTORUBACK-2973
  *  AUTORUBACK-2973 (#1268)
     
     * AUTORUBACK-2973

  *  AUTORUBACK-2923 Secure video field (#1263)
     
     * AUTORUBACK-2923 Secure video field
     
     * AUTORUBACK-2923 Fix tests
     
     * AUTORUBACK-2923 Add test
     
     * AUTORUBACK-2923 Add test
  *  AUTORUBACK-2864 (#1267)
     

  *  AUTORUBACK-2876: Set offer inactivated timestamp (#1264)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 09 Feb 2022 17:06:04 +0300

## yandex-vos2-autoru-ydb-workers:0.90.1 (Wed, 09 Feb 2022 11:45:37 +0300)

  *  AUTORUBACK-2936 eCredit worker (#1265)
     
     * AUTORUBACK-2936 eCredit worker
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2973

  *  Autoruback-2973 2 (#1269)
     
     * AUTORUBACK-2973
     
     * AUTORUBACK-2973
  *  AUTORUBACK-2973 (#1268)
     
     * AUTORUBACK-2973

  *  AUTORUBACK-2923 Secure video field (#1263)
     
     * AUTORUBACK-2923 Secure video field
     
     * AUTORUBACK-2923 Fix tests
     
     * AUTORUBACK-2923 Add test
     
     * AUTORUBACK-2923 Add test
  *  AUTORUBACK-2864 (#1267)
     

  *  AUTORUBACK-2876: Set offer inactivated timestamp (#1264)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 09 Feb 2022 11:45:37 +0300

## yandex-vos2-autoru-ydb-workers:0.90.0 (Mon, 07 Feb 2022 15:45:51 +0300)

  *  AUTORUBACK-2876: Set offer inactivated timestamp (#1264)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 07 Feb 2022 15:45:51 +0300

## yandex-vos2-autoru-ydb-workers:0.89.0 (Fri, 04 Feb 2022 15:11:07 +0300)

  *  AUTORUBACK-2957 (#1262)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 04 Feb 2022 15:11:07 +0300

## yandex-vos2-autoru-ydb-workers:0.88.1 (Fri, 04 Feb 2022 12:10:18 +0300)

  *  AUTORUBACK-2945 Send trusted_dealer_calls_accepted to searcher (#1261)
     

  *  VSDEALERS-1800 dealer pony full config integration (#1259)
     
     * VSDEALERS-1800 dealer pony full config integration
     
     * VSDEALERS-1800 fix dealer redir availability check
     
     * VSDEALERS-1800 minor refactoring
  *  AUTORUBACK-2700 (#1254)
     

  *  AUTORUBACK-2926 (#1258)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 04 Feb 2022 12:10:18 +0300

## yandex-vos2-autoru-ydb-workers:0.88.0 (Tue, 01 Feb 2022 15:38:00 +0300)

  *  AUTORUBACK-2700 (#1254)
     

  *  AUTORUBACK-2926 (#1258)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 01 Feb 2022 15:38:00 +0300

## yandex-vos2-autoru-ydb-workers:0.87.0 (Mon, 31 Jan 2022 14:45:21 +0300)

  *  VSDEALERSDECOMP-500 # MarketPriceOnDeactivation worker: log predictor response (#1257)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 31 Jan 2022 14:45:21 +0300

## yandex-vos2-autoru-ydb-workers:0.86.0 (Mon, 31 Jan 2022 13:32:35 +0300)

  *  #AUTORUBACK-1805 Removing of credits service (#1247)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 31 Jan 2022 13:32:35 +0300

## yandex-vos2-autoru-ydb-workers:0.85.1 (Mon, 31 Jan 2022 12:44:03 +0300)

  *  #AUTORUBACK-2918 autoru-carfax namespace support for MdsPhotoUtils (#1255)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 31 Jan 2022 12:44:03 +0300

## yandex-vos2-autoru-ydb-workers:0.85.0 (Fri, 28 Jan 2022 23:10:07 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 28 Jan 2022 23:10:07 +0300

## yandex-vos2-autoru-ydb-workers:0.84.0 (Thu, 27 Jan 2022 16:30:01 +0300)

  *  VS-1277_fix_phone_counter (#1251)
     
     * VS-1277_fix_phone_counter
     
     * VS-1277_add_test

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 27 Jan 2022 16:30:01 +0300

## yandex-vos2-autoru-ydb-workers:0.83.2 (Thu, 27 Jan 2022 10:36:29 +0300)

  *  AUTORUBACK-2901 (#1246)
     
     * AUTORUBACK-2901
  *  AUTORUBACK-2901

  *  AUTORUBACK-2901

  *  AUTORUBACK-2901 (#1245)
     

  *  AUTORUBACK-2895 (#1243)
     
     AUTORUBACK-2895

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 27 Jan 2022 10:36:29 +0300

## yandex-vos2-autoru-ydb-workers:0.83.1 (Wed, 26 Jan 2022 16:54:38 +0300)

  *  AUTORUBACK-2901

  *  AUTORUBACK-2901

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 26 Jan 2022 16:54:38 +0300

## yandex-vos2-autoru-ydb-workers:0.83.0 (Wed, 26 Jan 2022 16:19:07 +0300)

  *  AUTORUBACK-2901

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 26 Jan 2022 16:19:07 +0300

## yandex-vos2-autoru-ydb-workers:0.82.0 (Wed, 26 Jan 2022 15:47:37 +0300)

  *  AUTORUBACK-2901 (#1245)
     

  *  AUTORUBACK-2895 (#1243)
     
     AUTORUBACK-2895

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 26 Jan 2022 15:47:37 +0300

## yandex-vos2-autoru-ydb-workers:0.81.2 (Mon, 24 Jan 2022 13:09:35 +0300)

  *  AUTORUBACK-2869 (#1236)
     
     * AUTORUBACK-2869

  *  AUTORUBACK-2700 (#1237)
     
     * AUTORUBACK-2700

  *  Autoruback-2822 removed timestamp (#1240)
     
     * AUTORUBACK-2822

  *  AUTORUBACK-2069_mds_orig_getinfo (#1241)
     
     * AUTORUBACK-2069_mds_orig_getinfo
     
     * AUTORUBACK-2069_mds_orig_getinfo: format
  *  AUTORUBACK-2855 (#1238)
     
     * AUTORUBACK-2855
  *  VS-1277_add_phone_calls_counter_for_shard (#1239)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 24 Jan 2022 13:09:35 +0300

## yandex-vos2-autoru-ydb-workers:0.81.1 (Sat, 22 Jan 2022 10:39:27 +0300)

  *  AUTORUBACK-2700 (#1237)
     
     * AUTORUBACK-2700

  *  Autoruback-2822 removed timestamp (#1240)
     
     * AUTORUBACK-2822

  *  AUTORUBACK-2069_mds_orig_getinfo (#1241)
     
     * AUTORUBACK-2069_mds_orig_getinfo
     
     * AUTORUBACK-2069_mds_orig_getinfo: format
  *  AUTORUBACK-2855 (#1238)
     
     * AUTORUBACK-2855
  *  VS-1277_add_phone_calls_counter_for_shard (#1239)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 22 Jan 2022 10:39:27 +0300

## yandex-vos2-autoru-ydb-workers:0.81.0 (Fri, 21 Jan 2022 13:15:49 +0300)

  *  VS-1277_add_phone_calls_counter_for_shard (#1239)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 21 Jan 2022 13:15:49 +0300

## yandex-vos2-autoru-ydb-workers:0.80.3 (Thu, 20 Jan 2022 10:24:33 +0300)

  *  AUTORUBACK-2843_user_migration_fixes: todo (#1234)
     
     * AUTORUBACK-2843

  *  AUTORUBACK-2860-remove-old-consumers (#1235)
     
     * AUTORUBACK-2860
     
     * AUTORUBACK-2860
     
     * AUTORUBACK-2860

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 20 Jan 2022 10:24:33 +0300

## yandex-vos2-autoru-ydb-workers:0.80.2 (Tue, 18 Jan 2022 09:45:10 +0300)

  *  AUTORUBACK-2843

  *  AUTORUBACK-2843-users-migration (#1231)
     
     * AUTORUBACK-2843
     Co-authored-by: aborunov <aborunov@yandex-team.ru>
  *  AUTORUBACK-2634-drafts-zio (#1224)
     
     AUTORUBACK-2634

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 18 Jan 2022 09:45:10 +0300

## yandex-vos2-autoru-ydb-workers:0.80.1 (Tue, 18 Jan 2022 09:29:15 +0300)

  *  AUTORUBACK-2843

  *  AUTORUBACK-2843-users-migration (#1231)
     
     * AUTORUBACK-2843
     Co-authored-by: aborunov <aborunov@yandex-team.ru>
  *  AUTORUBACK-2634-drafts-zio (#1224)
     
     AUTORUBACK-2634

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 18 Jan 2022 09:29:15 +0300

## yandex-vos2-autoru-ydb-workers:0.80.0 (Mon, 17 Jan 2022 15:55:07 +0300)

  *  AUTORUBACK-2843-users-migration (#1231)
     
     * AUTORUBACK-2843
     Co-authored-by: aborunov <aborunov@yandex-team.ru>
  *  AUTORUBACK-2634-drafts-zio (#1224)
     
     AUTORUBACK-2634

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 17 Jan 2022 15:55:07 +0300

## yandex-vos2-autoru-ydb-workers:0.79.1 (Fri, 14 Jan 2022 18:58:38 +0300)

  *  AUTORUBACK-2825-blur-fixes (#1230)
     
     * AUTORUBACK-2825-blur-fixes
     
     * AUTORUBACK-2825-blur-fixes: some changes
  *  AUTORUBACK-2714 Store allow_show_offers (#1226)
     
     * AUTORUBACK-2714 Add User.allow_offers_show
     
     * AUTORUBACK-2714 Set Offer.allow_user_offers_show
     
     * AUTORUBACK-2714 Clean up following PR discussion
     
     * AUTORUBACK-2714 Update schema-registry

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 14 Jan 2022 18:58:38 +0300

## yandex-vos2-autoru-ydb-workers:0.79.0 (Fri, 14 Jan 2022 14:00:57 +0300)

  *  AUTORUBACK-2714 Store allow_show_offers (#1226)
     
     * AUTORUBACK-2714 Add User.allow_offers_show
     
     * AUTORUBACK-2714 Set Offer.allow_user_offers_show
     
     * AUTORUBACK-2714 Clean up following PR discussion
     
     * AUTORUBACK-2714 Update schema-registry

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 14 Jan 2022 14:00:57 +0300

## yandex-vos2-autoru-ydb-workers:0.78.0 (Fri, 14 Jan 2022 11:26:56 +0300)

  *  AUTORUBACK-2815 (#1228)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 14 Jan 2022 11:26:56 +0300

## yandex-vos2-autoru-ydb-workers:0.77.0 (Wed, 12 Jan 2022 17:50:57 +0300)

  *  VSDEALERSDECOMP-500 # Dont clear market_price_on_deactivation field on migration (#1227)
     

  *  AUTORUBACK-2718-photo-quality (#1219)
     
     * AUTORUBACK-2718

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 12 Jan 2022 17:50:57 +0300

## yandex-vos2-autoru-ydb-workers:0.76.0 (Wed, 29 Dec 2021 17:27:11 +0300)

  *  AUTORUBACK-2776 consumer logging (#1223)
     
     * AUTORUBACK-2776

  *  AUTORUBACK-1549 (#1222)
     
     * AUTORUBACK-1549
     
     * AUTORUBACK-1549

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 29 Dec 2021 17:27:11 +0300

## yandex-vos2-autoru-ydb-workers:0.75.0 (Wed, 29 Dec 2021 11:57:53 +0300)

  *  AUTORUBACK-1549: php migration fix

  *  AUTORUBACK-2734-wrong-time-fix (#1221)
     
     * AUTORUBACK-2734
     
     * AUTORUBACK-2734
     
     * AUTORUBACK-2734
  *  AUTORUBACK-1549 (#1220)
     

  *  AUTORUBACK-2734 wrong call time (#1218)
     
     * AUTORUBACK-2734

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 29 Dec 2021 11:57:53 +0300

## yandex-vos2-autoru-ydb-workers:0.74.2 (Mon, 27 Dec 2021 10:24:18 +0300)

  *  AUTORUBACK-1549 (#1214)
     
     * AUTORUBACK-1549
  *  AUTORUBACK-1549 (#1193)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 27 Dec 2021 10:24:18 +0300

## yandex-vos2-autoru-ydb-workers:0.74.1 (Fri, 24 Dec 2021 18:32:33 +0300)

  *  AUTORUBACK-1549 (#1214)
     
     * AUTORUBACK-1549
  *  AUTORUBACK-1549 (#1193)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 24 Dec 2021 18:32:33 +0300

## yandex-vos2-autoru-ydb-workers:0.74.0 (Mon, 20 Dec 2021 15:21:57 +0300)

  *  AUTORUBACK-1549 (#1207)
     
     * AUTORUBACK-1549
     AUTORUBACK-2674

  *  Autoruback-1679 moderation ban 2 (#1213)
     
     * AUTORUBACK-1679

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 20 Dec 2021 15:21:57 +0300

## yandex-vos2-autoru-ydb-workers:0.73.4 (Mon, 20 Dec 2021 14:18:11 +0300)

  *  AUTORUBACK-2706_editor_fixes (#1210)
     
     * AUTORUBACK-2706_editor_fixes
     
     * AUTORUBACK-2706_editor_fixes: removed rateLimiter
  *  AUTORUBACK-2730_callcenter_reseller_fix (#1212)
     
     * AUTORUBACK-2730_callcenter_reseller_fix
     
     * AUTORUBACK-2730 Fix tests
     
     Co-authored-by: aborunov <aborunov@yandex-team.ru>
  *  separate logic of multiposting statuses conversion (#1211)
     

  *  AUTORUBACK-578: Set proven owner state fix (#1209)
     

  *  AUTORUBACK-1679 (#1206)
     
     * AUTORUBACK-1679
  *  AUTORUBACK-2693 Add reseller status accepted for moderation (#1205)
     

  *  AUTORUBACK-2639: Color filter worker fix (#1208)
     

  *  AUTORUBACK-2712 Add color name for moderation (#1204)
     
     * AUTORUBACK-2712 Add color name for moderation
     
     * AUTORUBACK-2712 Refactor
     
     * AUTORUBACK-2712 Refactor
  *  AUTORUBACK-2639: Add color filter (#1203)
     

  *  VSDEALERS-1688 # Check predictor required params in worker shouldProcess section (#1201)
     
     * VSDEALERS-1688 # Check predictor required params in worker shouldProcess section
     
     * VSDEALERS-1688 # Check predictor required params in worker shouldProcess section: unit
  *  Autoruback-2711 (#1200)
     
     * AUTORUBACK-2711

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 20 Dec 2021 14:18:11 +0300

## yandex-vos2-autoru-ydb-workers:0.73.3 (Fri, 17 Dec 2021 14:16:37 +0300)

  *  separate logic of multiposting statuses conversion (#1211)
     

  *  AUTORUBACK-578: Set proven owner state fix (#1209)
     

  *  AUTORUBACK-1679 (#1206)
     
     * AUTORUBACK-1679
  *  AUTORUBACK-2693 Add reseller status accepted for moderation (#1205)
     

  *  AUTORUBACK-2639: Color filter worker fix (#1208)
     

  *  AUTORUBACK-2712 Add color name for moderation (#1204)
     
     * AUTORUBACK-2712 Add color name for moderation
     
     * AUTORUBACK-2712 Refactor
     
     * AUTORUBACK-2712 Refactor
  *  AUTORUBACK-2639: Add color filter (#1203)
     

  *  VSDEALERS-1688 # Check predictor required params in worker shouldProcess section (#1201)
     
     * VSDEALERS-1688 # Check predictor required params in worker shouldProcess section
     
     * VSDEALERS-1688 # Check predictor required params in worker shouldProcess section: unit
  *  Autoruback-2711 (#1200)
     
     * AUTORUBACK-2711

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 17 Dec 2021 14:16:37 +0300

## yandex-vos2-autoru-ydb-workers:0.73.2 (Thu, 16 Dec 2021 11:07:06 +0300)

  *  AUTORUBACK-2639: Color filter worker fix (#1208)
     

  *  AUTORUBACK-2712 Add color name for moderation (#1204)
     
     * AUTORUBACK-2712 Add color name for moderation
     
     * AUTORUBACK-2712 Refactor
     
     * AUTORUBACK-2712 Refactor
  *  AUTORUBACK-2639: Add color filter (#1203)
     

  *  VSDEALERS-1688 # Check predictor required params in worker shouldProcess section (#1201)
     
     * VSDEALERS-1688 # Check predictor required params in worker shouldProcess section
     
     * VSDEALERS-1688 # Check predictor required params in worker shouldProcess section: unit
  *  Autoruback-2711 (#1200)
     
     * AUTORUBACK-2711

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 16 Dec 2021 11:07:06 +0300

## yandex-vos2-autoru-ydb-workers:0.73.1 (Tue, 14 Dec 2021 19:49:59 +0300)

  *  AUTORUBACK-2639: Add color filter (#1203)
     

  *  VSDEALERS-1688 # Check predictor required params in worker shouldProcess section (#1201)
     
     * VSDEALERS-1688 # Check predictor required params in worker shouldProcess section
     
     * VSDEALERS-1688 # Check predictor required params in worker shouldProcess section: unit
  *  Autoruback-2711 (#1200)
     
     * AUTORUBACK-2711

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 14 Dec 2021 19:49:59 +0300

## yandex-vos2-autoru-ydb-workers:0.73.0 (Tue, 14 Dec 2021 18:15:36 +0300)

  *  VSDEALERS-1688 # Check predictor required params in worker shouldProcess section (#1201)
     
     * VSDEALERS-1688 # Check predictor required params in worker shouldProcess section
     
     * VSDEALERS-1688 # Check predictor required params in worker shouldProcess section: unit
  *  Autoruback-2711 (#1200)
     
     * AUTORUBACK-2711

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 14 Dec 2021 18:15:36 +0300

## yandex-vos2-autoru-ydb-workers:0.72.0 (Sun, 12 Dec 2021 12:31:40 +0300)

  *  VSDEALERS-1688 # Adds market price on deactivation worker in Launcher (#1199)
     
     * VSDEALERS-1688 # YdbWorker for saving car market price on offer deactivation
     
     * VSDEALERS-1688 # Save offer market price on deactivation in separate offer field
     
     * VSDEALERS-1688 # Retry delay refactoring
     
     * VSDEALERS-1688 # Already processed guard for worker
     
     * VSDEALERS-1688 # Unit tests
     
     * VSDEALERS-1688 # Unit tests
     
     * VSDEALERS-1688 # Throw error on predict price errors instead of custom retry
     
     * VSDEALERS-1688 # Log user
     
     * VSDEALERS-1688 # Adds market price on deactivation worker in Launcher

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 12 Dec 2021 12:31:40 +0300

## yandex-vos2-autoru-ydb-workers:0.71.1 (Thu, 09 Dec 2021 16:49:34 +0300)

  *  VSDEALERS-1688 # YdbWorker for saving car market price on offer deactivation (#1188)
     
     * VSDEALERS-1688 # YdbWorker for saving car market price on offer deactivation
     
     * VSDEALERS-1688 # Save offer market price on deactivation in separate offer field
     
     * VSDEALERS-1688 # Retry delay refactoring
     
     * VSDEALERS-1688 # Already processed guard for worker
     
     * VSDEALERS-1688 # Unit tests
     
     * VSDEALERS-1688 # Unit tests
     
     * VSDEALERS-1688 # Throw error on predict price errors instead of custom retry
     
     * VSDEALERS-1688 # Log user
  *  CARFAX-2203  - [Гараж] Добавить флаг "подходящий офер" в VOS offer (#1195)
     
     * CARFAX-2203  - [Гараж] Добавить флаг "подходящий офер" в VOS offer
     
     * fix
  *  AUTORUBACK-2304: Add draft list endpoint (#1183)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 09 Dec 2021 16:49:34 +0300

## yandex-vos2-autoru-ydb-workers:0.71.0 (Tue, 07 Dec 2021 16:23:35 +0300)

  *  CARFAX-2203  - [Гараж] Добавить флаг "подходящий офер" в VOS offer (#1195)
     
     * CARFAX-2203  - [Гараж] Добавить флаг "подходящий офер" в VOS offer
     
     * fix
  *  AUTORUBACK-2304: Add draft list endpoint (#1183)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 07 Dec 2021 16:23:35 +0300

## yandex-vos2-autoru-ydb-workers:0.70.1 (Mon, 06 Dec 2021 11:26:16 +0300)

  *  AUTORUBACK-2658 (#1191)
     
     * AUTORUBACK-2658
     
     * AUTORUBACK-2658
  *  Autoruback-2636 updates throttling 2 (#1189)
     
     * AUTORUBACK-2636
  *  Autoruback-2506 prod to test migrations (#1159)
     
     * AUTORUBACK-2506
  *  AUTORUBACK-2637 (#1187)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 06 Dec 2021 11:26:16 +0300

## yandex-vos2-autoru-ydb-workers:0.70.0 (Fri, 03 Dec 2021 18:02:57 +0300)

  *  AUTORUBACK-2658 (#1191)
     
     * AUTORUBACK-2658
     
     * AUTORUBACK-2658
  *  Autoruback-2636 updates throttling 2 (#1189)
     
     * AUTORUBACK-2636
  *  Autoruback-2506 prod to test migrations (#1159)
     
     * AUTORUBACK-2506
  *  AUTORUBACK-2637 (#1187)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 03 Dec 2021 18:02:57 +0300

## yandex-vos2-autoru-ydb-workers:0.69.0 (Wed, 01 Dec 2021 13:23:34 +0300)

  *  AUTORUBACK-2457_callcenter_reseller_as_protected (#1186)
     

  *  CARFAX-2033: Can view no docs offer (#1185)
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 01 Dec 2021 13:23:34 +0300

## yandex-vos2-autoru-ydb-workers:0.68.0 (Mon, 29 Nov 2021 15:43:44 +0300)

  *  AUTORUBACK-1549 (#1184)
     
     * AUTORUBACK-1549

  *  AUTORUBACK-2305 (#1182)
     
     * AUTORUBACK-2305

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 29 Nov 2021 15:43:44 +0300

## yandex-vos2-autoru-ydb-workers:0.67.2 (Thu, 25 Nov 2021 12:49:12 +0300)

  *  CARFAX-2203 - [Гараж] [Back]. Добавить флаг "подходящий офер" в VOS offer (#1179)
     
     * CARFAX-2203 - [Гараж] [Back]. Добавить флаг "подходящий офер" в VOS offer
     
     Сделал конвертацию GarageInfo
     
     * fix
     
     * fmt
     
     * fix test again
  *  VS-1211 support shard transition (#1181)
     
     * VS-1211 support shark transition
     
     * VS-1211 add is_safe_deal_disabled to builder
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2610 (#1180)
     
     * AUTORUBACK-2610
     
     * AUTORUBACK-2610
  *  Autoruback-1549 refactoring fix 2 (#1178)
     
     * AUTORUBACK-1549

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 25 Nov 2021 12:49:12 +0300

## yandex-vos2-autoru-ydb-workers:0.67.1 (Thu, 25 Nov 2021 11:41:27 +0300)

  *  CARFAX-2203 - [Гараж] [Back]. Добавить флаг "подходящий офер" в VOS offer (#1179)
     
     * CARFAX-2203 - [Гараж] [Back]. Добавить флаг "подходящий офер" в VOS offer
     
     Сделал конвертацию GarageInfo
     
     * fix
     
     * fmt
     
     * fix test again
  *  VS-1211 support shard transition (#1181)
     
     * VS-1211 support shark transition
     
     * VS-1211 add is_safe_deal_disabled to builder
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2610 (#1180)
     
     * AUTORUBACK-2610
     
     * AUTORUBACK-2610
  *  Autoruback-1549 refactoring fix 2 (#1178)
     
     * AUTORUBACK-1549

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 25 Nov 2021 11:41:27 +0300

## yandex-vos2-autoru-ydb-workers:0.67.0 (Wed, 24 Nov 2021 21:22:25 +0300)

  *  VS-1211 support shard transition (#1181)
     
     * VS-1211 support shark transition
     
     * VS-1211 add is_safe_deal_disabled to builder
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2610 (#1180)
     
     * AUTORUBACK-2610
     
     * AUTORUBACK-2610
  *  Autoruback-1549 refactoring fix 2 (#1178)
     
     * AUTORUBACK-1549

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 24 Nov 2021 21:22:25 +0300

## yandex-vos2-autoru-ydb-workers:0.66.0 (Tue, 23 Nov 2021 15:45:25 +0300)

  *  VSDEALERSDECOMP-452 ignore invalid trade-in offers (#1177)
     

  *  AUTORUBACK-1549 (#1176)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 23 Nov 2021 15:45:25 +0300

## yandex-vos2-autoru-ydb-workers:0.65.1 (Tue, 23 Nov 2021 09:38:27 +0300)

  *  AUTORUBACK-2554 (#1172)
     
     * AUTORUBACK-2554

  *  AUTORUBACK-1549 refactoring (#1173)
     
     * AUTORUBACK-1549 batch fixing
  *  AUTORUBACK-2494 create path without user (#1171)
     
     * AUTORUBACK-2494 create path without user
     
     * AUTORUBACK-2494
     
     * AUTORUBACK-2494 make fmt
     
     * AUTORUBACK-2494 make fmt
     
     * errors fix
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: DmitrySafonov <fripe@yandex-team.ru>
  *  lazy tvm fix

  *  AUTORUBACK-2520 edited by in mileage/price history (#1167)
     
     * AUTORUBACK-2520 edited by in mileage/price history
  *  VS-1145: Add some logs (#1166)
     
     * VS-1145: Add some logs

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 23 Nov 2021 09:38:27 +0300

## yandex-vos2-autoru-ydb-workers:0.65.0 (Fri, 19 Nov 2021 15:28:19 +0300)

  *  AUTORUBACK-2520 edited by in mileage/price history (#1167)
     
     * AUTORUBACK-2520 edited by in mileage/price history
  *  VS-1145: Add some logs (#1166)
     
     * VS-1145: Add some logs

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 19 Nov 2021 15:28:19 +0300

## yandex-vos2-autoru-ydb-workers:0.64.4 (Thu, 18 Nov 2021 10:22:21 +0300)

  *  fixed changelog

  *  AUTORUBACK-2480_panorama_messages_off_moto_komtrans AUTORUBACK-2537_send_ext_panorama_promo_offer_to_chat (#1170)
     
     * AUTORUBACK-2480_panorama_messages_off_moto_komtrans
     
     * AUTORUBACK-2480_panorama_messages_off_moto_komtrans: format
     
     * AUTORUBACK-2537_send_ext_panorama_promo_offer_to_chat
  *  AUTORUBACK-2563 (#1169)
     
     * AUTORUBACK-2563
  *  AUTORUBACK-1549 (#1168)
     
     * AUTORUBACK-1549
     

  *  AUTORUBACK-2512 is safe deal disabled (#1165)
     
     * AUTORUBACK-2512 is safe deal disabled
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  VS-1145: Add TVM to vs-receiver grpc service client (#1164)
     
     * VS-1145: Add TVM to vs-receiver grpc service client

  *  AUTORUBACK-2533 Fix unblur (#1162)
     
     * AUTORUBACK-2533 Fix unblur
     
     * AUTORUBACK-2533 Add prev needBlur to offer data
     
     * AUTORUBACK-2533 Refactor

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 18 Nov 2021 10:22:21 +0300

## yandex-vos2-autoru-ydb-workers:0.64.3 (Wed, 17 Nov 2021 21:14:06 +0300)

*  AUTORUBACK-2480_panorama_messages_off_moto_komtrans AUTORUBACK-2537_send_ext_panorama_promo_offer_to_chat (#1170)
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]      * AUTORUBACK-2480_panorama_messages_off_moto_komtrans
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]      * AUTORUBACK-2480_panorama_messages_off_moto_komtrans: format
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]      * AUTORUBACK-2537_send_ext_panorama_promo_offer_to_chat
   [10:09:43] :	 [Step 1/3]   *  AUTORUBACK-2563 (#1169)
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]      * AUTORUBACK-2563
   [10:09:43] :	 [Step 1/3]   *  AUTORUBACK-1549 (#1168)
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]      * AUTORUBACK-1549
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]
   [10:09:43] :	 [Step 1/3]   *  AUTORUBACK-2512 is safe deal disabled (#1165)
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]      * AUTORUBACK-2512 is safe deal disabled
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]      Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
   [10:09:43] :	 [Step 1/3]   *  VS-1145: Add TVM to vs-receiver grpc service client (#1164)
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]      * VS-1145: Add TVM to vs-receiver grpc service client
   [10:09:43] :	 [Step 1/3]
   [10:09:43] :	 [Step 1/3]   *  AUTORUBACK-2533 Fix unblur (#1162)
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]      * AUTORUBACK-2533 Fix unblur
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]      * AUTORUBACK-2533 Add prev needBlur to offer data
   [10:09:43] :	 [Step 1/3]      
   [10:09:43] :	 [Step 1/3]      * AUTORUBACK-2533 Refactor

## yandex-vos2-autoru-ydb-workers:0.64.2 (Wed, 17 Nov 2021 17:14:06 +0300)

  *  AUTORUBACK-2563 (#1169)
     
     * AUTORUBACK-2563
  *  AUTORUBACK-1549 (#1168)
     
     * AUTORUBACK-1549
     

  *  AUTORUBACK-2512 is safe deal disabled (#1165)
     
     * AUTORUBACK-2512 is safe deal disabled
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  VS-1145: Add TVM to vs-receiver grpc service client (#1164)
     
     * VS-1145: Add TVM to vs-receiver grpc service client

  *  AUTORUBACK-2533 Fix unblur (#1162)
     
     * AUTORUBACK-2533 Fix unblur
     
     * AUTORUBACK-2533 Add prev needBlur to offer data
     
     * AUTORUBACK-2533 Refactor

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 17 Nov 2021 17:14:06 +0300

## yandex-vos2-autoru-ydb-workers:0.64.1 (Wed, 17 Nov 2021 14:49:15 +0300)

  *  AUTORUBACK-1549 (#1168)
     
     * AUTORUBACK-1549
     

  *  AUTORUBACK-2512 is safe deal disabled (#1165)
     
     * AUTORUBACK-2512 is safe deal disabled
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  VS-1145: Add TVM to vs-receiver grpc service client (#1164)
     
     * VS-1145: Add TVM to vs-receiver grpc service client

  *  AUTORUBACK-2533 Fix unblur (#1162)
     
     * AUTORUBACK-2533 Fix unblur
     
     * AUTORUBACK-2533 Add prev needBlur to offer data
     
     * AUTORUBACK-2533 Refactor

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 17 Nov 2021 14:49:15 +0300

## yandex-vos2-autoru-ydb-workers:0.64.0 (Tue, 16 Nov 2021 14:54:41 +0300)

  *  VS-1145: Add TVM to vs-receiver grpc service client (#1164)
     
     * VS-1145: Add TVM to vs-receiver grpc service client

  *  AUTORUBACK-2533 Fix unblur (#1162)
     
     * AUTORUBACK-2533 Fix unblur
     
     * AUTORUBACK-2533 Add prev needBlur to offer data
     
     * AUTORUBACK-2533 Refactor

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 16 Nov 2021 14:54:41 +0300

## yandex-vos2-autoru-ydb-workers:0.63.0 (Mon, 15 Nov 2021 13:30:57 +0300)

  *  AUTORUBACK-2457_experiment_info_moderation (#1161)
     

  *  AUTORUBACK-1679 (#1160)
     
     * AUTORUBACK-1679
  *  VSDEALERS-1603 adding squashing for removed banned offers (#1155)
     
     * VSDEALERS-1603 adding squashing for removed banned offers
     
     * typo
     
     * fix tests
     
     * fix filtering
     
     * fmt
  *  Autoruback 2493 check belong (#1154)
     
     * AUTORUBACK-2493
  *  VSDEALERS-1535 - set NeedActivation for Avito and Active for Drom for enabled classifieds when multiposting turned on (#1158)
     
     * VSDEALERS-1535 - set NeedActivation for Avito and Active for Drom for enabled classifieds when multiposting turned on
     
     * VSDEALERS-1535
     
     * VSDEALERS-1535 - add tests
     
     * VSDEALERS-1535

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 15 Nov 2021 13:30:57 +0300

## yandex-vos2-autoru-ydb-workers:0.62.0 (Wed, 10 Nov 2021 19:57:28 +0300)

  *  VSDEALERS-1538 - add missing activation (#1157)
     
     * VSDEALERS-1538 - add worker for fixing not true active avito classified
     
     * VSDEALERS-1538
     
     * VSDEALERS-1538 - add tests
     
     * VSDEALERS-1538 - add mock response
     
     * VSDEALERS-1538
     
     * VSDEALERS-1538 - fix tests
     
     * VSDEALERS-1538 - add missing activation
  *  AUTORUBACK-2492 multiposting refactoring (#1153)
     
     * AUTORUBACK-2492 multiposting refactoring
  *  Merge remote-tracking branch 'origin/master'

  *  updated logging: log draft id

  *  AUTORUBACK-2401 (#1151)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 10 Nov 2021 19:57:28 +0300

## yandex-vos2-autoru-ydb-workers:0.61.0 (Thu, 04 Nov 2021 14:00:59 +0300)

  *  AUTORUBACK-1549 (#1149)
     
     * AUTORUBACK-1549
  *  AUTORUBACK-2481 (#1150)
     
     * AUTORUBACK-2481

  *  Autoruback 2401 consumers baker ydb fix (#1148)
     
     * AUTORUBACK-2401-CONSUMERS-YDB-FIX

  *  AUTORUBACK-2454 remove generation version check from should process (#1145)
     

  *  autoruback-2305 (#1144)
     
     * AUTORUBACK-2305

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 04 Nov 2021 14:00:59 +0300

## yandex-vos2-autoru-ydb-workers:0.60.2 (Tue, 02 Nov 2021 11:31:43 +0300)

  *  added operational to story photos client to enable metrics

  *  story photos client: increased timeout

  *  remove validation for alternative description (#1146)
     

  *  VERTISADMIN-27168: удаляем ссылки на dataexport.auto.ru и Amazon S3 (#1147)
     
     Удаляем:
     1) vos2.auto.export.*
     2) vos2.auto.amazon.*
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-1549 (#882)
     
     * AUTORUBACK-1549
  *  tokenDistributionFix

  *  autoruback-2401-baker-consumers (#1143)
     
     * autoruback-2401-baker-consumers 
  *  workers refactoring (#1140)
     
     * workers refactoring

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 02 Nov 2021 11:31:43 +0300

## yandex-vos2-autoru-ydb-workers:0.60.1 (Tue, 02 Nov 2021 11:16:53 +0300)

  *  remove validation for alternative description (#1146)
     

  *  VERTISADMIN-27168: удаляем ссылки на dataexport.auto.ru и Amazon S3 (#1147)
     
     Удаляем:
     1) vos2.auto.export.*
     2) vos2.auto.amazon.*
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-1549 (#882)
     
     * AUTORUBACK-1549
  *  tokenDistributionFix

  *  autoruback-2401-baker-consumers (#1143)
     
     * autoruback-2401-baker-consumers 
  *  workers refactoring (#1140)
     
     * workers refactoring

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 02 Nov 2021 11:16:53 +0300

## yandex-vos2-autoru-ydb-workers:0.60.0 (Tue, 02 Nov 2021 10:58:05 +0300)

  *  remove validation for alternative description (#1146)
     

  *  VERTISADMIN-27168: удаляем ссылки на dataexport.auto.ru и Amazon S3 (#1147)
     
     Удаляем:
     1) vos2.auto.export.*
     2) vos2.auto.amazon.*
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-1549 (#882)
     
     * AUTORUBACK-1549
  *  tokenDistributionFix

  *  autoruback-2401-baker-consumers (#1143)
     
     * autoruback-2401-baker-consumers 
  *  workers refactoring (#1140)
     
     * workers refactoring

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 02 Nov 2021 10:58:05 +0300

## yandex-vos2-autoru-ydb-workers:0.59.1 (Thu, 28 Oct 2021 18:29:43 +0300)

  *  AUTORUBACK-2454 limit vin decoder requests (#1142)
     
     * AUTORUBACK-2454 limit vin decoder requests
     
     * AUTORUBACK-2454 limit vin decoder requests

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 28 Oct 2021 18:29:43 +0300

## yandex-vos2-autoru-ydb-workers:0.59.0 (Thu, 28 Oct 2021 17:47:11 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 28 Oct 2021 17:47:11 +0300

## yandex-vos2-autoru-ydb-workers:0.58.1 (Thu, 28 Oct 2021 15:51:57 +0300)

  *  VSDEALERS-1591 - refactor MultipostingWorkerYdb (#1139)
     
     * VSDEALERS-1591 - refactor MultipostingWorkerYdb
     
     * VSDEALERS-1591
     
     * VSDEALERS-1591 - add tests
     
     * VSDEALERS-1591
  *  config fix

  *  config fix

  *  Autoruback-2401 baker consumers (#1133)
     
     * AUTORUBACK-2401
  *  AUTORUBACK-2417 send price_includes_nds to shard for moto (#1136)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 28 Oct 2021 15:51:57 +0300

## yandex-vos2-autoru-ydb-workers:0.58.0 (Wed, 27 Oct 2021 21:25:06 +0300)

  *  Autoruback-2401 baker consumers (#1133)
     
     * AUTORUBACK-2401
  *  AUTORUBACK-2417 send price_includes_nds to shard for moto (#1136)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 27 Oct 2021 21:25:06 +0300

## yandex-vos2-autoru-ydb-workers:0.57.1 (Wed, 27 Oct 2021 11:48:03 +0300)

  *  VSDEALERS-1537 - add check for changing avito status while classified activation (#1127)
     
     * VSDEALERS-1537 - add check for changing avito status while classified activation
     
     * VSDEALERS-1537 - add tests
     
     * VSDEALERS-1537 - fix updating method in tests
     
     * VSDEALERS-1537 - add logs
     
     * VSDEALERS-1537
  *  AUTORUBACK-2434_holocron_validation_fix (#1138)
     
     * AUTORUBACK-2434_holocron_validation_fix
     
     * AUTORUBACK-2434_holocron_validation_fix: fixed compilation
     
     * AUTORUBACK-2434_holocron_validation_fix: fixed compilation
     
     * AUTORUBACK-2434_holocron_validation_fix: minor changes, added test
  *  VS-1111: Add support for vasgen receiver (#1135)
     
     * VS-1111: Add support for vasgen receiver
     - it is necessary to define the variables `host` and `port` in the `auto.vasgen` config section in production and testing environment

  *  AUTORUBACK-2305-draft-id (#1137)
     
     * AUTORUBACK-2305
  *  AUTORUBACK-2395: Add editor type for moderation (#1134)
     

  *  VSDEALERS-1585 adding avitoDescription check for drafts (#1131)
     
     * VSDEALERS-1585 adding avitoDescription check for drafts + little bit of refactoring in tests

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 27 Oct 2021 11:48:03 +0300

## yandex-vos2-autoru-ydb-workers:0.57.0 (Tue, 26 Oct 2021 23:57:53 +0300)

  *  AUTORUBACK-2434_holocron_validation_fix (#1138)
     
     * AUTORUBACK-2434_holocron_validation_fix
     
     * AUTORUBACK-2434_holocron_validation_fix: fixed compilation
     
     * AUTORUBACK-2434_holocron_validation_fix: fixed compilation
     
     * AUTORUBACK-2434_holocron_validation_fix: minor changes, added test
  *  VS-1111: Add support for vasgen receiver (#1135)
     
     * VS-1111: Add support for vasgen receiver
     - it is necessary to define the variables `host` and `port` in the `auto.vasgen` config section in production and testing environment

  *  AUTORUBACK-2305-draft-id (#1137)
     
     * AUTORUBACK-2305
  *  AUTORUBACK-2395: Add editor type for moderation (#1134)
     

  *  VSDEALERS-1585 adding avitoDescription check for drafts (#1131)
     
     * VSDEALERS-1585 adding avitoDescription check for drafts + little bit of refactoring in tests

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 26 Oct 2021 23:57:53 +0300

## yandex-vos2-autoru-ydb-workers:0.56.1 (Mon, 25 Oct 2021 17:48:48 +0300)

  *  VSDLEARS-1536 - update logic in setting classified statuses (#1125)
     
     * VSDLEARS-1536 - update logic in setting classified statuses
     
     * VSDEALERS-1536 - fix test text
     
     * VSDEALERS-1536 - review + fix tests
     
     * VSDEALERS-1536 - test1
  *  VSDEALERS-1538 - add worker for fixing not true active avito classified (#1128)
     
     * VSDEALERS-1538 - add worker for fixing not true active avito classified
     
     * VSDEALERS-1538
     
     * VSDEALERS-1538 - add tests
     
     * VSDEALERS-1538 - add mock response
     
     * VSDEALERS-1538
     
     * VSDEALERS-1538 - fix tests
  *  CARFAX-2086 reseller status to model (#1132)
     

  *  Merge remote-tracking branch 'origin/master'

  *  updated feature name

  *  AUTORUBACK-2397 Add a new recall reason (#1130)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 25 Oct 2021 17:48:48 +0300

## yandex-vos2-autoru-ydb-workers:0.56.0 (Mon, 25 Oct 2021 10:59:31 +0300)

  *  VSDEALERS-1538 - add worker for fixing not true active avito classified (#1128)
     
     * VSDEALERS-1538 - add worker for fixing not true active avito classified
     
     * VSDEALERS-1538
     
     * VSDEALERS-1538 - add tests
     
     * VSDEALERS-1538 - add mock response
     
     * VSDEALERS-1538
     
     * VSDEALERS-1538 - fix tests
  *  CARFAX-2086 reseller status to model (#1132)
     

  *  Merge remote-tracking branch 'origin/master'

  *  updated feature name

  *  AUTORUBACK-2397 Add a new recall reason (#1130)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 25 Oct 2021 10:59:31 +0300

## yandex-vos2-autoru-ydb-workers:0.55.1 (Fri, 22 Oct 2021 12:45:17 +0300)

  *  validate-offer-ratelimiter (#1129)
     

  *  AUTORUBACK-2254-story-worker: fixed stories namespace

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2315_rolf_dealer_list: yet another fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 22 Oct 2021 12:45:17 +0300

## yandex-vos2-autoru-ydb-workers:0.55.0 (Wed, 20 Oct 2021 12:03:09 +0300)

  *  threads fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 20 Oct 2021 12:03:09 +0300

## yandex-vos2-autoru-ydb-workers:0.54.0 (Wed, 20 Oct 2021 09:52:25 +0300)

  *  photoPreview and photoSorting thread up (#1124)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 20 Oct 2021 09:52:25 +0300

## yandex-vos2-autoru-ydb-workers:0.53.0 (Mon, 18 Oct 2021 15:51:10 +0300)

  *  AUTORUBACK-2315_rolf_dealer_list (#1122)
     
     * AUTORUBACK-2315_rolf_dealer_list
     
     * AUTORUBACK-2315_rolf_dealer_list: fixed compilation
     
     * AUTORUBACK-2315_rolf_dealer_list: another fix
  *  AUTORUBACK-2344: Update safe-deal restrictions (#1112)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 18 Oct 2021 15:51:10 +0300

## yandex-vos2-autoru-ydb-workers:0.52.0 (Mon, 18 Oct 2021 12:33:25 +0300)

  *  Autoruback 2386 credit tag worker logging (#1121)
     
     * #AUTORUBACK-2386 Temporary logging for CreditTagWorkerYdb
     
     * #AUTORUBACK-2386 Dont reset shark monthly payment value when remigrating
     
     * #AUTORUBACK-2386 Remove temporary logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 18 Oct 2021 12:33:25 +0300

## yandex-vos2-autoru-ydb-workers:0.51.0 (Mon, 18 Oct 2021 10:47:16 +0300)

  *  #AUTORUBACK-2386 Temporary logging for CreditTagWorkerYdb (#1120)
     

  *  VSDEALERSDECOMP-276 # Multiposting photos: fix classified photos (#1117)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 18 Oct 2021 10:47:16 +0300

## yandex-vos2-autoru-ydb-workers:0.50.0 (Fri, 15 Oct 2021 17:36:32 +0300)

  *  #AUTORUBACK-2376 CreditTagWorkerYdb fix (#1118)
     
     * #AUTORUBACK-2376 CreditTagWorkerYdb fix
     
     * #AUTORUBACK-2376 EvolveWorkerYdbTest update
     
     * #AUTORUBACK-2376 EvolveWorkerYdbTest fix
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2376: fix tags

  *  AUTORUBACK-1549

  *  AUTORUBACK-2349_mds_micro_preview (#1115)
     
     * AUTORUBACK-2349_mds_micro_preview
     AUTORUBACK-2255_story_photos_to_searcher
     
     * AUTORUBACK-2349_mds_micro_preview, AUTORUBACK-2255_story_photos_to_searcher: fixed converter
  *  AUTORUBACK-2242 Allow editing the license plate once (#1113)
     
     * AUTORUBACK-2242 Allow editing the license plate once
     
     * AUTORUBACK-2242 Update license plate edit error message
     
     Co-authored-by: Sergey Kozlov <slider5@yandex-team.ru>
  *  Merge remote-tracking branch 'origin/master'

  *  updated logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 15 Oct 2021 17:36:32 +0300

## yandex-vos2-autoru-ydb-workers:0.49.9 (Thu, 14 Oct 2021 19:07:28 +0300)
* up
## yandex-vos2-autoru-ydb-workers:0.49.8 (Thu, 14 Oct 2021 19:07:28 +0300)

  *  AUTORUBACK-2349_mds_micro_preview (#1115)
     
     * AUTORUBACK-2349_mds_micro_preview
     AUTORUBACK-2255_story_photos_to_searcher
     
     * AUTORUBACK-2349_mds_micro_preview, AUTORUBACK-2255_story_photos_to_searcher: fixed converter
  *  AUTORUBACK-2242 Allow editing the license plate once (#1113)
     
     * AUTORUBACK-2242 Allow editing the license plate once
     
     * AUTORUBACK-2242 Update license plate edit error message
     
     Co-authored-by: Sergey Kozlov <slider5@yandex-team.ru>
  *  Merge remote-tracking branch 'origin/master'

  *  updated logging

  *  AUTORUBACK-2270 Set seller type in preconditions request to Shark (#1111)
     
     * AUTORUBACK-2270 Set seller type in preconitions request to Shark
     
     * AUTORUBACK-2270 Use a macro instead of the if/has*/get* combo
  *  AUTORUBACK-2254-story-worker: more fixes

  *  AUTORUBACK-2254-story-worker: minor fix

  *  Autoruback 2254 add new worker (#1110)
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2255 set param in searcher
     
     * AUTORUBACK-2255 set param in searcher
     
     * AutoruIdxRequestBuilderTest
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 add log
     
     * AUTORUBACK-2254 add log
     
     * AUTORUBACK-2254-add-new-worker: updated logging
     
     * AUTORUBACK-2254-add-new-worker: updated logging and minor refactoring
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     Co-authored-by: aborunov <aborunov@yandex-team.ru>
  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2315_rolf_cert

  *  AUTORUBACK-2299_disable_mosru (#1109)
     
     * AUTORUBACK-2299_disable_mosru
     
     * AUTORUBACK-2299_disable_mosru: minor fix
     
     * AUTORUBACK-2299_disable_mosru: minor fix 2
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

  *  AUTORUBACK-2254 add new YdbWorker (#1092)
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2255 set param in searcher
     
     * AUTORUBACK-2255 set param in searcher
     
     * AutoruIdxRequestBuilderTest
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2177 Add preview 16x9 for panorama (#1105)
     

  *  AUTORUBACK-2324 (#1107)
     

  *  PhotoPreviewWorkerYdb fix (#1106)
     

  *  Autoruback-2281 extended warranty idx (#1100)
     
     * AUTORUBACK-2281
  *  AUTORUBACK-2169_photos_add_url_to_listing (#1103)
     

  *  AUTORUBACK-2074 update shark monthly payment only if needed (#1104)
     

  *  AUTORUBACK-2074 rename shark api host keys (#1102)
     

  *  AUTORUBACK-2074 get shark_monthly_payment_rub from shark (#1097)
     

  *  VSDEALERS-1417 Добавление нового фильтра для офферов (#1095)
     
     * VSDEALERS-1417 adding new filter
     
     * VSDEALERS-1417 adding one more parameter in swagger
     
     * code review: directive change + swagger info change
     
     * added test

  *  AUTORUBACK-2295 add dates to public model (#1096)
     
     * AUTORUBACK-2295 add dates to public model
     
     * up schema
  *  AUTORUBACK-2301 (#1094)
     

  *  VSDEALERS-1413 added watcher for classified status (#1091)
     
     * VSDEALERS-1413 added watcher for classified status
     
     * code review
  *  AUTORUBACK-2275 (#1090)
     

  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1087)
     
     * Revert "Revert "Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)" (#1086)"
     
     This reverts commit 095f43d352b4e82b4800d71349a97f3720bb4af0.
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: remove logs
  *  VSDEALERS-1412 adding index table in resources (#1088)
     

  *  Autoruback 2260 (#1089)
     
     * AUTORUBACK-2260
     
     * AUTORUBACK-2260

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 14 Oct 2021 19:07:28 +0300

## yandex-vos2-autoru-ydb-workers:0.49.7 (Thu, 14 Oct 2021 08:14:10 +0300)

  *  AUTORUBACK-2270 Set seller type in preconditions request to Shark (#1111)
     
     * AUTORUBACK-2270 Set seller type in preconitions request to Shark
     
     * AUTORUBACK-2270 Use a macro instead of the if/has*/get* combo
  *  AUTORUBACK-2254-story-worker: more fixes

  *  AUTORUBACK-2254-story-worker: minor fix

  *  Autoruback 2254 add new worker (#1110)
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2255 set param in searcher
     
     * AUTORUBACK-2255 set param in searcher
     
     * AutoruIdxRequestBuilderTest
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 add log
     
     * AUTORUBACK-2254 add log
     
     * AUTORUBACK-2254-add-new-worker: updated logging
     
     * AUTORUBACK-2254-add-new-worker: updated logging and minor refactoring
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     Co-authored-by: aborunov <aborunov@yandex-team.ru>
  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2315_rolf_cert

  *  AUTORUBACK-2299_disable_mosru (#1109)
     
     * AUTORUBACK-2299_disable_mosru
     
     * AUTORUBACK-2299_disable_mosru: minor fix
     
     * AUTORUBACK-2299_disable_mosru: minor fix 2
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

  *  AUTORUBACK-2254 add new YdbWorker (#1092)
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2255 set param in searcher
     
     * AUTORUBACK-2255 set param in searcher
     
     * AutoruIdxRequestBuilderTest
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2177 Add preview 16x9 for panorama (#1105)
     

  *  AUTORUBACK-2324 (#1107)
     

  *  PhotoPreviewWorkerYdb fix (#1106)
     

  *  Autoruback-2281 extended warranty idx (#1100)
     
     * AUTORUBACK-2281
  *  AUTORUBACK-2169_photos_add_url_to_listing (#1103)
     

  *  AUTORUBACK-2074 update shark monthly payment only if needed (#1104)
     

  *  AUTORUBACK-2074 rename shark api host keys (#1102)
     

  *  AUTORUBACK-2074 get shark_monthly_payment_rub from shark (#1097)
     

  *  VSDEALERS-1417 Добавление нового фильтра для офферов (#1095)
     
     * VSDEALERS-1417 adding new filter
     
     * VSDEALERS-1417 adding one more parameter in swagger
     
     * code review: directive change + swagger info change
     
     * added test

  *  AUTORUBACK-2295 add dates to public model (#1096)
     
     * AUTORUBACK-2295 add dates to public model
     
     * up schema
  *  AUTORUBACK-2301 (#1094)
     

  *  VSDEALERS-1413 added watcher for classified status (#1091)
     
     * VSDEALERS-1413 added watcher for classified status
     
     * code review
  *  AUTORUBACK-2275 (#1090)
     

  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1087)
     
     * Revert "Revert "Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)" (#1086)"
     
     This reverts commit 095f43d352b4e82b4800d71349a97f3720bb4af0.
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: remove logs
  *  VSDEALERS-1412 adding index table in resources (#1088)
     

  *  Autoruback 2260 (#1089)
     
     * AUTORUBACK-2260
     
     * AUTORUBACK-2260

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 14 Oct 2021 08:14:10 +0300

## yandex-vos2-autoru-ydb-workers:0.49.6 (Thu, 14 Oct 2021 07:31:40 +0300)

  *  AUTORUBACK-2270 Set seller type in preconditions request to Shark (#1111)
     
     * AUTORUBACK-2270 Set seller type in preconitions request to Shark
     
     * AUTORUBACK-2270 Use a macro instead of the if/has*/get* combo
  *  AUTORUBACK-2254-story-worker: more fixes

  *  AUTORUBACK-2254-story-worker: minor fix

  *  Autoruback 2254 add new worker (#1110)
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2255 set param in searcher
     
     * AUTORUBACK-2255 set param in searcher
     
     * AutoruIdxRequestBuilderTest
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 add log
     
     * AUTORUBACK-2254 add log
     
     * AUTORUBACK-2254-add-new-worker: updated logging
     
     * AUTORUBACK-2254-add-new-worker: updated logging and minor refactoring
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     Co-authored-by: aborunov <aborunov@yandex-team.ru>
  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2315_rolf_cert

  *  AUTORUBACK-2299_disable_mosru (#1109)
     
     * AUTORUBACK-2299_disable_mosru
     
     * AUTORUBACK-2299_disable_mosru: minor fix
     
     * AUTORUBACK-2299_disable_mosru: minor fix 2
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

  *  AUTORUBACK-2254 add new YdbWorker (#1092)
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2255 set param in searcher
     
     * AUTORUBACK-2255 set param in searcher
     
     * AutoruIdxRequestBuilderTest
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2177 Add preview 16x9 for panorama (#1105)
     

  *  AUTORUBACK-2324 (#1107)
     

  *  PhotoPreviewWorkerYdb fix (#1106)
     

  *  Autoruback-2281 extended warranty idx (#1100)
     
     * AUTORUBACK-2281
  *  AUTORUBACK-2169_photos_add_url_to_listing (#1103)
     

  *  AUTORUBACK-2074 update shark monthly payment only if needed (#1104)
     

  *  AUTORUBACK-2074 rename shark api host keys (#1102)
     

  *  AUTORUBACK-2074 get shark_monthly_payment_rub from shark (#1097)
     

  *  VSDEALERS-1417 Добавление нового фильтра для офферов (#1095)
     
     * VSDEALERS-1417 adding new filter
     
     * VSDEALERS-1417 adding one more parameter in swagger
     
     * code review: directive change + swagger info change
     
     * added test

  *  AUTORUBACK-2295 add dates to public model (#1096)
     
     * AUTORUBACK-2295 add dates to public model
     
     * up schema
  *  AUTORUBACK-2301 (#1094)
     

  *  VSDEALERS-1413 added watcher for classified status (#1091)
     
     * VSDEALERS-1413 added watcher for classified status
     
     * code review
  *  AUTORUBACK-2275 (#1090)
     

  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1087)
     
     * Revert "Revert "Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)" (#1086)"
     
     This reverts commit 095f43d352b4e82b4800d71349a97f3720bb4af0.
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: remove logs
  *  VSDEALERS-1412 adding index table in resources (#1088)
     

  *  Autoruback 2260 (#1089)
     
     * AUTORUBACK-2260
     
     * AUTORUBACK-2260

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 14 Oct 2021 07:31:40 +0300

## yandex-vos2-autoru-ydb-workers:0.49.5 (Tue, 12 Oct 2021 10:48:34 +0300)

  *  Autoruback 2254 add new worker (#1110)
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2255 set param in searcher
     
     * AUTORUBACK-2255 set param in searcher
     
     * AutoruIdxRequestBuilderTest
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 add log
     
     * AUTORUBACK-2254 add log
     
     * AUTORUBACK-2254-add-new-worker: updated logging
     
     * AUTORUBACK-2254-add-new-worker: updated logging and minor refactoring
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     Co-authored-by: aborunov <aborunov@yandex-team.ru>
  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2315_rolf_cert

  *  AUTORUBACK-2299_disable_mosru (#1109)
     
     * AUTORUBACK-2299_disable_mosru
     
     * AUTORUBACK-2299_disable_mosru: minor fix
     
     * AUTORUBACK-2299_disable_mosru: minor fix 2
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

  *  AUTORUBACK-2254 add new YdbWorker (#1092)
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2255 set param in searcher
     
     * AUTORUBACK-2255 set param in searcher
     
     * AutoruIdxRequestBuilderTest
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2177 Add preview 16x9 for panorama (#1105)
     

  *  AUTORUBACK-2324 (#1107)
     

  *  PhotoPreviewWorkerYdb fix (#1106)
     

  *  Autoruback-2281 extended warranty idx (#1100)
     
     * AUTORUBACK-2281
  *  AUTORUBACK-2169_photos_add_url_to_listing (#1103)
     

  *  AUTORUBACK-2074 update shark monthly payment only if needed (#1104)
     

  *  AUTORUBACK-2074 rename shark api host keys (#1102)
     

  *  AUTORUBACK-2074 get shark_monthly_payment_rub from shark (#1097)
     

  *  VSDEALERS-1417 Добавление нового фильтра для офферов (#1095)
     
     * VSDEALERS-1417 adding new filter
     
     * VSDEALERS-1417 adding one more parameter in swagger
     
     * code review: directive change + swagger info change
     
     * added test

  *  AUTORUBACK-2295 add dates to public model (#1096)
     
     * AUTORUBACK-2295 add dates to public model
     
     * up schema
  *  AUTORUBACK-2301 (#1094)
     

  *  VSDEALERS-1413 added watcher for classified status (#1091)
     
     * VSDEALERS-1413 added watcher for classified status
     
     * code review
  *  AUTORUBACK-2275 (#1090)
     

  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1087)
     
     * Revert "Revert "Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)" (#1086)"
     
     This reverts commit 095f43d352b4e82b4800d71349a97f3720bb4af0.
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: remove logs
  *  VSDEALERS-1412 adding index table in resources (#1088)
     

  *  Autoruback 2260 (#1089)
     
     * AUTORUBACK-2260
     
     * AUTORUBACK-2260

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 12 Oct 2021 10:48:34 +0300

## yandex-vos2-autoru-ydb-workers:0.49.4 (Mon, 11 Oct 2021 13:42:31 +0300)

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2315_rolf_cert

  *  AUTORUBACK-2299_disable_mosru (#1109)
     
     * AUTORUBACK-2299_disable_mosru
     
     * AUTORUBACK-2299_disable_mosru: minor fix
     
     * AUTORUBACK-2299_disable_mosru: minor fix 2
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

  *  AUTORUBACK-2254 add new YdbWorker (#1092)
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2254 add new YdbWorker
     
     * AUTORUBACK-2255 set param in searcher
     
     * AUTORUBACK-2255 set param in searcher
     
     * AutoruIdxRequestBuilderTest
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     * AUTORUBACK-2254 fix after review
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2177 Add preview 16x9 for panorama (#1105)
     

  *  AUTORUBACK-2324 (#1107)
     

  *  PhotoPreviewWorkerYdb fix (#1106)
     

  *  Autoruback-2281 extended warranty idx (#1100)
     
     * AUTORUBACK-2281
  *  AUTORUBACK-2169_photos_add_url_to_listing (#1103)
     

  *  AUTORUBACK-2074 update shark monthly payment only if needed (#1104)
     

  *  AUTORUBACK-2074 rename shark api host keys (#1102)
     

  *  AUTORUBACK-2074 get shark_monthly_payment_rub from shark (#1097)
     

  *  VSDEALERS-1417 Добавление нового фильтра для офферов (#1095)
     
     * VSDEALERS-1417 adding new filter
     
     * VSDEALERS-1417 adding one more parameter in swagger
     
     * code review: directive change + swagger info change
     
     * added test

  *  AUTORUBACK-2295 add dates to public model (#1096)
     
     * AUTORUBACK-2295 add dates to public model
     
     * up schema
  *  AUTORUBACK-2301 (#1094)
     

  *  VSDEALERS-1413 added watcher for classified status (#1091)
     
     * VSDEALERS-1413 added watcher for classified status
     
     * code review
  *  AUTORUBACK-2275 (#1090)
     

  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1087)
     
     * Revert "Revert "Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)" (#1086)"
     
     This reverts commit 095f43d352b4e82b4800d71349a97f3720bb4af0.
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: remove logs
  *  VSDEALERS-1412 adding index table in resources (#1088)
     

  *  Autoruback 2260 (#1089)
     
     * AUTORUBACK-2260
     
     * AUTORUBACK-2260

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 11 Oct 2021 13:42:31 +0300

## yandex-vos2-autoru-ydb-workers:0.49.3 (Thu, 07 Oct 2021 12:00:31 +0300)

  *  AUTORUBACK-2177 Add preview 16x9 for panorama (#1105)
     

  *  AUTORUBACK-2324 (#1107)
     

  *  PhotoPreviewWorkerYdb fix (#1106)
     

  *  Autoruback-2281 extended warranty idx (#1100)
     
     * AUTORUBACK-2281
  *  AUTORUBACK-2169_photos_add_url_to_listing (#1103)
     

  *  AUTORUBACK-2074 update shark monthly payment only if needed (#1104)
     

  *  AUTORUBACK-2074 rename shark api host keys (#1102)
     

  *  AUTORUBACK-2074 get shark_monthly_payment_rub from shark (#1097)
     

  *  VSDEALERS-1417 Добавление нового фильтра для офферов (#1095)
     
     * VSDEALERS-1417 adding new filter
     
     * VSDEALERS-1417 adding one more parameter in swagger
     
     * code review: directive change + swagger info change
     
     * added test

  *  AUTORUBACK-2295 add dates to public model (#1096)
     
     * AUTORUBACK-2295 add dates to public model
     
     * up schema
  *  AUTORUBACK-2301 (#1094)
     

  *  VSDEALERS-1413 added watcher for classified status (#1091)
     
     * VSDEALERS-1413 added watcher for classified status
     
     * code review
  *  AUTORUBACK-2275 (#1090)
     

  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1087)
     
     * Revert "Revert "Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)" (#1086)"
     
     This reverts commit 095f43d352b4e82b4800d71349a97f3720bb4af0.
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: remove logs
  *  VSDEALERS-1412 adding index table in resources (#1088)
     

  *  Autoruback 2260 (#1089)
     
     * AUTORUBACK-2260
     
     * AUTORUBACK-2260

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 07 Oct 2021 12:00:31 +0300

## yandex-vos2-autoru-ydb-workers:0.49.2 (Wed, 06 Oct 2021 19:06:16 +0300)

  *  PhotoPreviewWorkerYdb fix (#1106)
     

  *  Autoruback-2281 extended warranty idx (#1100)
     
     * AUTORUBACK-2281
  *  AUTORUBACK-2169_photos_add_url_to_listing (#1103)
     

  *  AUTORUBACK-2074 update shark monthly payment only if needed (#1104)
     

  *  AUTORUBACK-2074 rename shark api host keys (#1102)
     

  *  AUTORUBACK-2074 get shark_monthly_payment_rub from shark (#1097)
     

  *  VSDEALERS-1417 Добавление нового фильтра для офферов (#1095)
     
     * VSDEALERS-1417 adding new filter
     
     * VSDEALERS-1417 adding one more parameter in swagger
     
     * code review: directive change + swagger info change
     
     * added test

  *  AUTORUBACK-2295 add dates to public model (#1096)
     
     * AUTORUBACK-2295 add dates to public model
     
     * up schema
  *  AUTORUBACK-2301 (#1094)
     

  *  VSDEALERS-1413 added watcher for classified status (#1091)
     
     * VSDEALERS-1413 added watcher for classified status
     
     * code review
  *  AUTORUBACK-2275 (#1090)
     

  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1087)
     
     * Revert "Revert "Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)" (#1086)"
     
     This reverts commit 095f43d352b4e82b4800d71349a97f3720bb4af0.
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: remove logs
  *  VSDEALERS-1412 adding index table in resources (#1088)
     

  *  Autoruback 2260 (#1089)
     
     * AUTORUBACK-2260
     
     * AUTORUBACK-2260

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 06 Oct 2021 19:06:16 +0300

## yandex-vos2-autoru-ydb-workers:0.49.1 (Wed, 06 Oct 2021 10:34:04 +0300)

  *  Autoruback-2281 extended warranty idx (#1100)
     
     * AUTORUBACK-2281
  *  AUTORUBACK-2169_photos_add_url_to_listing (#1103)
     

  *  AUTORUBACK-2074 update shark monthly payment only if needed (#1104)
     

  *  AUTORUBACK-2074 rename shark api host keys (#1102)
     

  *  AUTORUBACK-2074 get shark_monthly_payment_rub from shark (#1097)
     

  *  VSDEALERS-1417 Добавление нового фильтра для офферов (#1095)
     
     * VSDEALERS-1417 adding new filter
     
     * VSDEALERS-1417 adding one more parameter in swagger
     
     * code review: directive change + swagger info change
     
     * added test

  *  AUTORUBACK-2295 add dates to public model (#1096)
     
     * AUTORUBACK-2295 add dates to public model
     
     * up schema
  *  AUTORUBACK-2301 (#1094)
     

  *  VSDEALERS-1413 added watcher for classified status (#1091)
     
     * VSDEALERS-1413 added watcher for classified status
     
     * code review
  *  AUTORUBACK-2275 (#1090)
     

  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1087)
     
     * Revert "Revert "Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)" (#1086)"
     
     This reverts commit 095f43d352b4e82b4800d71349a97f3720bb4af0.
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: remove logs
  *  VSDEALERS-1412 adding index table in resources (#1088)
     

  *  Autoruback 2260 (#1089)
     
     * AUTORUBACK-2260
     
     * AUTORUBACK-2260

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 06 Oct 2021 10:34:04 +0300

## yandex-vos2-autoru-ydb-workers:0.49.0 (Tue, 05 Oct 2021 11:33:01 +0300)

  *  AUTORUBACK-2074 update shark monthly payment only if needed (#1104)
     

  *  AUTORUBACK-2074 rename shark api host keys (#1102)
     

  *  AUTORUBACK-2074 get shark_monthly_payment_rub from shark (#1097)
     

  *  VSDEALERS-1417 Добавление нового фильтра для офферов (#1095)
     
     * VSDEALERS-1417 adding new filter
     
     * VSDEALERS-1417 adding one more parameter in swagger
     
     * code review: directive change + swagger info change
     
     * added test

  *  AUTORUBACK-2295 add dates to public model (#1096)
     
     * AUTORUBACK-2295 add dates to public model
     
     * up schema
  *  AUTORUBACK-2301 (#1094)
     

  *  VSDEALERS-1413 added watcher for classified status (#1091)
     
     * VSDEALERS-1413 added watcher for classified status
     
     * code review
  *  AUTORUBACK-2275 (#1090)
     

  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1087)
     
     * Revert "Revert "Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)" (#1086)"
     
     This reverts commit 095f43d352b4e82b4800d71349a97f3720bb4af0.
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: classified name only
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: log autoru form photos
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: merge draft
     
     * VSDEALERS-1289 # Debug photos convertiation problem: remove logs
  *  VSDEALERS-1412 adding index table in resources (#1088)
     

  *  Autoruback 2260 (#1089)
     
     * AUTORUBACK-2260
     
     * AUTORUBACK-2260

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 05 Oct 2021 11:33:01 +0300

## yandex-vos2-autoru-ydb-workers:0.48.0 (Thu, 23 Sep 2021 10:25:44 +0300)

  *  #AUTORUBACK-2172 Keep switched off options (#1070)
     
     * #AUTORUBACK-2172 Keep switched off options
     
     * #AUTORUBACK-2172 Keep switched off equpments
     
     * #AUTORUBACK-2172 Restoring of absent equipments from meta
     
     * #AUTORUBACK-2172 Revert isSuitable

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 23 Sep 2021 10:25:44 +0300

## yandex-vos2-autoru-ydb-workers:0.47.1 (Wed, 22 Sep 2021 15:11:53 +0300)

  *  AUTORUBACK-2239 Добавил в оффер тег расширенной гарантии из CarFax (#1085)
     
     * AUTORUBACK-2239 Добавил в оффер тег расширенной гарантии из CarFax
     
     * release 0.46.5
     
     * AUTORUBACK-2239 Enable VIN checks for new cars
     
     * Revert "AUTORUBACK-2239 Enable VIN checks for new cars"
     
     This reverts commit 410b0d59c8bd29f267e3f2ca5e595e532b3a39a0.
     
     * AUTORUBACK-2239 Вынес константы
     
     * AUTORUBACK-2239 Scalafmt
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  Revert "Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)" (#1086)
     
     This reverts commit 79db1d6f10f070664297bac517c268ec9146496f.
  *  AUTORUBACK-2069_tvm_for_mds: getinfo instead of get: revert

  *  Update CHANGELOG.md
  *  VSDEALERS-1290 # Multiposting: transform photos endpoints (#1075)
     
     * VSDEALERS-1290 # Multiposting: transform photos endpoints
     
     * VSDEALERS-1290 # Multiposting: transform photos endpoints: documentation
     
     * VSDEALERS-1289 # FIX swagger param draftId
     
     * VSDEALERS-1289 # update libs version
     
     * VSDEALERS-1290 # CodeReview FIX
  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)
     
     * Revert "Revert "VSDEALERS-1289 # Convert classifieds photos (#1052)" (#1079)"
     
     This reverts commit 68cf5f7e625636ade9ceb48f06b2ae614379e72f.
     
     * VSDEALERS-1289 # FIX form-offer classifieds photo convertation
  *  AUTORUBACK-2169_photos_add_url: not finished (#1082)
     
     * AUTORUBACK-2169_photos_add_url: not finished
     
     * AUTORUBACK-2169_photos_add_url
     
     * AUTORUBACK-2169_photos_add_url: format
     
     * AUTORUBACK-2169_photos_add_url: fixes
     
     * AUTORUBACK-2169_photos_add_url: fixed compilation
     
     * AUTORUBACK-2169_photos_add_url: fixed test, added feature
     
     * AUTORUBACK-2169_photos_add_url: added tests
     
     * AUTORUBACK-2169_photos_add_url: fixed compilation
     
     * AUTORUBACK-2169_photos_add_url: fixed compilation

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 22 Sep 2021 15:11:53 +0300

## yandex-vos2-autoru-ydb-workers:0.47.0 (Tue, 21 Sep 2021 14:32:06 +0300)

  *  AUTORUBACK-2069_tvm_for_mds: getinfo instead of get: revert

  *  Update CHANGELOG.md
  *  VSDEALERS-1290 # Multiposting: transform photos endpoints (#1075)
     
     * VSDEALERS-1290 # Multiposting: transform photos endpoints
     
     * VSDEALERS-1290 # Multiposting: transform photos endpoints: documentation
     
     * VSDEALERS-1289 # FIX swagger param draftId
     
     * VSDEALERS-1289 # update libs version
     
     * VSDEALERS-1290 # CodeReview FIX
  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)
     
     * Revert "Revert "VSDEALERS-1289 # Convert classifieds photos (#1052)" (#1079)"
     
     This reverts commit 68cf5f7e625636ade9ceb48f06b2ae614379e72f.
     
     * VSDEALERS-1289 # FIX form-offer classifieds photo convertation
  *  AUTORUBACK-2169_photos_add_url: not finished (#1082)
     
     * AUTORUBACK-2169_photos_add_url: not finished
     
     * AUTORUBACK-2169_photos_add_url
     
     * AUTORUBACK-2169_photos_add_url: format
     
     * AUTORUBACK-2169_photos_add_url: fixes
     
     * AUTORUBACK-2169_photos_add_url: fixed compilation
     
     * AUTORUBACK-2169_photos_add_url: fixed test, added feature
     
     * AUTORUBACK-2169_photos_add_url: added tests
     
     * AUTORUBACK-2169_photos_add_url: fixed compilation
     
     * AUTORUBACK-2169_photos_add_url: fixed compilation

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 21 Sep 2021 14:32:06 +0300

## yandex-vos2-autoru-ydb-workers:0.46.5 (Tue, 21 Sep 2021 11:40:27 +0300)

  *  AUTORUBACK-2239 Добавил в оффер тег расширенной гарантии из CarFax

  *  VSDEALERS-1290 # Multiposting: transform photos endpoints (#1075)
     
     * VSDEALERS-1290 # Multiposting: transform photos endpoints
     
     * VSDEALERS-1290 # Multiposting: transform photos endpoints: documentation
     
     * VSDEALERS-1289 # FIX swagger param draftId
     
     * VSDEALERS-1289 # update libs version
     
     * VSDEALERS-1290 # CodeReview FIX
  *  Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)
     
     * Revert "Revert "VSDEALERS-1289 # Convert classifieds photos (#1052)" (#1079)"
     
     This reverts commit 68cf5f7e625636ade9ceb48f06b2ae614379e72f.
     
     * VSDEALERS-1289 # FIX form-offer classifieds photo convertation
  *  AUTORUBACK-2169_photos_add_url: not finished (#1082)
     
     * AUTORUBACK-2169_photos_add_url: not finished
     
     * AUTORUBACK-2169_photos_add_url
     
     * AUTORUBACK-2169_photos_add_url: format
     
     * AUTORUBACK-2169_photos_add_url: fixes
     
     * AUTORUBACK-2169_photos_add_url: fixed compilation
     
     * AUTORUBACK-2169_photos_add_url: fixed test, added feature
     
     * AUTORUBACK-2169_photos_add_url: added tests
     
     * AUTORUBACK-2169_photos_add_url: fixed compilation
     
     * AUTORUBACK-2169_photos_add_url: fixed compilation
  *  AUTORUBACK-2220 proven owner from garage (#1083)
     
     * AUTORUBACK-2220 proven owner from garage
  *  AUTORUBACK-2152_autoru_expert_no_more (#1080)
     
     * AUTORUBACK-2152_autoru_expert_no_more
     
     * AUTORUBACK-2152_autoru_expert_no_more: format
     
     * AUTORUBACK-2152_autoru_expert_no_more: fixed compilation
     
     * AUTORUBACK-2152_autoru_expert_no_more: removed no longer needed test
     
     * AUTORUBACK-2152_autoru_expert_no_more: removed more tests
  *  Revert "VSDEALERS-1289 # Convert classifieds photos (#1052)" (#1079)
     
     This reverts commit 6b949273a88502a19f91f2c2ad57462b350c5031.
  *  AUTORUBACK-2224 mark/model/supergen (#1078)
     
     * AUTORUBACK-2224 mark/model/supergen + tests
  *  AUTORUBACK-1679 (#1072)
     
     * AUTORUBACK-1679
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2125 (#1067)
     
     * AUTORUBACK-2125

  *  #AUTORUBACK-2172 Keep enabled VIN_DECODER equipments (#1071)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 21 Sep 2021 11:40:27 +0300

## yandex-vos2-autoru-ydb-workers:0.46.4 (Fri, 17 Sep 2021 15:53:25 +0300)

  *  AUTORUBACK-2220 proven owner from garage (#1083)
     
     * AUTORUBACK-2220 proven owner from garage
  *  AUTORUBACK-2152_autoru_expert_no_more (#1080)
     
     * AUTORUBACK-2152_autoru_expert_no_more
     
     * AUTORUBACK-2152_autoru_expert_no_more: format
     
     * AUTORUBACK-2152_autoru_expert_no_more: fixed compilation
     
     * AUTORUBACK-2152_autoru_expert_no_more: removed no longer needed test
     
     * AUTORUBACK-2152_autoru_expert_no_more: removed more tests
  *  Revert "VSDEALERS-1289 # Convert classifieds photos (#1052)" (#1079)
     
     This reverts commit 6b949273a88502a19f91f2c2ad57462b350c5031.
  *  AUTORUBACK-2224 mark/model/supergen (#1078)
     
     * AUTORUBACK-2224 mark/model/supergen + tests
  *  AUTORUBACK-1679 (#1072)
     
     * AUTORUBACK-1679
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2125 (#1067)
     
     * AUTORUBACK-2125

  *  #AUTORUBACK-2172 Keep enabled VIN_DECODER equipments (#1071)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 17 Sep 2021 15:53:25 +0300

## yandex-vos2-autoru-ydb-workers:0.46.3 (Thu, 16 Sep 2021 17:55:52 +0300)

  *  AUTORUBACK-2152_autoru_expert_no_more (#1080)
     
     * AUTORUBACK-2152_autoru_expert_no_more
     
     * AUTORUBACK-2152_autoru_expert_no_more: format
     
     * AUTORUBACK-2152_autoru_expert_no_more: fixed compilation
     
     * AUTORUBACK-2152_autoru_expert_no_more: removed no longer needed test
     
     * AUTORUBACK-2152_autoru_expert_no_more: removed more tests
  *  Revert "VSDEALERS-1289 # Convert classifieds photos (#1052)" (#1079)
     
     This reverts commit 6b949273a88502a19f91f2c2ad57462b350c5031.
  *  AUTORUBACK-2224 mark/model/supergen (#1078)
     
     * AUTORUBACK-2224 mark/model/supergen + tests
  *  AUTORUBACK-1679 (#1072)
     
     * AUTORUBACK-1679
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2125 (#1067)
     
     * AUTORUBACK-2125

  *  #AUTORUBACK-2172 Keep enabled VIN_DECODER equipments (#1071)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 16 Sep 2021 17:55:52 +0300

## yandex-vos2-autoru-ydb-workers:0.46.2 (Tue, 14 Sep 2021 15:08:41 +0300)

  *  AUTORUBACK-1679 (#1072)
     
     * AUTORUBACK-1679
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2125 (#1067)
     
     * AUTORUBACK-2125

  *  #AUTORUBACK-2172 Keep enabled VIN_DECODER equipments (#1071)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 14 Sep 2021 15:08:41 +0300

## yandex-vos2-autoru-ydb-workers:0.46.1 (Mon, 13 Sep 2021 22:29:05 +0300)

  *  AUTORUBACK-1679 (#1072)
     
     * AUTORUBACK-1679
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2125 (#1067)
     
     * AUTORUBACK-2125

  *  #AUTORUBACK-2172 Keep enabled VIN_DECODER equipments (#1071)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 13 Sep 2021 22:29:05 +0300

## yandex-vos2-autoru-ydb-workers:0.46.0 (Mon, 13 Sep 2021 22:15:53 +0300)

  *  AUTORUBACK-1679 (#1072)
     
     * AUTORUBACK-1679
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2125 (#1067)
     
     * AUTORUBACK-2125

  *  #AUTORUBACK-2172 Keep enabled VIN_DECODER equipments (#1071)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 13 Sep 2021 22:15:53 +0300

## yandex-vos2-autoru-ydb-workers:0.45.1 (Mon, 13 Sep 2021 15:42:19 +0300)

  *  AUTORUBACK-1679 (#1072)
     
     * AUTORUBACK-1679
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-2125 (#1067)
     
     * AUTORUBACK-2125

  *  #AUTORUBACK-2172 Keep enabled VIN_DECODER equipments (#1071)
     

  *  VSDEALERS-1363 trade-in-notification check offer status (#1069)
     
     * VSDEALERS-1363 trade-in-notification check offer status
     
     * VSDEALERS-1363 send trade-in notifications about private offers only
  *  AUTORUBACK-2156 Fix allowChatsCreation default population (#1068)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 13 Sep 2021 15:42:19 +0300

## yandex-vos2-autoru-ydb-workers:0.45.0 (Fri, 10 Sep 2021 19:13:27 +0300)

  *  VSDEALERS-1363 trade-in-notification check offer status (#1069)
     
     * VSDEALERS-1363 trade-in-notification check offer status
     
     * VSDEALERS-1363 send trade-in notifications about private offers only
  *  AUTORUBACK-2156 Fix allowChatsCreation default population (#1068)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 10 Sep 2021 19:13:27 +0300

## yandex-vos2-autoru-ydb-workers:0.44.5 (Thu, 09 Sep 2021 14:47:58 +0300)

  *  AUTORUBACK-2173

  *  AUTORUBACK-2173

  *  Autoruback 2199 fix (#1066)
     
     * #AUTORUBACK-2199 VinDecoderDecider fix
     
     * #AUTORUBACK-2199 Update
  *  AUTORUBACK-2156 Add parameter canDisableChats (#1061)
     

  *  #AUTORUBACK-2199 Old options convertation when enrich from vin-decoder (#1065)
     

  *  AUTORUBACK-1691_dealer_NO_ANSWER_ban (#1064)
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban: updated test
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban: updated another test
  *  AUTORUBACK-2125 (#1063)
     
     * AUTORUBACK-2125

  *  VSDEALERS-1289 # Convert classifieds photos (#1052)
     

  *  VSDEALERS-1288 - add route for saving classified photos (#1049)
     
     * VSDEALERS-1288 - add route for saving classified photos
     
     * VSDEALERS-1288 - update doc
     
     * VSDEALERS-1288
     
     * VSDEALERS-1288 review
     
     * VSDEALERS-1288
     
     * VSDEALERS-1288 - review 2
     
     * VSDEALERS-1288 - add accuracy to log string
  *  AUTORUBACK-2173

  *  AUTORUBACK-2173 (#1060)
     

  *  AUTORUBACK-2173

  *  AUTORUBACK-2069_tvm_for_mds: getinfo instead of get (#1056)
     

  *  AUTORUBACK-2173 (#1055)
     

  *  AUTORUBACK-2125 (#1053)
     
     * AUTORUBACK-2125
  *  AUTORUBACK-2175 (#1057)
     

  *  AUTORUBACK-2174 (#1058)
     

  *  AUTORUBACK-2171 (#1054)
     

  *  AUTORUBACK-2069_tvm_for_mds: minor fix

  *  AUTORUBACK-2069_tvm_for_mds (#1051)
     
     * AUTORUBACK-2069_tvm_for_mds
     
     * AUTORUBACK-2069_tvm_for_mds: test, refactoring
     
     * AUTORUBACK-2069_tvm_for_mds: fixed tests
  *  AUTORUBACK-2137_clean_name_gallery_photo_no_verification (#1050)
     

  *  fix for workers (#1042)
     
     * fix for workers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 09 Sep 2021 14:47:58 +0300

## yandex-vos2-autoru-ydb-workers:0.44.4 (Thu, 09 Sep 2021 14:38:01 +0300)

  *  Autoruback 2199 fix (#1066)
     
     * #AUTORUBACK-2199 VinDecoderDecider fix
     
     * #AUTORUBACK-2199 Update
  *  AUTORUBACK-2156 Add parameter canDisableChats (#1061)
     

  *  #AUTORUBACK-2199 Old options convertation when enrich from vin-decoder (#1065)
     

  *  AUTORUBACK-1691_dealer_NO_ANSWER_ban (#1064)
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban: updated test
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban: updated another test
  *  AUTORUBACK-2125 (#1063)
     
     * AUTORUBACK-2125

  *  VSDEALERS-1289 # Convert classifieds photos (#1052)
     

  *  VSDEALERS-1288 - add route for saving classified photos (#1049)
     
     * VSDEALERS-1288 - add route for saving classified photos
     
     * VSDEALERS-1288 - update doc
     
     * VSDEALERS-1288
     
     * VSDEALERS-1288 review
     
     * VSDEALERS-1288
     
     * VSDEALERS-1288 - review 2
     
     * VSDEALERS-1288 - add accuracy to log string
  *  AUTORUBACK-2173

  *  AUTORUBACK-2173 (#1060)
     

  *  AUTORUBACK-2173

  *  AUTORUBACK-2069_tvm_for_mds: getinfo instead of get (#1056)
     

  *  AUTORUBACK-2173 (#1055)
     

  *  AUTORUBACK-2125 (#1053)
     
     * AUTORUBACK-2125
  *  AUTORUBACK-2175 (#1057)
     

  *  AUTORUBACK-2174 (#1058)
     

  *  AUTORUBACK-2171 (#1054)
     

  *  AUTORUBACK-2069_tvm_for_mds: minor fix

  *  AUTORUBACK-2069_tvm_for_mds (#1051)
     
     * AUTORUBACK-2069_tvm_for_mds
     
     * AUTORUBACK-2069_tvm_for_mds: test, refactoring
     
     * AUTORUBACK-2069_tvm_for_mds: fixed tests
  *  AUTORUBACK-2137_clean_name_gallery_photo_no_verification (#1050)
     

  *  fix for workers (#1042)
     
     * fix for workers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 09 Sep 2021 14:38:01 +0300

## yandex-vos2-autoru-ydb-workers:0.44.3 (Mon, 06 Sep 2021 15:54:36 +0300)

  *  AUTORUBACK-2173

  *  AUTORUBACK-2173 (#1060)
     

  *  AUTORUBACK-2173

  *  AUTORUBACK-2069_tvm_for_mds: getinfo instead of get (#1056)
     

  *  AUTORUBACK-2173 (#1055)
     

  *  AUTORUBACK-2125 (#1053)
     
     * AUTORUBACK-2125
  *  AUTORUBACK-2175 (#1057)
     

  *  AUTORUBACK-2174 (#1058)
     

  *  AUTORUBACK-2171 (#1054)
     

  *  AUTORUBACK-2069_tvm_for_mds: minor fix

  *  AUTORUBACK-2069_tvm_for_mds (#1051)
     
     * AUTORUBACK-2069_tvm_for_mds
     
     * AUTORUBACK-2069_tvm_for_mds: test, refactoring
     
     * AUTORUBACK-2069_tvm_for_mds: fixed tests
  *  AUTORUBACK-2137_clean_name_gallery_photo_no_verification (#1050)
     

  *  fix for workers (#1042)
     
     * fix for workers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 06 Sep 2021 15:54:36 +0300

## yandex-vos2-autoru-ydb-workers:0.44.2 (Mon, 06 Sep 2021 14:03:49 +0300)

  *  AUTORUBACK-2173

  *  AUTORUBACK-2069_tvm_for_mds: getinfo instead of get (#1056)
     

  *  AUTORUBACK-2173 (#1055)
     

  *  AUTORUBACK-2125 (#1053)
     
     * AUTORUBACK-2125
  *  AUTORUBACK-2175 (#1057)
     

  *  AUTORUBACK-2174 (#1058)
     

  *  AUTORUBACK-2171 (#1054)
     

  *  AUTORUBACK-2069_tvm_for_mds: minor fix

  *  AUTORUBACK-2069_tvm_for_mds (#1051)
     
     * AUTORUBACK-2069_tvm_for_mds
     
     * AUTORUBACK-2069_tvm_for_mds: test, refactoring
     
     * AUTORUBACK-2069_tvm_for_mds: fixed tests
  *  AUTORUBACK-2137_clean_name_gallery_photo_no_verification (#1050)
     

  *  fix for workers (#1042)
     
     * fix for workers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 06 Sep 2021 14:03:49 +0300

## yandex-vos2-autoru-ydb-workers:0.44.1 (Mon, 06 Sep 2021 09:24:14 +0300)

  *  AUTORUBACK-2173 (#1055)
     

  *  AUTORUBACK-2125 (#1053)
     
     * AUTORUBACK-2125
  *  AUTORUBACK-2175 (#1057)
     

  *  AUTORUBACK-2174 (#1058)
     

  *  AUTORUBACK-2171 (#1054)
     

  *  AUTORUBACK-2069_tvm_for_mds: minor fix

  *  AUTORUBACK-2069_tvm_for_mds (#1051)
     
     * AUTORUBACK-2069_tvm_for_mds
     
     * AUTORUBACK-2069_tvm_for_mds: test, refactoring
     
     * AUTORUBACK-2069_tvm_for_mds: fixed tests
  *  AUTORUBACK-2137_clean_name_gallery_photo_no_verification (#1050)
     

  *  fix for workers (#1042)
     
     * fix for workers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 06 Sep 2021 09:24:14 +0300

## yandex-vos2-autoru-ydb-workers:0.44.0 (Tue, 31 Aug 2021 08:55:10 +0300)

  *  AUTORUBACK-2137_clean_name_gallery_photo_no_verification (#1050)
     

  *  fix for workers (#1042)
     
     * fix for workers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 31 Aug 2021 08:55:10 +0300

## yandex-vos2-autoru-ydb-workers:0.43.3 (Sun, 29 Aug 2021 19:12:05 +0300)

  *  fix for workers (#1042)
     
     * fix for workers
  *  AUTORUBACK-1685 Add poi_count to pamoramas (#1046)
     

  *  AUTORUBACK-2100_new_vas_show-in-stories (#1048)
     

  *  AUTORUBACK-1862 (#1047)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 29 Aug 2021 19:12:05 +0300

## yandex-vos2-autoru-ydb-workers:0.43.2 (Fri, 27 Aug 2021 15:12:01 +0300)

  *  AUTORUBACK-1685 Add poi_count to pamoramas (#1046)
     

  *  AUTORUBACK-2100_new_vas_show-in-stories (#1048)
     

  *  AUTORUBACK-1862 (#1047)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 27 Aug 2021 15:12:01 +0300

## yandex-vos2-autoru-ydb-workers:0.43.1 (Fri, 27 Aug 2021 13:21:00 +0300)

  *  AUTORUBACK-2100_new_vas_show-in-stories (#1048)
     

  *  AUTORUBACK-1862 (#1047)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 27 Aug 2021 13:21:00 +0300

## yandex-vos2-autoru-ydb-workers:0.43.0 (Thu, 26 Aug 2021 17:11:59 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 26 Aug 2021 17:11:59 +0300

## yandex-vos2-autoru-ydb-workers:0.42.5 (Thu, 26 Aug 2021 11:38:28 +0300)

  *  VSDEALERS-1285 # Multiposting: photos for classifieds (#1045)
     

  *  VSDEALERS-1262 adding global_status to holocron models data filling (#1044)
     
     * VSDEALERS-1262 adding global_status to holocron models data filling
     
     * fix error || -> |
     
     * code review
  *  VSDEALERS-1317 add logging in trade-in-notification worker (#1043)
     
     * VSDEALERS-1317 add logging in trade-in-notification worker
     
     * VSDEALERS-1317 abandon if matching for match
     
     * VSDEALERS-1317 refine trade-in logging
  *  GapsSummary

  *  some logs

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix: set unconfirmedTimeout to 0 for all

  *  AUTORUBACK-2036_new_filters: not finished (#1037)
     
     * AUTORUBACK-2036_new_filters: not finished
     
     * AUTORUBACK-2036_new_filters: schema registry version
     
     * AUTORUBACK-2036_new_filters: schema registry fix
     
     * AUTORUBACK-2036_new_filters: updated swagger doc, updated Filters
     
     * AUTORUBACK-2036_new_filters: more code
     
     * AUTORUBACK-2036_new_filters: more code
     
     * AUTORUBACK-2036_new_filters: fixed test
     
     * AUTORUBACK-2036_new_filters: minor fix
     
     * AUTORUBACK-2036_new_filters: stable schema registry
  *  AUTORUBACK-2086 fix check create offer (#1041)
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix: compilation fix

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 26 Aug 2021 11:38:28 +0300

## yandex-vos2-autoru-ydb-workers:0.42.4 (Wed, 25 Aug 2021 18:51:38 +0300)

  *  VSDEALERS-1262 adding global_status to holocron models data filling (#1044)
     
     * VSDEALERS-1262 adding global_status to holocron models data filling
     
     * fix error || -> |
     
     * code review
  *  VSDEALERS-1317 add logging in trade-in-notification worker (#1043)
     
     * VSDEALERS-1317 add logging in trade-in-notification worker
     
     * VSDEALERS-1317 abandon if matching for match
     
     * VSDEALERS-1317 refine trade-in logging
  *  GapsSummary

  *  some logs

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix: set unconfirmedTimeout to 0 for all

  *  AUTORUBACK-2036_new_filters: not finished (#1037)
     
     * AUTORUBACK-2036_new_filters: not finished
     
     * AUTORUBACK-2036_new_filters: schema registry version
     
     * AUTORUBACK-2036_new_filters: schema registry fix
     
     * AUTORUBACK-2036_new_filters: updated swagger doc, updated Filters
     
     * AUTORUBACK-2036_new_filters: more code
     
     * AUTORUBACK-2036_new_filters: more code
     
     * AUTORUBACK-2036_new_filters: fixed test
     
     * AUTORUBACK-2036_new_filters: minor fix
     
     * AUTORUBACK-2036_new_filters: stable schema registry
  *  AUTORUBACK-2086 fix check create offer (#1041)
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix: compilation fix

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 25 Aug 2021 18:51:38 +0300

## yandex-vos2-autoru-ydb-workers:0.42.3 (Wed, 25 Aug 2021 13:39:40 +0300)

  *  VSDEALERS-1317 add logging in trade-in-notification worker (#1043)
     
     * VSDEALERS-1317 add logging in trade-in-notification worker
     
     * VSDEALERS-1317 abandon if matching for match
     
     * VSDEALERS-1317 refine trade-in logging
  *  GapsSummary

  *  some logs

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix: set unconfirmedTimeout to 0 for all

  *  AUTORUBACK-2036_new_filters: not finished (#1037)
     
     * AUTORUBACK-2036_new_filters: not finished
     
     * AUTORUBACK-2036_new_filters: schema registry version
     
     * AUTORUBACK-2036_new_filters: schema registry fix
     
     * AUTORUBACK-2036_new_filters: updated swagger doc, updated Filters
     
     * AUTORUBACK-2036_new_filters: more code
     
     * AUTORUBACK-2036_new_filters: more code
     
     * AUTORUBACK-2036_new_filters: fixed test
     
     * AUTORUBACK-2036_new_filters: minor fix
     
     * AUTORUBACK-2036_new_filters: stable schema registry
  *  AUTORUBACK-2086 fix check create offer (#1041)
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix: compilation fix

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 25 Aug 2021 13:39:40 +0300

## yandex-vos2-autoru-ydb-workers:0.42.2 (Wed, 25 Aug 2021 12:26:30 +0300)

  *  VSDEALERS-1317 add logging in trade-in-notification worker (#1043)
     
     * VSDEALERS-1317 add logging in trade-in-notification worker
     
     * VSDEALERS-1317 abandon if matching for match
     
     * VSDEALERS-1317 refine trade-in logging
  *  GapsSummary

  *  some logs

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix: set unconfirmedTimeout to 0 for all

  *  AUTORUBACK-2036_new_filters: not finished (#1037)
     
     * AUTORUBACK-2036_new_filters: not finished
     
     * AUTORUBACK-2036_new_filters: schema registry version
     
     * AUTORUBACK-2036_new_filters: schema registry fix
     
     * AUTORUBACK-2036_new_filters: updated swagger doc, updated Filters
     
     * AUTORUBACK-2036_new_filters: more code
     
     * AUTORUBACK-2036_new_filters: more code
     
     * AUTORUBACK-2036_new_filters: fixed test
     
     * AUTORUBACK-2036_new_filters: minor fix
     
     * AUTORUBACK-2036_new_filters: stable schema registry
  *  AUTORUBACK-2086 fix check create offer (#1041)
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix: compilation fix

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 25 Aug 2021 12:26:30 +0300

## yandex-vos2-autoru-ydb-workers:0.42.1 (Tue, 24 Aug 2021 16:32:03 +0300)

  *  AUTORUBACK-2036_new_filters: not finished (#1037)
     
     * AUTORUBACK-2036_new_filters: not finished
     
     * AUTORUBACK-2036_new_filters: schema registry version
     
     * AUTORUBACK-2036_new_filters: schema registry fix
     
     * AUTORUBACK-2036_new_filters: updated swagger doc, updated Filters
     
     * AUTORUBACK-2036_new_filters: more code
     
     * AUTORUBACK-2036_new_filters: more code
     
     * AUTORUBACK-2036_new_filters: fixed test
     
     * AUTORUBACK-2036_new_filters: minor fix
     
     * AUTORUBACK-2036_new_filters: stable schema registry
  *  AUTORUBACK-2086 fix check create offer (#1041)
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix: compilation fix

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 24 Aug 2021 16:32:03 +0300

## yandex-vos2-autoru-ydb-workers:0.42.0 (Tue, 24 Aug 2021 13:46:33 +0300)

  *  AUTORUBACK-2086 fix check create offer (#1041)
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 fix check create offer
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     * AUTORUBACK-2086 add test
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix: compilation fix

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 24 Aug 2021 13:46:33 +0300

## yandex-vos2-autoru-ydb-workers:0.41.1 (Fri, 20 Aug 2021 17:45:38 +0300)

  *  VSDEALERS-1196 # Log NEED_ACTIVATION flag updates (#1040)
     
     * VSDEALERS-1196 # Log NEED_ACTIVATION flag updates
  *  AUTORUBACK-1589 Make panoramas request in notify center (#1014)
     

  *  make fmt

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862 (#1032)
     
     * AUTORUBACK-1862

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 20 Aug 2021 17:45:38 +0300

## yandex-vos2-autoru-ydb-workers:0.41.0 (Fri, 20 Aug 2021 14:12:25 +0300)

  *  AUTORUBACK-1589 Make panoramas request in notify center (#1014)
     

  *  make fmt

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862 (#1032)
     
     * AUTORUBACK-1862

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 20 Aug 2021 14:12:25 +0300

## yandex-vos2-autoru-ydb-workers:0.40.1 (Thu, 19 Aug 2021 19:26:31 +0300)

  *  AUTORUBACK-1862 (#1032)
     
     * AUTORUBACK-1862

  *  rename statist counter (#1039)
     

  *  AUTORUBACK-2102_do_not_migrate_statuses: added logging

  *  AUTORUBACK-2102_do_not_migrate_statuses (#1038)
     
     * AUTORUBACK-2102_do_not_migrate_statuses
     
     * AUTORUBACK-2102_do_not_migrate_statuses: added test, minor changes
  *  #AUTORUBACK-1672 Operator support

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 19 Aug 2021 19:26:31 +0300

## yandex-vos2-autoru-ydb-workers:0.40.0 (Thu, 19 Aug 2021 17:31:26 +0300)

  *  rename statist counter (#1039)
     

  *  AUTORUBACK-2102_do_not_migrate_statuses: added logging

  *  AUTORUBACK-2102_do_not_migrate_statuses (#1038)
     
     * AUTORUBACK-2102_do_not_migrate_statuses
     
     * AUTORUBACK-2102_do_not_migrate_statuses: added test, minor changes
  *  #AUTORUBACK-1672 Operator support

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 19 Aug 2021 17:31:26 +0300

## yandex-vos2-autoru-ydb-workers:0.39.5 (Tue, 17 Aug 2021 11:41:15 +0300)

  *  FutureUtilSpec fix

  *  #AUTORUBACK-1672 Features update (#1033)
     
     * #AUTORUBACK-1672 Features update
     
     * #AUTORUBACK-1672 Features update
  *  VSDEALERS-1243 schema-registry update with new TradeInInfo type (#1031)
     
     * VSDEALERS-1243 schema-registry update with new TradeInInfo type
     
     * VSDEALERS-1243 schema-registry breaking changes
     
     * VSDEALERS-1243 more safe_deal-related breaking changes
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  #AUTORUBACK-1654 Dealer offers equipments enrichment from vin-decoder (#1022)
     
     * #AUTORUBACK-1654 Dealer offers equipments enrichment from vin-decoder
     
     * #AUTORUBACK-1654 Review fixes
     
     * #AUTORUBACK-1654 Review fixes
     
     * #AUTORUBACK-1654 Review fixes
     
     * Unused imports fix
  *  AUTORUBACK-2064_custom_dealer_address: reverted, added test (#1030)
     
     * AUTORUBACK-2064_custom_dealer_address: reverted, added test
     
     * AUTORUBACK-2064_custom_dealer_address: fixed other test
  *  AUTORUBACK-2062_allow_edit_active_unpaid_reseller_callcenter_offers (#1029)
     

  *  [AUTORUBACK-1677] app2app disable flag (#1025)
     
     * Add app2app disable flag to autoru offer and support the  same flag from common offer. WIP: schema registry needs to be updated
     
     * Update schema registry
     
     Co-authored-by: Tymur Lysenko <tymur-lysenko@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-1219 - add alternative discription to Classified (#1028)
     

  *  #AUTORUBACK-1983 Fixes (#1027)
     

  *  AUTORUBACK-2049_mod_notification_with_link (#1026)
     

  *  AUTORUBACK-2053_emodzi fixes (#1024)
     
     * AUTORUBACK-2053_emodzi fixes
     
     * AUTORUBACK-2053_emodzi fixes
  *  AUTORUBACK-1983 safe-deal consumer (#1019)
     
     * AUTORUBACK-1983 draft (need add SafeDealClient)
     
     * AUTORUBACK-1983 add safe-deal consumer
     
     * AUTORUBACK-1983 update processing and add safe-deal client
     
     * update
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2025_keep_callcenter_active (#1023)
     
     * AUTORUBACK-2025_keep_callcenter_active
     
     * AUTORUBACK-2025_keep_callcenter_active: added test
  *  AUTORUBACK-2026 (#1021)
     

  *  AUTORUBACK-2009 (#1020)
     
     * AUTORUBACK-2009
     
     * AUTORUBACK-2009
     
     Co-authored-by: Sergey Kozlov <slider5@yandex-team.ru>
  *  AUTORUBACK-2009

  *  AUTORUBACK-2009 (#1018)
     
     * AUTORUBACK-2009
     
     * AUTORUBACK-2009

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 17 Aug 2021 11:41:15 +0300

## yandex-vos2-autoru-ydb-workers:0.39.4 (Wed, 11 Aug 2021 11:29:28 +0300)

  *  AUTORUBACK-2064_custom_dealer_address: reverted, added test (#1030)
     
     * AUTORUBACK-2064_custom_dealer_address: reverted, added test
     
     * AUTORUBACK-2064_custom_dealer_address: fixed other test
  *  AUTORUBACK-2062_allow_edit_active_unpaid_reseller_callcenter_offers (#1029)
     

  *  [AUTORUBACK-1677] app2app disable flag (#1025)
     
     * Add app2app disable flag to autoru offer and support the  same flag from common offer. WIP: schema registry needs to be updated
     
     * Update schema registry
     
     Co-authored-by: Tymur Lysenko <tymur-lysenko@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-1219 - add alternative discription to Classified (#1028)
     

  *  #AUTORUBACK-1983 Fixes (#1027)
     

  *  AUTORUBACK-2049_mod_notification_with_link (#1026)
     

  *  AUTORUBACK-2053_emodzi fixes (#1024)
     
     * AUTORUBACK-2053_emodzi fixes
     
     * AUTORUBACK-2053_emodzi fixes
  *  AUTORUBACK-1983 safe-deal consumer (#1019)
     
     * AUTORUBACK-1983 draft (need add SafeDealClient)
     
     * AUTORUBACK-1983 add safe-deal consumer
     
     * AUTORUBACK-1983 update processing and add safe-deal client
     
     * update
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2025_keep_callcenter_active (#1023)
     
     * AUTORUBACK-2025_keep_callcenter_active
     
     * AUTORUBACK-2025_keep_callcenter_active: added test
  *  AUTORUBACK-2026 (#1021)
     

  *  AUTORUBACK-2009 (#1020)
     
     * AUTORUBACK-2009
     
     * AUTORUBACK-2009
     
     Co-authored-by: Sergey Kozlov <slider5@yandex-team.ru>
  *  AUTORUBACK-2009

  *  AUTORUBACK-2009 (#1018)
     
     * AUTORUBACK-2009
     
     * AUTORUBACK-2009

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 11 Aug 2021 11:29:28 +0300

## yandex-vos2-autoru-ydb-workers:0.39.3 (Fri, 30 Jul 2021 10:10:49 +0300)

  *  AUTORUBACK-2009

  *  AUTORUBACK-2009 (#1018)
     
     * AUTORUBACK-2009
     
     * AUTORUBACK-2009

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 30 Jul 2021 10:10:49 +0300

## yandex-vos2-autoru-ydb-workers:0.39.2 (Thu, 29 Jul 2021 19:24:51 +0300)

  *  AUTORUBACK-2009 (#1018)
     
     * AUTORUBACK-2009
     
     * AUTORUBACK-2009

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 29 Jul 2021 19:24:51 +0300

## yandex-vos2-autoru-ydb-workers:0.39.1 (Mon, 26 Jul 2021 12:44:29 +0300)

  *  Update CHANGELOG.md
  *  Update CHANGELOG.md
  *  Revert "Autoruback 1971 check photo callcenter (#1011)" (#1015)
     
     This reverts commit 87704649b3a57c2b92c443fe019956bacc79ae3b.
  *  do not clear deleted status when moderation update (#1013)
     

  *  [AUTORUBACK-1944] Convert offer price to rubles and clamp discount if possible (#1009)
     
     * [WIP] Convert offer price to rubles and clamp discount if possible
     
     * Inject the priceToRubConverter dependency to offerToModerationInstant
     
     * Add tests for offer to moderation instant conversion
     
     * Fix currency mappings and implement tests for offer to moderation conversion and update testcontainers versions
     
     * Remove extraneous PriceToRubConverter and generalize currency conversion when converting offer to moderation
     
     * Add info about ydb workers to readme
     
     * Update readme and remove redundat val from AutoruOfferPriceOps.maybeRubPrice
     
     Co-authored-by: Tymur Lysenko <tymur-lysenko@yandex-team.ru>
  *  Autoruback 1971 check photo callcenter (#1011)
     
     * AUTORUBACK-1971 isCallCenter check photo offer
     
     * AUTORUBACK-1971 isCallCenter check photo offer
     
     * AUTORUBACK-1971 isCallCenter check photo offer
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-1948 moderation allow update removed offers (#1012)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 26 Jul 2021 12:44:29 +0300

## yandex-vos2-autoru-ydb-workers:0.39.0 (Thu, 22 Jul 2021 17:43:06 +0300)

  * Up

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 22 Jul 2021 17:43:06 +0300

## yandex-vos2-autoru-ydb-workers:0.38.1 (Thu, 22 Jul 2021 17:43:06 +0300)

  *  [AUTORUBACK-1944] Convert offer price to rubles and clamp discount if possible (#1009)
     
     * [WIP] Convert offer price to rubles and clamp discount if possible
     
     * Inject the priceToRubConverter dependency to offerToModerationInstant
     
     * Add tests for offer to moderation instant conversion
     
     * Fix currency mappings and implement tests for offer to moderation conversion and update testcontainers versions
     
     * Remove extraneous PriceToRubConverter and generalize currency conversion when converting offer to moderation
     
     * Add info about ydb workers to readme
     
     * Update readme and remove redundat val from AutoruOfferPriceOps.maybeRubPrice
     
     Co-authored-by: Tymur Lysenko <tymur-lysenko@yandex-team.ru>
  *  Autoruback 1971 check photo callcenter (#1011)
     
     * AUTORUBACK-1971 isCallCenter check photo offer
     
     * AUTORUBACK-1971 isCallCenter check photo offer
     
     * AUTORUBACK-1971 isCallCenter check photo offer
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-1948 moderation allow update removed offers (#1012)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 22 Jul 2021 17:43:06 +0300

## yandex-vos2-autoru-ydb-workers:0.38.0 (Thu, 22 Jul 2021 11:27:53 +0300)

  *  Autoruback 1971 check photo callcenter (#1011)
     
     * AUTORUBACK-1971 isCallCenter check photo offer
     
     * AUTORUBACK-1971 isCallCenter check photo offer
     
     * AUTORUBACK-1971 isCallCenter check photo offer
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-1948 moderation allow update removed offers (#1012)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 22 Jul 2021 11:27:53 +0300

## yandex-vos2-autoru-ydb-workers:0.37.0 (Tue, 20 Jul 2021 17:33:18 +0300)

  *  AUTORUBACK-1972 delete check isCallCenter (#1010)
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-1786_app2app_back_to_chat_fix2: call source in call info properties (#1008)
     

  *  1711 consumers lost offers logging (#1007)
     

  *  1711 consumers lost offers logging (#1006)
     
     * 1711 consumers lost offers logging

  *  1711 fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 20 Jul 2021 17:33:18 +0300

## yandex-vos2-autoru-ydb-workers:0.36.5 (Fri, 16 Jul 2021 13:59:47 +0300)

  *  AUTORUBACK-1935 fix check vin resolution for section new (#1005)
     
     * AUTORUBACK-1935 fix check vin resolution for section new
  *  VSDEALERS-1114 # Update converters for tradeIn (#997)
     

  *  AUTORUBACK-1832 Rename metric (#1004)
     

  *  Autoruback 1711 fix duplication 2 (#1003)
     
     * AUTORUBACK-1711

  *  AUTORUBACK-1923 add allowed for safe deal tag (#998)
     
     * AUTORUBACK-1923 add allowed for safe deal tag
     
     * AUTORUBACK-1923 remove custom cleared check
     
     * AUTORUBACK-1923 update safe deal tag worker test
     
     * AUTORUBACK-1923 rollback CreditTagWorkerYdbTest change
     
     * AUTORUBACK-1923 add import to SafeDealTagWorkerYdbTest
     
     * AUTORUBACK-1923 update tests...
     
     * AUTORUBACK-1923 one more fix...
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-1935 allowed_for_credit for section NEW (#1000)
     
     * AUTORUBACK-1935 allowed_for_credit for section NEW
  *  AUTORUBACK-1711-fix-duplication (#1001)
     
     * AUTORUBACK-1711-fix-duplication
  *  AUTORUBACK-1832 Fix empty IDs, add metrics (#1002)
     

  *  AUTORUBACK-1832 Migrate from Java 9 method (#999)
     

  *  Autoruback 1832 reprocess panoram (#996)
     
     * AUTORUBACK-1832 Create Bypass Panorama worker
  *  Autoruback 1711 reverse migration (#973)
     
     * AUTORUBACK-1711

  *  AUTORUBACK-1786_app2app_back_to_chat_fixes (#995)
     
     * AUTORUBACK-1786_app2app_back_to_chat_fixes
     
     * AUTORUBACK-1786_app2app_back_to_chat_fixes: fixed compilation
  *  AUTORUBACK-1920 fix for daylight savings time 'gap' exception (#994)
     
     * AUTORUBACK-1920 fix for daylight savings time 'gap' exception

  *  AUTORUBACK-1817 - add TradeInApplyToNotifierWorkerYdb (#991)
     
     * AUTORUBACK-1817 - add TradeInApplyToNotifierWorkerYdb
     
     * AUTORUBACK-1817 - fix address
     
     * AUTORUBACK-1817 - fix config
     
     * AUTORUBACK-1817 - update test
     
     * AUTORUBACK-1817 - update test 2
     
     * AUTORUBACK-1817 - code review
     
     * AUTORUBACK-1817 - code review
     
     * AUTORUBACK-1817 - code review + add specificaly check grpc code on error
     
     * AUTORUBACK-1817 - add extra error grpc code
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>
  *  Autoruback 1907 workers lost offer status (#993)
     
     * AUTORUBACK-1907
  *  AUTORUBACK-1786_app2app_back_to_chat (#992)
     
     * AUTORUBACK-1786_app2app_back_to_chat
     
     * AUTORUBACK-1786_app2app_back_to_chat: format
  *  AUTORUBACK-1895 (#990)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 16 Jul 2021 13:59:47 +0300

## yandex-vos2-autoru-ydb-workers:0.36.4 (Fri, 16 Jul 2021 09:53:36 +0300)

  *  AUTORUBACK-1832 Rename metric (#1004)
     

  *  Autoruback 1711 fix duplication 2 (#1003)
     
     * AUTORUBACK-1711

  *  AUTORUBACK-1923 add allowed for safe deal tag (#998)
     
     * AUTORUBACK-1923 add allowed for safe deal tag
     
     * AUTORUBACK-1923 remove custom cleared check
     
     * AUTORUBACK-1923 update safe deal tag worker test
     
     * AUTORUBACK-1923 rollback CreditTagWorkerYdbTest change
     
     * AUTORUBACK-1923 add import to SafeDealTagWorkerYdbTest
     
     * AUTORUBACK-1923 update tests...
     
     * AUTORUBACK-1923 one more fix...
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-1935 allowed_for_credit for section NEW (#1000)
     
     * AUTORUBACK-1935 allowed_for_credit for section NEW
  *  AUTORUBACK-1711-fix-duplication (#1001)
     
     * AUTORUBACK-1711-fix-duplication
  *  AUTORUBACK-1832 Fix empty IDs, add metrics (#1002)
     

  *  AUTORUBACK-1832 Migrate from Java 9 method (#999)
     

  *  Autoruback 1832 reprocess panoram (#996)
     
     * AUTORUBACK-1832 Create Bypass Panorama worker
  *  Autoruback 1711 reverse migration (#973)
     
     * AUTORUBACK-1711

  *  AUTORUBACK-1786_app2app_back_to_chat_fixes (#995)
     
     * AUTORUBACK-1786_app2app_back_to_chat_fixes
     
     * AUTORUBACK-1786_app2app_back_to_chat_fixes: fixed compilation
  *  AUTORUBACK-1920 fix for daylight savings time 'gap' exception (#994)
     
     * AUTORUBACK-1920 fix for daylight savings time 'gap' exception

  *  AUTORUBACK-1817 - add TradeInApplyToNotifierWorkerYdb (#991)
     
     * AUTORUBACK-1817 - add TradeInApplyToNotifierWorkerYdb
     
     * AUTORUBACK-1817 - fix address
     
     * AUTORUBACK-1817 - fix config
     
     * AUTORUBACK-1817 - update test
     
     * AUTORUBACK-1817 - update test 2
     
     * AUTORUBACK-1817 - code review
     
     * AUTORUBACK-1817 - code review
     
     * AUTORUBACK-1817 - code review + add specificaly check grpc code on error
     
     * AUTORUBACK-1817 - add extra error grpc code
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>
  *  Autoruback 1907 workers lost offer status (#993)
     
     * AUTORUBACK-1907
  *  AUTORUBACK-1786_app2app_back_to_chat (#992)
     
     * AUTORUBACK-1786_app2app_back_to_chat
     
     * AUTORUBACK-1786_app2app_back_to_chat: format
  *  AUTORUBACK-1895 (#990)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 16 Jul 2021 09:53:36 +0300

## yandex-vos2-autoru-ydb-workers:0.36.3 (Thu, 15 Jul 2021 18:09:06 +0300)

  *  AUTORUBACK-1935 allowed_for_credit for section NEW (#1000)
     
     * AUTORUBACK-1935 allowed_for_credit for section NEW
  *  AUTORUBACK-1711-fix-duplication (#1001)
     
     * AUTORUBACK-1711-fix-duplication
  *  AUTORUBACK-1832 Fix empty IDs, add metrics (#1002)
     

  *  AUTORUBACK-1832 Migrate from Java 9 method (#999)
     

  *  Autoruback 1832 reprocess panoram (#996)
     
     * AUTORUBACK-1832 Create Bypass Panorama worker
  *  Autoruback 1711 reverse migration (#973)
     
     * AUTORUBACK-1711

  *  AUTORUBACK-1786_app2app_back_to_chat_fixes (#995)
     
     * AUTORUBACK-1786_app2app_back_to_chat_fixes
     
     * AUTORUBACK-1786_app2app_back_to_chat_fixes: fixed compilation
  *  AUTORUBACK-1920 fix for daylight savings time 'gap' exception (#994)
     
     * AUTORUBACK-1920 fix for daylight savings time 'gap' exception

  *  AUTORUBACK-1817 - add TradeInApplyToNotifierWorkerYdb (#991)
     
     * AUTORUBACK-1817 - add TradeInApplyToNotifierWorkerYdb
     
     * AUTORUBACK-1817 - fix address
     
     * AUTORUBACK-1817 - fix config
     
     * AUTORUBACK-1817 - update test
     
     * AUTORUBACK-1817 - update test 2
     
     * AUTORUBACK-1817 - code review
     
     * AUTORUBACK-1817 - code review
     
     * AUTORUBACK-1817 - code review + add specificaly check grpc code on error
     
     * AUTORUBACK-1817 - add extra error grpc code
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>
  *  Autoruback 1907 workers lost offer status (#993)
     
     * AUTORUBACK-1907
  *  AUTORUBACK-1786_app2app_back_to_chat (#992)
     
     * AUTORUBACK-1786_app2app_back_to_chat
     
     * AUTORUBACK-1786_app2app_back_to_chat: format
  *  AUTORUBACK-1895 (#990)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 15 Jul 2021 18:09:06 +0300

## yandex-vos2-autoru-ydb-workers:0.36.2 (Thu, 15 Jul 2021 15:42:31 +0300)

  *  AUTORUBACK-1832 Fix empty IDs, add metrics (#1002)
     

  *  AUTORUBACK-1832 Migrate from Java 9 method (#999)
     

  *  Autoruback 1832 reprocess panoram (#996)
     
     * AUTORUBACK-1832 Create Bypass Panorama worker
  *  Autoruback 1711 reverse migration (#973)
     
     * AUTORUBACK-1711

  *  AUTORUBACK-1786_app2app_back_to_chat_fixes (#995)
     
     * AUTORUBACK-1786_app2app_back_to_chat_fixes
     
     * AUTORUBACK-1786_app2app_back_to_chat_fixes: fixed compilation
  *  AUTORUBACK-1920 fix for daylight savings time 'gap' exception (#994)
     
     * AUTORUBACK-1920 fix for daylight savings time 'gap' exception

  *  AUTORUBACK-1817 - add TradeInApplyToNotifierWorkerYdb (#991)
     
     * AUTORUBACK-1817 - add TradeInApplyToNotifierWorkerYdb
     
     * AUTORUBACK-1817 - fix address
     
     * AUTORUBACK-1817 - fix config
     
     * AUTORUBACK-1817 - update test
     
     * AUTORUBACK-1817 - update test 2
     
     * AUTORUBACK-1817 - code review
     
     * AUTORUBACK-1817 - code review
     
     * AUTORUBACK-1817 - code review + add specificaly check grpc code on error
     
     * AUTORUBACK-1817 - add extra error grpc code
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>
  *  Autoruback 1907 workers lost offer status (#993)
     
     * AUTORUBACK-1907
  *  AUTORUBACK-1786_app2app_back_to_chat (#992)
     
     * AUTORUBACK-1786_app2app_back_to_chat
     
     * AUTORUBACK-1786_app2app_back_to_chat: format
  *  AUTORUBACK-1895 (#990)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 15 Jul 2021 15:42:31 +0300

## yandex-vos2-autoru-ydb-workers:0.36.1 (Wed, 14 Jul 2021 12:53:51 +0300)

  *  AUTORUBACK-1832 Migrate from Java 9 method (#999)
     

  *  Autoruback 1832 reprocess panoram (#996)
     
     * AUTORUBACK-1832 Create Bypass Panorama worker
  *  Autoruback 1711 reverse migration (#973)
     
     * AUTORUBACK-1711

  *  AUTORUBACK-1786_app2app_back_to_chat_fixes (#995)
     
     * AUTORUBACK-1786_app2app_back_to_chat_fixes
     
     * AUTORUBACK-1786_app2app_back_to_chat_fixes: fixed compilation
  *  AUTORUBACK-1920 fix for daylight savings time 'gap' exception (#994)
     
     * AUTORUBACK-1920 fix for daylight savings time 'gap' exception

  *  AUTORUBACK-1817 - add TradeInApplyToNotifierWorkerYdb (#991)
     
     * AUTORUBACK-1817 - add TradeInApplyToNotifierWorkerYdb
     
     * AUTORUBACK-1817 - fix address
     
     * AUTORUBACK-1817 - fix config
     
     * AUTORUBACK-1817 - update test
     
     * AUTORUBACK-1817 - update test 2
     
     * AUTORUBACK-1817 - code review
     
     * AUTORUBACK-1817 - code review
     
     * AUTORUBACK-1817 - code review + add specificaly check grpc code on error
     
     * AUTORUBACK-1817 - add extra error grpc code
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>
  *  Autoruback 1907 workers lost offer status (#993)
     
     * AUTORUBACK-1907
  *  AUTORUBACK-1786_app2app_back_to_chat (#992)
     
     * AUTORUBACK-1786_app2app_back_to_chat
     
     * AUTORUBACK-1786_app2app_back_to_chat: format
  *  AUTORUBACK-1895 (#990)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 14 Jul 2021 12:53:51 +0300

## yandex-vos2-autoru-ydb-workers:0.36.0 (Thu, 01 Jul 2021 19:00:15 +0300)

  *  Autoruback 1776 not prolong offer call center (#987)
     
     * AUTORUBACK-1776 fix create offer call center
     
     * AUTORUBACK-1776 fix create offer call center
     
     * AUTORUBACK-1776 fix create offer call center
     
     * AUTORUBACK-1776 add test
     
     * AUTORUBACK-1776 fix after review
     
     * AUTORUBACK-1776 fix after review
     
     * AUTORUBACK-1776 fix after review
     
     * AUTORUBACK-1776 fix after review
     
     * AUTORUBACK-1776 fix after review
     
     * AUTORUBACK-1813 add placement
     
     * AUTORUBACK-1776 add test
     
     * AUTORUBACK-1776 fix bag
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 01 Jul 2021 19:00:15 +0300

## yandex-vos2-autoru-ydb-workers:0.35.0 (Thu, 01 Jul 2021 15:14:59 +0300)

  *  AUTORUBACK-1776 fix create offer call center (#979)
     
     * AUTORUBACK-1776 fix create offer call center
     
     * AUTORUBACK-1776 fix create offer call center
     
     * AUTORUBACK-1776 fix create offer call center
     
     * AUTORUBACK-1776 add test
     
     * AUTORUBACK-1776 fix after review
     
     * AUTORUBACK-1776 fix after review
     
     * AUTORUBACK-1776 fix after review
     
     * AUTORUBACK-1776 fix after review
     
     * AUTORUBACK-1776 fix after review
     
     * AUTORUBACK-1813 add placement
     
     * AUTORUBACK-1776 add test
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: DmitrySafonov <70597019+DmitrySafonov@users.noreply.github.com>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 01 Jul 2021 15:14:59 +0300

## yandex-vos2-autoru-ydb-workers:0.34.0 (Thu, 01 Jul 2021 14:30:27 +0300)

  *  Update application.conf
     
     AUTORUBACK-1071 plaintext fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 01 Jul 2021 14:30:27 +0300

## yandex-vos2-autoru-ydb-workers:0.33.0 (Thu, 01 Jul 2021 13:03:17 +0300)

  *  AUTORUBACK-1873 fix RESELLER_CLEAN_NAME

  *  #AUTORUBACK-1871 New credit tag condition (#986)
     

  *  VSDEALERS-1089 # Fix DateTime.now for warranty expiration check (#985)
     

  *  VSDEALERS-1075 # Add logs (#983)
     

  *  AUTORUBACK-1861_moderation_consumer_fix: old db operation in try-catch (#984)
     
     * AUTORUBACK-1861_moderation_consumer_fix: old db operation in try-catch
     
     * AUTORUBACK-1861_moderation_consumer_fix: reverted ApiException NoStackTrace
     
     * AUTORUBACK-1861_moderation_consumer_fix: format
  *  AUTORUBACK-1861_consumer_metrics_update (#982)
     
     * AUTORUBACK-1861_consumer_metrics_update
     
     * AUTORUBACK-1861_consumer_metrics_update: format
  *  AUTORUBACK-1845 delete broken panorama (#980)
     
     * AUTORUBACK-1845 delete panoramas , not unpublish them

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 01 Jul 2021 13:03:17 +0300

## yandex-vos2-autoru-ydb-workers:0.32.1 (Thu, 24 Jun 2021 15:12:54 +0300)

  *  Autoruback 1071 oom (#977)
     
     AUTORUBACK-1841
     AUTORUBACK-1071
  *  AUTORUBACK-1833 # Multiposting: dont activate offer on Expired status via PreActivationStage (#978)
     
     * AUTORUBACK-1833 # Multiposting: dont activate offer on Expired status via PreActivationStage
     
     * AUTORUBACK-1833 # Dont work with Stopped and Deleted dealers
  *  VSDEALERS-962 # Update multiposting archive logic (#975)
     
     * VSDEALERS-962 # Update multiposting archive logic
     
     * VSDEALERS-962 # Use helper for changing multiposting status

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 24 Jun 2021 15:12:54 +0300

## yandex-vos2-autoru-ydb-workers:0.32.0 (Wed, 23 Jun 2021 13:49:54 +0300)

  *  AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 23 Jun 2021 13:49:54 +0300

## yandex-vos2-autoru-ydb-workers:0.31.0 (Wed, 23 Jun 2021 12:29:46 +0300)

  *  AUTORUBACK-1727 add is_reseller (#976)
     
     * AUTORUBACK-1727 add is_reseller
     
     * AUTORUBACK-1727 add is_reseller
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 23 Jun 2021 12:29:46 +0300

## yandex-vos2-autoru-ydb-workers:0.30.0 (Wed, 23 Jun 2021 09:08:15 +0300)

  *  AUTORUBACK-1812 added reschedule delay to reprocess deleted offers and delete them from indexer (#972)
     

  *  Autoruback 1693 add status update comment (#974)
     
     * AUTORUBACK-1663 add new param CheckType
     
     * AUTORUBACK-1663 fix name param CheckType
     
     * AUTORUBACK-1663 fix after review
     
     * AUTORUBACK-1663 fix after review
     
     * AUTORUBACK-1663 fix after review
     4379
     
     * AUTORUBACK-1663 fix after review
     4379
     
     * AUTORUBACK-1663 fix after review
     4379
     
     * AUTORUBACK-1663 fix after review
     4379
     
     * AUTORUBACK-1663 fix after review
     4379
     
     * AUTORUBACK-1663 fix after review
     4379
     
     * AUTORUBACK-1693 fix version schema-registry
     
     * AUTORUBACK-1693 add setStatusUpdateComment in convert
     
     * AUTORUBACK-1693 add setStatusUpdateComment in convert
     
     * AUTORUBACK-1693 add test
     
     * AUTORUBACK-1693 fix
     
     * AUTORUBACK-1693 fix
     
     * AUTORUBACK-1693 fix
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 23 Jun 2021 09:08:15 +0300

## yandex-vos2-autoru-ydb-workers:0.29.2 (Mon, 21 Jun 2021 18:49:36 +0300)

  *  AUTORUBACK-1071

  *  AUTORUBACK-1803 (#970)
     
     * AUTORUBACK-1803
  *  Autoruback 1663 add checktype (#964)
     
     * AUTORUBACK-1663 add new param CheckType
     
     * AUTORUBACK-1663 fix name param CheckType
     
     * AUTORUBACK-1663 fix after review
     
     * AUTORUBACK-1663 fix after review
     
     * AUTORUBACK-1663 fix after review
     4379
     
     * AUTORUBACK-1663 fix after review
     4379
     
     * AUTORUBACK-1663 fix after review
     4379
     
     * AUTORUBACK-1663 fix after review
     4379
     
     * AUTORUBACK-1663 fix after review
     4379
     
     * AUTORUBACK-1663 fix after review
     4379
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
  *  AUTORUBACK-1784 too strict offer merging (#971)
     
     * AUTORUBACK-1784 too strict offer merging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 21 Jun 2021 18:49:36 +0300

## yandex-vos2-autoru-ydb-workers:0.29.1 (Wed, 16 Jun 2021 11:43:44 +0300)

  *  AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 16 Jun 2021 11:43:44 +0300

## yandex-vos2-autoru-ydb-workers:0.29.0 (Wed, 16 Jun 2021 11:30:40 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 16 Jun 2021 11:30:40 +0300

## yandex-vos2-autoru-ydb-workers:0.28.0 (Wed, 16 Jun 2021 10:54:15 +0300)

  *  AUTORUBACK-1794

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 16 Jun 2021 10:54:15 +0300

## yandex-vos2-autoru-ydb-workers:0.27.2 (Tue, 15 Jun 2021 15:01:55 +0300)

  *  autoruback-1071 (#967)
     
     * AUTORUBACK-1071
  *  #AUTORUBACK-1769 CreditTag sum fix (#968)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 15 Jun 2021 15:01:55 +0300

## yandex-vos2-autoru-ydb-workers:0.27.1 (Thu, 10 Jun 2021 19:46:38 +0300)

  *  autoruback-1071 (#966)
     
     * autoruback-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 10 Jun 2021 19:46:38 +0300

## yandex-vos2-autoru-ydb-workers:0.27.0 (Tue, 08 Jun 2021 19:00:56 +0300)

  *  Autoruback 1071 workers 8 (#965)
     
     * autoruback-1071
  *  AUTORUBACK-1683_mod_notifications_critical (#963)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 08 Jun 2021 19:00:56 +0300

## yandex-vos2-autoru-ydb-workers:0.26.0 (Tue, 08 Jun 2021 15:45:33 +0300)

  *  autoruback-1071 (#962)
     
     * autoruback-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 08 Jun 2021 15:45:33 +0300

## yandex-vos2-autoru-ydb-workers:0.25.0 (Mon, 07 Jun 2021 16:25:50 +0300)

  *  autoruback-1071

  *  autoruback-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 07 Jun 2021 16:25:50 +0300

## yandex-vos2-autoru-ydb-workers:0.24.0 (Mon, 07 Jun 2021 15:05:42 +0300)

  *  Autoruback-1071 workers 6 (#920)
     
     * AUTORUBACK-1071
  *  Autoruback-1696 fix indexes (#961)
     
     * autoruback-1696
  *  delete normalized stickers (#960)
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 07 Jun 2021 15:05:42 +0300

## yandex-vos2-autoru-ydb-workers:0.23.0 (Mon, 07 Jun 2021 13:02:23 +0300)

  *  AUTORUBACK-1071-workers (#959)
     

  *  AUTORUBACK-1071-workers (#957)
     

  *  AUTORUBACK-1071-features-ydb (#956)
     

  *  Autoruback 1747 try in telepony stage (#955)
     
     * #AUTORUBACK-1747 Wrap API calls with try in TeleponyStage
     
     * #AUTORUBACK-1747 dealer-pony.plaintext = true
  *  AUTORUBACK-1684 флаг и серчтег "продает перекуп" (#954)
     

  *  VSDEALERS-480 - check both EXPIRED and INACTIVE status for hiding (#950)
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 07 Jun 2021 13:02:23 +0300

## yandex-vos2-autoru-ydb-workers:0.22.0 (Wed, 02 Jun 2021 16:39:30 +0300)

  *  AUTORUBACK-1722-fix-blur (#952)
     

  *  VSDEALERS-756 # Multiposting: pre-activation stage (#949)
     
     * VSDEALERS-756 # Multiposting: pre-activation stage
     
     * VSDEALERS-756 # Changelog fix
     
     * Revert "VSDEALERS-756 # Changelog fix"
     
     This reverts commit 8e752339fc7312cce40a339b0e696ee49d8f93e9.
     
     * VSDEALERS-756 # Hide stage over the feature
  *  VSDEALERS-976 - move def getTeleponyInfo from salesman to dealer-pony (#947)
     
     * VSDEALERS-976 - move def getTeleponyInfo from salesman to dealer-pony
     
     * VSDEALERS-976 - implement grpc client for dealer_pony/telepony receiving data
     
     * VSDEALERS-976 - add traced to call grpc get TeleponyInfo
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>
  *  Autoruback 1675 last offer not unpublish (#943)
     
     * AUTORUBACK-1675 clean excess logging
  *  AUTORUBACK-1689_mirror_from_mdb (#939)
     

  *  AUTORUBACK-1675 last offer not unpublish (#942)
     
     * AUTORUBACK-1675 check place where error happens
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-1675 unpublish broken (#936)
     
     * AUTORUBACK-1675 unpublish broken

  *  AUTORUBACK-1626 allow truck/moto category change (#938)
     

  *  AUTORUBACK-1261 (#934)
     
     * AUTORUBACK-1261
  *  CARFAX-1710 ручка для установки резолюции по проверенному собственнику (#931)
     
     * CARFAX-1710 ручка для установки резолюции по проверенному собственнику
  *  AUTORUBACK-1521_app2app_callinfo_fix (#935)
     
     * AUTORUBACK-1521_app2app_callinfo_fix
     
     * AUTORUBACK-1521_app2app_callinfo_fix: format
     
     * AUTORUBACK-1521_app2app_callinfo_fix: fixed tests and compilation
  *  AUTORUBACK-1620 kafka miss some records (#928)
     
     * AUTORUBACK-1620 rewriting panoramas on draft save
  *  AUTORUSUP-5421 # Log photo names on MaxPhotoCount error (#932)
     

  *  AUTORUBACK-1261 allow chat creation true if not set for private users

  *  AUTORUBACK-1261 Add chats_enabled processing (#921)
     
     * AUTORUBACK-1261 Add chats_enabled processing
     
     * AUTORUBACK-1261 Set allowChatsCreation as actual value
     
     * AUTORUBACK-1261 Remove redundant comments and sets
     
     * AUTORUBACK-1261 Remove redundant comments
     
     * AUTORUBACK-1261 Add tests
     
     * AUTORUBACK-1261 Add validations
     
     * AUTORUBACK-1261 Fix formatting
     
     * AUTORUBACK-1261 Address comments
     
     * AUTORUBACK-1261 Address comments
     
     * AUTORUBACK-1261 Address comments
     
     * Removed chats_enabled from AutoruModel;
     * AtLeastCallsOrChats set as NonFatalError;
     * If chatEnabled=false and chatOnly=false
        then set chatEnabled=true
     
     * AUTORUBACK-1261 Add chats setter for migration entity
     
     * AUTORUBACK-1261 Fix formatting
     
     * AUTORUBACK-1261 Address comments
     
     * test fix
     
     Co-authored-by: DmitrySafonov <fripe@yandex-team.ru>
  *  Autoruback 1667 fix transparency photo (#929)
     
     * AUTORUBACK-1667 moderation-PHOTO-fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 02 Jun 2021 16:39:30 +0300

## yandex-vos2-autoru-ydb-workers:0.21.4 (Wed, 19 May 2021 17:47:30 +0300)

  *  AUTORUBACK-1667 moderation-PHOTO-fix

  *  CARFAX-1645 up schema (#927)
     
     * CARFAX-1645 up schema
     
     * CARFAX-1645 delete redundant
  *  VSDEALERS-954 # Add handler getOfferIds (#923)
     

  *  AUTORUBACK-1444_mod_protection_editor_remove (#924)
     
     * AUTORUBACK-1444_mod_protection_editor_remove
     
     * AUTORUBACK-1444_mod_protection_editor_remove: format
     
     * AUTORUBACK-1444_mod_protection_editor_remove: updated swagger
  *  Autoruback 1071 workers 5 (#918)
     
     * AUTORUBACK-1071-workers-5
  *  AUTORUBACK-1450 Add badges update (#917)
     
     * AUTORUBACK-1450 Add badges update
     
     * AUTORUBACK-1450 Update parent pom
     
     * AUTORUBACK-1450 Refactor badges updating
     
     * AUTORUBACK-1450 Add tests for badges
     
     * AUTORUBACK-1450 Fix formatting for badges
     
     * AUTORUBACK-1450 Set new schema-registry version
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 19 May 2021 17:47:30 +0300

## yandex-vos2-autoru-ydb-workers:0.21.3 (Fri, 14 May 2021 10:56:48 +0300)

  *  Autoruback 1071 workers 5 (#918)
     
     * AUTORUBACK-1071-workers-5
  *  AUTORUBACK-1450 Add badges update (#917)
     
     * AUTORUBACK-1450 Add badges update
     
     * AUTORUBACK-1450 Update parent pom
     
     * AUTORUBACK-1450 Refactor badges updating
     
     * AUTORUBACK-1450 Add tests for badges
     
     * AUTORUBACK-1450 Fix formatting for badges
     
     * AUTORUBACK-1450 Set new schema-registry version
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 14 May 2021 10:56:48 +0300

## yandex-vos2-autoru-ydb-workers:0.21.2 (Fri, 30 Apr 2021 14:50:43 +0300)

  *  AUTORUBACK-1071-another-ydb-workers (#911)
     
     * AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 30 Apr 2021 14:50:43 +0300

## yandex-vos2-autoru-ydb-workers:0.21.1 (Fri, 30 Apr 2021 13:53:51 +0300)

  *  AUTORUBACK-1071-another-ydb-workers (#911)
     
     * AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 30 Apr 2021 13:53:51 +0300

## yandex-vos2-autoru-ydb-workers:0.21.0 (Fri, 23 Apr 2021 16:36:22 +0300)

  *  AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 23 Apr 2021 16:36:22 +0300

## yandex-vos2-autoru-ydb-workers:0.20.0 (Fri, 23 Apr 2021 15:42:17 +0300)

  *  AUTORUBACK-1071

  *  AUTORUBACK-1543: Add GosUslugi tag writer (#906)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 23 Apr 2021 15:42:17 +0300

## yandex-vos2-autoru-ydb-workers:0.19.1 (Fri, 23 Apr 2021 11:12:07 +0300)

  *  AUTORUBACK-1071

  *  AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 23 Apr 2021 11:12:07 +0300

## yandex-vos2-autoru-ydb-workers:0.19.0 (Fri, 23 Apr 2021 10:28:31 +0300)

  *  AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 23 Apr 2021 10:28:31 +0300

## yandex-vos2-autoru-ydb-workers:0.18.2 (Thu, 22 Apr 2021 17:15:43 +0300)

  *  AUTORUBACK-1268

  *  AUTORUBACK-1071 (#904)
     

  *  AUTORUBACK-1268 (#881)
     
     * AUTORUBACK-1268
  *  AUTORUBACK-1071

  *  AUTORUBACK-1071

  *  AUTORUBACK-1574_price_int_overflow (#901)
     
     * AUTORUBACK-1574_price_int_overflow
     
     * AUTORUBACK-1574_price_int_overflow: style
  *  AUTORUBACK-1069-fix-threadpool (#878)
     
     * AUTORUBACK-1069

  *  AUTORUBACK-1352 fix (#899)
     
     * AUTORUBACK-1352 fix interior panoramas api
  *  VSDEALERS-880 Refactor AUTORU logic, improve reusability (#896)
     

  *  AUTORUBACK-1511_dealer_duplicates_fix (#894)
     
     * AUTORUBACK-1511_dealer_duplicates_fix
     
     * AUTORUBACK-1511_dealer_duplicates_fix: fixed tests
  *  VSDEALERS-880 Add broker fields to holo offer (#895)
     
     * VSDEALERS-880 Add broker fields to holo offer
     
     * Fix AUTORU status
     
     * Fix AVTORU status definition
     
     * Fix id types
  *  AUTORUBACK-1575 (#892)
     

  *  AUTORUBACK-418 (#889)
     
     * AUTORUBACK-418 fix logback.xml in docker
  *  AUTORUBACK-1433 changed panoramas scheduler to kafka consumer (#879)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 22 Apr 2021 17:15:43 +0300

## yandex-vos2-autoru-ydb-workers:0.18.1 (Thu, 22 Apr 2021 16:24:27 +0300)

  *  AUTORUBACK-1071 (#904)
     

  *  AUTORUBACK-1268 (#881)
     
     * AUTORUBACK-1268
  *  AUTORUBACK-1071

  *  AUTORUBACK-1071

  *  AUTORUBACK-1574_price_int_overflow (#901)
     
     * AUTORUBACK-1574_price_int_overflow
     
     * AUTORUBACK-1574_price_int_overflow: style
  *  AUTORUBACK-1069-fix-threadpool (#878)
     
     * AUTORUBACK-1069

  *  AUTORUBACK-1352 fix (#899)
     
     * AUTORUBACK-1352 fix interior panoramas api
  *  VSDEALERS-880 Refactor AUTORU logic, improve reusability (#896)
     

  *  AUTORUBACK-1511_dealer_duplicates_fix (#894)
     
     * AUTORUBACK-1511_dealer_duplicates_fix
     
     * AUTORUBACK-1511_dealer_duplicates_fix: fixed tests
  *  VSDEALERS-880 Add broker fields to holo offer (#895)
     
     * VSDEALERS-880 Add broker fields to holo offer
     
     * Fix AUTORU status
     
     * Fix AVTORU status definition
     
     * Fix id types
  *  AUTORUBACK-1575 (#892)
     

  *  AUTORUBACK-418 (#889)
     
     * AUTORUBACK-418 fix logback.xml in docker
  *  AUTORUBACK-1433 changed panoramas scheduler to kafka consumer (#879)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 22 Apr 2021 16:24:27 +0300

## yandex-vos2-autoru-ydb-workers:0.18.0 (Sun, 04 Apr 2021 13:50:25 +0300)

  *  jdk15

  *  AUTORUBACK-1002_vos_mirror_fix (#863)
     
     * AUTORUBACK-1002_vos_mirror_fix
     
     * AUTORUBACK-1002_vos_mirror_fix: workers and stuff
     
     * AUTORUBACK-1002_vos_mirror_fix: more metrics and traces
     
     * AUTORUBACK-1002_vos_mirror_fix: removed unused
     
     * AUTORUBACK-1002_vos_mirror_fix: format
     
     * release 0.52.1
     
     * AUTORUBACK-1002_vos_mirror_fix: conf fix
     
     * release 0.52.2
     
     * AUTORUBACK-1002_vos_mirror_fix: conf fix
     
     * release 0.52.3
     
     * AUTORUBACK-1002_vos_mirror_fix: minor fix
     
     * AUTORUBACK-1002_vos_mirror_fix: minor fix
     
     * release 0.52.4
     
     * AUTORUBACK-1002_vos_mirror_fix: refactoring, separate tables
     
     * release 0.53.0
     
     * AUTORUBACK-1002_vos_mirror_fix: straight join
     
     * AUTORUBACK-1002_vos_mirror_fix: limit 5000
     
     * release 0.54.0
     
     * release 0.54.1
     
     * AUTORUBACK-1002_vos_mirror_fix: day zk interface
     
     * release 0.54.2
     
     * AUTORUBACK-1002_vos_mirror_fix: ensure first slash
     
     * release 0.55.0
     
     * AUTORUBACK-1002_vos_mirror_fix: fat offer limit 16 Mb
     
     * release 0.56.0
     
     * AUTORUBACK-1002_vos_mirror_fix: metered yt exporter, baker 15,
     
     * AUTORUBACK-1002_vos_mirror_fix: distinct photos
     
     * AUTORUBACK-1002_vos_mirror_fix: compilation fix
     
     * AUTORUBACK-1002_vos_mirror_fix: compilation fix
     
     * AUTORUBACK-1002_vos_mirror_fix: test fixes
     
     * AUTORUBACK-1002_vos_mirror_fix: test fixes
     
     * AUTORUBACK-1002_vos_mirror_fix: test fixes
     
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-1071 ydb workers (#866)
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
  *  AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 04 Apr 2021 13:50:25 +0300

## yandex-vos2-autoru-ydb-workers:0.17.2 (Thu, 01 Apr 2021 14:53:30 +0300)

  *  Autoruback 1071 ydb hiccup (#865)
     
     * AUTORUBACK-1071 added java_hiccup support
  *  AUTORUBACK-1499 revert occasionnaly pushed to master (#864)
     

  *  AUTORUBACK-1499 revert occasionnaly pushed to master

  *  AUTORUBACK-1499 bad data parsed occasionally

  *  Autoruback 1268 spam premium users ydb storage (#852)
     
     * AUTORUBACK-1268
  *  VSDEALERS-824 # Dont set is_revoked flag for active multiposting offers (#862)
     
     * VSDEALERS-824 # Dont set is_revoked flag for active multiposting offers
     
     * VSDEALERS-824 # Dont set is_revoked flag for active multiposting offers
     
     * VSDEALERS-824 # Unit
     
     * VSDEALERS-824 # Unit
     
     * VSDEALERS-824 # Unit
  *  CARFAX-1566: Refactor telepony stage to make it like public api logic (#861)
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>
  *  Revert "CARFAX-1566: Refactor telepony stage to make it like public api logic (#854)"
     
     This reverts commit 75f9541a

  *  Revert "CARFAX-1566: Refactor telepony stage to make it like public api logic (#854)"
     
     This reverts commit 75f9541a

  *  AUTORUBACK-1458 low resolution video in panoramas (#859)
     

  *  CARFAX-1566: Refactor telepony stage to make it like public api logic (#854)
     
     * CARFAX-1566: Refactor telepony stage to mke it like public api logic
     
     * CARFAX-1566: Fix error
     
     * CARFAX-1566: Make TeleponyWorkerYdb like TeleponyStage
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>
  *  CARFAX-1508 - Отдавать клиентам в отчёт забаненные офферы (#858)
     
     fix can_view for CS_REMOVED
  *  AUTORUBACK-1424_no_new_fields_in_searcher (#857)
     

  *  AUTORUBACK-1225-moderationUpdate-fix (#856)
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
  *  AUTORUBACK-277: Get salon from verba (#853)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 01 Apr 2021 14:53:30 +0300

## yandex-vos2-autoru-ydb-workers:0.17.1 (Tue, 30 Mar 2021 20:17:25 +0300)

  *  Autoruback 1268 spam premium users ydb storage (#852)
     
     * AUTORUBACK-1268
  *  VSDEALERS-824 # Dont set is_revoked flag for active multiposting offers (#862)
     
     * VSDEALERS-824 # Dont set is_revoked flag for active multiposting offers
     
     * VSDEALERS-824 # Dont set is_revoked flag for active multiposting offers
     
     * VSDEALERS-824 # Unit
     
     * VSDEALERS-824 # Unit
     
     * VSDEALERS-824 # Unit
  *  CARFAX-1566: Refactor telepony stage to make it like public api logic (#861)
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>
  *  Revert "CARFAX-1566: Refactor telepony stage to make it like public api logic (#854)"
     
     This reverts commit 75f9541a

  *  Revert "CARFAX-1566: Refactor telepony stage to make it like public api logic (#854)"
     
     This reverts commit 75f9541a

  *  AUTORUBACK-1458 low resolution video in panoramas (#859)
     

  *  CARFAX-1566: Refactor telepony stage to make it like public api logic (#854)
     
     * CARFAX-1566: Refactor telepony stage to mke it like public api logic
     
     * CARFAX-1566: Fix error
     
     * CARFAX-1566: Make TeleponyWorkerYdb like TeleponyStage
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>
  *  CARFAX-1508 - Отдавать клиентам в отчёт забаненные офферы (#858)
     
     fix can_view for CS_REMOVED
  *  AUTORUBACK-1424_no_new_fields_in_searcher (#857)
     

  *  AUTORUBACK-1225-moderationUpdate-fix (#856)
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
  *  AUTORUBACK-277: Get salon from verba (#853)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 30 Mar 2021 20:17:25 +0300

## yandex-vos2-autoru-ydb-workers:0.17.0 (Thu, 28 Jan 2021 14:57:13 +0300)

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller

  *  autoruback-1214 (#794)
     
     * autoruback-1214
     
     * autoruback-1214
     
     * autoruback-1214
  *  Revert "AUTORUBACK-308_can_view: fix"
     
     This reverts commit 3de8004e

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-308_can_view: fix

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala

  *  VSDEALERS-515 Don't edit multiposting offers with non-editable ban reasons (#788)
     
     * VSDEALERS-515 Don't edit multiposting offers with non-editable ban reasons
     
     * VSDEALERS-515 Fixed banned offers check
  *  VSDEALERS-624 Fixed multiposting offers archivation (#791)
     
     * VSDEALERS-624 Fixed multiposting offers archivation
     
     * VSDEALERS-624 Fixed empty multiposting status in tests
     
     * VSDEALERS-624 multiposting inactive->removed
     
     * VSDEALERS-624 Remove all multiposting statuses
  *  VSDEALERS-603 # Multiposting: multiposting fix stage Feature.value -> CabinetApi.isMultipostingEnabled (#787)
     
     * VSDEALERS-603 # Multiposting: multiposting fix stage Feature.value -> CabinetApi.isMultipostingEnabled
     
     * VSDEALERS-603 # Multiposting: multiposting fix stage Feature.value -> CabinetApi.isMultipostingEnabled
     
     * VSDEALERS-612 # FIX tests
  *  AUTORUBACK-1071

  *  zk test datasources update

  *  http license plate blur int test

  *  Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/WorkersSupport.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  autoruback-1071

  *  autoruback-1071

  *  Merge branch 'AUTORUBACK-1071-ydb-scheduller' of https://github.com/YandexClassifieds/vos2-autoru into AUTORUBACK-1071-ydb-scheduller

  *  autoruback-1071

  *  autoruback-1071

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
  *  autoruback-1071

  *  autoruback-1071

  *  autoruback-1071

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/OfferRow.scala

  *  Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/OfferRow.scala

  *  AUTORUBACK-1069 ydb

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 28 Jan 2021 14:57:13 +0300

## yandex-vos2-autoru-ydb-workers:0.16.0 (Tue, 19 Jan 2021 09:37:12 +0300)

  *  AUTORUBACK-1190 (#790)
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1190
  *  AUTORUBACK-308_can_view (#789)
     

  *  Autoruback 1190 index tables (#785)
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1190
     
     * AUTORUBACK-1190
  *  VSDEALERS-600 pledge_number support (#784)
     

  *  VSDEALERS-599 pledge_number (#782)
     

  *  VSDEALERS-588 # Add logs (#781)
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  test fix

  *  VSDEALERSDECOMP-147 # CommericalActivationStage with CabinetClient multiposting enabled check (#778)
     
     * VSDEALERSDECOMP-147 # New CommercialActivationStage: multiposting activation
     
     * VSDEALERSDECOMP-147 # FIX test
     
     * VSDEALERSDECOMP-147 # FIX test
     
     * VSDEALERSDECOMP-147 # CommericalActivationStage with CabinetClient multiposting enabled check
     
     * VSDEALERSDECOMP-147 # FIX HttpCabinetClient object
     
     * VSDEALERSDECOMP-147 # FIX feature names
     
     * VSDEALERSDECOMP-147 # rm test
     
     * VSDEALERSDECOMP-147 # Unit
     
     * VSDEALERSDECOMP-147 # FIX Unit
     
     * VSDEALERSDECOMP-147 # Logs
  *  VSDEALERSDECOMP-134 don't skip badges from active services (#779)
     

  *  VSDEALERS-588 Preserve classifieds support (#777)
     
     * VSDEALERS-588 Preserve classifieds support
     
     * VSDEALERS-588 variable reusage
  *  Autoruback 1069 ydb fix2 (#772)
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
  *  VSDEALERS-584 # MultipostingFixStage: clear multiposting field in broken offers (#773)
     

  *  VSDEALERS-566 # Multiposting: OfferFormConverter extended logging (#771)
     
     * VSDEALERS-566 # FormOfferConverter extended logging
     
     * VSDEALERS-566 # Multiposting: FormConverters extended logging
     
     * VSDEALERS-566 # Multiposting: FormConverters extended logging
     
     * VSDEALERS-566 # Multiposting: OfferFormConverter extended logging
  *  AUTORUBACK-1110: Keep name prefix (#766)
     

  *  VSDEALERS-566 # Multiposting: FormConverters extended logging (#769)
     
     * VSDEALERS-566 # FormOfferConverter extended logging
     
     * VSDEALERS-566 # Multiposting: FormConverters extended logging
     
     * VSDEALERS-566 # Multiposting: FormConverters extended logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 19 Jan 2021 09:37:12 +0300

## yandex-vos2-autoru-ydb-workers:0.15.0 (Wed, 23 Dec 2020 13:40:04 +0300)

  *  AUTORUBACK-1069 migrator-fix (#767)
     
     * AUTORUBACK-1069 migrator-fix
     
     * AUTORUBACK-1069 migrator-fix
     
     * AUTORUBACK-1069 migrator-fix
  *  VSDEALERS-566 # FormOfferConverter extended logging (#768)
     

  *  Autoruback 1069 ydb fix (#764)
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 23 Dec 2020 13:40:04 +0300

## yandex-vos2-autoru-ydb-workers:0.14.1 (Mon, 21 Dec 2020 14:48:36 +0300)

  *  AUTORUBACK-1069 ydb (#763)
     

  *  AUTORUBACK-1127_owners_number_4 (#762)
     

  *  Autoruback 1069 ydb tables (#761)
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
  *  VSDEALERSDECOMP-147 # Revert changing offe.status in FormOfferConverter for multiposting offer (#759)
     

  *  AUTORUBACK-687 (#749)
     
     Поддержать возможность удалять видео из офферов
  *  VSDEALERSDECOMP-147 # Move offer.status to INACTIVE if offer has multiposting and auto.ru classified is disabled (#758)
     
     * VSDEALERS-517 # Multiposting sync classifieds filter feature
     
     * VSDEALERS-517 # Move offer.status to INACTIVE if offer has multiposting and auto.ru classified is disabled
     
     * VSDEALERS-517 # fmt
     
     * VSDEALERS-517 # Check isNew offer
     
     * VSDEALERS-517 # Statuses list for fix
     
     * VSDEALERS-517 # Only isNew
     
     * VSDEALERSDECOMP-147 # Move offer.status to INACTIVE if offer has multiposting and auto.ru classified is disabled
  *  VSDEALERSDECOMP-147 # Move offer.status to INACTIVE if offer has multiposting and auto.ru classified is disabled (#756)
     
     * VSDEALERS-517 # Multiposting sync classifieds filter feature
     
     * VSDEALERS-517 # Move offer.status to INACTIVE if offer has multiposting and auto.ru classified is disabled
     
     * VSDEALERS-517 # fmt
     
     * VSDEALERS-517 # Check isNew offer
     
     * VSDEALERS-517 # Statuses list for fix
     
     * VSDEALERS-517 # Only isNew
  *  AUTORUBACK-1069 naming (#753)
     
     * AUTORUBACK-1069 naming
     
     * AUTORUBACK-1069 naming
     
     * AUTORUBACK-1069 naming
     
     * AUTORUBACK-1069 naming
  *  AUTORUBACK-1090: Add tvm config (#752)
     

  *  AUTORUBACK-1122 license plate suggest (#750)
     
     * AUTORUBACK-1122 license plate suggest
  *  AUTORUBACK-1069 fallback (#751)
     
     * AUTORUBACK-1069 fallback
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/OffersReader.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/OffersReader.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-1069 fallback
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-1069 ydb metering (#748)
     
     * AUTORUBACK-1069 ydb metering
     
     * AUTORUBACK-1069 ydb metering
     
     * AUTORUBACK-1069 ydb metering
     
     * AUTORUBACK-1069 ydb metering
  *  minor refactoring

  *  AUTORUBACK-1069 bugfix (#747)
     

  *  AUTORUBACK-1096 search by licence plate (#746)
     
     * AUTORUBACK-1096 search by licence plate (VOS part)
  *  VSDEALERS-517 # Multiposting sync classifieds filter feature (#745)
     

  *  AUTORUBACK-1069 (#740)
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1059
     
     * AUTORUBACK-1059
     
     * AUTORUBACK-1059 fixed vos feature
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * VSDEALERS-459 # Multiposting sync classifieds consumer [part-2] (#739)
     
     * VSDEALERS-459 # Multiposting sync classifieds consumer
     
     * VSDEALERS-459 # Use FeatureManager
     
     * VSDEALERS-459 # CodeReview FIX
     
     * VSDEALERS-459 #  Multiposting sync classifieds consumer [part-2]
     
     * VSDEALERS-459 # Tests
     
     * VSDEALERS-459 # Tests
     
     * VSDEALERS-459 # Return feature
     
     * VSDEALERS-459 # FIX unit
     
     * VSDEALERS-459 # fm
     
     * VSDEALERS-459 # fmt
     
     * VSDEALERS-459 # Prometheus metrics + CodeReview FIX
     
     * VSDEALERS-459 # fmt
     
     * VSDEALERS-459 # FIX test
     
     * VSDEALERS-459 # FIX test
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * tests fix
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-459 # Multiposting sync classifieds consumer [part-2] (#739)
     
     * VSDEALERS-459 # Multiposting sync classifieds consumer
     
     * VSDEALERS-459 # Use FeatureManager
     
     * VSDEALERS-459 # CodeReview FIX
     
     * VSDEALERS-459 #  Multiposting sync classifieds consumer [part-2]
     
     * VSDEALERS-459 # Tests
     
     * VSDEALERS-459 # Tests
     
     * VSDEALERS-459 # Return feature
     
     * VSDEALERS-459 # FIX unit
     
     * VSDEALERS-459 # fm
     
     * VSDEALERS-459 # fmt
     
     * VSDEALERS-459 # Prometheus metrics + CodeReview FIX
     
     * VSDEALERS-459 # fmt
     
     * VSDEALERS-459 # FIX test
     
     * VSDEALERS-459 # FIX test
  *  Autoruback 1055 new car from future (#744)
     
     * AUTORUBACK-1055_new_car_from_future
     
     * AUTORUBACK-1055_new_car_from_future: from october
     
     * AUTORUBACK-1055_new_car_from_future: tests
  *  AUTORUBACK-1053 (#741)
     
     Панорамы в пуше "Дозаполни объявление"
  *  VSDEALERS-459 # Multiposting sync classifieds consumer [part-1] (#737)
     
     * VSDEALERS-459 # Multiposting sync classifieds consumer
     
     * VSDEALERS-459 # Use FeatureManager
     
     * VSDEALERS-459 # CodeReview FIX
  *  AUTORUBACK-1059-mdb-readonly (#738)
     
     * AUTORUBACK-1059-mdb-readonly
     
     * AUTORUBACK-972-fix-gc-log
     
     * AUTORUBACK-1059
  *  AUTORUBACK-997 poi counts (#736)
     
     * AUTORUBACK-997 poi counts
  *  AUTORUBACK-972-fix-gc-log (#735)
     

  *  VSDEALERS-479 # MaxUpdateBatchSize: 500 -> 300 for `Packet for query is too large` error (#734)
     
     * VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 600 -> 500 for `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 500 -> 300 for `Packet for query is too large` error
  *  VSDEALERS-479 # MaxUpdateBatchSize: 600 -> 500 for `Packet for query is too large` error (#733)
     
     * VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 600 -> 500 for `Packet for query is too large` error
  *  VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error (#732)
     
     * VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error
  *  VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error (#731)
     

  *  VS-467 Отправляем score в Cёрчер (#730)
     
     * VS-467 send score to searcher
     
     * micro-core 0.13.63
     
     * rf
  *  VSDEALERS-455 # update multiposting models (#726)
     

  *  Fix formatting issue (#727)
     

  *  AUTORUBACK-1020 process_emergency_queue feature

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 21 Dec 2020 14:48:36 +0300

## yandex-vos2-autoru-ydb-workers:0.14.0 (Mon, 21 Dec 2020 13:13:49 +0300)

  *  Autoruback 1069 ydb tables (#761)
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
  *  VSDEALERSDECOMP-147 # Revert changing offe.status in FormOfferConverter for multiposting offer (#759)
     

  *  AUTORUBACK-687 (#749)
     
     Поддержать возможность удалять видео из офферов
  *  VSDEALERSDECOMP-147 # Move offer.status to INACTIVE if offer has multiposting and auto.ru classified is disabled (#758)
     
     * VSDEALERS-517 # Multiposting sync classifieds filter feature
     
     * VSDEALERS-517 # Move offer.status to INACTIVE if offer has multiposting and auto.ru classified is disabled
     
     * VSDEALERS-517 # fmt
     
     * VSDEALERS-517 # Check isNew offer
     
     * VSDEALERS-517 # Statuses list for fix
     
     * VSDEALERS-517 # Only isNew
     
     * VSDEALERSDECOMP-147 # Move offer.status to INACTIVE if offer has multiposting and auto.ru classified is disabled
  *  VSDEALERSDECOMP-147 # Move offer.status to INACTIVE if offer has multiposting and auto.ru classified is disabled (#756)
     
     * VSDEALERS-517 # Multiposting sync classifieds filter feature
     
     * VSDEALERS-517 # Move offer.status to INACTIVE if offer has multiposting and auto.ru classified is disabled
     
     * VSDEALERS-517 # fmt
     
     * VSDEALERS-517 # Check isNew offer
     
     * VSDEALERS-517 # Statuses list for fix
     
     * VSDEALERS-517 # Only isNew
  *  AUTORUBACK-1069 naming (#753)
     
     * AUTORUBACK-1069 naming
     
     * AUTORUBACK-1069 naming
     
     * AUTORUBACK-1069 naming
     
     * AUTORUBACK-1069 naming
  *  AUTORUBACK-1090: Add tvm config (#752)
     

  *  AUTORUBACK-1122 license plate suggest (#750)
     
     * AUTORUBACK-1122 license plate suggest
  *  AUTORUBACK-1069 fallback (#751)
     
     * AUTORUBACK-1069 fallback
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/OffersReader.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/OffersReader.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-1069 fallback
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-1069 ydb metering (#748)
     
     * AUTORUBACK-1069 ydb metering
     
     * AUTORUBACK-1069 ydb metering
     
     * AUTORUBACK-1069 ydb metering
     
     * AUTORUBACK-1069 ydb metering
  *  minor refactoring

  *  AUTORUBACK-1069 bugfix (#747)
     

  *  AUTORUBACK-1096 search by licence plate (#746)
     
     * AUTORUBACK-1096 search by licence plate (VOS part)
  *  VSDEALERS-517 # Multiposting sync classifieds filter feature (#745)
     

  *  AUTORUBACK-1069 (#740)
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1059
     
     * AUTORUBACK-1059
     
     * AUTORUBACK-1059 fixed vos feature
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * VSDEALERS-459 # Multiposting sync classifieds consumer [part-2] (#739)
     
     * VSDEALERS-459 # Multiposting sync classifieds consumer
     
     * VSDEALERS-459 # Use FeatureManager
     
     * VSDEALERS-459 # CodeReview FIX
     
     * VSDEALERS-459 #  Multiposting sync classifieds consumer [part-2]
     
     * VSDEALERS-459 # Tests
     
     * VSDEALERS-459 # Tests
     
     * VSDEALERS-459 # Return feature
     
     * VSDEALERS-459 # FIX unit
     
     * VSDEALERS-459 # fm
     
     * VSDEALERS-459 # fmt
     
     * VSDEALERS-459 # Prometheus metrics + CodeReview FIX
     
     * VSDEALERS-459 # fmt
     
     * VSDEALERS-459 # FIX test
     
     * VSDEALERS-459 # FIX test
     
     * AUTORUBACK-1069
     
     * AUTORUBACK-1069
     
     * tests fix
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-459 # Multiposting sync classifieds consumer [part-2] (#739)
     
     * VSDEALERS-459 # Multiposting sync classifieds consumer
     
     * VSDEALERS-459 # Use FeatureManager
     
     * VSDEALERS-459 # CodeReview FIX
     
     * VSDEALERS-459 #  Multiposting sync classifieds consumer [part-2]
     
     * VSDEALERS-459 # Tests
     
     * VSDEALERS-459 # Tests
     
     * VSDEALERS-459 # Return feature
     
     * VSDEALERS-459 # FIX unit
     
     * VSDEALERS-459 # fm
     
     * VSDEALERS-459 # fmt
     
     * VSDEALERS-459 # Prometheus metrics + CodeReview FIX
     
     * VSDEALERS-459 # fmt
     
     * VSDEALERS-459 # FIX test
     
     * VSDEALERS-459 # FIX test
  *  Autoruback 1055 new car from future (#744)
     
     * AUTORUBACK-1055_new_car_from_future
     
     * AUTORUBACK-1055_new_car_from_future: from october
     
     * AUTORUBACK-1055_new_car_from_future: tests
  *  AUTORUBACK-1053 (#741)
     
     Панорамы в пуше "Дозаполни объявление"
  *  VSDEALERS-459 # Multiposting sync classifieds consumer [part-1] (#737)
     
     * VSDEALERS-459 # Multiposting sync classifieds consumer
     
     * VSDEALERS-459 # Use FeatureManager
     
     * VSDEALERS-459 # CodeReview FIX
  *  AUTORUBACK-1059-mdb-readonly (#738)
     
     * AUTORUBACK-1059-mdb-readonly
     
     * AUTORUBACK-972-fix-gc-log
     
     * AUTORUBACK-1059
  *  AUTORUBACK-997 poi counts (#736)
     
     * AUTORUBACK-997 poi counts
  *  AUTORUBACK-972-fix-gc-log (#735)
     

  *  VSDEALERS-479 # MaxUpdateBatchSize: 500 -> 300 for `Packet for query is too large` error (#734)
     
     * VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 600 -> 500 for `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 500 -> 300 for `Packet for query is too large` error
  *  VSDEALERS-479 # MaxUpdateBatchSize: 600 -> 500 for `Packet for query is too large` error (#733)
     
     * VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 600 -> 500 for `Packet for query is too large` error
  *  VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error (#732)
     
     * VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error
  *  VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error (#731)
     

  *  VS-467 Отправляем score в Cёрчер (#730)
     
     * VS-467 send score to searcher
     
     * micro-core 0.13.63
     
     * rf
  *  VSDEALERS-455 # update multiposting models (#726)
     

  *  Fix formatting issue (#727)
     

  *  AUTORUBACK-1020 process_emergency_queue feature

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 21 Dec 2020 13:13:49 +0300

## yandex-vos2-autoru-ydb-workers:0.13.1 (Mon, 23 Nov 2020 22:20:52 +0300)

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: lag stats: fix

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: lag stats

  *  VSDEALERS-423 # Deduplicate Avito services (#725)
     
     * VSDEALERS-423 # Deduplicate Avito services
  *  AUTORUBACK-496: Replace cars_catalog with cars_palma_catalog (#719)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 23 Nov 2020 22:20:52 +0300

## yandex-vos2-autoru-ydb-workers:0.13.0 (Mon, 23 Nov 2020 20:31:58 +0300)

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: lag stats

  *  VSDEALERS-423 # Deduplicate Avito services (#725)
     
     * VSDEALERS-423 # Deduplicate Avito services
  *  AUTORUBACK-496: Replace cars_catalog with cars_palma_catalog (#719)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 23 Nov 2020 20:31:58 +0300

## yandex-vos2-autoru-ydb-workers:0.12.4 (Sat, 21 Nov 2020 00:21:39 +0300)

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: query executor fix

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: query fix

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: query name fix

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: query fix

  *  AUTORUBACK-126: batch updated support in query executor, mysql-to-ydb… (#721)
     
     * AUTORUBACK-126: batch updated support in query executor, mysql-to-ydb-migrator, statistician
     
     * AUTORUBACK-126: mysql-to-ydb-migrator stats
  *  AUTORUBACK-1006 palma 2.13 -> 2.12 fix 2

  *  AUTORUBACK-1006 palma 2.13 -> 2.12 fix

  *  AUTORUBACK-999: Don't show broken price ranges (#718)
     

  *  AUTORUBACK-977 new resolutions from moderation (#722)
     
     * AUTORUBACK-977 new resolutions from moderation
     
     * AUTORUBACK-977 new resolutions from moderation
     
     * AUTORUBACK-977 new resolutions from moderation
  *  VSDEALERSDECOMP-132 all drafts statuses sync (#720)
     
     * VSDEALERSDECOMP-132 set create_date if not presented
     
     * VSDEALERSDECOMP-132 multiposting and classified statuses set if not presented
     
     * VSDEALERSDECOMP-132 Code deduplication
     
     * VSDEALERSDECOMP-132 sync user-related statuses with enabled
     
     * VSDEALERSDECOMP-132 create_date only for enabled classifieds
     
     * VSDEALERSDECOMP-132 offer hidden check fixed
     
     * VSDEALERSDECOMP-132 statuses sync for drafts only
     
     * VSDEALERSDECOMP-132 removed redundant OfferFormConverter changes
     
     * VSDEALERSDECOMP-132 readable names for variables
     
     * VSDEALERSDECOMP-132 all drafts statuses sync
  *  VSDEALERSDECOMP-132 [multiposting] set create_date and statuses if not presented (#717)
     
     * VSDEALERSDECOMP-132 set create_date if not presented
     
     * VSDEALERSDECOMP-132 multiposting and classified statuses set if not presented
     
     * VSDEALERSDECOMP-132 Code deduplication
     
     * VSDEALERSDECOMP-132 sync user-related statuses with enabled
     
     * VSDEALERSDECOMP-132 create_date only for enabled classifieds
     
     * VSDEALERSDECOMP-132 offer hidden check fixed
     
     * VSDEALERSDECOMP-132 statuses sync for drafts only
     
     * VSDEALERSDECOMP-132 removed redundant OfferFormConverter changes
     
     * VSDEALERSDECOMP-132 readable names for variables
  *  compilation fix

  *  AUTORUBACK-1000 fixed holocron optLastDeactivateMoment calculation when no active events exist

  *  temporary test fix

  *  skypper: 11

  *  AUTORUBACK-879 interior panoramas routes for moderation (#715)
     
     * AUTORUBACK-879 interior panoramas routes for moderation +  fix status change
  *  AUTORUBACK-875 send images meta to broker (#716)
     
     * AUTORUBACK-875 send images meta to broker
     
     * review fixes
  *  AUTORUBACK-959: Не писать логи в файлы (#713)
     

  *  AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue (#712)
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydq update queue
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: fixed tests
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: added foreign key, fixed code
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: format
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: removed drop functionality
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: style
  *  Autoruback 126 ydb blobs update queue (#632)
     
     * AUTORUBACK-126_ydb_blobs_update_queue: fixed create methods to work in transactions
     
     * AUTORUBACK-126_ydb_blobs_update_queue: ydb error logging
  *  AUTORUBACK-976_archive_banned_dealers_fix (#711)
     

  *  VSDEALERS-436 # With removed offers for multiposting set status (#714)
     

  *  AUTORUBACK-754 send old holocron events: emergency queue scaling

  *  VSDEALERS-429 # FIX multiposting offer status migration (#709)
     
     * VSDEALERS-429 # FIX multiposting offer status migration
     
     * VSDEALERS-429 # More tests
  *  Autoruback 961 passport client and carfax report scoring fix (#706)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-911-fix-premium-user (#705)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-911 fixed issue with wrong premium
     
     * AUTORUBACK-911
  *  VSDEALERS-413 # Add offer_ids/by_vins handler (#703)
     

  *  AUTORUBACK-961 fixed issue with userNotFound (#704)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-807 callback to salon: added api to get salon from vos by verba-code

  *  VSDEALERS-416 # Set multiposting service expire_date sync + UpperCase FIX (#702)
     
     * VSDEALERS-416 # Set multiposting service expire_date sync + UpperCase fix
     
     * VSDEALERS-416 # Better naming
  *  AUTORUBACK-954 fixed issue with ComplaintsClient (#701)
     
     * AUTORUBACK-954 fixed issue with ComplaintsClient
     
     * AUTORUBACK-954 fixed issue with ComplaintsClient
  *  VSDEALERS-400 distinct services from form (#689)
     
     * VSDEALERS-400 clear services before add
     
     * VSDEALERS-400 distinct services from form
  *  VSDEALERS-402 Active services check fixed (#700)
     
     * VSDEALERS-402 Active services check fixed
     
     * VSDEALERS-402 uppercase index fields for multiposting services
     
     * VSDEALERS-402 uppercase classifieds services
     
     * VSDEALERS-402 tests fixed
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  AUTORUBACK-944 fixed issue with empty vin (#697)
     
     * fixed issue with empty vin
     
     * fixed issue with empty vin
     
     * additional logging update
  *  create_date for new classifieds (#698)
     
     * create_date for new classifieds
     
     * Sync classified create date with offer.create
     
     * compilation fixed
  *  Autoruback 911 fix containers (#695)
     
     * fixed version after merge
     
     * fixed version after merge
  *  fixed version after merge (#693)
     

  *  CARFAX-1157: Add options_updated flag (#690)
     

  *  AUTORUBACK-911 premium seller exp (#682)
     
     * autoruback-9§§
     
     * autoruback-911
     
     * autoruback-911 updated java version
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/UserAssistanceStage.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Merge branch 'master' into AUTORUBACK-911-premuim-seller-exp
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-400 clear services before add (#688)
     

  *  VSDEALERS-395 # Multiposting offer actions (#687)
     

  *  VSDEALERS-323 user ref parsing fixed (#686)
     

  *  VSDEALERS-323 Fixed producer config (#685)
     
     * VSDEALERS-323 multiposting events consumer
     
     * VSDEALERS-323 Fixed producer config
  *  VSDEALERS-323 multiposting events consumer (#681)
     

  *  AUTORUBACK-684 Allow to update offer discount options (#628)
     
     * AUTORUBACK-684 Allow to update offer discount options
     
     * AUTORUBACK-684_update-offer-discount
     
     * query, uptime, workers, todo
     
     * updated schema registry
     
     * AUTORUBACK-684_update-offer-discount: style
     
     * AUTORUBACK-684_update-offer-discount: fixed tests
     
     * AUTORUBACK-684_update-offer-discount: save discount options to old db (not finished), updated responses, updated tests, refactoring
     
     * AUTORUBACK-684_update-offer-discount: todo
     
     * Merge branch 'master' into AUTORUBACK-684_update-offer-discount
     
     # Conflicts:
     #	pom.xml
     #	vos2-autoru-api/src/main/scala/ru/yandex/vos2/autoru/api/v1/offer/OfferHandler.scala
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/OffersWriter.scala
     
     * AUTORUBACK-684_update-offer-discount: fixes after merge
     
     * AUTORUBACK-684_update-offer-discount: style
     
     * AUTORUBACK-684_update-offer-discount: updated schema-registry
     
     * AUTORUBACK-684_update-offer-discount: revert some changes
     
     * AUTORUBACK-684_update-offer-discount: revert some changes
     
     * AUTORUBACK-684_update-offer-discount: compilation fixes and refactoring
     
     * AUTORUBACK-684_update-offer-discount: removed photo utils from statuses manager
     
     * AUTORUBACK-684_price_attribute_return
     
     * AUTORUBACK-684_update-offer-discount_model_update: save discount options to old db
     
     * AUTORUBACK-684_update-offer-discount_model_update: fixed tests, refactoring
     
     * AUTORUBACK-684_update-offer-discount_model_update: fix after merge
     
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-373 # Allow to enable/disable multiposting for user by id (#679)
     
     * VSDEALERS-373 # Allow to enable/disable multiposting for user by id
     
     * VSDEALERS-373 # Update tests
     
     * VSDEALERS-373 # Minor refactor
     
     * VSDEALERS-373 # Minor refactor
     
     * VSDEALERS-373 # Minor fixes
     
     * VSDEALERS-373 # Select all offers when activate multiposting
     
     * VSDEALERS-373 # Explicitly filter statuses
     
     * VSDEALERS-373 # Wrap in withoutErrors
  *  VSDEALERS-289 Fixed services duplication (#680)
     

  *  AUTORUBACK-904 silent push (#678)
     

  *  AUTORUBACK-922: added kafka props for extended holocron

  *  VSDEALERS-277 # Update classified state handlers logic (#677)
     
     * VSDEALERS-277 # Update classified state handlers logic
     
     * VSDEALERS-277 # Update OfferHandlerTest
  *  VSDEALERS-289 services deduplication (#675)
     
     * VSDEALERS-289 classified services model changed
     
     * VSDEALERS-289 services deduplication
     
     * VSDEALERS-289 build the builder
     
     * VSDEALERS-289 fixed doc
     
     * VSDEALERS-289 Don't reactivated disabled services
     
     * VSDEALERS-289 Don't remove old services
     
     * VSDEALERS-289 classified -> multiposting
     
     * VSDEALERS-289 renaming
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  AUTORUBACK-835 change call info renderer message (#674)
     

  *  AUTORUBACK-906 remove nullable fields (#673)
     

  *  AUTORUBACK-906 extend common feature response with tags and info (#672)
     

  *  AUTORUBACK-718 feature spamalot push (#670)
     

  *  Revert "AUTORUBACK-718 feature spamalot push"
     
     This reverts commit 2bbdf9d2

  *  AUTORUBACK-718 feature spamalot push

  *  AUTORUBACK-718 turn off pushnoy in offer incomplete form (#669)
     

  *  minor changes

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-829 offer-form converter fix

  *  AUTORUBACK-718 add logged and metered for spamalot push (#668)
     
     * AUTORUBACK-718 add logged and metered for spamalot push
     
     * AUTORUBACK-718 npe hotfix
     
     * AUTORUBACK-718 test fix try
  *  AUTORUBACK-718 send offerincomplete push to spamalot (#666)
     
     * AUTORUBACK-718 send offerincomplete push to spamalot
     
     * AUTORUBACK-718 remove unused ConcurrencyUtils.scala
     
     * AUTORUBACK-718 add spamalot mock for test
     
     * AUTORUBACK-718 format
     review fix
     
     * AUTORUBACK-718 remove execution context from spamalot client
     fix spamalot config name
     
     * AUTORUBACK-718 try tests without lazy spamalotClient
     
     * AUTORUBACK-718 topic
  *  compilation fix

  *  update blur logging

  *  update blur parsing and logging

  *  Autoruback 870 spinkar ekt only (#665)
     
     * AUTORUBACK-870_spinkar_ekt_only
     
     * AUTORUBACK-870_spinkar_ekt_only: updated converter for searcher
  *  autoruback-632 (#664)
     
     * autoruback-632
     
     * autoruback-632
     
     * autoruback-632
     
     * autoruback-632
  *  Autoruback 632 (#660)
     
     * autoruback-632 -feature name fix
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
  *  VSDEALERS-297 # Set multiposting status (#658)
     

  *  AUTORUBACK-870_spinkar_ekt_only (#659)
     

  *  AUTORUBACK-753 refactoring (#654)
     
     * AUTORUBACK-753 refactoring
     
     * AUTORUBACK-753 format
  *  VSDEALERS-278 (#655)
     
     * added handler endpoints, service method, dao method
     
     * tests, doc, logic
     
     * it works
     
     * removed unused exception
     
     * review improvements
     
     * adde st to log
     
     * renamed trace
  *  VSDEALERS-256 hidden -> dealer_hidden for multiposting (#657)
     

  *  VSDEALERS-302 multiposting converters (#656)
     
     * VSDEALERS-302 multiposting converters
     
     * VSDEALERS-302 removed duplicated code
     
     * VSDEALERS-302 classified convertion
     
     * VSDEALERS-302 fixed test without multiposting
     
     * VSDEALERS-302 removed default multiposting status
     
     * VSDEALERS-302 redundant import removed
     
     * VSDEALERS-302 multiposting converter refactored
  *  VSDEALERS-256 Multiposting fields to shard propagation (#649)
     
     * VSDEALERS-256 Multiposting fields to shard propagation (for cars only yet)
     
     * VSDEALERS-256 Fixed offer generation in tests
     
     * VSDEALERS-256 multiposting propagation for trucks and moto
     
     * VSDEALERS-256 isActive utility usage + dealer offer check
     
     * VSDEALERS-256 tests fixed
     
     * VSDEALERS-256 hidden for user offers, dead code removed
     
     * VSDEALERS-256 banned offers disabled on dealer showcase
     
     * VSDEALERS-256 utility usage for ban check
  *  VSDEALERS-252 # Convert multiposting model VOS -> ApiOfferModel (#653)
     
     * VSDEALERS-252 # Convert multiposting model VOS -> ApiOfferModel
     
     * VSDEALERS-252 # fmt
  *  AUTORUBACK-753 upload document photos to offer (#646)
     
     * AUTORUBACK-753 add offer doc photo
     
     * AUTORUBACK-753 uncomment line
     
     * AUTORUBACK-753 remove DomainExceptionRenderer from PhotoDirectives
     
     * AUTORUBACK-753 imports optimized
     
     * AUTORUBACK-753 fix routing issues
     
     * AUTORUBACK-753 remove capturing group
     
     * code review todo
     
     * AUTORUBACK-753 revert draft id path segment behaviour
     
     * AUTORUBACK-753 fix issues
     
     * AUTORUBACK-753 rename toPhotoResponse
     
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-254 # Filter offers by multiposting_status and multiposting_service (#651)
     
     * VSDEALERS-254 # Filter offers by multiposting_status and multiposting_service
     
     * VSDEALERS-254 # FIX application.conf
     
     * VSDEALERS-254 # FIX dev configurations
     
     * VSDEALERS-254 # FIX remove service without expire_date
     
     * VSDEALERS-254 # FIX remove service without expire_date
     
     * VSDEALERS-254 # FIX swagger documentation
     
     * VSDEALERS-254 # CodeReview FIX
  *  autoruback-632 -feature name fix (#652)
     

  *  VSDEALERS-265 # Стейдж мультипостинга в VOS (#650)
     
     * VSDEALERS-265 # Стейдж мультипостинга в VOS
     
     * VSDEALERS-265 # Rename stage; minor fixes
     
     * VSDEALERS-265 # Refactor MultipostingStage#process
     
     * VSDEALERS-265 # Refactor MultipostingStage#process
  *  AUTORUBACK-829_vin_recognition_flag (#648)
     
     * AUTORUBACK-829_vin_recognition_flag
     
     * AUTORUBACK-829_vin_recognition_flag: updated schema-registry
  *  comments

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-857: updated logging and tracing error annotation

  *  VSDEALERS-308 # Multiposting classified is_enabled flag (#647)
     

  *  Revert "VSDEALERS-280 # Активация мультипостинговых объявлений по условию (#644)" (#645)
     
     This reverts commit 957e3d4f54bdc610ca4580b3b9fee66c047c635c.
  *  AUTORUBACK-632-scoring (#641)
     
     * AUTORUBACK-632-scoring
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/components/AutoruCoreComponents.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-280 # Активация мультипостинговых объявлений по условию (#644)
     
     * VSDEALERS-280 # Активация мультипостинговых объявлений по условию
     
     * VSDEALERS-280 # Refactor CommercialActivationStage#shouldProcess
     
     * VSDEALERS-280 # Check multiposting status
     
     * VSDEALERS-280 # Move hasActiveAutoruClassified to utils
     
     * VSDEALERS-280 # Refactor CommercialActivationStage#shouldProcess
  *  added drom classified (#643)
     

  *  AUTORUBACK-172_request_id_in_logs: fixed request context copy

  *  VSDEALERS-253 # Add index fields for multiposting (#639)
     
     * VSDEALERS-253 # Add index fields for multiposting
     
     * VSDEALERS-253 # Update DDL for index fields
     
     * VSDEALERS-253 # Add multiposting fields to AutoruOfferDao
  *  AUTORUBACK-172_request_id_in_logs, not finished (#636)
     
     * AUTORUBACK-172_request_id_in_logs, not finished
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, not finished
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, not finished: updated offer handler
     
     * AUTORUBACK-172_request_id_in_logs: exceptions refactoring
     
     * AUTORUBACK-172_request_id_in_logs: updated more managers and handlers
     
     * AUTORUBACK-172_request_id_in_logs: removed managers default error handling
     
     * AUTORUBACK-172_request_id_in_logs: able to compile and run
     
     * AUTORUBACK-172_request_id_in_logs: style and marshaller fixes
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: improved tests
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: short access logging
     
     * AUTORUBACK-172_request_id_in_logs: fixed test, todo
  *  VSDEALERS-252 added multiposting field (#638)
     
     * added multiposting field
     
     * removed field options
     
     * fixed id
  *  AUTORUBACK-745-ban (#637)
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/services/chat/HttpChatClient.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-679_photo_class (#635)
     
     * AUTORUBACK-679_photo_class
     
     * AUTORUBACK-679_photo_class: more changes
     
     * AUTORUBACK-679_photo_class: refactoring
     
     * AUTORUBACK-679_photo_class: AUTO_VIEW_3_4_BACK support
  *  AUTORUBACK-795 tracing fix (#633)
     
     * AUTORUBACK-795_tracing_fix
     
     * AUTORUBACK-795_tracing_fix: fixed more
     
     * AUTORUBACK-795_tracing_fix: refactoring
     
     * AUTORUBACK-795_tracing_fix: fixed test
     
     * AUTORUBACK-795_tracing_fix: style
  *  AUTORUBACK-603: Add stats endpoint (#625)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 21 Nov 2020 00:21:39 +0300

## yandex-vos2-autoru-ydb-workers:0.12.3 (Sat, 21 Nov 2020 00:08:20 +0300)

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: query fix

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: query name fix

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: query fix

  *  AUTORUBACK-126: batch updated support in query executor, mysql-to-ydb… (#721)
     
     * AUTORUBACK-126: batch updated support in query executor, mysql-to-ydb-migrator, statistician
     
     * AUTORUBACK-126: mysql-to-ydb-migrator stats
  *  AUTORUBACK-1006 palma 2.13 -> 2.12 fix 2

  *  AUTORUBACK-1006 palma 2.13 -> 2.12 fix

  *  AUTORUBACK-999: Don't show broken price ranges (#718)
     

  *  AUTORUBACK-977 new resolutions from moderation (#722)
     
     * AUTORUBACK-977 new resolutions from moderation
     
     * AUTORUBACK-977 new resolutions from moderation
     
     * AUTORUBACK-977 new resolutions from moderation
  *  VSDEALERSDECOMP-132 all drafts statuses sync (#720)
     
     * VSDEALERSDECOMP-132 set create_date if not presented
     
     * VSDEALERSDECOMP-132 multiposting and classified statuses set if not presented
     
     * VSDEALERSDECOMP-132 Code deduplication
     
     * VSDEALERSDECOMP-132 sync user-related statuses with enabled
     
     * VSDEALERSDECOMP-132 create_date only for enabled classifieds
     
     * VSDEALERSDECOMP-132 offer hidden check fixed
     
     * VSDEALERSDECOMP-132 statuses sync for drafts only
     
     * VSDEALERSDECOMP-132 removed redundant OfferFormConverter changes
     
     * VSDEALERSDECOMP-132 readable names for variables
     
     * VSDEALERSDECOMP-132 all drafts statuses sync
  *  VSDEALERSDECOMP-132 [multiposting] set create_date and statuses if not presented (#717)
     
     * VSDEALERSDECOMP-132 set create_date if not presented
     
     * VSDEALERSDECOMP-132 multiposting and classified statuses set if not presented
     
     * VSDEALERSDECOMP-132 Code deduplication
     
     * VSDEALERSDECOMP-132 sync user-related statuses with enabled
     
     * VSDEALERSDECOMP-132 create_date only for enabled classifieds
     
     * VSDEALERSDECOMP-132 offer hidden check fixed
     
     * VSDEALERSDECOMP-132 statuses sync for drafts only
     
     * VSDEALERSDECOMP-132 removed redundant OfferFormConverter changes
     
     * VSDEALERSDECOMP-132 readable names for variables
  *  compilation fix

  *  AUTORUBACK-1000 fixed holocron optLastDeactivateMoment calculation when no active events exist

  *  temporary test fix

  *  skypper: 11

  *  AUTORUBACK-879 interior panoramas routes for moderation (#715)
     
     * AUTORUBACK-879 interior panoramas routes for moderation +  fix status change
  *  AUTORUBACK-875 send images meta to broker (#716)
     
     * AUTORUBACK-875 send images meta to broker
     
     * review fixes
  *  AUTORUBACK-959: Не писать логи в файлы (#713)
     

  *  AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue (#712)
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydq update queue
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: fixed tests
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: added foreign key, fixed code
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: format
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: removed drop functionality
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: style
  *  Autoruback 126 ydb blobs update queue (#632)
     
     * AUTORUBACK-126_ydb_blobs_update_queue: fixed create methods to work in transactions
     
     * AUTORUBACK-126_ydb_blobs_update_queue: ydb error logging
  *  AUTORUBACK-976_archive_banned_dealers_fix (#711)
     

  *  VSDEALERS-436 # With removed offers for multiposting set status (#714)
     

  *  AUTORUBACK-754 send old holocron events: emergency queue scaling

  *  VSDEALERS-429 # FIX multiposting offer status migration (#709)
     
     * VSDEALERS-429 # FIX multiposting offer status migration
     
     * VSDEALERS-429 # More tests
  *  Autoruback 961 passport client and carfax report scoring fix (#706)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-911-fix-premium-user (#705)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-911 fixed issue with wrong premium
     
     * AUTORUBACK-911
  *  VSDEALERS-413 # Add offer_ids/by_vins handler (#703)
     

  *  AUTORUBACK-961 fixed issue with userNotFound (#704)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-807 callback to salon: added api to get salon from vos by verba-code

  *  VSDEALERS-416 # Set multiposting service expire_date sync + UpperCase FIX (#702)
     
     * VSDEALERS-416 # Set multiposting service expire_date sync + UpperCase fix
     
     * VSDEALERS-416 # Better naming
  *  AUTORUBACK-954 fixed issue with ComplaintsClient (#701)
     
     * AUTORUBACK-954 fixed issue with ComplaintsClient
     
     * AUTORUBACK-954 fixed issue with ComplaintsClient
  *  VSDEALERS-400 distinct services from form (#689)
     
     * VSDEALERS-400 clear services before add
     
     * VSDEALERS-400 distinct services from form
  *  VSDEALERS-402 Active services check fixed (#700)
     
     * VSDEALERS-402 Active services check fixed
     
     * VSDEALERS-402 uppercase index fields for multiposting services
     
     * VSDEALERS-402 uppercase classifieds services
     
     * VSDEALERS-402 tests fixed
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  AUTORUBACK-944 fixed issue with empty vin (#697)
     
     * fixed issue with empty vin
     
     * fixed issue with empty vin
     
     * additional logging update
  *  create_date for new classifieds (#698)
     
     * create_date for new classifieds
     
     * Sync classified create date with offer.create
     
     * compilation fixed
  *  Autoruback 911 fix containers (#695)
     
     * fixed version after merge
     
     * fixed version after merge
  *  fixed version after merge (#693)
     

  *  CARFAX-1157: Add options_updated flag (#690)
     

  *  AUTORUBACK-911 premium seller exp (#682)
     
     * autoruback-9§§
     
     * autoruback-911
     
     * autoruback-911 updated java version
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/UserAssistanceStage.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Merge branch 'master' into AUTORUBACK-911-premuim-seller-exp
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-400 clear services before add (#688)
     

  *  VSDEALERS-395 # Multiposting offer actions (#687)
     

  *  VSDEALERS-323 user ref parsing fixed (#686)
     

  *  VSDEALERS-323 Fixed producer config (#685)
     
     * VSDEALERS-323 multiposting events consumer
     
     * VSDEALERS-323 Fixed producer config
  *  VSDEALERS-323 multiposting events consumer (#681)
     

  *  AUTORUBACK-684 Allow to update offer discount options (#628)
     
     * AUTORUBACK-684 Allow to update offer discount options
     
     * AUTORUBACK-684_update-offer-discount
     
     * query, uptime, workers, todo
     
     * updated schema registry
     
     * AUTORUBACK-684_update-offer-discount: style
     
     * AUTORUBACK-684_update-offer-discount: fixed tests
     
     * AUTORUBACK-684_update-offer-discount: save discount options to old db (not finished), updated responses, updated tests, refactoring
     
     * AUTORUBACK-684_update-offer-discount: todo
     
     * Merge branch 'master' into AUTORUBACK-684_update-offer-discount
     
     # Conflicts:
     #	pom.xml
     #	vos2-autoru-api/src/main/scala/ru/yandex/vos2/autoru/api/v1/offer/OfferHandler.scala
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/OffersWriter.scala
     
     * AUTORUBACK-684_update-offer-discount: fixes after merge
     
     * AUTORUBACK-684_update-offer-discount: style
     
     * AUTORUBACK-684_update-offer-discount: updated schema-registry
     
     * AUTORUBACK-684_update-offer-discount: revert some changes
     
     * AUTORUBACK-684_update-offer-discount: revert some changes
     
     * AUTORUBACK-684_update-offer-discount: compilation fixes and refactoring
     
     * AUTORUBACK-684_update-offer-discount: removed photo utils from statuses manager
     
     * AUTORUBACK-684_price_attribute_return
     
     * AUTORUBACK-684_update-offer-discount_model_update: save discount options to old db
     
     * AUTORUBACK-684_update-offer-discount_model_update: fixed tests, refactoring
     
     * AUTORUBACK-684_update-offer-discount_model_update: fix after merge
     
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-373 # Allow to enable/disable multiposting for user by id (#679)
     
     * VSDEALERS-373 # Allow to enable/disable multiposting for user by id
     
     * VSDEALERS-373 # Update tests
     
     * VSDEALERS-373 # Minor refactor
     
     * VSDEALERS-373 # Minor refactor
     
     * VSDEALERS-373 # Minor fixes
     
     * VSDEALERS-373 # Select all offers when activate multiposting
     
     * VSDEALERS-373 # Explicitly filter statuses
     
     * VSDEALERS-373 # Wrap in withoutErrors
  *  VSDEALERS-289 Fixed services duplication (#680)
     

  *  AUTORUBACK-904 silent push (#678)
     

  *  AUTORUBACK-922: added kafka props for extended holocron

  *  VSDEALERS-277 # Update classified state handlers logic (#677)
     
     * VSDEALERS-277 # Update classified state handlers logic
     
     * VSDEALERS-277 # Update OfferHandlerTest
  *  VSDEALERS-289 services deduplication (#675)
     
     * VSDEALERS-289 classified services model changed
     
     * VSDEALERS-289 services deduplication
     
     * VSDEALERS-289 build the builder
     
     * VSDEALERS-289 fixed doc
     
     * VSDEALERS-289 Don't reactivated disabled services
     
     * VSDEALERS-289 Don't remove old services
     
     * VSDEALERS-289 classified -> multiposting
     
     * VSDEALERS-289 renaming
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  AUTORUBACK-835 change call info renderer message (#674)
     

  *  AUTORUBACK-906 remove nullable fields (#673)
     

  *  AUTORUBACK-906 extend common feature response with tags and info (#672)
     

  *  AUTORUBACK-718 feature spamalot push (#670)
     

  *  Revert "AUTORUBACK-718 feature spamalot push"
     
     This reverts commit 2bbdf9d2

  *  AUTORUBACK-718 feature spamalot push

  *  AUTORUBACK-718 turn off pushnoy in offer incomplete form (#669)
     

  *  minor changes

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-829 offer-form converter fix

  *  AUTORUBACK-718 add logged and metered for spamalot push (#668)
     
     * AUTORUBACK-718 add logged and metered for spamalot push
     
     * AUTORUBACK-718 npe hotfix
     
     * AUTORUBACK-718 test fix try
  *  AUTORUBACK-718 send offerincomplete push to spamalot (#666)
     
     * AUTORUBACK-718 send offerincomplete push to spamalot
     
     * AUTORUBACK-718 remove unused ConcurrencyUtils.scala
     
     * AUTORUBACK-718 add spamalot mock for test
     
     * AUTORUBACK-718 format
     review fix
     
     * AUTORUBACK-718 remove execution context from spamalot client
     fix spamalot config name
     
     * AUTORUBACK-718 try tests without lazy spamalotClient
     
     * AUTORUBACK-718 topic
  *  compilation fix

  *  update blur logging

  *  update blur parsing and logging

  *  Autoruback 870 spinkar ekt only (#665)
     
     * AUTORUBACK-870_spinkar_ekt_only
     
     * AUTORUBACK-870_spinkar_ekt_only: updated converter for searcher
  *  autoruback-632 (#664)
     
     * autoruback-632
     
     * autoruback-632
     
     * autoruback-632
     
     * autoruback-632
  *  Autoruback 632 (#660)
     
     * autoruback-632 -feature name fix
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
  *  VSDEALERS-297 # Set multiposting status (#658)
     

  *  AUTORUBACK-870_spinkar_ekt_only (#659)
     

  *  AUTORUBACK-753 refactoring (#654)
     
     * AUTORUBACK-753 refactoring
     
     * AUTORUBACK-753 format
  *  VSDEALERS-278 (#655)
     
     * added handler endpoints, service method, dao method
     
     * tests, doc, logic
     
     * it works
     
     * removed unused exception
     
     * review improvements
     
     * adde st to log
     
     * renamed trace
  *  VSDEALERS-256 hidden -> dealer_hidden for multiposting (#657)
     

  *  VSDEALERS-302 multiposting converters (#656)
     
     * VSDEALERS-302 multiposting converters
     
     * VSDEALERS-302 removed duplicated code
     
     * VSDEALERS-302 classified convertion
     
     * VSDEALERS-302 fixed test without multiposting
     
     * VSDEALERS-302 removed default multiposting status
     
     * VSDEALERS-302 redundant import removed
     
     * VSDEALERS-302 multiposting converter refactored
  *  VSDEALERS-256 Multiposting fields to shard propagation (#649)
     
     * VSDEALERS-256 Multiposting fields to shard propagation (for cars only yet)
     
     * VSDEALERS-256 Fixed offer generation in tests
     
     * VSDEALERS-256 multiposting propagation for trucks and moto
     
     * VSDEALERS-256 isActive utility usage + dealer offer check
     
     * VSDEALERS-256 tests fixed
     
     * VSDEALERS-256 hidden for user offers, dead code removed
     
     * VSDEALERS-256 banned offers disabled on dealer showcase
     
     * VSDEALERS-256 utility usage for ban check
  *  VSDEALERS-252 # Convert multiposting model VOS -> ApiOfferModel (#653)
     
     * VSDEALERS-252 # Convert multiposting model VOS -> ApiOfferModel
     
     * VSDEALERS-252 # fmt
  *  AUTORUBACK-753 upload document photos to offer (#646)
     
     * AUTORUBACK-753 add offer doc photo
     
     * AUTORUBACK-753 uncomment line
     
     * AUTORUBACK-753 remove DomainExceptionRenderer from PhotoDirectives
     
     * AUTORUBACK-753 imports optimized
     
     * AUTORUBACK-753 fix routing issues
     
     * AUTORUBACK-753 remove capturing group
     
     * code review todo
     
     * AUTORUBACK-753 revert draft id path segment behaviour
     
     * AUTORUBACK-753 fix issues
     
     * AUTORUBACK-753 rename toPhotoResponse
     
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-254 # Filter offers by multiposting_status and multiposting_service (#651)
     
     * VSDEALERS-254 # Filter offers by multiposting_status and multiposting_service
     
     * VSDEALERS-254 # FIX application.conf
     
     * VSDEALERS-254 # FIX dev configurations
     
     * VSDEALERS-254 # FIX remove service without expire_date
     
     * VSDEALERS-254 # FIX remove service without expire_date
     
     * VSDEALERS-254 # FIX swagger documentation
     
     * VSDEALERS-254 # CodeReview FIX
  *  autoruback-632 -feature name fix (#652)
     

  *  VSDEALERS-265 # Стейдж мультипостинга в VOS (#650)
     
     * VSDEALERS-265 # Стейдж мультипостинга в VOS
     
     * VSDEALERS-265 # Rename stage; minor fixes
     
     * VSDEALERS-265 # Refactor MultipostingStage#process
     
     * VSDEALERS-265 # Refactor MultipostingStage#process
  *  AUTORUBACK-829_vin_recognition_flag (#648)
     
     * AUTORUBACK-829_vin_recognition_flag
     
     * AUTORUBACK-829_vin_recognition_flag: updated schema-registry
  *  comments

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-857: updated logging and tracing error annotation

  *  VSDEALERS-308 # Multiposting classified is_enabled flag (#647)
     

  *  Revert "VSDEALERS-280 # Активация мультипостинговых объявлений по условию (#644)" (#645)
     
     This reverts commit 957e3d4f54bdc610ca4580b3b9fee66c047c635c.
  *  AUTORUBACK-632-scoring (#641)
     
     * AUTORUBACK-632-scoring
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/components/AutoruCoreComponents.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-280 # Активация мультипостинговых объявлений по условию (#644)
     
     * VSDEALERS-280 # Активация мультипостинговых объявлений по условию
     
     * VSDEALERS-280 # Refactor CommercialActivationStage#shouldProcess
     
     * VSDEALERS-280 # Check multiposting status
     
     * VSDEALERS-280 # Move hasActiveAutoruClassified to utils
     
     * VSDEALERS-280 # Refactor CommercialActivationStage#shouldProcess
  *  added drom classified (#643)
     

  *  AUTORUBACK-172_request_id_in_logs: fixed request context copy

  *  VSDEALERS-253 # Add index fields for multiposting (#639)
     
     * VSDEALERS-253 # Add index fields for multiposting
     
     * VSDEALERS-253 # Update DDL for index fields
     
     * VSDEALERS-253 # Add multiposting fields to AutoruOfferDao
  *  AUTORUBACK-172_request_id_in_logs, not finished (#636)
     
     * AUTORUBACK-172_request_id_in_logs, not finished
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, not finished
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, not finished: updated offer handler
     
     * AUTORUBACK-172_request_id_in_logs: exceptions refactoring
     
     * AUTORUBACK-172_request_id_in_logs: updated more managers and handlers
     
     * AUTORUBACK-172_request_id_in_logs: removed managers default error handling
     
     * AUTORUBACK-172_request_id_in_logs: able to compile and run
     
     * AUTORUBACK-172_request_id_in_logs: style and marshaller fixes
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: improved tests
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: short access logging
     
     * AUTORUBACK-172_request_id_in_logs: fixed test, todo
  *  VSDEALERS-252 added multiposting field (#638)
     
     * added multiposting field
     
     * removed field options
     
     * fixed id
  *  AUTORUBACK-745-ban (#637)
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/services/chat/HttpChatClient.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-679_photo_class (#635)
     
     * AUTORUBACK-679_photo_class
     
     * AUTORUBACK-679_photo_class: more changes
     
     * AUTORUBACK-679_photo_class: refactoring
     
     * AUTORUBACK-679_photo_class: AUTO_VIEW_3_4_BACK support
  *  AUTORUBACK-795 tracing fix (#633)
     
     * AUTORUBACK-795_tracing_fix
     
     * AUTORUBACK-795_tracing_fix: fixed more
     
     * AUTORUBACK-795_tracing_fix: refactoring
     
     * AUTORUBACK-795_tracing_fix: fixed test
     
     * AUTORUBACK-795_tracing_fix: style
  *  AUTORUBACK-603: Add stats endpoint (#625)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 21 Nov 2020 00:08:20 +0300

## yandex-vos2-autoru-ydb-workers:0.12.2 (Fri, 20 Nov 2020 23:35:42 +0300)

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: query name fix

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: query fix

  *  AUTORUBACK-126: batch updated support in query executor, mysql-to-ydb… (#721)
     
     * AUTORUBACK-126: batch updated support in query executor, mysql-to-ydb-migrator, statistician
     
     * AUTORUBACK-126: mysql-to-ydb-migrator stats
  *  AUTORUBACK-1006 palma 2.13 -> 2.12 fix 2

  *  AUTORUBACK-1006 palma 2.13 -> 2.12 fix

  *  AUTORUBACK-999: Don't show broken price ranges (#718)
     

  *  AUTORUBACK-977 new resolutions from moderation (#722)
     
     * AUTORUBACK-977 new resolutions from moderation
     
     * AUTORUBACK-977 new resolutions from moderation
     
     * AUTORUBACK-977 new resolutions from moderation
  *  VSDEALERSDECOMP-132 all drafts statuses sync (#720)
     
     * VSDEALERSDECOMP-132 set create_date if not presented
     
     * VSDEALERSDECOMP-132 multiposting and classified statuses set if not presented
     
     * VSDEALERSDECOMP-132 Code deduplication
     
     * VSDEALERSDECOMP-132 sync user-related statuses with enabled
     
     * VSDEALERSDECOMP-132 create_date only for enabled classifieds
     
     * VSDEALERSDECOMP-132 offer hidden check fixed
     
     * VSDEALERSDECOMP-132 statuses sync for drafts only
     
     * VSDEALERSDECOMP-132 removed redundant OfferFormConverter changes
     
     * VSDEALERSDECOMP-132 readable names for variables
     
     * VSDEALERSDECOMP-132 all drafts statuses sync
  *  VSDEALERSDECOMP-132 [multiposting] set create_date and statuses if not presented (#717)
     
     * VSDEALERSDECOMP-132 set create_date if not presented
     
     * VSDEALERSDECOMP-132 multiposting and classified statuses set if not presented
     
     * VSDEALERSDECOMP-132 Code deduplication
     
     * VSDEALERSDECOMP-132 sync user-related statuses with enabled
     
     * VSDEALERSDECOMP-132 create_date only for enabled classifieds
     
     * VSDEALERSDECOMP-132 offer hidden check fixed
     
     * VSDEALERSDECOMP-132 statuses sync for drafts only
     
     * VSDEALERSDECOMP-132 removed redundant OfferFormConverter changes
     
     * VSDEALERSDECOMP-132 readable names for variables
  *  compilation fix

  *  AUTORUBACK-1000 fixed holocron optLastDeactivateMoment calculation when no active events exist

  *  temporary test fix

  *  skypper: 11

  *  AUTORUBACK-879 interior panoramas routes for moderation (#715)
     
     * AUTORUBACK-879 interior panoramas routes for moderation +  fix status change
  *  AUTORUBACK-875 send images meta to broker (#716)
     
     * AUTORUBACK-875 send images meta to broker
     
     * review fixes
  *  AUTORUBACK-959: Не писать логи в файлы (#713)
     

  *  AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue (#712)
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydq update queue
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: fixed tests
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: added foreign key, fixed code
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: format
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: removed drop functionality
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: style
  *  Autoruback 126 ydb blobs update queue (#632)
     
     * AUTORUBACK-126_ydb_blobs_update_queue: fixed create methods to work in transactions
     
     * AUTORUBACK-126_ydb_blobs_update_queue: ydb error logging
  *  AUTORUBACK-976_archive_banned_dealers_fix (#711)
     

  *  VSDEALERS-436 # With removed offers for multiposting set status (#714)
     

  *  AUTORUBACK-754 send old holocron events: emergency queue scaling

  *  VSDEALERS-429 # FIX multiposting offer status migration (#709)
     
     * VSDEALERS-429 # FIX multiposting offer status migration
     
     * VSDEALERS-429 # More tests
  *  Autoruback 961 passport client and carfax report scoring fix (#706)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-911-fix-premium-user (#705)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-911 fixed issue with wrong premium
     
     * AUTORUBACK-911
  *  VSDEALERS-413 # Add offer_ids/by_vins handler (#703)
     

  *  AUTORUBACK-961 fixed issue with userNotFound (#704)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-807 callback to salon: added api to get salon from vos by verba-code

  *  VSDEALERS-416 # Set multiposting service expire_date sync + UpperCase FIX (#702)
     
     * VSDEALERS-416 # Set multiposting service expire_date sync + UpperCase fix
     
     * VSDEALERS-416 # Better naming
  *  AUTORUBACK-954 fixed issue with ComplaintsClient (#701)
     
     * AUTORUBACK-954 fixed issue with ComplaintsClient
     
     * AUTORUBACK-954 fixed issue with ComplaintsClient
  *  VSDEALERS-400 distinct services from form (#689)
     
     * VSDEALERS-400 clear services before add
     
     * VSDEALERS-400 distinct services from form
  *  VSDEALERS-402 Active services check fixed (#700)
     
     * VSDEALERS-402 Active services check fixed
     
     * VSDEALERS-402 uppercase index fields for multiposting services
     
     * VSDEALERS-402 uppercase classifieds services
     
     * VSDEALERS-402 tests fixed
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  AUTORUBACK-944 fixed issue with empty vin (#697)
     
     * fixed issue with empty vin
     
     * fixed issue with empty vin
     
     * additional logging update
  *  create_date for new classifieds (#698)
     
     * create_date for new classifieds
     
     * Sync classified create date with offer.create
     
     * compilation fixed
  *  Autoruback 911 fix containers (#695)
     
     * fixed version after merge
     
     * fixed version after merge
  *  fixed version after merge (#693)
     

  *  CARFAX-1157: Add options_updated flag (#690)
     

  *  AUTORUBACK-911 premium seller exp (#682)
     
     * autoruback-9§§
     
     * autoruback-911
     
     * autoruback-911 updated java version
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/UserAssistanceStage.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Merge branch 'master' into AUTORUBACK-911-premuim-seller-exp
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-400 clear services before add (#688)
     

  *  VSDEALERS-395 # Multiposting offer actions (#687)
     

  *  VSDEALERS-323 user ref parsing fixed (#686)
     

  *  VSDEALERS-323 Fixed producer config (#685)
     
     * VSDEALERS-323 multiposting events consumer
     
     * VSDEALERS-323 Fixed producer config
  *  VSDEALERS-323 multiposting events consumer (#681)
     

  *  AUTORUBACK-684 Allow to update offer discount options (#628)
     
     * AUTORUBACK-684 Allow to update offer discount options
     
     * AUTORUBACK-684_update-offer-discount
     
     * query, uptime, workers, todo
     
     * updated schema registry
     
     * AUTORUBACK-684_update-offer-discount: style
     
     * AUTORUBACK-684_update-offer-discount: fixed tests
     
     * AUTORUBACK-684_update-offer-discount: save discount options to old db (not finished), updated responses, updated tests, refactoring
     
     * AUTORUBACK-684_update-offer-discount: todo
     
     * Merge branch 'master' into AUTORUBACK-684_update-offer-discount
     
     # Conflicts:
     #	pom.xml
     #	vos2-autoru-api/src/main/scala/ru/yandex/vos2/autoru/api/v1/offer/OfferHandler.scala
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/OffersWriter.scala
     
     * AUTORUBACK-684_update-offer-discount: fixes after merge
     
     * AUTORUBACK-684_update-offer-discount: style
     
     * AUTORUBACK-684_update-offer-discount: updated schema-registry
     
     * AUTORUBACK-684_update-offer-discount: revert some changes
     
     * AUTORUBACK-684_update-offer-discount: revert some changes
     
     * AUTORUBACK-684_update-offer-discount: compilation fixes and refactoring
     
     * AUTORUBACK-684_update-offer-discount: removed photo utils from statuses manager
     
     * AUTORUBACK-684_price_attribute_return
     
     * AUTORUBACK-684_update-offer-discount_model_update: save discount options to old db
     
     * AUTORUBACK-684_update-offer-discount_model_update: fixed tests, refactoring
     
     * AUTORUBACK-684_update-offer-discount_model_update: fix after merge
     
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-373 # Allow to enable/disable multiposting for user by id (#679)
     
     * VSDEALERS-373 # Allow to enable/disable multiposting for user by id
     
     * VSDEALERS-373 # Update tests
     
     * VSDEALERS-373 # Minor refactor
     
     * VSDEALERS-373 # Minor refactor
     
     * VSDEALERS-373 # Minor fixes
     
     * VSDEALERS-373 # Select all offers when activate multiposting
     
     * VSDEALERS-373 # Explicitly filter statuses
     
     * VSDEALERS-373 # Wrap in withoutErrors
  *  VSDEALERS-289 Fixed services duplication (#680)
     

  *  AUTORUBACK-904 silent push (#678)
     

  *  AUTORUBACK-922: added kafka props for extended holocron

  *  VSDEALERS-277 # Update classified state handlers logic (#677)
     
     * VSDEALERS-277 # Update classified state handlers logic
     
     * VSDEALERS-277 # Update OfferHandlerTest
  *  VSDEALERS-289 services deduplication (#675)
     
     * VSDEALERS-289 classified services model changed
     
     * VSDEALERS-289 services deduplication
     
     * VSDEALERS-289 build the builder
     
     * VSDEALERS-289 fixed doc
     
     * VSDEALERS-289 Don't reactivated disabled services
     
     * VSDEALERS-289 Don't remove old services
     
     * VSDEALERS-289 classified -> multiposting
     
     * VSDEALERS-289 renaming
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  AUTORUBACK-835 change call info renderer message (#674)
     

  *  AUTORUBACK-906 remove nullable fields (#673)
     

  *  AUTORUBACK-906 extend common feature response with tags and info (#672)
     

  *  AUTORUBACK-718 feature spamalot push (#670)
     

  *  Revert "AUTORUBACK-718 feature spamalot push"
     
     This reverts commit 2bbdf9d2

  *  AUTORUBACK-718 feature spamalot push

  *  AUTORUBACK-718 turn off pushnoy in offer incomplete form (#669)
     

  *  minor changes

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-829 offer-form converter fix

  *  AUTORUBACK-718 add logged and metered for spamalot push (#668)
     
     * AUTORUBACK-718 add logged and metered for spamalot push
     
     * AUTORUBACK-718 npe hotfix
     
     * AUTORUBACK-718 test fix try
  *  AUTORUBACK-718 send offerincomplete push to spamalot (#666)
     
     * AUTORUBACK-718 send offerincomplete push to spamalot
     
     * AUTORUBACK-718 remove unused ConcurrencyUtils.scala
     
     * AUTORUBACK-718 add spamalot mock for test
     
     * AUTORUBACK-718 format
     review fix
     
     * AUTORUBACK-718 remove execution context from spamalot client
     fix spamalot config name
     
     * AUTORUBACK-718 try tests without lazy spamalotClient
     
     * AUTORUBACK-718 topic
  *  compilation fix

  *  update blur logging

  *  update blur parsing and logging

  *  Autoruback 870 spinkar ekt only (#665)
     
     * AUTORUBACK-870_spinkar_ekt_only
     
     * AUTORUBACK-870_spinkar_ekt_only: updated converter for searcher
  *  autoruback-632 (#664)
     
     * autoruback-632
     
     * autoruback-632
     
     * autoruback-632
     
     * autoruback-632
  *  Autoruback 632 (#660)
     
     * autoruback-632 -feature name fix
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
  *  VSDEALERS-297 # Set multiposting status (#658)
     

  *  AUTORUBACK-870_spinkar_ekt_only (#659)
     

  *  AUTORUBACK-753 refactoring (#654)
     
     * AUTORUBACK-753 refactoring
     
     * AUTORUBACK-753 format
  *  VSDEALERS-278 (#655)
     
     * added handler endpoints, service method, dao method
     
     * tests, doc, logic
     
     * it works
     
     * removed unused exception
     
     * review improvements
     
     * adde st to log
     
     * renamed trace
  *  VSDEALERS-256 hidden -> dealer_hidden for multiposting (#657)
     

  *  VSDEALERS-302 multiposting converters (#656)
     
     * VSDEALERS-302 multiposting converters
     
     * VSDEALERS-302 removed duplicated code
     
     * VSDEALERS-302 classified convertion
     
     * VSDEALERS-302 fixed test without multiposting
     
     * VSDEALERS-302 removed default multiposting status
     
     * VSDEALERS-302 redundant import removed
     
     * VSDEALERS-302 multiposting converter refactored
  *  VSDEALERS-256 Multiposting fields to shard propagation (#649)
     
     * VSDEALERS-256 Multiposting fields to shard propagation (for cars only yet)
     
     * VSDEALERS-256 Fixed offer generation in tests
     
     * VSDEALERS-256 multiposting propagation for trucks and moto
     
     * VSDEALERS-256 isActive utility usage + dealer offer check
     
     * VSDEALERS-256 tests fixed
     
     * VSDEALERS-256 hidden for user offers, dead code removed
     
     * VSDEALERS-256 banned offers disabled on dealer showcase
     
     * VSDEALERS-256 utility usage for ban check
  *  VSDEALERS-252 # Convert multiposting model VOS -> ApiOfferModel (#653)
     
     * VSDEALERS-252 # Convert multiposting model VOS -> ApiOfferModel
     
     * VSDEALERS-252 # fmt
  *  AUTORUBACK-753 upload document photos to offer (#646)
     
     * AUTORUBACK-753 add offer doc photo
     
     * AUTORUBACK-753 uncomment line
     
     * AUTORUBACK-753 remove DomainExceptionRenderer from PhotoDirectives
     
     * AUTORUBACK-753 imports optimized
     
     * AUTORUBACK-753 fix routing issues
     
     * AUTORUBACK-753 remove capturing group
     
     * code review todo
     
     * AUTORUBACK-753 revert draft id path segment behaviour
     
     * AUTORUBACK-753 fix issues
     
     * AUTORUBACK-753 rename toPhotoResponse
     
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-254 # Filter offers by multiposting_status and multiposting_service (#651)
     
     * VSDEALERS-254 # Filter offers by multiposting_status and multiposting_service
     
     * VSDEALERS-254 # FIX application.conf
     
     * VSDEALERS-254 # FIX dev configurations
     
     * VSDEALERS-254 # FIX remove service without expire_date
     
     * VSDEALERS-254 # FIX remove service without expire_date
     
     * VSDEALERS-254 # FIX swagger documentation
     
     * VSDEALERS-254 # CodeReview FIX
  *  autoruback-632 -feature name fix (#652)
     

  *  VSDEALERS-265 # Стейдж мультипостинга в VOS (#650)
     
     * VSDEALERS-265 # Стейдж мультипостинга в VOS
     
     * VSDEALERS-265 # Rename stage; minor fixes
     
     * VSDEALERS-265 # Refactor MultipostingStage#process
     
     * VSDEALERS-265 # Refactor MultipostingStage#process
  *  AUTORUBACK-829_vin_recognition_flag (#648)
     
     * AUTORUBACK-829_vin_recognition_flag
     
     * AUTORUBACK-829_vin_recognition_flag: updated schema-registry
  *  comments

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-857: updated logging and tracing error annotation

  *  VSDEALERS-308 # Multiposting classified is_enabled flag (#647)
     

  *  Revert "VSDEALERS-280 # Активация мультипостинговых объявлений по условию (#644)" (#645)
     
     This reverts commit 957e3d4f54bdc610ca4580b3b9fee66c047c635c.
  *  AUTORUBACK-632-scoring (#641)
     
     * AUTORUBACK-632-scoring
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/components/AutoruCoreComponents.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-280 # Активация мультипостинговых объявлений по условию (#644)
     
     * VSDEALERS-280 # Активация мультипостинговых объявлений по условию
     
     * VSDEALERS-280 # Refactor CommercialActivationStage#shouldProcess
     
     * VSDEALERS-280 # Check multiposting status
     
     * VSDEALERS-280 # Move hasActiveAutoruClassified to utils
     
     * VSDEALERS-280 # Refactor CommercialActivationStage#shouldProcess
  *  added drom classified (#643)
     

  *  AUTORUBACK-172_request_id_in_logs: fixed request context copy

  *  VSDEALERS-253 # Add index fields for multiposting (#639)
     
     * VSDEALERS-253 # Add index fields for multiposting
     
     * VSDEALERS-253 # Update DDL for index fields
     
     * VSDEALERS-253 # Add multiposting fields to AutoruOfferDao
  *  AUTORUBACK-172_request_id_in_logs, not finished (#636)
     
     * AUTORUBACK-172_request_id_in_logs, not finished
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, not finished
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, not finished: updated offer handler
     
     * AUTORUBACK-172_request_id_in_logs: exceptions refactoring
     
     * AUTORUBACK-172_request_id_in_logs: updated more managers and handlers
     
     * AUTORUBACK-172_request_id_in_logs: removed managers default error handling
     
     * AUTORUBACK-172_request_id_in_logs: able to compile and run
     
     * AUTORUBACK-172_request_id_in_logs: style and marshaller fixes
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: improved tests
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: short access logging
     
     * AUTORUBACK-172_request_id_in_logs: fixed test, todo
  *  VSDEALERS-252 added multiposting field (#638)
     
     * added multiposting field
     
     * removed field options
     
     * fixed id
  *  AUTORUBACK-745-ban (#637)
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/services/chat/HttpChatClient.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-679_photo_class (#635)
     
     * AUTORUBACK-679_photo_class
     
     * AUTORUBACK-679_photo_class: more changes
     
     * AUTORUBACK-679_photo_class: refactoring
     
     * AUTORUBACK-679_photo_class: AUTO_VIEW_3_4_BACK support
  *  AUTORUBACK-795 tracing fix (#633)
     
     * AUTORUBACK-795_tracing_fix
     
     * AUTORUBACK-795_tracing_fix: fixed more
     
     * AUTORUBACK-795_tracing_fix: refactoring
     
     * AUTORUBACK-795_tracing_fix: fixed test
     
     * AUTORUBACK-795_tracing_fix: style
  *  AUTORUBACK-603: Add stats endpoint (#625)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 20 Nov 2020 23:35:42 +0300

## yandex-vos2-autoru-ydb-workers:0.12.1 (Fri, 20 Nov 2020 23:11:08 +0300)

  *  AUTORUBACK-126: mysql-to-ydb-migrator stats: query fix

  *  AUTORUBACK-126: batch updated support in query executor, mysql-to-ydb… (#721)
     
     * AUTORUBACK-126: batch updated support in query executor, mysql-to-ydb-migrator, statistician
     
     * AUTORUBACK-126: mysql-to-ydb-migrator stats
  *  AUTORUBACK-1006 palma 2.13 -> 2.12 fix 2

  *  AUTORUBACK-1006 palma 2.13 -> 2.12 fix

  *  AUTORUBACK-999: Don't show broken price ranges (#718)
     

  *  AUTORUBACK-977 new resolutions from moderation (#722)
     
     * AUTORUBACK-977 new resolutions from moderation
     
     * AUTORUBACK-977 new resolutions from moderation
     
     * AUTORUBACK-977 new resolutions from moderation
  *  VSDEALERSDECOMP-132 all drafts statuses sync (#720)
     
     * VSDEALERSDECOMP-132 set create_date if not presented
     
     * VSDEALERSDECOMP-132 multiposting and classified statuses set if not presented
     
     * VSDEALERSDECOMP-132 Code deduplication
     
     * VSDEALERSDECOMP-132 sync user-related statuses with enabled
     
     * VSDEALERSDECOMP-132 create_date only for enabled classifieds
     
     * VSDEALERSDECOMP-132 offer hidden check fixed
     
     * VSDEALERSDECOMP-132 statuses sync for drafts only
     
     * VSDEALERSDECOMP-132 removed redundant OfferFormConverter changes
     
     * VSDEALERSDECOMP-132 readable names for variables
     
     * VSDEALERSDECOMP-132 all drafts statuses sync
  *  VSDEALERSDECOMP-132 [multiposting] set create_date and statuses if not presented (#717)
     
     * VSDEALERSDECOMP-132 set create_date if not presented
     
     * VSDEALERSDECOMP-132 multiposting and classified statuses set if not presented
     
     * VSDEALERSDECOMP-132 Code deduplication
     
     * VSDEALERSDECOMP-132 sync user-related statuses with enabled
     
     * VSDEALERSDECOMP-132 create_date only for enabled classifieds
     
     * VSDEALERSDECOMP-132 offer hidden check fixed
     
     * VSDEALERSDECOMP-132 statuses sync for drafts only
     
     * VSDEALERSDECOMP-132 removed redundant OfferFormConverter changes
     
     * VSDEALERSDECOMP-132 readable names for variables
  *  compilation fix

  *  AUTORUBACK-1000 fixed holocron optLastDeactivateMoment calculation when no active events exist

  *  temporary test fix

  *  skypper: 11

  *  AUTORUBACK-879 interior panoramas routes for moderation (#715)
     
     * AUTORUBACK-879 interior panoramas routes for moderation +  fix status change
  *  AUTORUBACK-875 send images meta to broker (#716)
     
     * AUTORUBACK-875 send images meta to broker
     
     * review fixes
  *  AUTORUBACK-959: Не писать логи в файлы (#713)
     

  *  AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue (#712)
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydq update queue
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: fixed tests
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: added foreign key, fixed code
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: format
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: removed drop functionality
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: style
  *  Autoruback 126 ydb blobs update queue (#632)
     
     * AUTORUBACK-126_ydb_blobs_update_queue: fixed create methods to work in transactions
     
     * AUTORUBACK-126_ydb_blobs_update_queue: ydb error logging
  *  AUTORUBACK-976_archive_banned_dealers_fix (#711)
     

  *  VSDEALERS-436 # With removed offers for multiposting set status (#714)
     

  *  AUTORUBACK-754 send old holocron events: emergency queue scaling

  *  VSDEALERS-429 # FIX multiposting offer status migration (#709)
     
     * VSDEALERS-429 # FIX multiposting offer status migration
     
     * VSDEALERS-429 # More tests
  *  Autoruback 961 passport client and carfax report scoring fix (#706)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-911-fix-premium-user (#705)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-911 fixed issue with wrong premium
     
     * AUTORUBACK-911
  *  VSDEALERS-413 # Add offer_ids/by_vins handler (#703)
     

  *  AUTORUBACK-961 fixed issue with userNotFound (#704)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-807 callback to salon: added api to get salon from vos by verba-code

  *  VSDEALERS-416 # Set multiposting service expire_date sync + UpperCase FIX (#702)
     
     * VSDEALERS-416 # Set multiposting service expire_date sync + UpperCase fix
     
     * VSDEALERS-416 # Better naming
  *  AUTORUBACK-954 fixed issue with ComplaintsClient (#701)
     
     * AUTORUBACK-954 fixed issue with ComplaintsClient
     
     * AUTORUBACK-954 fixed issue with ComplaintsClient
  *  VSDEALERS-400 distinct services from form (#689)
     
     * VSDEALERS-400 clear services before add
     
     * VSDEALERS-400 distinct services from form
  *  VSDEALERS-402 Active services check fixed (#700)
     
     * VSDEALERS-402 Active services check fixed
     
     * VSDEALERS-402 uppercase index fields for multiposting services
     
     * VSDEALERS-402 uppercase classifieds services
     
     * VSDEALERS-402 tests fixed
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  AUTORUBACK-944 fixed issue with empty vin (#697)
     
     * fixed issue with empty vin
     
     * fixed issue with empty vin
     
     * additional logging update
  *  create_date for new classifieds (#698)
     
     * create_date for new classifieds
     
     * Sync classified create date with offer.create
     
     * compilation fixed
  *  Autoruback 911 fix containers (#695)
     
     * fixed version after merge
     
     * fixed version after merge
  *  fixed version after merge (#693)
     

  *  CARFAX-1157: Add options_updated flag (#690)
     

  *  AUTORUBACK-911 premium seller exp (#682)
     
     * autoruback-9§§
     
     * autoruback-911
     
     * autoruback-911 updated java version
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/UserAssistanceStage.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Merge branch 'master' into AUTORUBACK-911-premuim-seller-exp
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-400 clear services before add (#688)
     

  *  VSDEALERS-395 # Multiposting offer actions (#687)
     

  *  VSDEALERS-323 user ref parsing fixed (#686)
     

  *  VSDEALERS-323 Fixed producer config (#685)
     
     * VSDEALERS-323 multiposting events consumer
     
     * VSDEALERS-323 Fixed producer config
  *  VSDEALERS-323 multiposting events consumer (#681)
     

  *  AUTORUBACK-684 Allow to update offer discount options (#628)
     
     * AUTORUBACK-684 Allow to update offer discount options
     
     * AUTORUBACK-684_update-offer-discount
     
     * query, uptime, workers, todo
     
     * updated schema registry
     
     * AUTORUBACK-684_update-offer-discount: style
     
     * AUTORUBACK-684_update-offer-discount: fixed tests
     
     * AUTORUBACK-684_update-offer-discount: save discount options to old db (not finished), updated responses, updated tests, refactoring
     
     * AUTORUBACK-684_update-offer-discount: todo
     
     * Merge branch 'master' into AUTORUBACK-684_update-offer-discount
     
     # Conflicts:
     #	pom.xml
     #	vos2-autoru-api/src/main/scala/ru/yandex/vos2/autoru/api/v1/offer/OfferHandler.scala
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/OffersWriter.scala
     
     * AUTORUBACK-684_update-offer-discount: fixes after merge
     
     * AUTORUBACK-684_update-offer-discount: style
     
     * AUTORUBACK-684_update-offer-discount: updated schema-registry
     
     * AUTORUBACK-684_update-offer-discount: revert some changes
     
     * AUTORUBACK-684_update-offer-discount: revert some changes
     
     * AUTORUBACK-684_update-offer-discount: compilation fixes and refactoring
     
     * AUTORUBACK-684_update-offer-discount: removed photo utils from statuses manager
     
     * AUTORUBACK-684_price_attribute_return
     
     * AUTORUBACK-684_update-offer-discount_model_update: save discount options to old db
     
     * AUTORUBACK-684_update-offer-discount_model_update: fixed tests, refactoring
     
     * AUTORUBACK-684_update-offer-discount_model_update: fix after merge
     
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-373 # Allow to enable/disable multiposting for user by id (#679)
     
     * VSDEALERS-373 # Allow to enable/disable multiposting for user by id
     
     * VSDEALERS-373 # Update tests
     
     * VSDEALERS-373 # Minor refactor
     
     * VSDEALERS-373 # Minor refactor
     
     * VSDEALERS-373 # Minor fixes
     
     * VSDEALERS-373 # Select all offers when activate multiposting
     
     * VSDEALERS-373 # Explicitly filter statuses
     
     * VSDEALERS-373 # Wrap in withoutErrors
  *  VSDEALERS-289 Fixed services duplication (#680)
     

  *  AUTORUBACK-904 silent push (#678)
     

  *  AUTORUBACK-922: added kafka props for extended holocron

  *  VSDEALERS-277 # Update classified state handlers logic (#677)
     
     * VSDEALERS-277 # Update classified state handlers logic
     
     * VSDEALERS-277 # Update OfferHandlerTest
  *  VSDEALERS-289 services deduplication (#675)
     
     * VSDEALERS-289 classified services model changed
     
     * VSDEALERS-289 services deduplication
     
     * VSDEALERS-289 build the builder
     
     * VSDEALERS-289 fixed doc
     
     * VSDEALERS-289 Don't reactivated disabled services
     
     * VSDEALERS-289 Don't remove old services
     
     * VSDEALERS-289 classified -> multiposting
     
     * VSDEALERS-289 renaming
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  AUTORUBACK-835 change call info renderer message (#674)
     

  *  AUTORUBACK-906 remove nullable fields (#673)
     

  *  AUTORUBACK-906 extend common feature response with tags and info (#672)
     

  *  AUTORUBACK-718 feature spamalot push (#670)
     

  *  Revert "AUTORUBACK-718 feature spamalot push"
     
     This reverts commit 2bbdf9d2

  *  AUTORUBACK-718 feature spamalot push

  *  AUTORUBACK-718 turn off pushnoy in offer incomplete form (#669)
     

  *  minor changes

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-829 offer-form converter fix

  *  AUTORUBACK-718 add logged and metered for spamalot push (#668)
     
     * AUTORUBACK-718 add logged and metered for spamalot push
     
     * AUTORUBACK-718 npe hotfix
     
     * AUTORUBACK-718 test fix try
  *  AUTORUBACK-718 send offerincomplete push to spamalot (#666)
     
     * AUTORUBACK-718 send offerincomplete push to spamalot
     
     * AUTORUBACK-718 remove unused ConcurrencyUtils.scala
     
     * AUTORUBACK-718 add spamalot mock for test
     
     * AUTORUBACK-718 format
     review fix
     
     * AUTORUBACK-718 remove execution context from spamalot client
     fix spamalot config name
     
     * AUTORUBACK-718 try tests without lazy spamalotClient
     
     * AUTORUBACK-718 topic
  *  compilation fix

  *  update blur logging

  *  update blur parsing and logging

  *  Autoruback 870 spinkar ekt only (#665)
     
     * AUTORUBACK-870_spinkar_ekt_only
     
     * AUTORUBACK-870_spinkar_ekt_only: updated converter for searcher
  *  autoruback-632 (#664)
     
     * autoruback-632
     
     * autoruback-632
     
     * autoruback-632
     
     * autoruback-632
  *  Autoruback 632 (#660)
     
     * autoruback-632 -feature name fix
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
  *  VSDEALERS-297 # Set multiposting status (#658)
     

  *  AUTORUBACK-870_spinkar_ekt_only (#659)
     

  *  AUTORUBACK-753 refactoring (#654)
     
     * AUTORUBACK-753 refactoring
     
     * AUTORUBACK-753 format
  *  VSDEALERS-278 (#655)
     
     * added handler endpoints, service method, dao method
     
     * tests, doc, logic
     
     * it works
     
     * removed unused exception
     
     * review improvements
     
     * adde st to log
     
     * renamed trace
  *  VSDEALERS-256 hidden -> dealer_hidden for multiposting (#657)
     

  *  VSDEALERS-302 multiposting converters (#656)
     
     * VSDEALERS-302 multiposting converters
     
     * VSDEALERS-302 removed duplicated code
     
     * VSDEALERS-302 classified convertion
     
     * VSDEALERS-302 fixed test without multiposting
     
     * VSDEALERS-302 removed default multiposting status
     
     * VSDEALERS-302 redundant import removed
     
     * VSDEALERS-302 multiposting converter refactored
  *  VSDEALERS-256 Multiposting fields to shard propagation (#649)
     
     * VSDEALERS-256 Multiposting fields to shard propagation (for cars only yet)
     
     * VSDEALERS-256 Fixed offer generation in tests
     
     * VSDEALERS-256 multiposting propagation for trucks and moto
     
     * VSDEALERS-256 isActive utility usage + dealer offer check
     
     * VSDEALERS-256 tests fixed
     
     * VSDEALERS-256 hidden for user offers, dead code removed
     
     * VSDEALERS-256 banned offers disabled on dealer showcase
     
     * VSDEALERS-256 utility usage for ban check
  *  VSDEALERS-252 # Convert multiposting model VOS -> ApiOfferModel (#653)
     
     * VSDEALERS-252 # Convert multiposting model VOS -> ApiOfferModel
     
     * VSDEALERS-252 # fmt
  *  AUTORUBACK-753 upload document photos to offer (#646)
     
     * AUTORUBACK-753 add offer doc photo
     
     * AUTORUBACK-753 uncomment line
     
     * AUTORUBACK-753 remove DomainExceptionRenderer from PhotoDirectives
     
     * AUTORUBACK-753 imports optimized
     
     * AUTORUBACK-753 fix routing issues
     
     * AUTORUBACK-753 remove capturing group
     
     * code review todo
     
     * AUTORUBACK-753 revert draft id path segment behaviour
     
     * AUTORUBACK-753 fix issues
     
     * AUTORUBACK-753 rename toPhotoResponse
     
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-254 # Filter offers by multiposting_status and multiposting_service (#651)
     
     * VSDEALERS-254 # Filter offers by multiposting_status and multiposting_service
     
     * VSDEALERS-254 # FIX application.conf
     
     * VSDEALERS-254 # FIX dev configurations
     
     * VSDEALERS-254 # FIX remove service without expire_date
     
     * VSDEALERS-254 # FIX remove service without expire_date
     
     * VSDEALERS-254 # FIX swagger documentation
     
     * VSDEALERS-254 # CodeReview FIX
  *  autoruback-632 -feature name fix (#652)
     

  *  VSDEALERS-265 # Стейдж мультипостинга в VOS (#650)
     
     * VSDEALERS-265 # Стейдж мультипостинга в VOS
     
     * VSDEALERS-265 # Rename stage; minor fixes
     
     * VSDEALERS-265 # Refactor MultipostingStage#process
     
     * VSDEALERS-265 # Refactor MultipostingStage#process
  *  AUTORUBACK-829_vin_recognition_flag (#648)
     
     * AUTORUBACK-829_vin_recognition_flag
     
     * AUTORUBACK-829_vin_recognition_flag: updated schema-registry
  *  comments

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-857: updated logging and tracing error annotation

  *  VSDEALERS-308 # Multiposting classified is_enabled flag (#647)
     

  *  Revert "VSDEALERS-280 # Активация мультипостинговых объявлений по условию (#644)" (#645)
     
     This reverts commit 957e3d4f54bdc610ca4580b3b9fee66c047c635c.
  *  AUTORUBACK-632-scoring (#641)
     
     * AUTORUBACK-632-scoring
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/components/AutoruCoreComponents.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-280 # Активация мультипостинговых объявлений по условию (#644)
     
     * VSDEALERS-280 # Активация мультипостинговых объявлений по условию
     
     * VSDEALERS-280 # Refactor CommercialActivationStage#shouldProcess
     
     * VSDEALERS-280 # Check multiposting status
     
     * VSDEALERS-280 # Move hasActiveAutoruClassified to utils
     
     * VSDEALERS-280 # Refactor CommercialActivationStage#shouldProcess
  *  added drom classified (#643)
     

  *  AUTORUBACK-172_request_id_in_logs: fixed request context copy

  *  VSDEALERS-253 # Add index fields for multiposting (#639)
     
     * VSDEALERS-253 # Add index fields for multiposting
     
     * VSDEALERS-253 # Update DDL for index fields
     
     * VSDEALERS-253 # Add multiposting fields to AutoruOfferDao
  *  AUTORUBACK-172_request_id_in_logs, not finished (#636)
     
     * AUTORUBACK-172_request_id_in_logs, not finished
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, not finished
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, not finished: updated offer handler
     
     * AUTORUBACK-172_request_id_in_logs: exceptions refactoring
     
     * AUTORUBACK-172_request_id_in_logs: updated more managers and handlers
     
     * AUTORUBACK-172_request_id_in_logs: removed managers default error handling
     
     * AUTORUBACK-172_request_id_in_logs: able to compile and run
     
     * AUTORUBACK-172_request_id_in_logs: style and marshaller fixes
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: improved tests
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: short access logging
     
     * AUTORUBACK-172_request_id_in_logs: fixed test, todo
  *  VSDEALERS-252 added multiposting field (#638)
     
     * added multiposting field
     
     * removed field options
     
     * fixed id
  *  AUTORUBACK-745-ban (#637)
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/services/chat/HttpChatClient.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-679_photo_class (#635)
     
     * AUTORUBACK-679_photo_class
     
     * AUTORUBACK-679_photo_class: more changes
     
     * AUTORUBACK-679_photo_class: refactoring
     
     * AUTORUBACK-679_photo_class: AUTO_VIEW_3_4_BACK support
  *  AUTORUBACK-795 tracing fix (#633)
     
     * AUTORUBACK-795_tracing_fix
     
     * AUTORUBACK-795_tracing_fix: fixed more
     
     * AUTORUBACK-795_tracing_fix: refactoring
     
     * AUTORUBACK-795_tracing_fix: fixed test
     
     * AUTORUBACK-795_tracing_fix: style
  *  AUTORUBACK-603: Add stats endpoint (#625)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 20 Nov 2020 23:11:08 +0300

## yandex-vos2-autoru-ydb-workers:0.12.0 (Fri, 20 Nov 2020 22:31:25 +0300)

  *  AUTORUBACK-126: batch updated support in query executor, mysql-to-ydb… (#721)
     
     * AUTORUBACK-126: batch updated support in query executor, mysql-to-ydb-migrator, statistician
     
     * AUTORUBACK-126: mysql-to-ydb-migrator stats
  *  AUTORUBACK-1006 palma 2.13 -> 2.12 fix 2

  *  AUTORUBACK-1006 palma 2.13 -> 2.12 fix

  *  AUTORUBACK-999: Don't show broken price ranges (#718)
     

  *  AUTORUBACK-977 new resolutions from moderation (#722)
     
     * AUTORUBACK-977 new resolutions from moderation
     
     * AUTORUBACK-977 new resolutions from moderation
     
     * AUTORUBACK-977 new resolutions from moderation
  *  VSDEALERSDECOMP-132 all drafts statuses sync (#720)
     
     * VSDEALERSDECOMP-132 set create_date if not presented
     
     * VSDEALERSDECOMP-132 multiposting and classified statuses set if not presented
     
     * VSDEALERSDECOMP-132 Code deduplication
     
     * VSDEALERSDECOMP-132 sync user-related statuses with enabled
     
     * VSDEALERSDECOMP-132 create_date only for enabled classifieds
     
     * VSDEALERSDECOMP-132 offer hidden check fixed
     
     * VSDEALERSDECOMP-132 statuses sync for drafts only
     
     * VSDEALERSDECOMP-132 removed redundant OfferFormConverter changes
     
     * VSDEALERSDECOMP-132 readable names for variables
     
     * VSDEALERSDECOMP-132 all drafts statuses sync
  *  VSDEALERSDECOMP-132 [multiposting] set create_date and statuses if not presented (#717)
     
     * VSDEALERSDECOMP-132 set create_date if not presented
     
     * VSDEALERSDECOMP-132 multiposting and classified statuses set if not presented
     
     * VSDEALERSDECOMP-132 Code deduplication
     
     * VSDEALERSDECOMP-132 sync user-related statuses with enabled
     
     * VSDEALERSDECOMP-132 create_date only for enabled classifieds
     
     * VSDEALERSDECOMP-132 offer hidden check fixed
     
     * VSDEALERSDECOMP-132 statuses sync for drafts only
     
     * VSDEALERSDECOMP-132 removed redundant OfferFormConverter changes
     
     * VSDEALERSDECOMP-132 readable names for variables
  *  compilation fix

  *  AUTORUBACK-1000 fixed holocron optLastDeactivateMoment calculation when no active events exist

  *  temporary test fix

  *  skypper: 11

  *  AUTORUBACK-879 interior panoramas routes for moderation (#715)
     
     * AUTORUBACK-879 interior panoramas routes for moderation +  fix status change
  *  AUTORUBACK-875 send images meta to broker (#716)
     
     * AUTORUBACK-875 send images meta to broker
     
     * review fixes
  *  AUTORUBACK-959: Не писать логи в файлы (#713)
     

  *  AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue (#712)
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydq update queue
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: fixed tests
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: added foreign key, fixed code
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: format
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: removed drop functionality
     
     * AUTORUBACK-126_vos_in_ydb: save offer ids to ydb update queue: style
  *  Autoruback 126 ydb blobs update queue (#632)
     
     * AUTORUBACK-126_ydb_blobs_update_queue: fixed create methods to work in transactions
     
     * AUTORUBACK-126_ydb_blobs_update_queue: ydb error logging
  *  AUTORUBACK-976_archive_banned_dealers_fix (#711)
     

  *  VSDEALERS-436 # With removed offers for multiposting set status (#714)
     

  *  AUTORUBACK-754 send old holocron events: emergency queue scaling

  *  VSDEALERS-429 # FIX multiposting offer status migration (#709)
     
     * VSDEALERS-429 # FIX multiposting offer status migration
     
     * VSDEALERS-429 # More tests
  *  Autoruback 961 passport client and carfax report scoring fix (#706)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-911-fix-premium-user (#705)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-911 fixed issue with wrong premium
     
     * AUTORUBACK-911
  *  VSDEALERS-413 # Add offer_ids/by_vins handler (#703)
     

  *  AUTORUBACK-961 fixed issue with userNotFound (#704)
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961 fixed issue with userNotFound
     
     * AUTORUBACK-961
     
     * AUTORUBACK-961
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-807 callback to salon: added api to get salon from vos by verba-code

  *  VSDEALERS-416 # Set multiposting service expire_date sync + UpperCase FIX (#702)
     
     * VSDEALERS-416 # Set multiposting service expire_date sync + UpperCase fix
     
     * VSDEALERS-416 # Better naming
  *  AUTORUBACK-954 fixed issue with ComplaintsClient (#701)
     
     * AUTORUBACK-954 fixed issue with ComplaintsClient
     
     * AUTORUBACK-954 fixed issue with ComplaintsClient
  *  VSDEALERS-400 distinct services from form (#689)
     
     * VSDEALERS-400 clear services before add
     
     * VSDEALERS-400 distinct services from form
  *  VSDEALERS-402 Active services check fixed (#700)
     
     * VSDEALERS-402 Active services check fixed
     
     * VSDEALERS-402 uppercase index fields for multiposting services
     
     * VSDEALERS-402 uppercase classifieds services
     
     * VSDEALERS-402 tests fixed
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  AUTORUBACK-944 fixed issue with empty vin (#697)
     
     * fixed issue with empty vin
     
     * fixed issue with empty vin
     
     * additional logging update
  *  create_date for new classifieds (#698)
     
     * create_date for new classifieds
     
     * Sync classified create date with offer.create
     
     * compilation fixed
  *  Autoruback 911 fix containers (#695)
     
     * fixed version after merge
     
     * fixed version after merge
  *  fixed version after merge (#693)
     

  *  CARFAX-1157: Add options_updated flag (#690)
     

  *  AUTORUBACK-911 premium seller exp (#682)
     
     * autoruback-9§§
     
     * autoruback-911
     
     * autoruback-911 updated java version
     
     * Update vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/UserAssistanceStage.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Merge branch 'master' into AUTORUBACK-911-premuim-seller-exp
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     * fixed tests
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-400 clear services before add (#688)
     

  *  VSDEALERS-395 # Multiposting offer actions (#687)
     

  *  VSDEALERS-323 user ref parsing fixed (#686)
     

  *  VSDEALERS-323 Fixed producer config (#685)
     
     * VSDEALERS-323 multiposting events consumer
     
     * VSDEALERS-323 Fixed producer config
  *  VSDEALERS-323 multiposting events consumer (#681)
     

  *  AUTORUBACK-684 Allow to update offer discount options (#628)
     
     * AUTORUBACK-684 Allow to update offer discount options
     
     * AUTORUBACK-684_update-offer-discount
     
     * query, uptime, workers, todo
     
     * updated schema registry
     
     * AUTORUBACK-684_update-offer-discount: style
     
     * AUTORUBACK-684_update-offer-discount: fixed tests
     
     * AUTORUBACK-684_update-offer-discount: save discount options to old db (not finished), updated responses, updated tests, refactoring
     
     * AUTORUBACK-684_update-offer-discount: todo
     
     * Merge branch 'master' into AUTORUBACK-684_update-offer-discount
     
     # Conflicts:
     #	pom.xml
     #	vos2-autoru-api/src/main/scala/ru/yandex/vos2/autoru/api/v1/offer/OfferHandler.scala
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/OffersWriter.scala
     
     * AUTORUBACK-684_update-offer-discount: fixes after merge
     
     * AUTORUBACK-684_update-offer-discount: style
     
     * AUTORUBACK-684_update-offer-discount: updated schema-registry
     
     * AUTORUBACK-684_update-offer-discount: revert some changes
     
     * AUTORUBACK-684_update-offer-discount: revert some changes
     
     * AUTORUBACK-684_update-offer-discount: compilation fixes and refactoring
     
     * AUTORUBACK-684_update-offer-discount: removed photo utils from statuses manager
     
     * AUTORUBACK-684_price_attribute_return
     
     * AUTORUBACK-684_update-offer-discount_model_update: save discount options to old db
     
     * AUTORUBACK-684_update-offer-discount_model_update: fixed tests, refactoring
     
     * AUTORUBACK-684_update-offer-discount_model_update: fix after merge
     
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-373 # Allow to enable/disable multiposting for user by id (#679)
     
     * VSDEALERS-373 # Allow to enable/disable multiposting for user by id
     
     * VSDEALERS-373 # Update tests
     
     * VSDEALERS-373 # Minor refactor
     
     * VSDEALERS-373 # Minor refactor
     
     * VSDEALERS-373 # Minor fixes
     
     * VSDEALERS-373 # Select all offers when activate multiposting
     
     * VSDEALERS-373 # Explicitly filter statuses
     
     * VSDEALERS-373 # Wrap in withoutErrors
  *  VSDEALERS-289 Fixed services duplication (#680)
     

  *  AUTORUBACK-904 silent push (#678)
     

  *  AUTORUBACK-922: added kafka props for extended holocron

  *  VSDEALERS-277 # Update classified state handlers logic (#677)
     
     * VSDEALERS-277 # Update classified state handlers logic
     
     * VSDEALERS-277 # Update OfferHandlerTest
  *  VSDEALERS-289 services deduplication (#675)
     
     * VSDEALERS-289 classified services model changed
     
     * VSDEALERS-289 services deduplication
     
     * VSDEALERS-289 build the builder
     
     * VSDEALERS-289 fixed doc
     
     * VSDEALERS-289 Don't reactivated disabled services
     
     * VSDEALERS-289 Don't remove old services
     
     * VSDEALERS-289 classified -> multiposting
     
     * VSDEALERS-289 renaming
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  AUTORUBACK-835 change call info renderer message (#674)
     

  *  AUTORUBACK-906 remove nullable fields (#673)
     

  *  AUTORUBACK-906 extend common feature response with tags and info (#672)
     

  *  AUTORUBACK-718 feature spamalot push (#670)
     

  *  Revert "AUTORUBACK-718 feature spamalot push"
     
     This reverts commit 2bbdf9d2

  *  AUTORUBACK-718 feature spamalot push

  *  AUTORUBACK-718 turn off pushnoy in offer incomplete form (#669)
     

  *  minor changes

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-829 offer-form converter fix

  *  AUTORUBACK-718 add logged and metered for spamalot push (#668)
     
     * AUTORUBACK-718 add logged and metered for spamalot push
     
     * AUTORUBACK-718 npe hotfix
     
     * AUTORUBACK-718 test fix try
  *  AUTORUBACK-718 send offerincomplete push to spamalot (#666)
     
     * AUTORUBACK-718 send offerincomplete push to spamalot
     
     * AUTORUBACK-718 remove unused ConcurrencyUtils.scala
     
     * AUTORUBACK-718 add spamalot mock for test
     
     * AUTORUBACK-718 format
     review fix
     
     * AUTORUBACK-718 remove execution context from spamalot client
     fix spamalot config name
     
     * AUTORUBACK-718 try tests without lazy spamalotClient
     
     * AUTORUBACK-718 topic
  *  compilation fix

  *  update blur logging

  *  update blur parsing and logging

  *  Autoruback 870 spinkar ekt only (#665)
     
     * AUTORUBACK-870_spinkar_ekt_only
     
     * AUTORUBACK-870_spinkar_ekt_only: updated converter for searcher
  *  autoruback-632 (#664)
     
     * autoruback-632
     
     * autoruback-632
     
     * autoruback-632
     
     * autoruback-632
  *  Autoruback 632 (#660)
     
     * autoruback-632 -feature name fix
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
     
     * autoruback-632 -fix for lost scoring naming
  *  VSDEALERS-297 # Set multiposting status (#658)
     

  *  AUTORUBACK-870_spinkar_ekt_only (#659)
     

  *  AUTORUBACK-753 refactoring (#654)
     
     * AUTORUBACK-753 refactoring
     
     * AUTORUBACK-753 format
  *  VSDEALERS-278 (#655)
     
     * added handler endpoints, service method, dao method
     
     * tests, doc, logic
     
     * it works
     
     * removed unused exception
     
     * review improvements
     
     * adde st to log
     
     * renamed trace
  *  VSDEALERS-256 hidden -> dealer_hidden for multiposting (#657)
     

  *  VSDEALERS-302 multiposting converters (#656)
     
     * VSDEALERS-302 multiposting converters
     
     * VSDEALERS-302 removed duplicated code
     
     * VSDEALERS-302 classified convertion
     
     * VSDEALERS-302 fixed test without multiposting
     
     * VSDEALERS-302 removed default multiposting status
     
     * VSDEALERS-302 redundant import removed
     
     * VSDEALERS-302 multiposting converter refactored
  *  VSDEALERS-256 Multiposting fields to shard propagation (#649)
     
     * VSDEALERS-256 Multiposting fields to shard propagation (for cars only yet)
     
     * VSDEALERS-256 Fixed offer generation in tests
     
     * VSDEALERS-256 multiposting propagation for trucks and moto
     
     * VSDEALERS-256 isActive utility usage + dealer offer check
     
     * VSDEALERS-256 tests fixed
     
     * VSDEALERS-256 hidden for user offers, dead code removed
     
     * VSDEALERS-256 banned offers disabled on dealer showcase
     
     * VSDEALERS-256 utility usage for ban check
  *  VSDEALERS-252 # Convert multiposting model VOS -> ApiOfferModel (#653)
     
     * VSDEALERS-252 # Convert multiposting model VOS -> ApiOfferModel
     
     * VSDEALERS-252 # fmt
  *  AUTORUBACK-753 upload document photos to offer (#646)
     
     * AUTORUBACK-753 add offer doc photo
     
     * AUTORUBACK-753 uncomment line
     
     * AUTORUBACK-753 remove DomainExceptionRenderer from PhotoDirectives
     
     * AUTORUBACK-753 imports optimized
     
     * AUTORUBACK-753 fix routing issues
     
     * AUTORUBACK-753 remove capturing group
     
     * code review todo
     
     * AUTORUBACK-753 revert draft id path segment behaviour
     
     * AUTORUBACK-753 fix issues
     
     * AUTORUBACK-753 rename toPhotoResponse
     
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
  *  VSDEALERS-254 # Filter offers by multiposting_status and multiposting_service (#651)
     
     * VSDEALERS-254 # Filter offers by multiposting_status and multiposting_service
     
     * VSDEALERS-254 # FIX application.conf
     
     * VSDEALERS-254 # FIX dev configurations
     
     * VSDEALERS-254 # FIX remove service without expire_date
     
     * VSDEALERS-254 # FIX remove service without expire_date
     
     * VSDEALERS-254 # FIX swagger documentation
     
     * VSDEALERS-254 # CodeReview FIX
  *  autoruback-632 -feature name fix (#652)
     

  *  VSDEALERS-265 # Стейдж мультипостинга в VOS (#650)
     
     * VSDEALERS-265 # Стейдж мультипостинга в VOS
     
     * VSDEALERS-265 # Rename stage; minor fixes
     
     * VSDEALERS-265 # Refactor MultipostingStage#process
     
     * VSDEALERS-265 # Refactor MultipostingStage#process
  *  AUTORUBACK-829_vin_recognition_flag (#648)
     
     * AUTORUBACK-829_vin_recognition_flag
     
     * AUTORUBACK-829_vin_recognition_flag: updated schema-registry
  *  comments

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-857: updated logging and tracing error annotation

  *  VSDEALERS-308 # Multiposting classified is_enabled flag (#647)
     

  *  Revert "VSDEALERS-280 # Активация мультипостинговых объявлений по условию (#644)" (#645)
     
     This reverts commit 957e3d4f54bdc610ca4580b3b9fee66c047c635c.
  *  AUTORUBACK-632-scoring (#641)
     
     * AUTORUBACK-632-scoring
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     
     # Conflicts:
     #	vos2-core/src/main/proto/offer_model.proto
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/components/AutoruCoreComponents.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     * Merge branch 'master' into AUTORUBACK-632-scoring
     # Please enter a commit message to explain why this merge is necessary,
     # especially if it merges an updated upstream into a topic branch.
     #
     # Lines starting with '#' will be ignored, and an empty message aborts
     # the commit.
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  VSDEALERS-280 # Активация мультипостинговых объявлений по условию (#644)
     
     * VSDEALERS-280 # Активация мультипостинговых объявлений по условию
     
     * VSDEALERS-280 # Refactor CommercialActivationStage#shouldProcess
     
     * VSDEALERS-280 # Check multiposting status
     
     * VSDEALERS-280 # Move hasActiveAutoruClassified to utils
     
     * VSDEALERS-280 # Refactor CommercialActivationStage#shouldProcess
  *  added drom classified (#643)
     

  *  AUTORUBACK-172_request_id_in_logs: fixed request context copy

  *  VSDEALERS-253 # Add index fields for multiposting (#639)
     
     * VSDEALERS-253 # Add index fields for multiposting
     
     * VSDEALERS-253 # Update DDL for index fields
     
     * VSDEALERS-253 # Add multiposting fields to AutoruOfferDao
  *  AUTORUBACK-172_request_id_in_logs, not finished (#636)
     
     * AUTORUBACK-172_request_id_in_logs, not finished
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, not finished
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, not finished: updated offer handler
     
     * AUTORUBACK-172_request_id_in_logs: exceptions refactoring
     
     * AUTORUBACK-172_request_id_in_logs: updated more managers and handlers
     
     * AUTORUBACK-172_request_id_in_logs: removed managers default error handling
     
     * AUTORUBACK-172_request_id_in_logs: able to compile and run
     
     * AUTORUBACK-172_request_id_in_logs: style and marshaller fixes
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: refactoring, fixed tests
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: improved tests
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed test
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: fixed compilation
     
     * AUTORUBACK-172_request_id_in_logs: short access logging
     
     * AUTORUBACK-172_request_id_in_logs: fixed test, todo
  *  VSDEALERS-252 added multiposting field (#638)
     
     * added multiposting field
     
     * removed field options
     
     * fixed id
  *  AUTORUBACK-745-ban (#637)
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/services/chat/HttpChatClient.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     * AUTORUBACK-745-ban
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-679_photo_class (#635)
     
     * AUTORUBACK-679_photo_class
     
     * AUTORUBACK-679_photo_class: more changes
     
     * AUTORUBACK-679_photo_class: refactoring
     
     * AUTORUBACK-679_photo_class: AUTO_VIEW_3_4_BACK support
  *  AUTORUBACK-795 tracing fix (#633)
     
     * AUTORUBACK-795_tracing_fix
     
     * AUTORUBACK-795_tracing_fix: fixed more
     
     * AUTORUBACK-795_tracing_fix: refactoring
     
     * AUTORUBACK-795_tracing_fix: fixed test
     
     * AUTORUBACK-795_tracing_fix: style
  *  AUTORUBACK-603: Add stats endpoint (#625)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 20 Nov 2020 22:31:25 +0300

## yandex-vos2-autoru-ydb-workers:0.11.0 (Fri, 04 Sep 2020 12:54:26 +0300)

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-126_ydb_blobs: updated maxUpdated

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 04 Sep 2020 12:54:26 +0300

## yandex-vos2-autoru-ydb-workers:0.10.0 (Fri, 04 Sep 2020 10:07:58 +0300)

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-126_ydb_blobs: updated logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 04 Sep 2020 10:07:58 +0300

## yandex-vos2-autoru-ydb-workers:0.9.0 (Fri, 04 Sep 2020 01:59:26 +0300)

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-126_ydb_blobs: updated logging

  *  #AUTORUBACK-772 Booking state validation fix (#631)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 04 Sep 2020 01:59:26 +0300

## yandex-vos2-autoru-ydb-workers:0.8.0 (Thu, 03 Sep 2020 23:52:25 +0300)

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-126_ydb_blobs: maxUpdated fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 03 Sep 2020 23:52:25 +0300

## yandex-vos2-autoru-ydb-workers:0.7.0 (Thu, 03 Sep 2020 20:48:27 +0300)

  *  AUTORUBACK-126_ydb_blobs: increased maxUpdated

  *  AUTORUBACK-126_ydb_blobs: timestampAnyUpdate update fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 03 Sep 2020 20:48:27 +0300

## yandex-vos2-autoru-ydb-workers:0.6.0 (Mon, 31 Aug 2020 09:37:59 +0300)

  *  AUTORUBACK-126_ydb_blobs: maxUpdated

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-126_ydb_blobs: style

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 31 Aug 2020 09:37:59 +0300

## yandex-vos2-autoru-ydb-workers:0.5.0 (Sun, 30 Aug 2020 15:42:46 +0300)

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-126_ydb_blobs: updated logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 30 Aug 2020 15:42:46 +0300

## yandex-vos2-autoru-ydb-workers:0.4.0 (Sun, 30 Aug 2020 00:38:20 +0300)

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  zookeeper client fix: creatingParentsIfNeeded

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 30 Aug 2020 00:38:20 +0300

## yandex-vos2-autoru-ydb-workers:0.3.0 (Sat, 29 Aug 2020 19:40:52 +0300)

  *  AUTORUBACK-126_ydb_blobs: read from master

  *  ZookeeperNodeImpl ensureExists

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-126_ydb_blobs: update timestamp_any_update in offer for timestamp_check changes too

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 29 Aug 2020 19:40:52 +0300

## yandex-vos2-autoru-ydb-workers:0.2.0 (Wed, 26 Aug 2020 17:31:42 +0300)

  *  AUTORUBACK-126_ydb_blobs: fixed should process next check

  *  AUTORUBACK-749: Don't blur photos without license number (#627)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 26 Aug 2020 17:31:42 +0300

## yandex-vos2-autoru-ydb-workers:0.1.0 (Wed, 26 Aug 2020 00:50:39 +0300)

  *  AUTORUBACK-126_ydb_blobs: skypper 9, increased upsert timeout

  *  style

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-747: fixed username save to old db

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 26 Aug 2020 00:50:39 +0300

## yandex-vos2-autoru-ydb-workers:0.0.8 (Tue, 25 Aug 2020 13:49:43 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 25 Aug 2020 13:49:43 +0300

## yandex-vos2-autoru-ydb-workers:0.0.7 (Tue, 25 Aug 2020 10:29:17 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 25 Aug 2020 10:29:17 +0300

## yandex-vos2-autoru-ydb-workers:0.0.6 (Mon, 24 Aug 2020 20:40:08 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 24 Aug 2020 20:40:08 +0300

## yandex-vos2-autoru-ydb-workers:0.0.5 (Sun, 23 Aug 2020 22:43:50 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 23 Aug 2020 22:43:50 +0300

## yandex-vos2-autoru-ydb-workers:0.0.4 (Sun, 23 Aug 2020 14:11:06 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 23 Aug 2020 14:11:06 +0300

## yandex-vos2-autoru-ydb-workers:0.0.3 (Sun, 23 Aug 2020 13:41:39 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 23 Aug 2020 13:41:39 +0300

## yandex-vos2-autoru-ydb-workers:0.0.2 (Sun, 23 Aug 2020 01:12:15 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 23 Aug 2020 01:12:15 +0300

## yandex-vos2-autoru-ydb-workers:0.0.1 (16 Aug 2020 10:19:00 +0300)

  * initial release
