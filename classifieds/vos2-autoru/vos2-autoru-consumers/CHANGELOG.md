## vos2-autoru-consumers:0.192.24 (Thu, 14 Apr 2022 09:39:29 +0300)

  *  AUTORUBACK-3052 (#1347)
     

  *  AUTORUBACK-3173 (#1351)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata (#1350)
     
     * AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata
     
     * AUTORUBACK-3141 Clean up duplicated logic
  *  AUTORUBACK-3089_new_zookeeper_hosts (#1349)
     

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 14 Apr 2022 09:39:29 +0300

## vos2-autoru-consumers:0.192.23 (Wed, 13 Apr 2022 15:47:48 +0300)

  *  AUTORUBACK-3052 (#1347)
     

  *  AUTORUBACK-3173 (#1351)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata (#1350)
     
     * AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata
     
     * AUTORUBACK-3141 Clean up duplicated logic
  *  AUTORUBACK-3089_new_zookeeper_hosts (#1349)
     

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 13 Apr 2022 15:47:48 +0300

## vos2-autoru-consumers:0.192.22 (Mon, 11 Apr 2022 18:34:37 +0300)

  *  AUTORUBACK-3173 (#1351)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata (#1350)
     
     * AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata
     
     * AUTORUBACK-3141 Clean up duplicated logic
  *  AUTORUBACK-3089_new_zookeeper_hosts (#1349)
     

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 11 Apr 2022 18:34:37 +0300

## vos2-autoru-consumers:0.192.21 (Mon, 11 Apr 2022 15:23:27 +0300)

  *  AUTORUBACK-3173 (#1351)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
  *  AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata (#1350)
     
     * AUTORUBACK-3141 Support multiple verdicts in ProvenOwnerMetadata
     
     * AUTORUBACK-3141 Clean up duplicated logic
  *  AUTORUBACK-3089_new_zookeeper_hosts (#1349)
     

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 11 Apr 2022 15:23:27 +0300

## vos2-autoru-consumers:0.192.20 (Fri, 08 Apr 2022 13:08:14 +0300)

  *  AUTORUBACK-3173 (#1348)
     
     * AUTORUBACK-3173

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 08 Apr 2022 13:08:14 +0300

## vos2-autoru-consumers:0.192.19 (Fri, 08 Apr 2022 09:04:25 +0300)

  *  AUTORUBACK-3173 (#1346)
     
     * AUTORUBACK-3173
     
     * AUTORUBACK-3173
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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 08 Apr 2022 09:04:25 +0300

## vos2-autoru-consumers:0.192.18 (Wed, 06 Apr 2022 09:38:40 +0300)

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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 06 Apr 2022 09:38:40 +0300

## vos2-autoru-consumers:0.192.17 (Tue, 05 Apr 2022 20:31:20 +0300)

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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 05 Apr 2022 20:31:20 +0300

## vos2-autoru-consumers:0.192.16 (Fri, 01 Apr 2022 11:46:52 +0300)

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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 01 Apr 2022 11:46:52 +0300

## vos2-autoru-consumers:0.192.15 (Fri, 01 Apr 2022 11:07:44 +0300)

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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 01 Apr 2022 11:07:44 +0300

## vos2-autoru-consumers:0.192.14 (Thu, 31 Mar 2022 10:34:32 +0300)

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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 31 Mar 2022 10:34:32 +0300

## vos2-autoru-consumers:0.192.13 (Thu, 31 Mar 2022 10:09:04 +0300)

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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 31 Mar 2022 10:09:04 +0300

## vos2-autoru-consumers:0.192.12 (Mon, 28 Mar 2022 09:49:51 +0300)

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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 28 Mar 2022 09:49:51 +0300

## vos2-autoru-consumers:0.192.11 (Wed, 23 Mar 2022 16:02:06 +0300)

  *  AUTORUBACK-3052 (#1331)
     

  *  AUTORUBACK-3052 (#1330)
     

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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 23 Mar 2022 16:02:06 +0300

## vos2-autoru-consumers:0.192.10 (Tue, 22 Mar 2022 17:17:24 +0300)

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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 22 Mar 2022 17:17:24 +0300

## vos2-autoru-consumers:0.192.9 (Mon, 21 Mar 2022 13:57:13 +0300)

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

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 21 Mar 2022 13:57:13 +0300

## vos2-autoru-consumers:0.192.8 (Thu, 17 Mar 2022 16:49:04 +0300)

  *  fix

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Mar 2022 16:49:04 +0300

## vos2-autoru-consumers:0.192.7 (Thu, 17 Mar 2022 16:12:25 +0300)

  *  Autoruback-3052 migration tables fix (#1322)
     
     * AUTORUBACK-3052
     * AUTORUBACK-3052
  *  AUTORUBACK-3052 (#1320)
     
     * AUTORUBACK-3052
  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Mar 2022 16:12:25 +0300

## vos2-autoru-consumers:0.192.6 (Thu, 17 Mar 2022 11:32:51 +0300)

  *  AUTORUBACK-3092 (#1319)
     

  *  AUTORUBACK-3052 (#1308)
     
     * AUTORUBACK-3052

  *  AUTORUBACK-3091 Send inactive offers to moderation (#1317)
     

  *  AUTORUBACK-3081 Fix flaky tests (#1315)
     
     * AUTORUBACK-3081 Fix flaky test in OffersReaderTest
     
     * AUTORUBACK-3081 Fix flaky test in FormValidatorTest
     
     * AUTORUBACK-3081 Clean up a test to avoid asInstanceOf
  *  AUTORUBACK-3087 Add ability to force send offer to indexer (#1316)
     
     * AUTORUBACK-3087 Add ability to force send offer to indexer
     
     * AUTORUBACK-3087 Migrate hashIdx
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
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Mar 2022 11:32:51 +0300

## vos2-autoru-consumers:0.192.5 (Mon, 14 Mar 2022 12:20:22 +0300)

  *  AUTORUBACK-3083 expiration fix (#1313)
     
     * AUTORUBACK-3083

  *  AUTORUBACK-3082 (#1311)
     
     * AUTORUBACK-3082

  *  AUTORUBACK-3001 (#1312)
     

  *  AUTORUBACK-3020 Send last_editor to Holocron (#1307)
     

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 14 Mar 2022 12:20:22 +0300

## vos2-autoru-consumers:0.192.4 (Fri, 11 Mar 2022 08:50:02 +0300)

  *  AUTORUBACK-2854 Add garage_id fields for holocron (#1310)
     

  *  AUTORUBACK-3065 (#1306)
     

  *  AUTORUBACK-2854 Add garage_id to inner model (#1302)
     

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 11 Mar 2022 08:50:02 +0300

## vos2-autoru-consumers:0.192.3 (Fri, 04 Mar 2022 17:09:35 +0300)

  *  AUTORUBACK-3047 (#1295)
     
     * AUTORUBACK-3047

  *  AUTORUBACK-3060 (#1303)
     
     * AUTORUBACK-3060
     
     * AUTORUBACK-3060
  *  AUTORUBACK-3001

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
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 04 Mar 2022 17:09:35 +0300

## vos2-autoru-consumers:0.192.2 (Wed, 02 Mar 2022 11:21:32 +0300)

  *  AUTORUBACK-3047 (#1297)
     

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 02 Mar 2022 11:21:32 +0300

## vos2-autoru-consumers:0.192.1 (Tue, 01 Mar 2022 17:47:29 +0300)

  *  AUTORUBACK-2978

  *  AUTORUBACK-2978 shiva (#1292)
     
     * AUTORUBACK-2978
  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 01 Mar 2022 17:47:29 +0300

## vos2-autoru-consumers:0.192.0 (Mon, 28 Feb 2022 16:52:06 +0300)

## yandex-vos2-autoru-consumers:0.191.2 (Mon, 28 Feb 2022 16:52:06 +0300)

  *  AUTORUBACK-3040 (#1294)
     
     * AUTORUBACK-3040
     
     * AUTORUBACK-3040
  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 28 Feb 2022 16:52:06 +0300

## yandex-vos2-autoru-consumers:0.191.1 (Mon, 21 Feb 2022 18:28:05 +0300)

  *  AUTORUBACK-2994 (#1290)
     
     * AUTORUBACK-2994

  *  AUTORUBACK-3027 (#1293)
     
     AUTORUBACK-3027 

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 21 Feb 2022 18:28:05 +0300

## yandex-vos2-autoru-consumers:0.191.0 (Fri, 18 Feb 2022 19:25:44 +0300)

  *  Autoruback-2994 fix (#1289)
     
     * AUTORUBACK-2994
     
     * AUTORUBACK-2994
  *  AUTORUBACK-3001-3 (#1287)
     
     * AUTORUBACK-3001
     
     * AUTORUBACK-3001
  *  AUTORUBACK-2965

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 18 Feb 2022 19:25:44 +0300

## yandex-vos2-autoru-consumers:0.190.0 (Fri, 18 Feb 2022 11:10:07 +0300)

  *  AUTORUBACK-3015 (#1285)
     

  *  AUTORUBACK-3012 send orig sizes to searcher (#1284)
     
     * AUTORUBACK-3012 send orig sizes to searcher
     
     * AUTORUBACK-3012 send original sizes to searcher
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-3001 (#1282)
     
     * AUTORUBACK-3001

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 18 Feb 2022 11:10:07 +0300

## yandex-vos2-autoru-consumers:0.189.0 (Thu, 17 Feb 2022 13:23:25 +0300)

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

  *  AUTORUBACK-2962 (#1280)
     

  *  AUTORUBACK-2936 use PriceHistory (#1275)
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Feb 2022 13:23:25 +0300

## yandex-vos2-autoru-consumers:0.188.1 (Fri, 11 Feb 2022 10:54:10 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 11 Feb 2022 10:54:10 +0300

## yandex-vos2-autoru-consumers:0.188.0 (Thu, 10 Feb 2022 14:54:55 +0300)

  *  AUTORUBACK-2940 Уведомление о провале повторной валидации оффера (#1271)
     
     * AUTORUBACK-2940 Parse banned revalidation settings from Bunker
     
     * AUTORUBACK-2940 Add BannedRevalidationRenderer
     
     * AUTORUBACK-2940 Convert COMPLETE_CHECK_FAILED opinions into notifications
     
     * AUTORUBACK-2940 Change message template to match templates in other renderers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 10 Feb 2022 14:54:55 +0300

## yandex-vos2-autoru-consumers:0.187.3 (Thu, 10 Feb 2022 13:30:49 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 10 Feb 2022 13:30:49 +0300

## yandex-vos2-autoru-consumers:0.187.2 (Wed, 09 Feb 2022 17:05:55 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 09 Feb 2022 17:05:55 +0300

## yandex-vos2-autoru-consumers:0.187.1 (Wed, 09 Feb 2022 08:31:57 +0300)

  *  AUTORUBACK-2973

  *  Autoruback-2973 2 (#1269)
     
     * AUTORUBACK-2973
     
     * AUTORUBACK-2973

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 09 Feb 2022 08:31:57 +0300

## yandex-vos2-autoru-consumers:0.187.0 (Wed, 09 Feb 2022 08:22:02 +0300)

  *  Autoruback-2973 2 (#1269)
     
     * AUTORUBACK-2973
     
     * AUTORUBACK-2973

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 09 Feb 2022 08:22:02 +0300

## yandex-vos2-autoru-consumers:0.186.0 (Wed, 09 Feb 2022 00:31:12 +0300)

  *  AUTORUBACK-2973 (#1268)
     
     * AUTORUBACK-2973

  *  AUTORUBACK-2923 Secure video field (#1263)
     
     * AUTORUBACK-2923 Secure video field
     
     * AUTORUBACK-2923 Fix tests
     
     * AUTORUBACK-2923 Add test
     
     * AUTORUBACK-2923 Add test
  *  AUTORUBACK-2864 (#1267)
     

  *  AUTORUBACK-2876: Set offer inactivated timestamp (#1264)
     

  *  AUTORUBACK-2957 (#1262)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 09 Feb 2022 00:31:12 +0300

## yandex-vos2-autoru-consumers:0.185.1 (Fri, 04 Feb 2022 12:58:05 +0300)

  *  AUTORUBACK-2945 Send trusted_dealer_calls_accepted to searcher (#1261)
     

  *  VSDEALERS-1800 dealer pony full config integration (#1259)
     
     * VSDEALERS-1800 dealer pony full config integration
     
     * VSDEALERS-1800 fix dealer redir availability check
     
     * VSDEALERS-1800 minor refactoring
  *  AUTORUBACK-2700 (#1254)
     

  *  AUTORUBACK-2928 (#1260)
     

  *  AUTORUBACK-2926 (#1258)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 04 Feb 2022 12:58:05 +0300

## yandex-vos2-autoru-consumers:0.185.0 (Tue, 01 Feb 2022 14:41:43 +0300)

  *  AUTORUBACK-2928 (#1260)
     

  *  AUTORUBACK-2926 (#1258)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 01 Feb 2022 14:41:43 +0300

## yandex-vos2-autoru-consumers:0.184.0 (Mon, 31 Jan 2022 13:32:20 +0300)

  *  #AUTORUBACK-1805 Removing of credits service (#1247)
     

  *  #AUTORUBACK-2918 autoru-carfax namespace support for MdsPhotoUtils (#1255)
     

  *  VS-1277_fix_phone_counter (#1251)
     
     * VS-1277_fix_phone_counter
     
     * VS-1277_add_test
  *  AUTORUBACK-2895 (#1243)
     
     AUTORUBACK-2895

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 31 Jan 2022 13:32:20 +0300

## yandex-vos2-autoru-consumers:0.183.0 (Wed, 26 Jan 2022 10:12:16 +0300)

  *  AUTORUBACK-2897 (#1244)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 26 Jan 2022 10:12:16 +0300

## yandex-vos2-autoru-consumers:0.182.1 (Mon, 24 Jan 2022 13:09:33 +0300)

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
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 24 Jan 2022 13:09:33 +0300

## yandex-vos2-autoru-consumers:0.182.0 (Sat, 22 Jan 2022 10:39:20 +0300)

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
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 22 Jan 2022 10:39:20 +0300

## yandex-vos2-autoru-consumers:0.181.1 (Thu, 20 Jan 2022 10:24:33 +0300)

  *  AUTORUBACK-2843_user_migration_fixes: todo (#1234)
     
     * AUTORUBACK-2843

  *  AUTORUBACK-2860-remove-old-consumers (#1235)
     
     * AUTORUBACK-2860
     
     * AUTORUBACK-2860
     
     * AUTORUBACK-2860

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 20 Jan 2022 10:24:33 +0300

## yandex-vos2-autoru-consumers:0.181.0 (Fri, 14 Jan 2022 12:43:11 +0300)

  *  AUTORUBACK-2714 Store allow_show_offers (#1226)
     
     * AUTORUBACK-2714 Add User.allow_offers_show
     
     * AUTORUBACK-2714 Set Offer.allow_user_offers_show
     
     * AUTORUBACK-2714 Clean up following PR discussion
     
     * AUTORUBACK-2714 Update schema-registry

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 14 Jan 2022 12:43:11 +0300

## yandex-vos2-autoru-consumers:0.180.0 (Wed, 12 Jan 2022 17:51:06 +0300)

  *  VSDEALERSDECOMP-500 # Dont clear market_price_on_deactivation field on migration (#1227)
     

  *  AUTORUBACK-2718-photo-quality (#1219)
     
     * AUTORUBACK-2718

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 12 Jan 2022 17:51:06 +0300

## yandex-vos2-autoru-consumers:0.179.1 (Wed, 29 Dec 2021 17:27:05 +0300)

  *  AUTORUBACK-2776 consumer logging (#1223)
     
     * AUTORUBACK-2776

  *  AUTORUBACK-1549 (#1222)
     
     * AUTORUBACK-1549
     
     * AUTORUBACK-1549
  *  AUTORUBACK-1549: php migration fix

  *  AUTORUBACK-2734-wrong-time-fix (#1221)
     
     * AUTORUBACK-2734
     
     * AUTORUBACK-2734
     
     * AUTORUBACK-2734
  *  AUTORUBACK-2776 feedprocessor fix (#1215)
     
     * AUTORUBACK-2776 feedprocessor fix

  *  AUTORUBACK-1549 (#1220)
     

  *  AUTORUBACK-2734 wrong call time (#1218)
     
     * AUTORUBACK-2734

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 29 Dec 2021 17:27:05 +0300

## yandex-vos2-autoru-consumers:0.179.0 (Tue, 28 Dec 2021 15:46:41 +0300)

  *  AUTORUBACK-2776 feedprocessor fix (#1215)
     
     * AUTORUBACK-2776 feedprocessor fix

  *  AUTORUBACK-1549 (#1220)
     

  *  AUTORUBACK-2734 wrong call time (#1218)
     
     * AUTORUBACK-2734

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 28 Dec 2021 15:46:41 +0300

## yandex-vos2-autoru-consumers:0.178.1 (Mon, 27 Dec 2021 10:24:11 +0300)

  *  AUTORUBACK-1549 (#1214)
     
     * AUTORUBACK-1549
  *  AUTORUBACK-1549 (#1193)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 27 Dec 2021 10:24:11 +0300

## yandex-vos2-autoru-consumers:0.178.0 (Fri, 24 Dec 2021 18:32:38 +0300)

  *  AUTORUBACK-1549 (#1214)
     
     * AUTORUBACK-1549
  *  AUTORUBACK-1549 (#1193)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 24 Dec 2021 18:32:38 +0300

## yandex-vos2-autoru-consumers:0.177.0 (Mon, 20 Dec 2021 15:21:52 +0300)

  *  AUTORUBACK-1549 (#1207)
     
     * AUTORUBACK-1549
     AUTORUBACK-2674

  *  Autoruback-1679 moderation ban 2 (#1213)
     
     * AUTORUBACK-1679

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 20 Dec 2021 15:21:52 +0300

## yandex-vos2-autoru-consumers:0.176.2 (Mon, 20 Dec 2021 14:19:07 +0300)

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
     

  *  Autoruback-2711 (#1200)
     
     * AUTORUBACK-2711

  *  VSDEALERS-1688 # YdbWorker for saving car market price on offer deactivation (#1188)
     
     * VSDEALERS-1688 # YdbWorker for saving car market price on offer deactivation
     
     * VSDEALERS-1688 # Save offer market price on deactivation in separate offer field
     
     * VSDEALERS-1688 # Retry delay refactoring
     
     * VSDEALERS-1688 # Already processed guard for worker
     
     * VSDEALERS-1688 # Unit tests
     
     * VSDEALERS-1688 # Unit tests
     
     * VSDEALERS-1688 # Throw error on predict price errors instead of custom retry
     
     * VSDEALERS-1688 # Log user

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 20 Dec 2021 14:19:07 +0300

## yandex-vos2-autoru-consumers:0.176.1 (Mon, 20 Dec 2021 13:22:37 +0300)

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
     

  *  Autoruback-2711 (#1200)
     
     * AUTORUBACK-2711

  *  VSDEALERS-1688 # YdbWorker for saving car market price on offer deactivation (#1188)
     
     * VSDEALERS-1688 # YdbWorker for saving car market price on offer deactivation
     
     * VSDEALERS-1688 # Save offer market price on deactivation in separate offer field
     
     * VSDEALERS-1688 # Retry delay refactoring
     
     * VSDEALERS-1688 # Already processed guard for worker
     
     * VSDEALERS-1688 # Unit tests
     
     * VSDEALERS-1688 # Unit tests
     
     * VSDEALERS-1688 # Throw error on predict price errors instead of custom retry
     
     * VSDEALERS-1688 # Log user

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 20 Dec 2021 13:22:37 +0300

## yandex-vos2-autoru-consumers:0.176.0 (Fri, 17 Dec 2021 14:16:32 +0300)

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
     

  *  Autoruback-2711 (#1200)
     
     * AUTORUBACK-2711

  *  VSDEALERS-1688 # YdbWorker for saving car market price on offer deactivation (#1188)
     
     * VSDEALERS-1688 # YdbWorker for saving car market price on offer deactivation
     
     * VSDEALERS-1688 # Save offer market price on deactivation in separate offer field
     
     * VSDEALERS-1688 # Retry delay refactoring
     
     * VSDEALERS-1688 # Already processed guard for worker
     
     * VSDEALERS-1688 # Unit tests
     
     * VSDEALERS-1688 # Unit tests
     
     * VSDEALERS-1688 # Throw error on predict price errors instead of custom retry
     
     * VSDEALERS-1688 # Log user

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 17 Dec 2021 14:16:32 +0300

## yandex-vos2-autoru-consumers:0.175.2 (Wed, 08 Dec 2021 16:34:16 +0300)

  *  VSDEALERS-1720 # Fix lazy collection (#1197)
     

  *  CARFAX-2203  - [Гараж] Добавить флаг "подходящий офер" в VOS offer (#1195)
     
     * CARFAX-2203  - [Гараж] Добавить флаг "подходящий офер" в VOS offer
     
     * fix
  *  AUTORUBACK-2304: Add draft list endpoint (#1183)
     

  *  AUTORUBACK-2658 (#1191)
     
     * AUTORUBACK-2658
     
     * AUTORUBACK-2658
  *  Autoruback-2636 updates throttling 2 (#1189)
     
     * AUTORUBACK-2636
  *  Autoruback-2506 prod to test migrations (#1159)
     
     * AUTORUBACK-2506

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 08 Dec 2021 16:34:16 +0300

## yandex-vos2-autoru-consumers:0.175.1 (Tue, 07 Dec 2021 16:22:34 +0300)

  *  CARFAX-2203  - [Гараж] Добавить флаг "подходящий офер" в VOS offer (#1195)
     
     * CARFAX-2203  - [Гараж] Добавить флаг "подходящий офер" в VOS offer
     
     * fix
  *  AUTORUBACK-2304: Add draft list endpoint (#1183)
     

  *  AUTORUBACK-2658 (#1191)
     
     * AUTORUBACK-2658
     
     * AUTORUBACK-2658
  *  Autoruback-2636 updates throttling 2 (#1189)
     
     * AUTORUBACK-2636
  *  Autoruback-2506 prod to test migrations (#1159)
     
     * AUTORUBACK-2506

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 07 Dec 2021 16:22:34 +0300

## yandex-vos2-autoru-consumers:0.175.0 (Fri, 03 Dec 2021 18:02:53 +0300)

  *  AUTORUBACK-2658 (#1191)
     
     * AUTORUBACK-2658
     
     * AUTORUBACK-2658
  *  Autoruback-2636 updates throttling 2 (#1189)
     
     * AUTORUBACK-2636
  *  Autoruback-2506 prod to test migrations (#1159)
     
     * AUTORUBACK-2506

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 03 Dec 2021 18:02:53 +0300

## yandex-vos2-autoru-consumers:0.174.0 (Thu, 02 Dec 2021 14:23:40 +0300)

  *  AUTORUBACK-2658 (#1190)
     

  *  AUTORUBACK-2637 (#1187)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 02 Dec 2021 14:23:40 +0300

## yandex-vos2-autoru-consumers:0.173.0 (Wed, 01 Dec 2021 13:23:29 +0300)

  *  AUTORUBACK-2457_callcenter_reseller_as_protected (#1186)
     

  *  CARFAX-2033: Can view no docs offer (#1185)
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 01 Dec 2021 13:23:29 +0300

## yandex-vos2-autoru-consumers:0.172.0 (Mon, 29 Nov 2021 15:43:17 +0300)

  *  AUTORUBACK-1549 (#1184)
     
     * AUTORUBACK-1549

  *  AUTORUBACK-2305 (#1182)
     
     * AUTORUBACK-2305

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 29 Nov 2021 15:43:17 +0300

## yandex-vos2-autoru-consumers:0.171.0 (Thu, 25 Nov 2021 11:59:12 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 25 Nov 2021 11:59:12 +0300

## yandex-vos2-autoru-consumers:0.170.0 (Wed, 24 Nov 2021 14:27:04 +0300)

  *  Autoruback-1549 refactoring fix 2 (#1178)
     
     * AUTORUBACK-1549

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 24 Nov 2021 14:27:04 +0300

## yandex-vos2-autoru-consumers:0.169.1 (Tue, 23 Nov 2021 14:31:06 +0300)

  *  AUTORUBACK-1549 (#1176)
     

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
  *  AUTORUBACK-2480_panorama_messages_off_moto_komtrans AUTORUBACK-2537_send_ext_panorama_promo_offer_to_chat (#1170)
     
     * AUTORUBACK-2480_panorama_messages_off_moto_komtrans
     
     * AUTORUBACK-2480_panorama_messages_off_moto_komtrans: format
     
     * AUTORUBACK-2537_send_ext_panorama_promo_offer_to_chat

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 23 Nov 2021 14:31:06 +0300

## yandex-vos2-autoru-consumers:0.169.0 (Tue, 23 Nov 2021 09:30:10 +0300)

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
  *  AUTORUBACK-2480_panorama_messages_off_moto_komtrans AUTORUBACK-2537_send_ext_panorama_promo_offer_to_chat (#1170)
     
     * AUTORUBACK-2480_panorama_messages_off_moto_komtrans
     
     * AUTORUBACK-2480_panorama_messages_off_moto_komtrans: format
     
     * AUTORUBACK-2537_send_ext_panorama_promo_offer_to_chat

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 23 Nov 2021 09:30:10 +0300

## yandex-vos2-autoru-consumers:0.168.3 (Wed, 17 Nov 2021 17:13:51 +0300)

  *  AUTORUBACK-2563 (#1169)
     
     * AUTORUBACK-2563
  *  AUTORUBACK-1549 (#1168)
     
     * AUTORUBACK-1549
     

  *  AUTORUBACK-2512 is safe deal disabled (#1165)
     
     * AUTORUBACK-2512 is safe deal disabled
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  VS-1145: Add TVM to vs-receiver grpc service client (#1164)
     
     * VS-1145: Add TVM to vs-receiver grpc service client

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
  *  AUTORUBACK-2492 multiposting refactoring (#1153)
     
     * AUTORUBACK-2492 multiposting refactoring

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 17 Nov 2021 17:13:51 +0300

## yandex-vos2-autoru-consumers:0.168.2 (Fri, 12 Nov 2021 13:08:23 +0300)

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
  *  AUTORUBACK-2492 multiposting refactoring (#1153)
     
     * AUTORUBACK-2492 multiposting refactoring

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 12 Nov 2021 13:08:23 +0300

## yandex-vos2-autoru-consumers:0.168.1 (Fri, 12 Nov 2021 10:57:12 +0300)

  *  Autoruback 2493 check belong (#1154)
     
     * AUTORUBACK-2493
  *  VSDEALERS-1535 - set NeedActivation for Avito and Active for Drom for enabled classifieds when multiposting turned on (#1158)
     
     * VSDEALERS-1535 - set NeedActivation for Avito and Active for Drom for enabled classifieds when multiposting turned on
     
     * VSDEALERS-1535
     
     * VSDEALERS-1535 - add tests
     
     * VSDEALERS-1535
  *  AUTORUBACK-2492 multiposting refactoring (#1153)
     
     * AUTORUBACK-2492 multiposting refactoring

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 12 Nov 2021 10:57:12 +0300

## yandex-vos2-autoru-consumers:0.168.0 (Tue, 09 Nov 2021 15:45:53 +0300)

  *  AUTORUBACK-2492 multiposting refactoring (#1153)
     
     * AUTORUBACK-2492 multiposting refactoring

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 09 Nov 2021 15:45:53 +0300

## yandex-vos2-autoru-consumers:0.167.0 (Mon, 08 Nov 2021 21:55:39 +0300)

  *  topic config fix

  *  Merge remote-tracking branch 'origin/master'

  *  updated logging: log draft id

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 08 Nov 2021 21:55:39 +0300

## yandex-vos2-autoru-consumers:0.166.0 (Mon, 08 Nov 2021 12:47:08 +0300)

  *  topics config fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 08 Nov 2021 12:47:08 +0300

## yandex-vos2-autoru-consumers:0.165.1 (Mon, 08 Nov 2021 10:54:37 +0300)

  *  AUTORUBACK-2401 (#1151)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 08 Nov 2021 10:54:37 +0300

## yandex-vos2-autoru-consumers:0.165.0 (Thu, 04 Nov 2021 14:00:51 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 04 Nov 2021 14:00:51 +0300

## yandex-vos2-autoru-consumers:0.164.11 (Wed, 03 Nov 2021 10:36:39 +0300)

  *  Autoruback 2401 consumers baker ydb fix (#1148)
     
     * AUTORUBACK-2401-CONSUMERS-YDB-FIX

  *  autoruback-2305 (#1144)
     
     * AUTORUBACK-2305
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
  *  autoruback-2401-baker-consumers (#1143)
     
     * autoruback-2401-baker-consumers 
  *  consumers-config-update

  *  config fix

  *  config fix

  *  config fix

  *   Autoruback-2401

  *   Autoruback-2401

  *  Autoruback-2401 baker consumers (#1133)
     
     * AUTORUBACK-2401
  *  AUTORUBACK-2417 send price_includes_nds to shard for moto (#1136)
     

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
     

  *  AUTORUBACK-2254-story-worker: fixed stories namespace

  *  AUTORUBACK-2315_rolf_dealer_list (#1122)
     
     * AUTORUBACK-2315_rolf_dealer_list
     
     * AUTORUBACK-2315_rolf_dealer_list: fixed compilation
     
     * AUTORUBACK-2315_rolf_dealer_list: another fix
  *  Autoruback 2386 credit tag worker logging (#1121)
     
     * #AUTORUBACK-2386 Temporary logging for CreditTagWorkerYdb
     
     * #AUTORUBACK-2386 Dont reset shark monthly payment value when remigrating
     
     * #AUTORUBACK-2386 Remove temporary logging
  *  VSDEALERSDECOMP-276 # Multiposting photos: fix classified photos (#1117)
     

  *  AUTORUBACK-1549

  *  AUTORUBACK-2308 recall offer if completed safe deal exists (#1114)
     
     * AUTORUBACK-2308 recall offer if completed safe deal exists
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2349_mds_micro_preview (#1115)
     
     * AUTORUBACK-2349_mds_micro_preview
     AUTORUBACK-2255_story_photos_to_searcher
     
     * AUTORUBACK-2349_mds_micro_preview, AUTORUBACK-2255_story_photos_to_searcher: fixed converter
  *  AUTORUBACK-2242 Allow editing the license plate once (#1113)
     
     * AUTORUBACK-2242 Allow editing the license plate once
     
     * AUTORUBACK-2242 Update license plate edit error message
     
     Co-authored-by: Sergey Kozlov <slider5@yandex-team.ru>
  *  AUTORUBACK-2270 Set seller type in preconditions request to Shark (#1111)
     
     * AUTORUBACK-2270 Set seller type in preconitions request to Shark
     
     * AUTORUBACK-2270 Use a macro instead of the if/has*/get* combo
  *  AUTORUBACK-2254-story-worker: more fixes

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
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 03 Nov 2021 10:36:39 +0300

## yandex-vos2-autoru-consumers:0.164.10 (Thu, 28 Oct 2021 17:59:03 +0300)

  *  consumers-config-update

  *  config fix

  *  config fix

  *  config fix

  *   Autoruback-2401

  *   Autoruback-2401

  *  Autoruback-2401 baker consumers (#1133)
     
     * AUTORUBACK-2401
  *  AUTORUBACK-2417 send price_includes_nds to shard for moto (#1136)
     

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
     

  *  AUTORUBACK-2254-story-worker: fixed stories namespace

  *  AUTORUBACK-2315_rolf_dealer_list (#1122)
     
     * AUTORUBACK-2315_rolf_dealer_list
     
     * AUTORUBACK-2315_rolf_dealer_list: fixed compilation
     
     * AUTORUBACK-2315_rolf_dealer_list: another fix
  *  Autoruback 2386 credit tag worker logging (#1121)
     
     * #AUTORUBACK-2386 Temporary logging for CreditTagWorkerYdb
     
     * #AUTORUBACK-2386 Dont reset shark monthly payment value when remigrating
     
     * #AUTORUBACK-2386 Remove temporary logging
  *  VSDEALERSDECOMP-276 # Multiposting photos: fix classified photos (#1117)
     

  *  AUTORUBACK-1549

  *  AUTORUBACK-2308 recall offer if completed safe deal exists (#1114)
     
     * AUTORUBACK-2308 recall offer if completed safe deal exists
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2349_mds_micro_preview (#1115)
     
     * AUTORUBACK-2349_mds_micro_preview
     AUTORUBACK-2255_story_photos_to_searcher
     
     * AUTORUBACK-2349_mds_micro_preview, AUTORUBACK-2255_story_photos_to_searcher: fixed converter
  *  AUTORUBACK-2242 Allow editing the license plate once (#1113)
     
     * AUTORUBACK-2242 Allow editing the license plate once
     
     * AUTORUBACK-2242 Update license plate edit error message
     
     Co-authored-by: Sergey Kozlov <slider5@yandex-team.ru>
  *  AUTORUBACK-2270 Set seller type in preconditions request to Shark (#1111)
     
     * AUTORUBACK-2270 Set seller type in preconitions request to Shark
     
     * AUTORUBACK-2270 Use a macro instead of the if/has*/get* combo
  *  AUTORUBACK-2254-story-worker: more fixes

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
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 28 Oct 2021 17:59:03 +0300

## yandex-vos2-autoru-consumers:0.164.9 (Wed, 27 Oct 2021 22:49:45 +0300)

  *  config fix

  *  config fix

  *  config fix

  *   Autoruback-2401

  *   Autoruback-2401

  *  Autoruback-2401 baker consumers (#1133)
     
     * AUTORUBACK-2401
  *  AUTORUBACK-2417 send price_includes_nds to shard for moto (#1136)
     

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
     

  *  AUTORUBACK-2254-story-worker: fixed stories namespace

  *  AUTORUBACK-2315_rolf_dealer_list (#1122)
     
     * AUTORUBACK-2315_rolf_dealer_list
     
     * AUTORUBACK-2315_rolf_dealer_list: fixed compilation
     
     * AUTORUBACK-2315_rolf_dealer_list: another fix
  *  Autoruback 2386 credit tag worker logging (#1121)
     
     * #AUTORUBACK-2386 Temporary logging for CreditTagWorkerYdb
     
     * #AUTORUBACK-2386 Dont reset shark monthly payment value when remigrating
     
     * #AUTORUBACK-2386 Remove temporary logging
  *  VSDEALERSDECOMP-276 # Multiposting photos: fix classified photos (#1117)
     

  *  AUTORUBACK-1549

  *  AUTORUBACK-2308 recall offer if completed safe deal exists (#1114)
     
     * AUTORUBACK-2308 recall offer if completed safe deal exists
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2349_mds_micro_preview (#1115)
     
     * AUTORUBACK-2349_mds_micro_preview
     AUTORUBACK-2255_story_photos_to_searcher
     
     * AUTORUBACK-2349_mds_micro_preview, AUTORUBACK-2255_story_photos_to_searcher: fixed converter
  *  AUTORUBACK-2242 Allow editing the license plate once (#1113)
     
     * AUTORUBACK-2242 Allow editing the license plate once
     
     * AUTORUBACK-2242 Update license plate edit error message
     
     Co-authored-by: Sergey Kozlov <slider5@yandex-team.ru>
  *  AUTORUBACK-2270 Set seller type in preconditions request to Shark (#1111)
     
     * AUTORUBACK-2270 Set seller type in preconitions request to Shark
     
     * AUTORUBACK-2270 Use a macro instead of the if/has*/get* combo
  *  AUTORUBACK-2254-story-worker: more fixes

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
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 27 Oct 2021 22:49:45 +0300

## yandex-vos2-autoru-consumers:0.164.8 (Wed, 27 Oct 2021 22:19:56 +0300)

  *  config fix

  *  config fix

  *   Autoruback-2401

  *   Autoruback-2401

  *  Autoruback-2401 baker consumers (#1133)
     
     * AUTORUBACK-2401
  *  AUTORUBACK-2417 send price_includes_nds to shard for moto (#1136)
     

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
     

  *  AUTORUBACK-2254-story-worker: fixed stories namespace

  *  AUTORUBACK-2315_rolf_dealer_list (#1122)
     
     * AUTORUBACK-2315_rolf_dealer_list
     
     * AUTORUBACK-2315_rolf_dealer_list: fixed compilation
     
     * AUTORUBACK-2315_rolf_dealer_list: another fix
  *  Autoruback 2386 credit tag worker logging (#1121)
     
     * #AUTORUBACK-2386 Temporary logging for CreditTagWorkerYdb
     
     * #AUTORUBACK-2386 Dont reset shark monthly payment value when remigrating
     
     * #AUTORUBACK-2386 Remove temporary logging
  *  VSDEALERSDECOMP-276 # Multiposting photos: fix classified photos (#1117)
     

  *  AUTORUBACK-1549

  *  AUTORUBACK-2308 recall offer if completed safe deal exists (#1114)
     
     * AUTORUBACK-2308 recall offer if completed safe deal exists
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2349_mds_micro_preview (#1115)
     
     * AUTORUBACK-2349_mds_micro_preview
     AUTORUBACK-2255_story_photos_to_searcher
     
     * AUTORUBACK-2349_mds_micro_preview, AUTORUBACK-2255_story_photos_to_searcher: fixed converter
  *  AUTORUBACK-2242 Allow editing the license plate once (#1113)
     
     * AUTORUBACK-2242 Allow editing the license plate once
     
     * AUTORUBACK-2242 Update license plate edit error message
     
     Co-authored-by: Sergey Kozlov <slider5@yandex-team.ru>
  *  AUTORUBACK-2270 Set seller type in preconditions request to Shark (#1111)
     
     * AUTORUBACK-2270 Set seller type in preconitions request to Shark
     
     * AUTORUBACK-2270 Use a macro instead of the if/has*/get* combo
  *  AUTORUBACK-2254-story-worker: more fixes

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
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 27 Oct 2021 22:19:56 +0300

## yandex-vos2-autoru-consumers:0.164.7 (Wed, 27 Oct 2021 21:58:39 +0300)

  *  config fix

  *   Autoruback-2401

  *   Autoruback-2401

  *  Autoruback-2401 baker consumers (#1133)
     
     * AUTORUBACK-2401
  *  AUTORUBACK-2417 send price_includes_nds to shard for moto (#1136)
     

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
     

  *  AUTORUBACK-2254-story-worker: fixed stories namespace

  *  AUTORUBACK-2315_rolf_dealer_list (#1122)
     
     * AUTORUBACK-2315_rolf_dealer_list
     
     * AUTORUBACK-2315_rolf_dealer_list: fixed compilation
     
     * AUTORUBACK-2315_rolf_dealer_list: another fix
  *  Autoruback 2386 credit tag worker logging (#1121)
     
     * #AUTORUBACK-2386 Temporary logging for CreditTagWorkerYdb
     
     * #AUTORUBACK-2386 Dont reset shark monthly payment value when remigrating
     
     * #AUTORUBACK-2386 Remove temporary logging
  *  VSDEALERSDECOMP-276 # Multiposting photos: fix classified photos (#1117)
     

  *  AUTORUBACK-1549

  *  AUTORUBACK-2308 recall offer if completed safe deal exists (#1114)
     
     * AUTORUBACK-2308 recall offer if completed safe deal exists
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2349_mds_micro_preview (#1115)
     
     * AUTORUBACK-2349_mds_micro_preview
     AUTORUBACK-2255_story_photos_to_searcher
     
     * AUTORUBACK-2349_mds_micro_preview, AUTORUBACK-2255_story_photos_to_searcher: fixed converter
  *  AUTORUBACK-2242 Allow editing the license plate once (#1113)
     
     * AUTORUBACK-2242 Allow editing the license plate once
     
     * AUTORUBACK-2242 Update license plate edit error message
     
     Co-authored-by: Sergey Kozlov <slider5@yandex-team.ru>
  *  AUTORUBACK-2270 Set seller type in preconditions request to Shark (#1111)
     
     * AUTORUBACK-2270 Set seller type in preconitions request to Shark
     
     * AUTORUBACK-2270 Use a macro instead of the if/has*/get* combo
  *  AUTORUBACK-2254-story-worker: more fixes

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
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 27 Oct 2021 21:58:39 +0300

## yandex-vos2-autoru-consumers:0.164.6 (Wed, 27 Oct 2021 21:50:57 +0300)

  *   Autoruback-2401

  *   Autoruback-2401

  *  Autoruback-2401 baker consumers (#1133)
     
     * AUTORUBACK-2401
  *  AUTORUBACK-2417 send price_includes_nds to shard for moto (#1136)
     

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
     

  *  AUTORUBACK-2254-story-worker: fixed stories namespace

  *  AUTORUBACK-2315_rolf_dealer_list (#1122)
     
     * AUTORUBACK-2315_rolf_dealer_list
     
     * AUTORUBACK-2315_rolf_dealer_list: fixed compilation
     
     * AUTORUBACK-2315_rolf_dealer_list: another fix
  *  Autoruback 2386 credit tag worker logging (#1121)
     
     * #AUTORUBACK-2386 Temporary logging for CreditTagWorkerYdb
     
     * #AUTORUBACK-2386 Dont reset shark monthly payment value when remigrating
     
     * #AUTORUBACK-2386 Remove temporary logging
  *  VSDEALERSDECOMP-276 # Multiposting photos: fix classified photos (#1117)
     

  *  AUTORUBACK-1549

  *  AUTORUBACK-2308 recall offer if completed safe deal exists (#1114)
     
     * AUTORUBACK-2308 recall offer if completed safe deal exists
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-2349_mds_micro_preview (#1115)
     
     * AUTORUBACK-2349_mds_micro_preview
     AUTORUBACK-2255_story_photos_to_searcher
     
     * AUTORUBACK-2349_mds_micro_preview, AUTORUBACK-2255_story_photos_to_searcher: fixed converter
  *  AUTORUBACK-2242 Allow editing the license plate once (#1113)
     
     * AUTORUBACK-2242 Allow editing the license plate once
     
     * AUTORUBACK-2242 Update license plate edit error message
     
     Co-authored-by: Sergey Kozlov <slider5@yandex-team.ru>
  *  AUTORUBACK-2270 Set seller type in preconditions request to Shark (#1111)
     
     * AUTORUBACK-2270 Set seller type in preconitions request to Shark
     
     * AUTORUBACK-2270 Use a macro instead of the if/has*/get* combo
  *  AUTORUBACK-2254-story-worker: more fixes

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
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 27 Oct 2021 21:50:57 +0300

## yandex-vos2-autoru-consumers:0.164.5 (Wed, 27 Oct 2021 21:39:38 +0300)

  *   Autoruback-2401

## yandex-vos2-autoru-consumers:0.164.3 (Wed, 27 Oct 2021 21:25:21 +0300)

  *  Autoruback-2401 baker consumers (#1133)
  
## yandex-vos2-autoru-consumers:0.164.1 (Thu, 14 Oct 2021 08:14:08 +0300)
 * up
## yandex-vos2-autoru-consumers:0.164.0 (Thu, 14 Oct 2021 08:14:08 +0300)

  *  AUTORUBACK-2270 Set seller type in preconditions request to Shark (#1111)
     
     * AUTORUBACK-2270 Set seller type in preconitions request to Shark
     
     * AUTORUBACK-2270 Use a macro instead of the if/has*/get* combo
  *  AUTORUBACK-2254-story-worker: more fixes

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
  *  AUTORUBACK-2316_supergen_name_cyrillic_fix (#1108)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 14 Oct 2021 08:14:08 +0300

## yandex-vos2-autoru-consumers:0.163.1 (Fri, 08 Oct 2021 15:06:29 +0300)

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
     

  *  Autoruback-2281 extended warranty idx (#1100)
     
     * AUTORUBACK-2281
  *  AUTORUBACK-2169_photos_add_url_to_listing (#1103)
     

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 08 Oct 2021 15:06:29 +0300

## yandex-vos2-autoru-consumers:0.163.0 (Fri, 08 Oct 2021 10:03:02 +0300)

  *  AUTORUBACK-2177 Add preview 16x9 for panorama (#1105)
     

  *  AUTORUBACK-2324 (#1107)
     

  *  Autoruback-2281 extended warranty idx (#1100)
     
     * AUTORUBACK-2281
  *  AUTORUBACK-2169_photos_add_url_to_listing (#1103)
     

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 08 Oct 2021 10:03:02 +0300

## yandex-vos2-autoru-consumers:0.162.2 (Thu, 23 Sep 2021 10:25:25 +0300)

  *  #AUTORUBACK-2172 Keep switched off options (#1070)
     
     * #AUTORUBACK-2172 Keep switched off options
     
     * #AUTORUBACK-2172 Keep switched off equpments
     
     * #AUTORUBACK-2172 Restoring of absent equipments from meta
     
     * #AUTORUBACK-2172 Revert isSuitable
  *  Revert "Restore "VSDEALERS-1289 # Convert classifieds photos" (#1084)" (#1086)
     
     This reverts commit 79db1d6f10f070664297bac517c268ec9146496f.
  *  AUTORUBACK-2069_tvm_for_mds: getinfo instead of get: revert

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 23 Sep 2021 10:25:25 +0300

## yandex-vos2-autoru-consumers:0.162.1 (Tue, 21 Sep 2021 14:32:03 +0300)

  *  AUTORUBACK-2069_tvm_for_mds: getinfo instead of get: revert

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 21 Sep 2021 14:32:03 +0300

## yandex-vos2-autoru-consumers:0.162.0 (Thu, 16 Sep 2021 17:55:42 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 16 Sep 2021 17:55:42 +0300

## yandex-vos2-autoru-consumers:0.161.1 (Wed, 15 Sep 2021 14:57:59 +0300)

  *  AUTORUBACK-1862 (#1077)
     

  *  Completed safe deal exists tag fix (#1076)
     
     * completed_safe_deal_exists tag
     
     * fix
     
     * wtfix
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-1679 (#1072)
     
     * AUTORUBACK-1679
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 15 Sep 2021 14:57:59 +0300

## yandex-vos2-autoru-consumers:0.161.0 (Tue, 14 Sep 2021 23:57:25 +0300)

  *  Completed safe deal exists tag fix (#1076)
     
     * completed_safe_deal_exists tag
     
     * fix
     
     * wtfix
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  AUTORUBACK-1679 (#1072)
     
     * AUTORUBACK-1679
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 14 Sep 2021 23:57:25 +0300

## yandex-vos2-autoru-consumers:0.160.0 (Mon, 13 Sep 2021 13:55:02 +0300)

  *  AUTORUBACK-2125 (#1067)
     
     * AUTORUBACK-2125

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 13 Sep 2021 13:55:02 +0300

## yandex-vos2-autoru-consumers:0.159.0 (Sat, 11 Sep 2021 10:40:14 +0300)

  *  #AUTORUBACK-2172 Keep enabled VIN_DECODER equipments (#1071)
     

  *  AUTORUBACK-2156 Fix allowChatsCreation default population (#1068)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 11 Sep 2021 10:40:14 +0300

## yandex-vos2-autoru-consumers:0.158.0 (Wed, 08 Sep 2021 18:12:45 +0300)

  *  Autoruback 2199 fix (#1066)
     
     * #AUTORUBACK-2199 VinDecoderDecider fix
     
     * #AUTORUBACK-2199 Update
  *  AUTORUBACK-2156 Add parameter canDisableChats (#1061)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 08 Sep 2021 18:12:45 +0300

## yandex-vos2-autoru-consumers:0.157.1 (Wed, 08 Sep 2021 11:02:30 +0300)

  *  #AUTORUBACK-2199 Old options convertation when enrich from vin-decoder (#1065)
     

  *  AUTORUBACK-1691_dealer_NO_ANSWER_ban (#1064)
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban: updated test
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban: updated another test

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 08 Sep 2021 11:02:30 +0300

## yandex-vos2-autoru-consumers:0.157.0 (Tue, 07 Sep 2021 20:42:27 +0300)

  *  AUTORUBACK-1691_dealer_NO_ANSWER_ban (#1064)
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban: updated test
     
     * AUTORUBACK-1691_dealer_NO_ANSWER_ban: updated another test

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 07 Sep 2021 20:42:27 +0300

## yandex-vos2-autoru-consumers:0.156.3 (Tue, 07 Sep 2021 19:37:23 +0300)

  *  AUTORUBACK-2125 (#1063)
     
     * AUTORUBACK-2125

  *  completed_safe_deal_exists tag (#1062)
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  VSDEALERS-1289 # Convert classifieds photos (#1052)
     

  *  VSDEALERS-1288 - add route for saving classified photos (#1049)
     
     * VSDEALERS-1288 - add route for saving classified photos
     
     * VSDEALERS-1288 - update doc
     
     * VSDEALERS-1288
     
     * VSDEALERS-1288 review
     
     * VSDEALERS-1288
     
     * VSDEALERS-1288 - review 2
     
     * VSDEALERS-1288 - add accuracy to log string
  *  AUTORUBACK-2069_tvm_for_mds: getinfo instead of get (#1056)
     

  *  Libticket parser fix (#1059)
     
     * AUTORUBACK-2125
     
     * AUTORUBACK-2125
  *  AUTORUBACK-2125 (#1053)
     
     * AUTORUBACK-2125
  *  AUTORUBACK-2175 (#1057)
     

  *  AUTORUBACK-2171 (#1054)
     

  *  AUTORUBACK-2069_tvm_for_mds: minor fix

  *  AUTORUBACK-2069_tvm_for_mds (#1051)
     
     * AUTORUBACK-2069_tvm_for_mds
     
     * AUTORUBACK-2069_tvm_for_mds: test, refactoring
     
     * AUTORUBACK-2069_tvm_for_mds: fixed tests
  *  AUTORUBACK-2137_clean_name_gallery_photo_no_verification (#1050)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 07 Sep 2021 19:37:23 +0300

## yandex-vos2-autoru-consumers:0.156.2 (Tue, 07 Sep 2021 17:26:49 +0300)

  *  completed_safe_deal_exists tag (#1062)
     
     Co-authored-by: kapavkin <kapavkin@yandex-team.ru>
  *  VSDEALERS-1289 # Convert classifieds photos (#1052)
     

  *  VSDEALERS-1288 - add route for saving classified photos (#1049)
     
     * VSDEALERS-1288 - add route for saving classified photos
     
     * VSDEALERS-1288 - update doc
     
     * VSDEALERS-1288
     
     * VSDEALERS-1288 review
     
     * VSDEALERS-1288
     
     * VSDEALERS-1288 - review 2
     
     * VSDEALERS-1288 - add accuracy to log string
  *  AUTORUBACK-2069_tvm_for_mds: getinfo instead of get (#1056)
     

  *  Libticket parser fix (#1059)
     
     * AUTORUBACK-2125
     
     * AUTORUBACK-2125
  *  AUTORUBACK-2125 (#1053)
     
     * AUTORUBACK-2125
  *  AUTORUBACK-2175 (#1057)
     

  *  AUTORUBACK-2171 (#1054)
     

  *  AUTORUBACK-2069_tvm_for_mds: minor fix

  *  AUTORUBACK-2069_tvm_for_mds (#1051)
     
     * AUTORUBACK-2069_tvm_for_mds
     
     * AUTORUBACK-2069_tvm_for_mds: test, refactoring
     
     * AUTORUBACK-2069_tvm_for_mds: fixed tests
  *  AUTORUBACK-2137_clean_name_gallery_photo_no_verification (#1050)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 07 Sep 2021 17:26:49 +0300

## yandex-vos2-autoru-consumers:0.156.1 (Mon, 06 Sep 2021 09:22:47 +0300)

  *  AUTORUBACK-2125 (#1053)
     
     * AUTORUBACK-2125
  *  AUTORUBACK-2175 (#1057)
     

  *  AUTORUBACK-2171 (#1054)
     

  *  AUTORUBACK-2069_tvm_for_mds: minor fix

  *  AUTORUBACK-2069_tvm_for_mds (#1051)
     
     * AUTORUBACK-2069_tvm_for_mds
     
     * AUTORUBACK-2069_tvm_for_mds: test, refactoring
     
     * AUTORUBACK-2069_tvm_for_mds: fixed tests
  *  AUTORUBACK-2137_clean_name_gallery_photo_no_verification (#1050)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 06 Sep 2021 09:22:47 +0300

## yandex-vos2-autoru-consumers:0.156.0 (Tue, 31 Aug 2021 08:55:04 +0300)

  *  AUTORUBACK-2137_clean_name_gallery_photo_no_verification (#1050)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 31 Aug 2021 08:55:04 +0300

## yandex-vos2-autoru-consumers:0.155.3 (Fri, 27 Aug 2021 15:11:18 +0300)

  *  AUTORUBACK-1685 Add poi_count to pamoramas (#1046)
     

  *  AUTORUBACK-2100_new_vas_show-in-stories (#1048)
     

  *  AUTORUBACK-1862 (#1047)
     

  *  VSDEALERS-1285 # Multiposting: photos for classifieds (#1045)
     

  *  VSDEALERS-1262 adding global_status to holocron models data filling (#1044)
     
     * VSDEALERS-1262 adding global_status to holocron models data filling
     
     * fix error || -> |
     
     * code review
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 27 Aug 2021 15:11:18 +0300

## yandex-vos2-autoru-consumers:0.155.2 (Fri, 27 Aug 2021 13:20:55 +0300)

  *  AUTORUBACK-2100_new_vas_show-in-stories (#1048)
     

  *  AUTORUBACK-1862 (#1047)
     

  *  VSDEALERS-1285 # Multiposting: photos for classifieds (#1045)
     

  *  VSDEALERS-1262 adding global_status to holocron models data filling (#1044)
     
     * VSDEALERS-1262 adding global_status to holocron models data filling
     
     * fix error || -> |
     
     * code review
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 27 Aug 2021 13:20:55 +0300

## yandex-vos2-autoru-consumers:0.155.1 (Tue, 24 Aug 2021 18:29:10 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 24 Aug 2021 18:29:10 +0300

## yandex-vos2-autoru-consumers:0.155.0 (Tue, 24 Aug 2021 16:31:10 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 24 Aug 2021 16:31:10 +0300

## yandex-vos2-autoru-consumers:0.154.3 (Fri, 20 Aug 2021 22:26:05 +0300)

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix: compilation fix

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2116: panoramas topic partition 0 freeze fix

  *  VSDEALERS-1196 # Log NEED_ACTIVATION flag updates (#1040)
     
     * VSDEALERS-1196 # Log NEED_ACTIVATION flag updates
  *  AUTORUBACK-1589 Make panoramas request in notify center (#1014)
     

  *  make fmt

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862 (#1032)
     
     * AUTORUBACK-1862

  *  rename statist counter (#1039)
     

  *  AUTORUBACK-2102_do_not_migrate_statuses: added logging

  *  AUTORUBACK-2102_do_not_migrate_statuses (#1038)
     
     * AUTORUBACK-2102_do_not_migrate_statuses
     
     * AUTORUBACK-2102_do_not_migrate_statuses: added test, minor changes

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 20 Aug 2021 22:26:05 +0300

## yandex-vos2-autoru-consumers:0.154.2 (Fri, 20 Aug 2021 17:45:49 +0300)

  *  VSDEALERS-1196 # Log NEED_ACTIVATION flag updates (#1040)
     
     * VSDEALERS-1196 # Log NEED_ACTIVATION flag updates
  *  AUTORUBACK-1589 Make panoramas request in notify center (#1014)
     

  *  make fmt

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862 (#1032)
     
     * AUTORUBACK-1862

  *  rename statist counter (#1039)
     

  *  AUTORUBACK-2102_do_not_migrate_statuses: added logging

  *  AUTORUBACK-2102_do_not_migrate_statuses (#1038)
     
     * AUTORUBACK-2102_do_not_migrate_statuses
     
     * AUTORUBACK-2102_do_not_migrate_statuses: added test, minor changes

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 20 Aug 2021 17:45:49 +0300

## yandex-vos2-autoru-consumers:0.154.1 (Thu, 19 Aug 2021 20:21:08 +0300)

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862

  *  AUTORUBACK-1862 (#1032)
     
     * AUTORUBACK-1862

  *  rename statist counter (#1039)
     

  *  AUTORUBACK-2102_do_not_migrate_statuses: added logging

  *  AUTORUBACK-2102_do_not_migrate_statuses (#1038)
     
     * AUTORUBACK-2102_do_not_migrate_statuses
     
     * AUTORUBACK-2102_do_not_migrate_statuses: added test, minor changes

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 19 Aug 2021 20:21:08 +0300

## yandex-vos2-autoru-consumers:0.154.0 (Thu, 19 Aug 2021 19:26:21 +0300)

  *  AUTORUBACK-1862 (#1032)
     
     * AUTORUBACK-1862

  *  rename statist counter (#1039)
     

  *  AUTORUBACK-2102_do_not_migrate_statuses: added logging

  *  AUTORUBACK-2102_do_not_migrate_statuses (#1038)
     
     * AUTORUBACK-2102_do_not_migrate_statuses
     
     * AUTORUBACK-2102_do_not_migrate_statuses: added test, minor changes

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 19 Aug 2021 19:26:21 +0300

## yandex-vos2-autoru-consumers:0.153.0 (Wed, 18 Aug 2021 16:31:48 +0300)

  *  AUTORUBACK-2101 move to new kafka topic for AutoruPassportEventsConsumer (#1036)
     

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  #AUTORUBACK-1672 Operator support

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 18 Aug 2021 16:31:48 +0300

## yandex-vos2-autoru-consumers:0.152.0 (Tue, 17 Aug 2021 17:15:29 +0300)

  *  #AUTORUBACK-1654 Do not process deleted offers (#1035)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 17 Aug 2021 17:15:29 +0300

## yandex-vos2-autoru-consumers:0.151.3 (Mon, 16 Aug 2021 11:56:58 +0300)

  *  #AUTORUBACK-1654 Latest offset for VinDecoderConsumer

  *  FutureUtilSpec fix

  *  #AUTORUBACK-1672 Features update (#1033)
     
     * #AUTORUBACK-1672 Features update
     
     * #AUTORUBACK-1672 Features update
  *  VSDEALERS-1243 schema-registry update with new TradeInInfo type (#1031)
     
     * VSDEALERS-1243 schema-registry update with new TradeInInfo type
     
     * VSDEALERS-1243 schema-registry breaking changes
     
     * VSDEALERS-1243 more safe_deal-related breaking changes
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2071 new doppel topic again

  *  #AUTORUBACK-1654 Dealer offers equipments enrichment from vin-decoder (#1022)
     
     * #AUTORUBACK-1654 Dealer offers equipments enrichment from vin-decoder
     
     * #AUTORUBACK-1654 Review fixes
     
     * #AUTORUBACK-1654 Review fixes
     
     * #AUTORUBACK-1654 Review fixes
     
     * Unused imports fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 16 Aug 2021 11:56:58 +0300

## yandex-vos2-autoru-consumers:0.151.2 (Mon, 16 Aug 2021 11:04:47 +0300)

  *  #AUTORUBACK-1672 Features update (#1033)
     
     * #AUTORUBACK-1672 Features update
     
     * #AUTORUBACK-1672 Features update
  *  VSDEALERS-1243 schema-registry update with new TradeInInfo type (#1031)
     
     * VSDEALERS-1243 schema-registry update with new TradeInInfo type
     
     * VSDEALERS-1243 schema-registry breaking changes
     
     * VSDEALERS-1243 more safe_deal-related breaking changes
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2071 new doppel topic again

  *  #AUTORUBACK-1654 Dealer offers equipments enrichment from vin-decoder (#1022)
     
     * #AUTORUBACK-1654 Dealer offers equipments enrichment from vin-decoder
     
     * #AUTORUBACK-1654 Review fixes
     
     * #AUTORUBACK-1654 Review fixes
     
     * #AUTORUBACK-1654 Review fixes
     
     * Unused imports fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 16 Aug 2021 11:04:47 +0300

## yandex-vos2-autoru-consumers:0.151.1 (Thu, 12 Aug 2021 19:13:34 +0300)

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-2071 new doppel topic again

  *  #AUTORUBACK-1654 Dealer offers equipments enrichment from vin-decoder (#1022)
     
     * #AUTORUBACK-1654 Dealer offers equipments enrichment from vin-decoder
     
     * #AUTORUBACK-1654 Review fixes
     
     * #AUTORUBACK-1654 Review fixes
     
     * #AUTORUBACK-1654 Review fixes
     
     * Unused imports fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 12 Aug 2021 19:13:34 +0300

## yandex-vos2-autoru-consumers:0.151.0 (Thu, 12 Aug 2021 15:07:53 +0300)

  *  #AUTORUBACK-1654 Dealer offers equipments enrichment from vin-decoder (#1022)
     
     * #AUTORUBACK-1654 Dealer offers equipments enrichment from vin-decoder
     
     * #AUTORUBACK-1654 Review fixes
     
     * #AUTORUBACK-1654 Review fixes
     
     * #AUTORUBACK-1654 Review fixes
     
     * Unused imports fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 12 Aug 2021 15:07:53 +0300

## yandex-vos2-autoru-consumers:0.150.0 (Thu, 12 Aug 2021 12:58:35 +0300)

  *  AUTORUBACK-2071 new doppel topic temporary revert

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 12 Aug 2021 12:58:35 +0300

## yandex-vos2-autoru-consumers:0.149.0 (Wed, 11 Aug 2021 11:29:01 +0300)

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
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 11 Aug 2021 11:29:01 +0300

## yandex-vos2-autoru-consumers:0.148.5 (Mon, 09 Aug 2021 13:08:43 +0300)

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  #AUTORUBACK-1983 SafeDealEngine start

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
     

  *  Convert regular price to rubles if rub_price is 0 when sending offer to moderation (#1017)
     
     Co-authored-by: Tymur Lysenko <tymur-lysenko@yandex-team.ru>
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
  *  AUTORUBACK-1948 moderation allow update removed offers (#1012)
     

  *  AUTORUBACK-1972 delete check isCallCenter (#1010)
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 09 Aug 2021 13:08:43 +0300

## yandex-vos2-autoru-consumers:0.148.4 (Mon, 09 Aug 2021 11:53:57 +0300)

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
     

  *  Convert regular price to rubles if rub_price is 0 when sending offer to moderation (#1017)
     
     Co-authored-by: Tymur Lysenko <tymur-lysenko@yandex-team.ru>
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
  *  AUTORUBACK-1948 moderation allow update removed offers (#1012)
     

  *  AUTORUBACK-1972 delete check isCallCenter (#1010)
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 09 Aug 2021 11:53:57 +0300

## yandex-vos2-autoru-consumers:0.148.3 (Mon, 09 Aug 2021 10:52:26 +0300)

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
     

  *  Convert regular price to rubles if rub_price is 0 when sending offer to moderation (#1017)
     
     Co-authored-by: Tymur Lysenko <tymur-lysenko@yandex-team.ru>
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
  *  AUTORUBACK-1948 moderation allow update removed offers (#1012)
     

  *  AUTORUBACK-1972 delete check isCallCenter (#1010)
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 09 Aug 2021 10:52:26 +0300

## yandex-vos2-autoru-consumers:0.148.2 (Fri, 06 Aug 2021 16:21:43 +0300)

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
     

  *  Convert regular price to rubles if rub_price is 0 when sending offer to moderation (#1017)
     
     Co-authored-by: Tymur Lysenko <tymur-lysenko@yandex-team.ru>
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
  *  AUTORUBACK-1948 moderation allow update removed offers (#1012)
     

  *  AUTORUBACK-1972 delete check isCallCenter (#1010)
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 06 Aug 2021 16:21:43 +0300

## yandex-vos2-autoru-consumers:0.148.1 (Thu, 05 Aug 2021 14:08:35 +0300)

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
     

  *  Convert regular price to rubles if rub_price is 0 when sending offer to moderation (#1017)
     
     Co-authored-by: Tymur Lysenko <tymur-lysenko@yandex-team.ru>
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
  *  AUTORUBACK-1948 moderation allow update removed offers (#1012)
     

  *  AUTORUBACK-1972 delete check isCallCenter (#1010)
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 05 Aug 2021 14:08:35 +0300

## yandex-vos2-autoru-consumers:0.148.0 (Thu, 05 Aug 2021 11:33:50 +0300)

  *  AUTORUBACK-2025_keep_callcenter_active (#1023)
     
     * AUTORUBACK-2025_keep_callcenter_active
     
     * AUTORUBACK-2025_keep_callcenter_active: added test
  *  AUTORUBACK-2026 (#1021)
     

  *  Convert regular price to rubles if rub_price is 0 when sending offer to moderation (#1017)
     
     Co-authored-by: Tymur Lysenko <tymur-lysenko@yandex-team.ru>
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
  *  AUTORUBACK-1948 moderation allow update removed offers (#1012)
     

  *  AUTORUBACK-1972 delete check isCallCenter (#1010)
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 05 Aug 2021 11:33:50 +0300

## yandex-vos2-autoru-consumers:0.147.0 (Mon, 19 Jul 2021 19:04:58 +0300)

  *  AUTORUBACK-1786_app2app_back_to_chat_fix2: call source in call info properties (#1008)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 19 Jul 2021 19:04:58 +0300

## yandex-vos2-autoru-consumers:0.146.0 (Mon, 19 Jul 2021 15:50:08 +0300)

  *  1711 consumers lost offers logging (#1007)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 19 Jul 2021 15:50:08 +0300

## yandex-vos2-autoru-consumers:0.145.0 (Mon, 19 Jul 2021 15:16:48 +0300)

  *  1711 consumers lost offers logging (#1006)
     
     * 1711 consumers lost offers logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 19 Jul 2021 15:16:48 +0300

## yandex-vos2-autoru-consumers:0.144.0 (Mon, 19 Jul 2021 15:02:34 +0300)

  *  1711 fix

  *  VSDEALERS-1114 # Update converters for tradeIn (#997)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 19 Jul 2021 15:02:34 +0300

## yandex-vos2-autoru-consumers:0.143.0 (Fri, 16 Jul 2021 09:41:02 +0300)

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
  *  AUTORUBACK-1832 Migrate from Java 9 method (#999)
     

  *  Autoruback 1832 reprocess panoram (#996)
     
     * AUTORUBACK-1832 Create Bypass Panorama worker
  *  Autoruback 1711 reverse migration (#973)
     
     * AUTORUBACK-1711

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 16 Jul 2021 09:41:02 +0300

## yandex-vos2-autoru-consumers:0.142.2 (Tue, 13 Jul 2021 10:05:37 +0300)

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
  *  AUTORUBACK-1786_app2app_back_to_chat (#992)
     
     * AUTORUBACK-1786_app2app_back_to_chat
     
     * AUTORUBACK-1786_app2app_back_to_chat: format
  *  AUTORUBACK-1895 (#990)
     

  *  AUTORUBACK-1815_new_doppel_topic (#989)
     

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 13 Jul 2021 10:05:37 +0300

## yandex-vos2-autoru-consumers:0.142.1 (Thu, 08 Jul 2021 18:34:53 +0300)

  *  AUTORUBACK-1786_app2app_back_to_chat (#992)
     
     * AUTORUBACK-1786_app2app_back_to_chat
     
     * AUTORUBACK-1786_app2app_back_to_chat: format
  *  AUTORUBACK-1895 (#990)
     

  *  AUTORUBACK-1815_new_doppel_topic (#989)
     

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 08 Jul 2021 18:34:53 +0300

## yandex-vos2-autoru-consumers:0.142.0 (Mon, 05 Jul 2021 15:54:17 +0300)

  *  AUTORUBACK-1815_new_doppel_topic (#989)
     

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 05 Jul 2021 15:54:17 +0300

## yandex-vos2-autoru-consumers:0.141.0 (Wed, 30 Jun 2021 17:17:40 +0300)

  *  VSDEALERS-1089 # Fix DateTime.now for warranty expiration check (#985)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 30 Jun 2021 17:17:40 +0300

## yandex-vos2-autoru-consumers:0.140.0 (Wed, 30 Jun 2021 12:37:01 +0300)

  *  VSDEALERS-1075 # Add logs (#983)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 30 Jun 2021 12:37:01 +0300

## yandex-vos2-autoru-consumers:0.139.1 (Tue, 29 Jun 2021 19:02:47 +0300)

  *  AUTORUBACK-1861_moderation_consumer_fix: old db operation in try-catch (#984)
     
     * AUTORUBACK-1861_moderation_consumer_fix: old db operation in try-catch
     
     * AUTORUBACK-1861_moderation_consumer_fix: reverted ApiException NoStackTrace
     
     * AUTORUBACK-1861_moderation_consumer_fix: format
  *  AUTORUBACK-1861_consumer_metrics_update (#982)
     
     * AUTORUBACK-1861_consumer_metrics_update
     
     * AUTORUBACK-1861_consumer_metrics_update: format
  *  AUTORUBACK-1845 delete broken panorama (#980)
     
     * AUTORUBACK-1845 delete panoramas , not unpublish them
  *  Autoruback 1071 oom (#977)
     
     AUTORUBACK-1841
     AUTORUBACK-1071
  *  VSDEALERS-962 # Update multiposting archive logic (#975)
     
     * VSDEALERS-962 # Update multiposting archive logic
     
     * VSDEALERS-962 # Use helper for changing multiposting status
  *  AUTORUBACK-1727 add is_reseller (#976)
     
     * AUTORUBACK-1727 add is_reseller
     
     * AUTORUBACK-1727 add is_reseller
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 29 Jun 2021 19:02:47 +0300

## yandex-vos2-autoru-consumers:0.139.0 (Tue, 29 Jun 2021 16:12:00 +0300)

  *  AUTORUBACK-1861_consumer_metrics_update (#982)
     
     * AUTORUBACK-1861_consumer_metrics_update
     
     * AUTORUBACK-1861_consumer_metrics_update: format
  *  AUTORUBACK-1845 delete broken panorama (#980)
     
     * AUTORUBACK-1845 delete panoramas , not unpublish them
  *  Autoruback 1071 oom (#977)
     
     AUTORUBACK-1841
     AUTORUBACK-1071
  *  VSDEALERS-962 # Update multiposting archive logic (#975)
     
     * VSDEALERS-962 # Update multiposting archive logic
     
     * VSDEALERS-962 # Use helper for changing multiposting status
  *  AUTORUBACK-1727 add is_reseller (#976)
     
     * AUTORUBACK-1727 add is_reseller
     
     * AUTORUBACK-1727 add is_reseller
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 29 Jun 2021 16:12:00 +0300

## yandex-vos2-autoru-consumers:0.138.0 (Fri, 18 Jun 2021 14:05:30 +0300)

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
  *  autoruback-1071 (#966)
     
     * autoruback-1071

  *  AUTORUBACK-1683_mod_notifications_critical (#963)
     

  *  autoruback-1071 (#962)
     
     * autoruback-1071

  *  Autoruback-1071 workers 6 (#920)
     
     * AUTORUBACK-1071
  *  Autoruback-1696 fix indexes (#961)
     
     * autoruback-1696
  *  delete normalized stickers (#960)
     
     Co-authored-by: strelkovajuli <strelkovajuli@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-1071-workers (#957)
     

  *  AUTORUBACK-1071-features-ydb (#956)
     

  *  Autoruback 1747 try in telepony stage (#955)
     
     * #AUTORUBACK-1747 Wrap API calls with try in TeleponyStage
     
     * #AUTORUBACK-1747 dealer-pony.plaintext = true
  *  AUTORUBACK-1684 флаг и серчтег "продает перекуп" (#954)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 18 Jun 2021 14:05:30 +0300

## yandex-vos2-autoru-consumers:0.137.0 (Thu, 03 Jun 2021 10:58:09 +0300)

  *  VSDEALERS-480 - check both EXPIRED and INACTIVE status for hiding (#950)
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 03 Jun 2021 10:58:09 +0300

## yandex-vos2-autoru-consumers:0.136.0 (Mon, 31 May 2021 19:59:49 +0300)

  *  VSDEALERS-1000 # Multiposting: update banned offers message template (#948)
     
     * VSDEALERS-1000 # Multiposting: update banned offers message template
     
     * VSDEALERS-1000 # Multiposting: update banned offers message template

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 31 May 2021 19:59:49 +0300

## yandex-vos2-autoru-consumers:0.135.0 (Fri, 28 May 2021 12:48:48 +0300)

  *  VSDEALERS-944 # Multiposting: FIX letter with banned offers (#944)
     
     * VSDEALERS-944 # Multiposting: FIX letter with banned offers
     
     * VSDEALERS-944 # Multiposting: FIX letter with banned offers
     
     * VSDEALERS-944 # Multiposting: FIX letter with banned offers
  *  Autoruback 1675 last offer not unpublish (#943)
     
     * AUTORUBACK-1675 clean excess logging
  *  AUTORUBACK-1689_mirror_from_mdb (#939)
     

  *  AUTORUBACK-1675 last offer not unpublish (#942)
     
     * AUTORUBACK-1675 check place where error happens
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 28 May 2021 12:48:48 +0300

## yandex-vos2-autoru-consumers:0.134.2 (Thu, 27 May 2021 14:25:18 +0300)

  *  VSDEALERS-900 - add some logs to sender banned offers (#941)
     
     * VSDEALERS-900 - send letter with banned offers from Avito
     
     * VSDEALERS-900 - fix test
     
     * VSDEALERS-900 - fix test 2
     
     * VSDEALERS-900 - code review
     
     * VSDEALERS-900 - fix template
     
     * VSDEALERS-900 - add tests
     
     * VSDEALERS-900 - code review
     
     * VSDEALERS-900 - code review 2
     
     * VSDEALERS-900 - add some logs to sender banned offers
     
     * VSDEALERS-900 - optimized
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
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
  *  VSDEALERS-900 - send letter with banned offers from Avito (#925)
     
     * VSDEALERS-900 - send letter with banned offers from Avito
     
     * VSDEALERS-900 - fix test
     
     * VSDEALERS-900 - fix test 2
     
     * VSDEALERS-900 - code review
     
     * VSDEALERS-900 - fix template
     
     * VSDEALERS-900 - add tests
     
     * VSDEALERS-900 - code review
     
     * VSDEALERS-900 - code review 2
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 27 May 2021 14:25:18 +0300

## yandex-vos2-autoru-consumers:0.134.1 (Mon, 24 May 2021 19:43:56 +0300)

  *  AUTORUBACK-1521_app2app_callinfo_fix (#935)
     
     * AUTORUBACK-1521_app2app_callinfo_fix
     
     * AUTORUBACK-1521_app2app_callinfo_fix: format
     
     * AUTORUBACK-1521_app2app_callinfo_fix: fixed tests and compilation
  *  AUTORUBACK-1620 kafka miss some records (#928)
     
     * AUTORUBACK-1620 rewriting panoramas on draft save
  *  VSDEALERS-900 - send letter with banned offers from Avito (#925)
     
     * VSDEALERS-900 - send letter with banned offers from Avito
     
     * VSDEALERS-900 - fix test
     
     * VSDEALERS-900 - fix test 2
     
     * VSDEALERS-900 - code review
     
     * VSDEALERS-900 - fix template
     
     * VSDEALERS-900 - add tests
     
     * VSDEALERS-900 - code review
     
     * VSDEALERS-900 - code review 2
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 24 May 2021 19:43:56 +0300

## yandex-vos2-autoru-consumers:0.134.0 (Fri, 21 May 2021 18:20:54 +0300)

  *  AUTORUBACK-1620 kafka miss some records (#928)
     
     * AUTORUBACK-1620 rewriting panoramas on draft save
  *  VSDEALERS-900 - send letter with banned offers from Avito (#925)
     
     * VSDEALERS-900 - send letter with banned offers from Avito
     
     * VSDEALERS-900 - fix test
     
     * VSDEALERS-900 - fix test 2
     
     * VSDEALERS-900 - code review
     
     * VSDEALERS-900 - fix template
     
     * VSDEALERS-900 - add tests
     
     * VSDEALERS-900 - code review
     
     * VSDEALERS-900 - code review 2
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 21 May 2021 18:20:54 +0300

## yandex-vos2-autoru-consumers:0.133.2 (Fri, 21 May 2021 11:07:26 +0300)

  *  AUTORUSUP-5421 # Log photo names on MaxPhotoCount error (#932)
     

  *  AUTORUBACK-1651 fix filter bloked calls for consumer (#930)
     

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 21 May 2021 11:07:26 +0300

## yandex-vos2-autoru-consumers:0.133.1 (Thu, 20 May 2021 19:50:17 +0300)

  *  AUTORUBACK-1651 fix filter bloked calls for consumer (#930)
     

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 20 May 2021 19:50:17 +0300

## yandex-vos2-autoru-consumers:0.133.0 (Thu, 20 May 2021 17:18:58 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 20 May 2021 17:18:58 +0300

## yandex-vos2-autoru-consumers:0.132.1 (Tue, 11 May 2021 18:53:21 +0300)

  *  VSDEALERSDECOMP-237 # FIX protobuf mergeFrom repeated fields duplication (#919)
     

  *  Autoruback-1071 workers 4 (#916)
     
     * AUTORUBACK-1071
  *  AUTORUBACK-1434_score_to_holocron (#915)
     

  *  AUTORUBACK-1071-another-ydb-workers (#911)
     
     * AUTORUBACK-1071
  *  VSDEALERS-865 - add new api for getting detailed offerIds by vins (#913)
     
     * VSDEALERS-865 - add new api for getting detailed offerIds by vins
     
     * VSDEALERS-865 - add doc for detailed offer id api
     
     * VSDEALERS-865 - fix new root path
     
     * VSDEALERS-865 - fix
     
     * VSDEALERS-865 - fix get parameter
     
     * VSDEALERS-865 - add convertion to scala collection
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 11 May 2021 18:53:21 +0300

## yandex-vos2-autoru-consumers:0.132.0 (Thu, 29 Apr 2021 12:19:18 +0300)

  *  VSDEALERS-865 - add new api for getting detailed offerIds by vins (#913)
     
     * VSDEALERS-865 - add new api for getting detailed offerIds by vins
     
     * VSDEALERS-865 - add doc for detailed offer id api
     
     * VSDEALERS-865 - fix new root path
     
     * VSDEALERS-865 - fix
     
     * VSDEALERS-865 - fix get parameter
     
     * VSDEALERS-865 - add convertion to scala collection
     
     Co-authored-by: Anton Kryachko <akryachko@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 29 Apr 2021 12:19:18 +0300

## yandex-vos2-autoru-consumers:0.131.3 (Tue, 27 Apr 2021 13:15:25 +0300)

  *  AUTORUBACK-1442_reseller_clean_name: more logs

  *  VSDEALERS-890 # Multiposting: update offer with new classified state values (#912)
     

  *  AUTORUBACK-1442_reseller_clean_name (#910)
     
     * AUTORUBACK-1442_reseller_clean_name
     
     * AUTORUBACK-1442_reseller_clean_name: proven owner tag, proven owner notification, repeated verdicts
  *  AUTORUBACK-1547_trusted_dealer_calls_accepted (#909)
     

  *  AUTORUBACK-1521_app2app_call_notifications (#908)
     
     (cherry picked from commit 4ee02991fbb7005193966c236066cb219401fad5)
  *  Revert "AUTORUBACK-1521_app2app_call_notifications"
     
     This reverts commit 4ee02991fbb7005193966c236066cb219401fad5.

  *  AUTORUBACK-1521_app2app_call_notifications

  *  AUTORUBACK-1444_mod_protection_editor (#907)
     

  *  AUTORUBACK-1543: Add GosUslugi tag writer (#906)
     

  *  AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 27 Apr 2021 13:15:25 +0300

## yandex-vos2-autoru-consumers:0.131.2 (Mon, 26 Apr 2021 17:09:04 +0300)

  *  AUTORUBACK-1442_reseller_clean_name (#910)
     
     * AUTORUBACK-1442_reseller_clean_name
     
     * AUTORUBACK-1442_reseller_clean_name: proven owner tag, proven owner notification, repeated verdicts
  *  AUTORUBACK-1547_trusted_dealer_calls_accepted (#909)
     

  *  AUTORUBACK-1521_app2app_call_notifications (#908)
     
     (cherry picked from commit 4ee02991fbb7005193966c236066cb219401fad5)
  *  Revert "AUTORUBACK-1521_app2app_call_notifications"
     
     This reverts commit 4ee02991fbb7005193966c236066cb219401fad5.

  *  AUTORUBACK-1521_app2app_call_notifications

  *  AUTORUBACK-1444_mod_protection_editor (#907)
     

  *  AUTORUBACK-1543: Add GosUslugi tag writer (#906)
     

  *  AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 26 Apr 2021 17:09:04 +0300

## yandex-vos2-autoru-consumers:0.131.1 (Sun, 25 Apr 2021 10:48:19 +0300)

  *  AUTORUBACK-1547_trusted_dealer_calls_accepted (#909)
     

  *  AUTORUBACK-1521_app2app_call_notifications (#908)
     
     (cherry picked from commit 4ee02991fbb7005193966c236066cb219401fad5)
  *  Revert "AUTORUBACK-1521_app2app_call_notifications"
     
     This reverts commit 4ee02991fbb7005193966c236066cb219401fad5.

  *  AUTORUBACK-1521_app2app_call_notifications

  *  AUTORUBACK-1444_mod_protection_editor (#907)
     

  *  AUTORUBACK-1543: Add GosUslugi tag writer (#906)
     

  *  AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 25 Apr 2021 10:48:19 +0300

## yandex-vos2-autoru-consumers:0.131.0 (Sat, 24 Apr 2021 22:20:39 +0300)

  *  AUTORUBACK-1521_app2app_call_notifications (#908)
     
     (cherry picked from commit 4ee02991fbb7005193966c236066cb219401fad5)
  *  Revert "AUTORUBACK-1521_app2app_call_notifications"
     
     This reverts commit 4ee02991fbb7005193966c236066cb219401fad5.

  *  AUTORUBACK-1521_app2app_call_notifications

  *  AUTORUBACK-1444_mod_protection_editor (#907)
     

  *  AUTORUBACK-1543: Add GosUslugi tag writer (#906)
     

  *  AUTORUBACK-1071

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 24 Apr 2021 22:20:39 +0300

## yandex-vos2-autoru-consumers:0.130.5 (Wed, 21 Apr 2021 19:23:01 +0300)

  *  AUTORUBACK-1584 fix vos consumer deploy (#903)
     
     * AUTORUBACK-1584 fix vos consumer deploy

  *  AUTORUBACK-1574_price_int_overflow (#901)
     
     * AUTORUBACK-1574_price_int_overflow
     
     * AUTORUBACK-1574_price_int_overflow: style
  *  AUTORUBACK-1352 fix (#902)
     
     * AUTORUBACK-1352 fix panoramas consumer
     
     * AUTORUBACK-1352 fix interior panoramas api
     
     * AUTORUBACK-1352 fix interior panoramas consumers
     
     * AUTORUBACK-1352 fix interior panoramas consumers
  *  AUTORUBACK-1352 fix (#900)
     
     
     * AUTORUBACK-1352 fix interior panoramas consumers
  *  AUTORUBACK-1069-fix-threadpool (#878)
     
     * AUTORUBACK-1069

  *  AUTORUBACK-1352 fix (#899)
     
     * AUTORUBACK-1352 fix interior panoramas api
  *  AUTORUBACK-1352 fix panoramas consumer (#897)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 21 Apr 2021 19:23:01 +0300

## yandex-vos2-autoru-consumers:0.130.4 (Wed, 21 Apr 2021 19:14:44 +0300)

  *  Merge branch 'master' into AUTORUBACK-1584_fix_vos_consumer_deploy
  *  AUTORUBACK-1352 fix interior panoramas consumers

  *  AUTORUBACK-1574_price_int_overflow (#901)
     
     * AUTORUBACK-1574_price_int_overflow
     
     * AUTORUBACK-1574_price_int_overflow: style
  *  AUTORUBACK-1352 fix (#902)
     
     * AUTORUBACK-1352 fix panoramas consumer
     
     * AUTORUBACK-1352 fix interior panoramas api
     
     * AUTORUBACK-1352 fix interior panoramas consumers
     
     * AUTORUBACK-1352 fix interior panoramas consumers
  *  AUTORUBACK-1352 fix (#900)
     
     
     * AUTORUBACK-1352 fix interior panoramas consumers
  *  AUTORUBACK-1069-fix-threadpool (#878)
     
     * AUTORUBACK-1069

  *  AUTORUBACK-1352 fix (#899)
     
     * AUTORUBACK-1352 fix interior panoramas api
  *  AUTORUBACK-1352 fix panoramas consumer (#897)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 21 Apr 2021 19:14:44 +0300

## yandex-vos2-autoru-consumers:0.130.3 (Wed, 21 Apr 2021 19:06:25 +0300)

  *  AUTORUBACK-1574_price_int_overflow (#901)
     
     * AUTORUBACK-1574_price_int_overflow
     
     * AUTORUBACK-1574_price_int_overflow: style
  *  AUTORUBACK-1352 fix (#902)
     
     * AUTORUBACK-1352 fix panoramas consumer
     
     * AUTORUBACK-1352 fix interior panoramas api
     
     * AUTORUBACK-1352 fix interior panoramas consumers
     
     * AUTORUBACK-1352 fix interior panoramas consumers
  *  AUTORUBACK-1352 fix (#900)
     
     
     * AUTORUBACK-1352 fix interior panoramas consumers
  *  AUTORUBACK-1069-fix-threadpool (#878)
     
     * AUTORUBACK-1069

  *  AUTORUBACK-1352 fix (#899)
     
     * AUTORUBACK-1352 fix interior panoramas api
  *  AUTORUBACK-1352 fix panoramas consumer (#897)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 21 Apr 2021 19:06:25 +0300

## yandex-vos2-autoru-consumers:0.130.2 (Wed, 21 Apr 2021 17:46:00 +0300)

  *  AUTORUBACK-1574_price_int_overflow (#901)
     
     * AUTORUBACK-1574_price_int_overflow
     
     * AUTORUBACK-1574_price_int_overflow: style
  *  AUTORUBACK-1352 fix (#902)
     
     * AUTORUBACK-1352 fix panoramas consumer
     
     * AUTORUBACK-1352 fix interior panoramas api
     
     * AUTORUBACK-1352 fix interior panoramas consumers
     
     * AUTORUBACK-1352 fix interior panoramas consumers
  *  AUTORUBACK-1352 fix (#900)
     
     
     * AUTORUBACK-1352 fix interior panoramas consumers
  *  AUTORUBACK-1069-fix-threadpool (#878)
     
     * AUTORUBACK-1069

  *  AUTORUBACK-1352 fix (#899)
     
     * AUTORUBACK-1352 fix interior panoramas api
  *  AUTORUBACK-1352 fix panoramas consumer (#897)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 21 Apr 2021 17:46:00 +0300

## yandex-vos2-autoru-consumers:0.130.1 (Wed, 21 Apr 2021 15:44:57 +0300)

  *  AUTORUBACK-1352 fix (#902)
     
     * AUTORUBACK-1352 fix panoramas consumer
     
     * AUTORUBACK-1352 fix interior panoramas api
     
     * AUTORUBACK-1352 fix interior panoramas consumers
     
     * AUTORUBACK-1352 fix interior panoramas consumers
  *  AUTORUBACK-1352 fix (#900)
     
     
     * AUTORUBACK-1352 fix interior panoramas consumers
  *  AUTORUBACK-1069-fix-threadpool (#878)
     
     * AUTORUBACK-1069

  *  AUTORUBACK-1352 fix (#899)
     
     * AUTORUBACK-1352 fix interior panoramas api
  *  AUTORUBACK-1352 fix panoramas consumer (#897)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 21 Apr 2021 15:44:57 +0300

## yandex-vos2-autoru-consumers:0.130.0 (Wed, 21 Apr 2021 14:49:09 +0300)

  *  AUTORUBACK-1352 fix (#900)
     
     
     * AUTORUBACK-1352 fix interior panoramas consumers
  *  AUTORUBACK-1069-fix-threadpool (#878)
     
     * AUTORUBACK-1069

  *  AUTORUBACK-1352 fix (#899)
     
     * AUTORUBACK-1352 fix interior panoramas api
  *  AUTORUBACK-1352 fix panoramas consumer (#897)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 21 Apr 2021 14:49:09 +0300

## yandex-vos2-autoru-consumers:0.129.2 (Tue, 20 Apr 2021 19:24:26 +0300)

  *  AUTORUBACK-1352 fix panoramas consumer (#897)
     

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
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 20 Apr 2021 19:24:26 +0300

## yandex-vos2-autoru-consumers:0.129.1 (Tue, 20 Apr 2021 18:28:59 +0300)

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
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 20 Apr 2021 18:28:59 +0300

## yandex-vos2-autoru-consumers:0.129.0 (Tue, 20 Apr 2021 16:17:42 +0300)

  *  AUTORUBACK-1511_dealer_duplicates_fix (#894)
     
     * AUTORUBACK-1511_dealer_duplicates_fix
     
     * AUTORUBACK-1511_dealer_duplicates_fix: fixed tests
  *  VSDEALERS-880 Add broker fields to holo offer (#895)
     
     * VSDEALERS-880 Add broker fields to holo offer
     
     * Fix AUTORU status
     
     * Fix AVTORU status definition
     
     * Fix id types
  *  AUTORUBACK-1575 (#892)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 20 Apr 2021 16:17:42 +0300

## yandex-vos2-autoru-consumers:0.128.8 (Fri, 16 Apr 2021 17:56:19 +0300)

  *  AUTORUBACK-418 (#889)
     
     * AUTORUBACK-418 fix logback.xml in docker
  *  Autoruback 1433 fixes (#885)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 changes+tests
     
     * AUTORUBACK-1433 changes+tests
     
     * AUTORUBACK-1433 more tests + fixes
     
     * AUTORUBACK-1433 panoramas routes adopted
     
     * AUTORUBACK-1433 panoramas routes adopted
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.
     
     * AUTORUBACK-1433 test fixes
     
     * AUTORUBACK-1433 fix consumer type
     
     * AUTORUBACK-1433 fix consumer type
     
     * AUTORUBACK-1433 check if consumer working
     
     * AUTORUBACK-1433 check if consumer working
  *  Autoruback 1433 fixes (#884)
     
     
     * AUTORUBACK-1433 check if consumer working
  *  AUTORUBACK-1433 fixes (#883)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     * AUTORUBACK-1433 fix consumer type
  *  AUTORUBACK-1433 changed panoramas scheduler to kafka consumer (#879)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.
  *  AUTORUBACK-1523 (#877)
     
     * AUTORUBACK-1523

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-1119_holocron_to_broker_2: fixed converters

  *  AUTORUBACK-1510 (#876)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1129: Update notifications topics (#874)
     

  *  Autoruback 1119 holocron to broker 2 (#872)
     
     * AUTORUBACK-1119_holocron_to_broker_2
     
     * AUTORUBACK-1119_holocron_to_broker_2: added more converters
     
     * AUTORUBACK-1119_holocron_to_broker_2: format
     
     * AUTORUBACK-1119_holocron_to_broker_2: fixed test
     
     * AUTORUBACK-1119_holocron_to_broker_2: added test
     
     * AUTORUBACK-1119_holocron_to_broker_2: fix
  *  Autoruback 1510 max photo count (#871)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1432 panoramas indexes in vos (#873)
     
     * AUTORUBACK-1432 panoramas indexes in vos
  *  AUTORUBACK-1483 (#869)
     
     * AUTORUBACK-1483
     
     * AUTORUBACK-1483
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 16 Apr 2021 17:56:19 +0300

## yandex-vos2-autoru-consumers:0.128.7 (Fri, 16 Apr 2021 13:18:35 +0300)

  *  Autoruback 1433 fixes (#885)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 changes+tests
     
     * AUTORUBACK-1433 changes+tests
     
     * AUTORUBACK-1433 more tests + fixes
     
     * AUTORUBACK-1433 panoramas routes adopted
     
     * AUTORUBACK-1433 panoramas routes adopted
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.
     
     * AUTORUBACK-1433 test fixes
     
     * AUTORUBACK-1433 fix consumer type
     
     * AUTORUBACK-1433 fix consumer type
     
     * AUTORUBACK-1433 check if consumer working
     
     * AUTORUBACK-1433 check if consumer working
  *  Autoruback 1433 fixes (#884)
     
     
     * AUTORUBACK-1433 check if consumer working
  *  AUTORUBACK-1433 fixes (#883)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     * AUTORUBACK-1433 fix consumer type
  *  AUTORUBACK-1433 changed panoramas scheduler to kafka consumer (#879)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.
  *  AUTORUBACK-1523 (#877)
     
     * AUTORUBACK-1523

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-1119_holocron_to_broker_2: fixed converters

  *  AUTORUBACK-1510 (#876)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1129: Update notifications topics (#874)
     

  *  Autoruback 1119 holocron to broker 2 (#872)
     
     * AUTORUBACK-1119_holocron_to_broker_2
     
     * AUTORUBACK-1119_holocron_to_broker_2: added more converters
     
     * AUTORUBACK-1119_holocron_to_broker_2: format
     
     * AUTORUBACK-1119_holocron_to_broker_2: fixed test
     
     * AUTORUBACK-1119_holocron_to_broker_2: added test
     
     * AUTORUBACK-1119_holocron_to_broker_2: fix
  *  Autoruback 1510 max photo count (#871)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1432 panoramas indexes in vos (#873)
     
     * AUTORUBACK-1432 panoramas indexes in vos
  *  AUTORUBACK-1483 (#869)
     
     * AUTORUBACK-1483
     
     * AUTORUBACK-1483
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 16 Apr 2021 13:18:35 +0300

## yandex-vos2-autoru-consumers:0.128.6 (Thu, 15 Apr 2021 20:06:00 +0300)

  *  Autoruback 1433 fixes (#885)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 changes+tests
     
     * AUTORUBACK-1433 changes+tests
     
     * AUTORUBACK-1433 more tests + fixes
     
     * AUTORUBACK-1433 panoramas routes adopted
     
     * AUTORUBACK-1433 panoramas routes adopted
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.
     
     * AUTORUBACK-1433 test fixes
     
     * AUTORUBACK-1433 fix consumer type
     
     * AUTORUBACK-1433 fix consumer type
     
     * AUTORUBACK-1433 check if consumer working
     
     * AUTORUBACK-1433 check if consumer working
  *  Autoruback 1433 fixes (#884)
     
     
     * AUTORUBACK-1433 check if consumer working
  *  AUTORUBACK-1433 fixes (#883)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     * AUTORUBACK-1433 fix consumer type
  *  AUTORUBACK-1433 changed panoramas scheduler to kafka consumer (#879)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.
  *  AUTORUBACK-1523 (#877)
     
     * AUTORUBACK-1523

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-1119_holocron_to_broker_2: fixed converters

  *  AUTORUBACK-1510 (#876)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1129: Update notifications topics (#874)
     

  *  Autoruback 1119 holocron to broker 2 (#872)
     
     * AUTORUBACK-1119_holocron_to_broker_2
     
     * AUTORUBACK-1119_holocron_to_broker_2: added more converters
     
     * AUTORUBACK-1119_holocron_to_broker_2: format
     
     * AUTORUBACK-1119_holocron_to_broker_2: fixed test
     
     * AUTORUBACK-1119_holocron_to_broker_2: added test
     
     * AUTORUBACK-1119_holocron_to_broker_2: fix
  *  Autoruback 1510 max photo count (#871)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1432 panoramas indexes in vos (#873)
     
     * AUTORUBACK-1432 panoramas indexes in vos
  *  AUTORUBACK-1483 (#869)
     
     * AUTORUBACK-1483
     
     * AUTORUBACK-1483
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 15 Apr 2021 20:06:00 +0300

## yandex-vos2-autoru-consumers:0.128.5 (Thu, 15 Apr 2021 19:50:58 +0300)

  *  Autoruback 1433 fixes (#885)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 changes+tests
     
     * AUTORUBACK-1433 changes+tests
     
     * AUTORUBACK-1433 more tests + fixes
     
     * AUTORUBACK-1433 panoramas routes adopted
     
     * AUTORUBACK-1433 panoramas routes adopted
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.
     
     * AUTORUBACK-1433 test fixes
     
     * AUTORUBACK-1433 fix consumer type
     
     * AUTORUBACK-1433 fix consumer type
     
     * AUTORUBACK-1433 check if consumer working
     
     * AUTORUBACK-1433 check if consumer working
  *  Autoruback 1433 fixes (#884)
     
     
     * AUTORUBACK-1433 check if consumer working
  *  AUTORUBACK-1433 fixes (#883)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     * AUTORUBACK-1433 fix consumer type
  *  AUTORUBACK-1433 changed panoramas scheduler to kafka consumer (#879)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.
  *  AUTORUBACK-1523 (#877)
     
     * AUTORUBACK-1523

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-1119_holocron_to_broker_2: fixed converters

  *  AUTORUBACK-1510 (#876)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1129: Update notifications topics (#874)
     

  *  Autoruback 1119 holocron to broker 2 (#872)
     
     * AUTORUBACK-1119_holocron_to_broker_2
     
     * AUTORUBACK-1119_holocron_to_broker_2: added more converters
     
     * AUTORUBACK-1119_holocron_to_broker_2: format
     
     * AUTORUBACK-1119_holocron_to_broker_2: fixed test
     
     * AUTORUBACK-1119_holocron_to_broker_2: added test
     
     * AUTORUBACK-1119_holocron_to_broker_2: fix
  *  Autoruback 1510 max photo count (#871)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1432 panoramas indexes in vos (#873)
     
     * AUTORUBACK-1432 panoramas indexes in vos
  *  AUTORUBACK-1483 (#869)
     
     * AUTORUBACK-1483
     
     * AUTORUBACK-1483
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 15 Apr 2021 19:50:58 +0300

## yandex-vos2-autoru-consumers:0.128.4 (Thu, 15 Apr 2021 18:45:11 +0300)

  *  AUTORUBACK-1433 fixes (#883)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     * AUTORUBACK-1433 fix consumer type
  *  AUTORUBACK-1433 changed panoramas scheduler to kafka consumer (#879)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.
  *  AUTORUBACK-1523 (#877)
     
     * AUTORUBACK-1523

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-1119_holocron_to_broker_2: fixed converters

  *  AUTORUBACK-1510 (#876)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1129: Update notifications topics (#874)
     

  *  Autoruback 1119 holocron to broker 2 (#872)
     
     * AUTORUBACK-1119_holocron_to_broker_2
     
     * AUTORUBACK-1119_holocron_to_broker_2: added more converters
     
     * AUTORUBACK-1119_holocron_to_broker_2: format
     
     * AUTORUBACK-1119_holocron_to_broker_2: fixed test
     
     * AUTORUBACK-1119_holocron_to_broker_2: added test
     
     * AUTORUBACK-1119_holocron_to_broker_2: fix
  *  Autoruback 1510 max photo count (#871)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1432 panoramas indexes in vos (#873)
     
     * AUTORUBACK-1432 panoramas indexes in vos
  *  AUTORUBACK-1483 (#869)
     
     * AUTORUBACK-1483
     
     * AUTORUBACK-1483
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 15 Apr 2021 18:45:11 +0300

## yandex-vos2-autoru-consumers:0.128.3 (Thu, 15 Apr 2021 17:01:56 +0300)

  *  AUTORUBACK-1433 changed panoramas scheduler to kafka consumer (#879)
     
     * AUTORUBACK-1433 changed panoramas scheduler to kafka consumer
     
     * AUTORUBACK-1433 added pauses to OffersReaderTest to give some time to database shards for sharing info between them. It was falling too frequently.
  *  AUTORUBACK-1523 (#877)
     
     * AUTORUBACK-1523

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-1119_holocron_to_broker_2: fixed converters

  *  AUTORUBACK-1510 (#876)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1129: Update notifications topics (#874)
     

  *  Autoruback 1119 holocron to broker 2 (#872)
     
     * AUTORUBACK-1119_holocron_to_broker_2
     
     * AUTORUBACK-1119_holocron_to_broker_2: added more converters
     
     * AUTORUBACK-1119_holocron_to_broker_2: format
     
     * AUTORUBACK-1119_holocron_to_broker_2: fixed test
     
     * AUTORUBACK-1119_holocron_to_broker_2: added test
     
     * AUTORUBACK-1119_holocron_to_broker_2: fix
  *  Autoruback 1510 max photo count (#871)
     
     * AUTORUBACK-1510
  *  AUTORUBACK-1432 panoramas indexes in vos (#873)
     
     * AUTORUBACK-1432 panoramas indexes in vos
  *  AUTORUBACK-1483 (#869)
     
     * AUTORUBACK-1483
     
     * AUTORUBACK-1483
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 15 Apr 2021 17:01:56 +0300

## yandex-vos2-autoru-consumers:0.128.2 (Tue, 06 Apr 2021 20:08:23 +0300)

  *  AUTORUBACK-1432 panoramas indexes in vos (#873)
     
     * AUTORUBACK-1432 panoramas indexes in vos
  *  AUTORUBACK-1483 (#869)
     
     * AUTORUBACK-1483
     
     * AUTORUBACK-1483
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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 06 Apr 2021 20:08:23 +0300

## yandex-vos2-autoru-consumers:0.128.1 (Thu, 01 Apr 2021 16:24:47 +0300)

  *  AUTORUBACK-1071

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 01 Apr 2021 16:24:47 +0300

## yandex-vos2-autoru-consumers:0.128.0 (Thu, 01 Apr 2021 16:00:22 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 01 Apr 2021 16:00:22 +0300

## yandex-vos2-autoru-consumers:0.127.1 (Thu, 25 Mar 2021 14:42:08 +0300)

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
     

  *  Autoruback 1268 spam premium users (#849)
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/WorkersSupport.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * minor changes
     
     * http license plate blur int test
     
     * zk test datasources update
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * release 0.17.0
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071 fix-path
     
     * AUTORUBACK-1071 update scoring worker
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * some comments
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * del
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  Autoruback 1071 ydb scheduller workers (#818)
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/OfferRow.scala
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/WorkersSupport.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * minor changes
     
     * http license plate blur int test
     
     * zk test datasources update
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * release 0.17.0
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071 fix-path
     
     * AUTORUBACK-1071 update scoring worker
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * some comments
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * del
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-1259-premium-users-fix (#847)
     
     * AUTORUBACK-1259-premium-users-fix
     
     * AUTORUBACK-1259-premium-users-fix
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 25 Mar 2021 14:42:08 +0300

## yandex-vos2-autoru-consumers:0.127.0 (Wed, 24 Mar 2021 12:59:35 +0300)

  *  AUTORUBACK-1424_no_new_fields_in_searcher (#857)
     

  *  AUTORUBACK-1225-moderationUpdate-fix (#856)
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
  *  AUTORUBACK-277: Get salon from verba (#853)
     

  *  Autoruback 1268 spam premium users (#849)
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/WorkersSupport.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * minor changes
     
     * http license plate blur int test
     
     * zk test datasources update
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * release 0.17.0
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071 fix-path
     
     * AUTORUBACK-1071 update scoring worker
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * some comments
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * del
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1268
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  Autoruback 1071 ydb scheduller workers (#818)
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/OfferRow.scala
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/WorkersSupport.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * minor changes
     
     * http license plate blur int test
     
     * zk test datasources update
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * release 0.17.0
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071 fix-path
     
     * AUTORUBACK-1071 update scoring worker
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * some comments
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * del
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1268
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  AUTORUBACK-1259-premium-users-fix (#847)
     
     * AUTORUBACK-1259-premium-users-fix
     
     * AUTORUBACK-1259-premium-users-fix
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 24 Mar 2021 12:59:35 +0300

## yandex-vos2-autoru-consumers:0.126.0 (Fri, 19 Mar 2021 11:01:29 +0300)

  *  AUTORUBACK-1144_vos_support_for_hires (#850)
     

  *  AUTORUBACK-1426_mod_auto_protect (#846)
     

  *  AUTORUBACK-1104 2 fix promocode sender stage (#845)
     
     * AUTORUBACK-1104 tests and small adjustments/ not sent email
     * AUTORUBACK-1296 fixed promocode length(21-22 for now)

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 19 Mar 2021 11:01:29 +0300

## yandex-vos2-autoru-consumers:0.125.0 (Mon, 15 Mar 2021 15:56:53 +0300)

  *  VSDEALERS-729  # revert (#844)
     
     * Revert "VSDEALERS-729 # Fix feature name (#841)"
     
     This reverts commit 474f9df63c07064e07c30ee9b8ff37aebabcdd7c.
     
     * Revert "VSDEALERS-729 # Use findSameOfferInVos instead of matchOfferByVitalFields (#837)"
     
     This reverts commit 1975a4197bb005295d5c992dc2094bdbb2c98c90.
  *  AUTORUBACK-1416 (#843)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 15 Mar 2021 15:56:53 +0300

## yandex-vos2-autoru-consumers:0.124.2 (Thu, 11 Mar 2021 16:38:08 +0300)

  *  VSDEALERS-729 # Fix feature name (#841)
     

  *  VSDEALERS-729 # Use findSameOfferInVos instead of matchOfferByVitalFields (#837)
     
     * VSDEALERS-729 # Use findSameOfferInVos instead of matchOfferByVitalFields
     
     * VSDEALERS-729 # Feature protection
  *  AUTORUBACK-1210_offer_position_cr_date (#839)
     

  *  AUTORUBACK-1331_same_section (#833)
     
     * AUTORUBACK-1331_same_section
     
     * AUTORUBACK-1331_same_section: compilation fix
     
     * AUTORUBACK-1331_same_section: compilation fix
     
     * AUTORUBACK-1331_same_section: added test
  *  AUTORUBACK-1225 (#836)
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
  *  AUTORUBACK-1259-clear-palma-premium (#832)
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
  *  CARFAX-1190 Новый роут для ручки /admin/any/reload (#829)
     
     CARFAX-1190 Новый роут для ручки /admin/any/reload
  *  VSDEALERS-766 Generate redirect for CHE and SVE salons (#827)
     

  *  AUTORUBACK-1331_old_db_status_fix (#830)
     
     * AUTORUBACK-1331_old_db_status_fix
     
     * AUTORUBACK-1331_old_db_status_fix: added test, fixed fix
     
     * AUTORUBACK-1331_old_db_status_fix: updated test, minor fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 11 Mar 2021 16:38:08 +0300

## yandex-vos2-autoru-consumers:0.124.1 (Thu, 11 Mar 2021 15:57:57 +0300)

  *  VSDEALERS-729 # Use findSameOfferInVos instead of matchOfferByVitalFields (#837)
     
     * VSDEALERS-729 # Use findSameOfferInVos instead of matchOfferByVitalFields
     
     * VSDEALERS-729 # Feature protection
  *  AUTORUBACK-1210_offer_position_cr_date (#839)
     

  *  AUTORUBACK-1331_same_section (#833)
     
     * AUTORUBACK-1331_same_section
     
     * AUTORUBACK-1331_same_section: compilation fix
     
     * AUTORUBACK-1331_same_section: compilation fix
     
     * AUTORUBACK-1331_same_section: added test
  *  AUTORUBACK-1225 (#836)
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
  *  AUTORUBACK-1259-clear-palma-premium (#832)
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
  *  CARFAX-1190 Новый роут для ручки /admin/any/reload (#829)
     
     CARFAX-1190 Новый роут для ручки /admin/any/reload
  *  VSDEALERS-766 Generate redirect for CHE and SVE salons (#827)
     

  *  AUTORUBACK-1331_old_db_status_fix (#830)
     
     * AUTORUBACK-1331_old_db_status_fix
     
     * AUTORUBACK-1331_old_db_status_fix: added test, fixed fix
     
     * AUTORUBACK-1331_old_db_status_fix: updated test, minor fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 11 Mar 2021 15:57:57 +0300

## yandex-vos2-autoru-consumers:0.124.0 (Thu, 11 Mar 2021 11:28:24 +0300)

  *  AUTORUBACK-1331_same_section (#833)
     
     * AUTORUBACK-1331_same_section
     
     * AUTORUBACK-1331_same_section: compilation fix
     
     * AUTORUBACK-1331_same_section: compilation fix
     
     * AUTORUBACK-1331_same_section: added test
  *  AUTORUBACK-1225 (#836)
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
  *  AUTORUBACK-1259-clear-palma-premium (#832)
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
  *  CARFAX-1190 Новый роут для ручки /admin/any/reload (#829)
     
     CARFAX-1190 Новый роут для ручки /admin/any/reload
  *  VSDEALERS-766 Generate redirect for CHE and SVE salons (#827)
     

  *  AUTORUBACK-1331_old_db_status_fix (#830)
     
     * AUTORUBACK-1331_old_db_status_fix
     
     * AUTORUBACK-1331_old_db_status_fix: added test, fixed fix
     
     * AUTORUBACK-1331_old_db_status_fix: updated test, minor fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 11 Mar 2021 11:28:24 +0300

## yandex-vos2-autoru-consumers:0.123.2 (Wed, 03 Mar 2021 17:39:31 +0300)

  *  CARFAX-1521: Send full old offer to calculate any diff (#828)
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>
  *  AUTORUBACK-1259 (#811)
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
     
     * AUTORUBACK-1259
  *  AUTORUBACK-1331_insert_or_update_form (#824)
     
     * AUTORUBACK-1331_insert_or_update_form
     
     * AUTORUBACK-1331_insert_or_update_form: format
     
     * AUTORUBACK-1331_insert_or_update_form: compilation fix
     
     * AUTORUBACK-1331_insert_or_update_form: added test, fixed after test addition
     
     * AUTORUBACK-1331_insert_or_update_form: fixed swagger
     
     * AUTORUBACK-1331_insert_or_update_form: removed unused method and tests for it
     
     * AUTORUBACK-1331_insert_or_update_form: minor test form generation fix
  *  AUTORUBACK-1351 (#825)
     

  *  Autoruback 1351 public transparency (#823)
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
     
     * AUTORUBACK-1351
  *  AUTORUBACK-1326 (#821)
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
  *  AUTORUBACK-1297 basic metrics (#817)
     
     * AUTORUBACK-1297 basic monitoring
  *  AUTORUBACK-1326 (#819)
     

  *  Autoruback 1071 ydb scheduller (#770)
     
     * AUTORUBACK-1069 ydb
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/OfferRow.scala
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * autoruback-1071
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/WorkersSupport.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * Update vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/WorkersOffersProcessor.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * minor changes
     
     * http license plate blur int test
     
     * zk test datasources update
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/ydb_schema_base.sql
     #	vos2-autoru-ydb-workers/src/main/scala/ru/yandex/vertis/vos2/autoru/workers/ydb/components/workers/mysql_ydb/MySqlYdbSynchronizer.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * release 0.17.0
     
     * Merge branch 'master' into AUTORUBACK-1071-ydb-scheduller
     
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStage.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorker.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ScoringStageTest.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/workers/ScoringWorkerTest.scala>
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071 fix-path
     
     * AUTORUBACK-1071 update scoring worker
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     * AUTORUBACK-1071
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     Co-authored-by: Andrey Borunov <aborunov@yandex-team.ru>
     Co-authored-by: robot-vertis-repo <robot-vertis-repo@yandex-team.ru>
  *  Autoruback 1332 transparency fix (#815)
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1332
     
     * Update ScoringWorker.scala
  *  AUTORUBACK-1104 feature 4 panorama promocodes (#813)
     
     * AUTORUBACK-1104
     
     * AUTORUBACK-1294 new panorama feature
     
     * AUTORUBACK-1295 generate_promocode
     
     * AUTORUBACK-1296 send promocode
  *  AUTORUBACK-1326 (#812)
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
  *  AUTORUBACK-1248-status-moderation-fix (#810)
     

  *  AUTORUBACK-1248 (#809)
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/converters/offerform/OfferFormConverter.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-1248
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-1225 notification fix (#808)
     
     * AUTORUBACK-1225 notification fix
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
  *  AUTORUBACK-1129: Update topics (#802)
     

  *  AUTORUBACK-1248 (#806)
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
  *  AUTORUBACK-1273 split databases (#807)
     
     * AUTORUBACK-1273 split databases
     
     * AUTORUBACK-1273 fix db logins issues
  *  AUTORUBACK-702 (#805)
     
     * AUTORUBACK-702
     
     * AUTORUBACK-702
     
     * AUTORUBACK-702
  *  VSDEALERS-694 # Activate multiposting offers in non-cars categories (#804)
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
  *  AUTORUBACK-1267 error naming (#801)
     
     * AUTORUBACK-1267 error naming
     
     * AUTORUBACK-1267 error naming
  *  AUTORUBACK-1129: Add spamalot pushes (#786)
     

  *  AUTORUBACK-308_can_view_2 (#795)
     
     * AUTORUBACK-308_can_view_2
     
     * fixed tests
     
     * fixed tests
  *  autoruback-1214 (#794)
     
     * autoruback-1214
     
     * autoruback-1214
     
     * autoruback-1214
  *  Revert "AUTORUBACK-308_can_view: fix"
     
     This reverts commit 3de8004e

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-308_can_view: fix

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 03 Mar 2021 17:39:31 +0300

## yandex-vos2-autoru-consumers:0.123.1 (Wed, 17 Feb 2021 18:48:08 +0300)

  *  Autoruback 1332 transparency fix (#815)
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1332
     
     * AUTORUBACK-1332
     
     * Update ScoringWorker.scala
  *  AUTORUBACK-1104 feature 4 panorama promocodes (#813)
     
     * AUTORUBACK-1104
     
     * AUTORUBACK-1294 new panorama feature
     
     * AUTORUBACK-1295 generate_promocode
     
     * AUTORUBACK-1296 send promocode
  *  AUTORUBACK-1326 (#812)
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
     
     * AUTORUBACK-1326
  *  AUTORUBACK-1248-status-moderation-fix (#810)
     

  *  AUTORUBACK-1248 (#809)
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/converters/offerform/OfferFormConverter.scala
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
     
     * AUTORUBACK-1248
     
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  AUTORUBACK-1225 notification fix (#808)
     
     * AUTORUBACK-1225 notification fix
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
     
     * AUTORUBACK-1225
  *  AUTORUBACK-1129: Update topics (#802)
     

  *  AUTORUBACK-1248 (#806)
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
     
     * AUTORUBACK-1248
  *  AUTORUBACK-1273 split databases (#807)
     
     * AUTORUBACK-1273 split databases
     
     * AUTORUBACK-1273 fix db logins issues
  *  AUTORUBACK-702 (#805)
     
     * AUTORUBACK-702
     
     * AUTORUBACK-702
     
     * AUTORUBACK-702
  *  VSDEALERS-694 # Activate multiposting offers in non-cars categories (#804)
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
  *  AUTORUBACK-1267 error naming (#801)
     
     * AUTORUBACK-1267 error naming
     
     * AUTORUBACK-1267 error naming
  *  AUTORUBACK-1129: Add spamalot pushes (#786)
     

  *  AUTORUBACK-308_can_view_2 (#795)
     
     * AUTORUBACK-308_can_view_2
     
     * fixed tests
     
     * fixed tests
  *  autoruback-1214 (#794)
     
     * autoruback-1214
     
     * autoruback-1214
     
     * autoruback-1214
  *  Revert "AUTORUBACK-308_can_view: fix"
     
     This reverts commit 3de8004e

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-308_can_view: fix

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 17 Feb 2021 18:48:08 +0300

## yandex-vos2-autoru-consumers:0.123.0 (Fri, 05 Feb 2021 15:44:48 +0300)

  *  AUTORUBACK-1273 split databases (#807)
     
     * AUTORUBACK-1273 split databases
     
     * AUTORUBACK-1273 fix db logins issues
  *  AUTORUBACK-702 (#805)
     
     * AUTORUBACK-702
     
     * AUTORUBACK-702
     
     * AUTORUBACK-702
  *  VSDEALERS-694 # Activate multiposting offers in non-cars categories (#804)
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
     
     * VSDEALERS-694 # Activate multiposting offers in non-cars categories
  *  AUTORUBACK-1267 error naming (#801)
     
     * AUTORUBACK-1267 error naming
     
     * AUTORUBACK-1267 error naming
  *  AUTORUBACK-1129: Add spamalot pushes (#786)
     

  *  AUTORUBACK-308_can_view_2 (#795)
     
     * AUTORUBACK-308_can_view_2
     
     * fixed tests
     
     * fixed tests
  *  autoruback-1214 (#794)
     
     * autoruback-1214
     
     * autoruback-1214
     
     * autoruback-1214
  *  Revert "AUTORUBACK-308_can_view: fix"
     
     This reverts commit 3de8004e

  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUBACK-308_can_view: fix

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 05 Feb 2021 15:44:48 +0300

## yandex-vos2-autoru-consumers:0.122.0 (Tue, 12 Jan 2021 17:34:14 +0300)

  *  VSDEALERS-600 pledge_number support (#784)
     

  *  VSDEALERS-599 pledge_number (#782)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 12 Jan 2021 17:34:14 +0300

## yandex-vos2-autoru-consumers:0.121.0 (Mon, 11 Jan 2021 19:08:44 +0300)

  *  VSDEALERS-588 # Add logs (#781)
     
     Co-authored-by: datichto <31860203+datichto@users.noreply.github.com>
  *  test fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 11 Jan 2021 19:08:44 +0300

## yandex-vos2-autoru-consumers:0.120.1 (Mon, 11 Jan 2021 13:05:48 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 11 Jan 2021 13:05:48 +0300

## yandex-vos2-autoru-consumers:0.120.0 (Wed, 30 Dec 2020 17:19:34 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 30 Dec 2020 17:19:34 +0300

## yandex-vos2-autoru-consumers:0.119.0 (Wed, 23 Dec 2020 12:56:59 +0300)

  *  VSDEALERS-566 # FormOfferConverter extended logging (#768)
     

  *  Autoruback 1069 ydb fix (#764)
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
     
     * AUTORUBACK-1069 ydb
  *  AUTORUBACK-1069 ydb (#763)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 23 Dec 2020 12:56:59 +0300

## yandex-vos2-autoru-consumers:0.118.5 (Mon, 21 Dec 2020 14:38:31 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 21 Dec 2020 14:38:31 +0300

## yandex-vos2-autoru-consumers:0.118.4 (Sun, 20 Dec 2020 14:19:04 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 20 Dec 2020 14:19:04 +0300

## yandex-vos2-autoru-consumers:0.118.3 (Thu, 17 Dec 2020 19:55:51 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Dec 2020 19:55:51 +0300

## yandex-vos2-autoru-consumers:0.118.2 (Thu, 17 Dec 2020 18:09:31 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Dec 2020 18:09:31 +0300

## yandex-vos2-autoru-consumers:0.118.1 (Thu, 17 Dec 2020 15:43:44 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 17 Dec 2020 15:43:44 +0300

## yandex-vos2-autoru-consumers:0.118.0 (Tue, 15 Dec 2020 19:11:27 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 15 Dec 2020 19:11:27 +0300

## yandex-vos2-autoru-consumers:0.117.2 (Mon, 14 Dec 2020 12:29:44 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 14 Dec 2020 12:29:44 +0300

## yandex-vos2-autoru-consumers:0.117.1 (Fri, 11 Dec 2020 21:39:50 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 11 Dec 2020 21:39:50 +0300

## yandex-vos2-autoru-consumers:0.117.0 (Fri, 11 Dec 2020 16:37:25 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 11 Dec 2020 16:37:25 +0300

## yandex-vos2-autoru-consumers:0.116.1 (Wed, 09 Dec 2020 20:21:55 +0300)

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
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 09 Dec 2020 20:21:55 +0300

## yandex-vos2-autoru-consumers:0.116.0 (Tue, 08 Dec 2020 15:36:20 +0300)

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
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 08 Dec 2020 15:36:20 +0300

## yandex-vos2-autoru-consumers:0.115.0 (Mon, 30 Nov 2020 19:33:27 +0300)

  *  VSDEALERS-479 # MaxUpdateBatchSize: 500 -> 300 for `Packet for query is too large` error (#734)
     
     * VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 600 -> 500 for `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 500 -> 300 for `Packet for query is too large` error

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 30 Nov 2020 19:33:27 +0300

## yandex-vos2-autoru-consumers:0.114.0 (Mon, 30 Nov 2020 18:20:49 +0300)

  *  VSDEALERS-479 # MaxUpdateBatchSize: 600 -> 500 for `Packet for query is too large` error (#733)
     
     * VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 600 -> 500 for `Packet for query is too large` error

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 30 Nov 2020 18:20:49 +0300

## yandex-vos2-autoru-consumers:0.113.0 (Mon, 30 Nov 2020 17:33:19 +0300)

  *  VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error (#732)
     
     * VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error
     
     * VSDEALERS-479 # MaxUpdateBatchSize: 1000 -> 500 for `Packet for query is too large` error

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 30 Nov 2020 17:33:19 +0300

## yandex-vos2-autoru-consumers:0.112.0 (Mon, 30 Nov 2020 15:42:42 +0300)

  *  VSDEALERS-479 # Batch update: FIX `Packet for query is too large` error (#731)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 30 Nov 2020 15:42:42 +0300

## yandex-vos2-autoru-consumers:0.111.0 (Thu, 26 Nov 2020 21:24:49 +0300)

  *  VS-467 Отправляем score в Cёрчер (#730)
     
     * VS-467 send score to searcher
     
     * micro-core 0.13.63
     
     * rf
  *  VSDEALERS-455 # update multiposting models (#726)
     

  *  Fix formatting issue (#727)
     

  *  AUTORUBACK-1020 process_emergency_queue feature

  *  VSDEALERS-423 # Deduplicate Avito services (#725)
     
     * VSDEALERS-423 # Deduplicate Avito services
  *  AUTORUBACK-496: Replace cars_catalog with cars_palma_catalog (#719)
     

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
  *  AUTORUBACK-1000 fixed holocron optLastDeactivateMoment calculation when no active events exist

  *  temporary test fix

  *  skypper: 11

  *  AUTORUBACK-879 interior panoramas routes for moderation (#715)
     
     * AUTORUBACK-879 interior panoramas routes for moderation +  fix status change
  *  AUTORUBACK-875 send images meta to broker (#716)
     
     * AUTORUBACK-875 send images meta to broker
     
     * review fixes
  *  AUTORUBACK-959: Не писать логи в файлы (#713)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 26 Nov 2020 21:24:49 +0300

## yandex-vos2-autoru-consumers:0.110.0 (Mon, 16 Nov 2020 18:21:58 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 16 Nov 2020 18:21:58 +0300

## yandex-vos2-autoru-consumers:0.109.0 (Thu, 12 Nov 2020 13:33:14 +0300)

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
  *  Autoruback 911 fix containers (#696)
     
     * fixed version after merge
     
     * fixed version after merge
     
     * fixed javax xml bind
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
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 12 Nov 2020 13:33:14 +0300

## yandex-vos2-autoru-consumers:0.108.2 (Thu, 29 Oct 2020 21:21:21 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 29 Oct 2020 21:21:21 +0300

## yandex-vos2-autoru-consumers:0.108.1 (Thu, 29 Oct 2020 19:14:05 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 29 Oct 2020 19:14:05 +0300

## yandex-vos2-autoru-consumers:0.108.0 (Thu, 29 Oct 2020 18:05:07 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 29 Oct 2020 18:05:07 +0300

## yandex-vos2-autoru-consumers:0.107.0 (Mon, 05 Oct 2020 16:47:29 +0300)

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

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 05 Oct 2020 16:47:29 +0300

## yandex-vos2-autoru-consumers:0.106.0 (Wed, 16 Sep 2020 13:42:50 +0300)

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
     

  *  #AUTORUBACK-772 Booking state validation fix (#631)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 16 Sep 2020 13:42:50 +0300

## yandex-vos2-autoru-consumers:0.105.0 (Thu, 03 Sep 2020 01:57:13 +0300)

  *  AUTORUBACK-126_ydb_blobs: timestampAnyUpdate update fix

  *  AUTORUBACK-126_ydb_blobs: update timestamp_any_update in offer for timestamp_check changes too

  *  AUTORUBACK-749: Don't blur photos without license number (#627)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 03 Sep 2020 01:57:13 +0300

## yandex-vos2-autoru-consumers:0.104.0 (Tue, 25 Aug 2020 19:32:15 +0300)

  *  AUTORUBACK-747: fixed username save to old db

  *  AUTORUBACK-126_ydb_blobs: fixes

  *  AUTORUBACK-126 ydb blobs (#535)
     
     * AUTORUBACK-126 ydb blobs: started
     
     * AUTORUBACK-126_ydb_blobs: new module - ydb workers, started
     
     * AUTORUBACK-126_ydb_blobs: ydb usert test
     
     * AUTORUBACK-126_ydb_blobs: ydb usert test continue
     
     * AUTORUBACK-126_ydb_blobs: MySqlYdbSynchronizer, not finished. added features and workers
     
     * AUTORUBACK-126_ydb_blobs: MySqlYdbSynchronizer continue, updatedAndGet in CachedZkNode
     
     * AUTORUBACK-126_ydb_blobs: MySqlYdbSynchronizer continue, features refactoring, zookeeper refactoring
     
     * AUTORUBACK-126_ydb_blobs: fixes and refactoring
     
     * AUTORUBACK-126_ydb_blobs: deploy scripts, ydb logging finished, minor changes
     
     * AUTORUBACK-126_ydb_blobs: updated ydb settings
     
     * AUTORUBACK-126_ydb_blobs: style
     
     * AUTORUBACK-126_ydb_blobs: fixed ydb props
     
     * AUTORUBACK-126_ydb_blobs: monitor refactoring, ydb common pool, worker monitoring, two workers for both shards
     
     * AUTORUBACK-126_ydb_blobs: added ydb pool settings to properties.conf, fixed ydb wrapper init, updated logging, ydb metrics, refactoring
     
     * skypper version up
  *  AUTORUBACK-612 interior panorama to searcher (#623)
     
     * AUTORUBACK-612 interior panorama to searcher

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 25 Aug 2020 19:32:15 +0300

## yandex-vos2-autoru-consumers:0.103.0 (Thu, 20 Aug 2020 14:02:14 +0300)

  *  AUTORUBACK-595: Return ResetShouldStayActiveStage (#622)
     

  *  AUTORUBACK-707_can_archive_ban_reasons (#621)
     

  *  AUTORUBACK-721: Handle empty list (#620)
     

  *  AUTORUBACK-721: Update error handling (#619)
     
     * AUTORUBACK-721: Update error handling
  *  AUTORUBACK-663 Add market price to offer (#613)
     

  *  AUTORUBACK-612 (#616)
     
     * AUTORUBACK-612 fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 20 Aug 2020 14:02:14 +0300

## yandex-vos2-autoru-consumers:0.102.1 (Fri, 14 Aug 2020 19:51:01 +0300)

  *  AUTORUBACK-612 interior panoramas (#614)
     
     * AUTORUBACK-612 interior panoramas
  *  AUTORUBACK-651_tech_support_notify_for_dealers_fix (#612)
     
     * AUTORUBACK-651_tech_support_notify_for_dealers_fix
     
     * AUTORUBACK-651_tech_support_notify_for_dealers_fix: updated tests
  *  AUTORUBACK-661_can_activate_without_phones (#611)
     
     * AUTORUBACK-661_can_activate_without_phones
     
     * AUTORUBACK-661_can_activate_without_phones
  *  AUTORUBACK-668: New computer vision api (#610)
     
     * AUTORUBACK-668: New computer vision api
     
     * AUTORUBACK-668: Fix HttpLicensePlateBlur test and remove unnecessary fields from model
     
     * AUTORUBACK-668: Fix imageMagic tests
     
     * AUTORUBACK-668: Fix imageMagic tests
     
     * AUTORUBACK-668: Fixes via comments pr#610
     
     * AUTORUBACK-668: Fix http integration with api
     
     * AUTORUBACK-668: Drop unused property
     
     * AUTORUBACK-668: api url v2 config
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  minor refactoring

  *  AUTORUBACK-595: updated stage to fix offers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 14 Aug 2020 19:51:01 +0300

## yandex-vos2-autoru-consumers:0.102.0 (Mon, 10 Aug 2020 15:42:45 +0300)

  *  AUTORUBACK-668: New computer vision api (#610)
     
     * AUTORUBACK-668: New computer vision api
     
     * AUTORUBACK-668: Fix HttpLicensePlateBlur test and remove unnecessary fields from model
     
     * AUTORUBACK-668: Fix imageMagic tests
     
     * AUTORUBACK-668: Fix imageMagic tests
     
     * AUTORUBACK-668: Fixes via comments pr#610
     
     * AUTORUBACK-668: Fix http integration with api
     
     * AUTORUBACK-668: Drop unused property
     
     * AUTORUBACK-668: api url v2 config
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>
     Co-authored-by: aborunov <31614119+aborunov@users.noreply.github.com>
  *  minor refactoring

  *  AUTORUBACK-595: updated stage to fix offers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 10 Aug 2020 15:42:45 +0300

## yandex-vos2-autoru-consumers:0.101.0 (Sat, 08 Aug 2020 11:48:10 +0300)



 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 08 Aug 2020 11:48:10 +0300

## yandex-vos2-autoru-consumers:0.100.1 (Thu, 06 Aug 2020 13:34:22 +0300)

  *  AUTORUBACK-595: Clear should_stay_active (#608)
     
     * AUTORUBACK-595: Clear should_stay_active
  *  AUTORUBACK-633 Add maxDiscount to moto offer (#607)
     

  *  AUTORUBACK-595: Handle should_stay_active (#604)
     
     * AUTORUBACK-595: Handle should_stay_active
  *  AUTORUBACK-620: Allow moderators to change offers purchase_date (#605)
     
     * AUTORUBACK-620: Allow moderators to change offers purchase_date
     
     * AUTORUBACK-620: Update schema-registry to release version
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>
  *  AUTORUBACK-541: New promo low rating offer push messages (#603)
     
     * AUTORUBACK-541: New promo low rating offer push messages
     
     * AUTORUBACK-541: Fix push message test
     
     * AUTORUBACK-541: Reformat code
     
     * AUTORUBACK-541: Fix LowRatingRenderTest
     
     * AUTORUBACK-541: Fix LowRatingEventTest
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 06 Aug 2020 13:34:22 +0300

## yandex-vos2-autoru-consumers:0.100.0 (Mon, 03 Aug 2020 18:49:39 +0300)

  *  AUTORUBACK-633 Add maxDiscount to moto offer (#607)
     

  *  AUTORUBACK-595: Handle should_stay_active (#604)
     
     * AUTORUBACK-595: Handle should_stay_active
  *  AUTORUBACK-620: Allow moderators to change offers purchase_date (#605)
     
     * AUTORUBACK-620: Allow moderators to change offers purchase_date
     
     * AUTORUBACK-620: Update schema-registry to release version
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>
  *  AUTORUBACK-541: New promo low rating offer push messages (#603)
     
     * AUTORUBACK-541: New promo low rating offer push messages
     
     * AUTORUBACK-541: Fix push message test
     
     * AUTORUBACK-541: Reformat code
     
     * AUTORUBACK-541: Fix LowRatingRenderTest
     
     * AUTORUBACK-541: Fix LowRatingEventTest
     
     Co-authored-by: Oleg Degtev <degtev-o@yandex-team.ru>

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 03 Aug 2020 18:49:39 +0300

## yandex-vos2-autoru-consumers:0.99.0 (Fri, 24 Jul 2020 12:58:22 +0300)

  *  добавлен новый размер в неймспейс autoru-vos (#602)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 24 Jul 2020 12:58:22 +0300

## yandex-vos2-autoru-consumers:0.98.2 (Fri, 17 Jul 2020 20:10:26 +0300)

  *  AUTORUBACK-547 обработка новых вердиктов модерации (#600)
     

  *  AUTORUBACK-350 удалить проверку по марке+модели (#599)
     
     * удалить проверку по марке+модели
     
     * добавить vin в тестовые данные
  *  AUTORUBACK-534 обработка флага should_stay_active для USER_RESELLER (#598)
     
     * обрабатывать флаг should_stay_active
  *  AUTORUBACK-578: Clear proven_owner_moderation (#597)
     
     * AUTORUBACK-578: Clear proven_owner_moderation
  *  AUTORUBACK-526 добавлено поле в FullCarOffer (#596)
     

  *  AUTORUBACK-533 добавлена поддержка chatOnly в защиту модерации (#595)
     
     * добавлена поддержка chatOnly в защиту модерации
     
     * форматирование
  *  AUTORUBACK-350 использовать VIN для определения похожего оффера (#594)
     
     * AUTORUBACK-350 использовать VIN для определения похожего оффера
     
     * тесты
     
     * использовать стандартную библиотеку
  *  AUTORUBACK-285: added complectation_id to ModerationVitalFieldsAndRelated

  *  #AUTORUBACK-482 Fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 17 Jul 2020 20:10:26 +0300

## yandex-vos2-autoru-consumers:0.98.1 (Fri, 17 Jul 2020 12:43:45 +0300)

  *  AUTORUBACK-534 обработка флага should_stay_active для USER_RESELLER (#598)
     
     * обрабатывать флаг should_stay_active
  *  AUTORUBACK-578: Clear proven_owner_moderation (#597)
     
     * AUTORUBACK-578: Clear proven_owner_moderation
  *  AUTORUBACK-526 добавлено поле в FullCarOffer (#596)
     

  *  AUTORUBACK-533 добавлена поддержка chatOnly в защиту модерации (#595)
     
     * добавлена поддержка chatOnly в защиту модерации
     
     * форматирование
  *  AUTORUBACK-350 использовать VIN для определения похожего оффера (#594)
     
     * AUTORUBACK-350 использовать VIN для определения похожего оффера
     
     * тесты
     
     * использовать стандартную библиотеку
  *  AUTORUBACK-285: added complectation_id to ModerationVitalFieldsAndRelated

  *  #AUTORUBACK-482 Fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 17 Jul 2020 12:43:45 +0300

## yandex-vos2-autoru-consumers:0.98.0 (Mon, 13 Jul 2020 16:42:36 +0300)

  *  AUTORUBACK-285: added complectation_id to ModerationVitalFieldsAndRelated

  *  #AUTORUBACK-482 Fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 13 Jul 2020 16:42:36 +0300

## yandex-vos2-autoru-consumers:0.97.1 (Wed, 08 Jul 2020 15:11:47 +0300)

  *  #AUTORUBACK-482 Fix

  *  Autoruback 482 default booking allowed (#591)
     
     * #AUTORUBACK-482 Default booking allowed status
     
     * #AUTORUBACK-482 Spec fix
     
     * make fmt-full
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-126: refactoring: removed some mySql usage, replaced magic number 2 with shardCount in some places

  *  AUTORUBACK-485 detailed validation error message for VIN (#590)
     
     * AUTORUBACK-485 detailed validation error message for VIN
  *  AUTORUBACK-490: redirect deadline fix

  *  AUTORUBACK-490: migration recall info fix: compilation fix

  *  AUTORUBACK-490: migration recall info fix: style

  *  AUTORUBACK-490: migration recall info fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 08 Jul 2020 15:11:47 +0300

## yandex-vos2-autoru-consumers:0.97.0 (Wed, 08 Jul 2020 12:34:13 +0300)

  *  Autoruback 482 default booking allowed (#591)
     
     * #AUTORUBACK-482 Default booking allowed status
     
     * #AUTORUBACK-482 Spec fix
     
     * make fmt-full
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-126: refactoring: removed some mySql usage, replaced magic number 2 with shardCount in some places

  *  AUTORUBACK-485 detailed validation error message for VIN (#590)
     
     * AUTORUBACK-485 detailed validation error message for VIN
  *  AUTORUBACK-490: redirect deadline fix

  *  AUTORUBACK-490: migration recall info fix: compilation fix

  *  AUTORUBACK-490: migration recall info fix: style

  *  AUTORUBACK-490: migration recall info fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 08 Jul 2020 12:34:13 +0300

## yandex-vos2-autoru-consumers:0.96.1 (Mon, 29 Jun 2020 16:49:36 +0300)

  *  AUTORUBACK-479_photo_duplication_fix: style

  *  AUTORUBACK-479_photo_duplication_fix: reverted in some places to reduce possible damage

  *  AUTORUBACK-479_photo_duplication_fix: style

  *  AUTORUBACK-479_photo_duplication_fix: foxed test

  *  AUTORUBACK-479_photo_duplication_fix: more fixes to converters

  *  AUTORUBACK-479_photo_duplication_fix: added fix to migration converter

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 29 Jun 2020 16:49:36 +0300

## yandex-vos2-autoru-consumers:0.96.0 (Mon, 29 Jun 2020 11:34:36 +0300)

  *  AUTORUBACK-479_photo_duplication_fix: style

  *  AUTORUBACK-479_photo_duplication_fix: foxed test

  *  AUTORUBACK-479_photo_duplication_fix: more fixes to converters

  *  AUTORUBACK-479_photo_duplication_fix: added fix to migration converter

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 29 Jun 2020 11:34:36 +0300

## yandex-vos2-autoru-consumers:0.95.1 (Sat, 27 Jun 2020 02:24:48 +0300)

  *  AUTORUBACK-479_photo_duplication_fix (#588)
     

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-478 fixed ForbiddenEditLicensePlate validation

  *  AUORUBACK-467 mosru ban (#587)
     
     * AUTORUBACK-435 withNds save fix 2
     
     * AUTORUBACK-435 withNds save fix 3
     
     * AUTORUBACK-435 withNds save fix: test
     
     * AUTORUBACK-467 ban on mosru validation opinion
  *  AUTORUBACK-467 mosru ban (#586)
     
     * AUTORUBACK-435 withNds save fix 2
     
     * AUTORUBACK-435 withNds save fix 3
  *  AUTORUBACK-435 withNds save fix

  *  #AUTORUBACK-440 Booking for cars category only (#585)
     
     * #AUTORUBACK-440 Booking for cars category only
     
     * #AUTORUBACK-440 Spec fix
     
     * #AUTORUBACK-440 Review fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sat, 27 Jun 2020 02:24:48 +0300

## yandex-vos2-autoru-consumers:0.95.0 (Thu, 25 Jun 2020 11:10:44 +0300)

  *  AUORUBACK-467 mosru ban (#587)
     
     * AUTORUBACK-435 withNds save fix 2
     
     * AUTORUBACK-435 withNds save fix 3
     
     * AUTORUBACK-435 withNds save fix: test
     
     * AUTORUBACK-467 ban on mosru validation opinion
  *  AUTORUBACK-467 mosru ban (#586)
     
     * AUTORUBACK-435 withNds save fix 2
     
     * AUTORUBACK-435 withNds save fix 3
  *  AUTORUBACK-435 withNds save fix

  *  #AUTORUBACK-440 Booking for cars category only (#585)
     
     * #AUTORUBACK-440 Booking for cars category only
     
     * #AUTORUBACK-440 Spec fix
     
     * #AUTORUBACK-440 Review fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 25 Jun 2020 11:10:44 +0300

## yandex-vos2-autoru-consumers:0.94.0 (Fri, 19 Jun 2020 12:45:10 +0300)

  *  VSMONEY-1808 Defult FALSE for booking.allowed removed (#584)
     
     * Defult FALSE for booking.allowed removed
     
     * Test for booking offer converter
     
     * Fmt fix
  *  AUTORUBACK-352: Fix photo converter on publishDraft (#583)
     
     * AUTORUBACK-352: Fix photo converter on publishDraft

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 19 Jun 2020 12:45:10 +0300

## yandex-vos2-autoru-consumers:0.93.0 (Wed, 17 Jun 2020 13:16:11 +0300)

  *  AUTORUBACK-437 old db writer none category fix (#582)
     
     * AUTORUBACK-437 old db writer none category fix
     
     * AUTORUBACK-437 old db writer none category fix: removed unused method
     
     * AUTORUBACK-437 old db writer none category fix: style
  *  AUTORUBACK-406: Clear proven owner status on photo upload (#581)
     
     * AUTORUBACK-406: Clear proven owner status on photo upload
  *  AUTORUSUP-5123 status change comments: refactoring, fixes

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUSUP-5123 updated logging for offer status change without comment: refactoring, added remigration check

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 17 Jun 2020 13:16:11 +0300

## yandex-vos2-autoru-consumers:0.92.0 (Tue, 16 Jun 2020 11:21:48 +0300)

  *  AUTORUSUP-5123 updated logging for offer status change without comment

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 16 Jun 2020 11:21:48 +0300

## yandex-vos2-autoru-consumers:0.91.0 (Thu, 11 Jun 2020 13:33:10 +0300)

  *  #AUTORUBACK-381 Booking allowed API handler (#579)
     

  *  AUTORUBACK-249 supported searcher (#578)
     
     * AUTORUBACK-249 supported searcher
  *  AUTORUBACK-249 new panoramas artifacts (#577)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 11 Jun 2020 13:33:10 +0300

## yandex-vos2-autoru-consumers:0.90.0 (Mon, 08 Jun 2020 04:25:47 +0300)

  *  #AUTORUBACK-403 Logging fix (#576)
     

  *  AUTORUBACK-412: delay send to holocron offers with old timestamp

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 08 Jun 2020 04:25:47 +0300

## yandex-vos2-autoru-consumers:0.89.0 (Fri, 05 Jun 2020 21:33:39 +0300)

  *  Autoruback 403 consumers fix (#575)
     
     * #AUTORUBACK-403 ObservedConsumer fix
     
     * #AUTORUBACK-403 BookingProcessor init fix
     
     * #AUTORUBACK-403 Logging in ObservedConsumer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 05 Jun 2020 21:33:39 +0300

## yandex-vos2-autoru-consumers:0.88.1 (Fri, 05 Jun 2020 14:39:50 +0300)

  *  Autoruback 403 Booking consumer & ObservedConsumer fix (#574)
     
     * #AUTORUBACK-403 ObservedConsumer fix
     
     * #AUTORUBACK-403 BookingProcessor init fix
  *  make fmt

  *  #AUTORUBACK-403 Consumers logging fix (#572)
     

  *  AUTORUBACK-373: send only active certification to holocron: added test
     AUTORUBACK-398 holocron: new recall reasons: added test

  *  AUTORUBACK-373: send only active certification to holocron

  *  AUTORUBACK-398 holocron new recall reasons (#570)
     
     * AUTORUBACK-398 holocron: new recall reasons
     
     * AUTORUBACK-398 holocron: new recall reasons: refactoring
     
     * AUTORUBACK-398 holocron: new recall reasons: updated converter
  *  AUTORUBACK-378 AUTORUBACK-362 send tags to searcher for moto and comtrans

  *  AUTORUBACK-382 fixed old telepony call notifications: fixed test

  *  CARFAX-907 import reload feature (#569)
     
     * CARFAX-907 init
     
     * CARFAX-907 formatting
     
     * CARFAX-907 temporarily pending failed test
     
     * CARFAX-907 delete pending
  *  AUTORUBACK-365 holocron fixes: updated metrics

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-365 fixed old telepony call notifications

  *  AUTORUBACK-352: Photo uploader fixes (#568)
     

  *  #AUTORUBACK-369 Check for dealer offer in CalltrackingCounterUpdateStage (#567)
     
     * #AUTORUBACK-369 Check for dealer offer in CalltrackingCounterUpdateStage
     
     * #AUTORUBACK-369 Review fix
     
     * #AUTORUBACK-369 Spec fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 05 Jun 2020 14:39:50 +0300

## yandex-vos2-autoru-consumers:0.88.0 (Fri, 05 Jun 2020 00:48:56 +0300)

  *  make fmt

  *  #AUTORUBACK-403 Consumers logging fix (#572)
     

  *  AUTORUBACK-373: send only active certification to holocron: added test
     AUTORUBACK-398 holocron: new recall reasons: added test

  *  AUTORUBACK-373: send only active certification to holocron

  *  AUTORUBACK-398 holocron new recall reasons (#570)
     
     * AUTORUBACK-398 holocron: new recall reasons
     
     * AUTORUBACK-398 holocron: new recall reasons: refactoring
     
     * AUTORUBACK-398 holocron: new recall reasons: updated converter
  *  AUTORUBACK-378 AUTORUBACK-362 send tags to searcher for moto and comtrans

  *  AUTORUBACK-382 fixed old telepony call notifications: fixed test

  *  CARFAX-907 import reload feature (#569)
     
     * CARFAX-907 init
     
     * CARFAX-907 formatting
     
     * CARFAX-907 temporarily pending failed test
     
     * CARFAX-907 delete pending
  *  AUTORUBACK-365 holocron fixes: updated metrics

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-365 fixed old telepony call notifications

  *  AUTORUBACK-352: Photo uploader fixes (#568)
     

  *  #AUTORUBACK-369 Check for dealer offer in CalltrackingCounterUpdateStage (#567)
     
     * #AUTORUBACK-369 Check for dealer offer in CalltrackingCounterUpdateStage
     
     * #AUTORUBACK-369 Review fix
     
     * #AUTORUBACK-369 Spec fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 05 Jun 2020 00:48:56 +0300

## yandex-vos2-autoru-consumers:0.87.0 (Mon, 01 Jun 2020 14:05:52 +0300)

  *  AUTORUBACK-372 new recall reasons save error (#566)
     
     3 моля в мапу добавил, врядли чтото сломает или пойдет не так
  *  AUTORUBACK-352: Add document_photo (#560)
     
     * AUTORUBACK-352: Add document photo endpoints
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-368: fixed holocron converter for comtrans

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 01 Jun 2020 14:05:52 +0300

## yandex-vos2-autoru-consumers:0.86.0 (Fri, 29 May 2020 22:10:52 +0300)

  *  Increase of XMX & XMS limits for vos2-autoru-consumers (#565)
     

  *  AUTORUBACK-313 no callinfo for dealer initiated calls (#563)
     
     * AUTORUBACK-313 no callinfo for dealer initiated calls
  *  AUTORUBACK-365 holocron conversion fixes (#561)
     
     * AUTORUBACK-365 holocron fixes: send max sent holo ts plus 1 second, refactoring
     
     * AUTORUBACK-365 holocron fixes: moved shouldReturn to stage, converter now always return HoloOffer
     
     * AUTORUBACK-365 holocron fixes: added checkLastEventsValid, ceckNeedToSend refactoring, updated tests
     
     * AUTORUBACK-365 holocron fixes: style
     
     * AUTORUBACK-365 holocron fixes: fixed tests
     
     * AUTORUBACK-365 holocron fixes: updated logging
  *  VSMONEY-1686 fix dealer call counters (#562)
     

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  BookingConsumerSpec fix

  *  AUTORUBACK-354: migration refactoring (#558)
     
     * AUTORUBACK-354: migration refactoring
     
     * AUTORUBACK-354: migration refactoring: fixed compilation
     
     * AUTORUBACK-354: migration refactoring: minor fix

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 29 May 2020 22:10:52 +0300

## yandex-vos2-autoru-consumers:0.85.0 (Wed, 27 May 2020 11:31:02 +0300)

  *  AUTORUBACK-232 booking consumer (#555)
     
     * #AUTORUBACK-224 Offer booking
     
     * #AUTORUBACK-224 Fixes
     
     * #AUTORUBACK-224 #AUTORUBACK-225 Booking support
     
     * #AUTORUBACK-224 Schema-registry version
     
     * Conflict resolve
     
     * #AUTORUBACK-224 Spec fix
     
     * #AUTORUBACK-224 Fix
     
     * #AUTORUBACK-225 Schema-registry version
     
     * #AUTORUBACK-224 #AUTORUBACK-225 Send booking state to indexer
     
     * #AUTORUBACK-232 BookingConsumer
     
     * #AUTORUBACK-232 BatchingConsumerSpec fix
     
     * #AUTORUBACK-232 Review fix
     
     * #AUTORUBACK-232 Fix package
     
     * #AUTORUBACK-232 Metering fix
     
     * #AUTORUBACK-232 minor
     
     * #AUTORUBACK-232 fix
     
     * #AUTORUBACK-232 Dpendency fix
     
     * #AUTORUBACK-232 Booking topic

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 27 May 2020 11:31:02 +0300

## yandex-vos2-autoru-consumers:0.84.0 (Tue, 26 May 2020 17:45:49 +0300)

  *  AUTORUBACK-358 unban when mos ru validation (#559)
     
     * AUTORUBACK-358 mos_ru_validation only should be unbanned

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-137: validation fixes: fixed trailer type

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 26 May 2020 17:45:49 +0300

## yandex-vos2-autoru-consumers:0.83.0 (Mon, 25 May 2020 13:46:32 +0300)

  *  AUTORUBACK-137 no holocron worker (#556)
     
     * AUTORUBACK-137: send from stage, because of race conditions with worker
     
     * AUTORUBACK-137: send from stage, because of race conditions with worker: refactoring
     
     * AUTORUBACK-137: send from stage, because of race conditions with worker: fixed holocron stage tests, set delay 5 minutes on send errors
     
     * AUTORUBACK-137: send from stage, because of race conditions with worker: added tests from worker to stage, fixed stage
     
     * AUTORUBACK-137: send from stage, because of race conditions with worker: removed worker
     
     * AUTORUBACK-137: send from stage, because of race conditions with worker: removed big queue holocron sender
  *  AUTORUBACK-314: Send message to support chat on offer creation (#554)
     
     * AUTORUBACK-314: Send message to support chat on offer creation
  *  AUTORUBACK-341 batch holocron worker: updated logs and metrics

  *  AUTORUBACK-341 batch holocron worker (#552)
     
     * AUTORUBACK-341 batch holocron worker
     
     * AUTORUBACK-341 batch holocron worker: fixed tests
     
     * AUTORUBACK-341 batch holocron worker: fixed test
  *  #AUTORUBACK-224 Offer booking (#542)
     
     * #AUTORUBACK-224 Offer booking
     
     * #AUTORUBACK-224 Fixes
     
     * #AUTORUBACK-224 #AUTORUBACK-225 Booking support
     
     * #AUTORUBACK-224 Schema-registry version
     
     * Conflict resolve
     
     * #AUTORUBACK-224 Spec fix
     
     * #AUTORUBACK-224 Fix
     
     * #AUTORUBACK-225 Schema-registry version
     
     * #AUTORUBACK-224 #AUTORUBACK-225 Send booking state to indexer
  *  AUTORUBACK-137 holocron improvements: set simple holocron status after migration

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 25 May 2020 13:46:32 +0300

## yandex-vos2-autoru-consumers:0.82.1 (Thu, 14 May 2020 17:36:43 +0300)

  *  AUTORUBACK-248 Support for recall comment (#551)
     
     * AUTORUBACK-248 Support for recall comment

  *  SomeCompilationWarningsSuppressed (#548)
     
     * SomeCompilationWarningsSuppressed
     
     * Fix
  *  AUTORUBACK-137 holocron improvements: send if feature generation chan… (#549)
     
     * AUTORUBACK-137 holocron improvements: send if feature generation changed and lastEvent wasSent=false, resend DEACTIVATE event if no last events exist
     
     * AUTORUBACK-137 holocron improvements: another test
     
     * AUTORUBACK-137 holocron improvements: fixed tests
  *  AUTORUBACK-137 holocron fixes: fixed optLastDeactivateMoment

  *  fixed conflicts

  *  AUTORUBACK-137 holocron fixes: fixed feature

  *  AUTORUBACK-137 holocron fixes: validate only if we going to send, sen… (#537)
     
     * AUTORUBACK-137 holocron fixes: validate only if we going to send, send to kafka directly, inc change_version only if we sent, do not validate DEACTIVATE event
     
     * AUTORUBACK-137 holocron fixes: continue refactoring: worker started
     
     * AUTORUBACK-137 holocron fixes: workers queue and workers refactoring
     
     * AUTORUBACK-137 holocron fixes: updated stage, continue worker, not finished
     
     * AUTORUBACK-137 holocron fixes: refactoring, extended and simple holocron separation
     
     * AUTORUBACK-137 holocron fixes: extended and simple holocron separation continue, use feature with generation
     
     * AUTORUBACK-137 holocron fixes: was_sent, last_sent_moment, holo_timestamp, refactoring
     
     * AUTORUBACK-137 holocron fixes: refactoring, fixed setArchived, fixed setTimestamp for deactivation events
     
     * AUTORUBACK-137 holocron fixes: fixed compilation, removed archived, fixed tests, added tests, refactoring, unify stages (not finished)
     
     * AUTORUBACK-137 holocron fixes: unify stages finished
     
     * AUTORUBACK-137 holocron fixes: updated stage: check only non-zero feature generations, get holocron status if simple holocron status doesn't exist
     
     * AUTORUBACK-137 holocron fixes: fixed stage test
     
     * AUTORUBACK-137 holocron fixes: async process in stage
     
     * AUTORUBACK-137 holocron fixes: simple stage tests
     
     * AUTORUBACK-137 holocron fixes: unify workers
     
     * AUTORUBACK-137 holocron fixes: refactoring, more tests, holocron worrker tests started
     
     * AUTORUBACK-137 holocron fixes: holocron worrker tests
     
     * AUTORUBACK-137 holocron fixes: renamed fields, added worker tests
     
     * AUTORUBACK-137 holocron fixes: finished holocron worker tests
     
     * AUTORUBACK-137 holocron fixes: stage tests refactoring, added more stage tests
     
     * AUTORUBACK-137 holocron fixes: get previous changeVersion from last event, refactoring, added logs (not finished)
     
     * AUTORUBACK-137 holocron fixes: style
     
     * AUTORUBACK-137 holocron fixes: converters refactoring and tests
     
     * AUTORUBACK-137 holocron fixes: kafka enable.idempotence
     
     * AUTORUBACK-137 holocron fixes: added logs to holocron worker
     
     * AUTORUBACK-137 holocron fixes: refactoring, holocron stage name
     
     * AUTORUBACK-137 holocron fixes: converter setArchived test
     
     * AUTORUBACK-137 holocron fixes: inmemory queue tests
     
     * AUTORUBACK-137 holocron fixes: inmemory queue tests
     
     * AUTORUBACK-137 holocron fixes: inmemory queue tests, refactoring: dequeue2
     
     * AUTORUBACK-137 holocron fixes: fixed MeteredHolocronValidator, MaxLastEventsSize test
  *  AUTORUBACK-137 holocron fixes: fixed MeteredHolocronValidator, MaxLastEventsSize test

  *  AUTORUBACK-137 holocron fixes: converter setArchived test

  *  AUTORUBACK-137 holocron fixes: kafka enable.idempotence

  *  AUTORUBACK-137 holocron fixes: converters refactoring and tests

  *  Merge branch 'master' into AUTORUBACK-137_holocron_fixes
  *  AUTORUBACK-137 holocron fixes: style

  *  AUTORUBACK-137 holocron fixes: get previous changeVersion from last event, refactoring, added logs (not finished)

  *  AUTORUBACK-137 holocron fixes: renamed fields, added worker tests

  *  CARFAX-682: send vin resolution to holocron (#539)
     
     * CARFAX-682: send vin resolution to holocron
     
     * schema-registry version bump
     
     * schema-registry version bump
  *  AUTORUBACK-309 updated StatusBanned text

  *  VSMONEY-1520 # Push ADD service to old database to change offer expire_date (#545)
     
     * Fix for VSMONEY-1520, VSMONEY-1523
     
     * fmt
     
     * fix test generator
     
     * VSMONEY-1520 # CodeReview fix
     
     * VSMONEY-1520 # FIX test
     
     * fmt
     
     * VSMONEY-1520 # Push add service to old db
     
     * VSMONEY-1520 # Unit  test
     
     * VSMONEY-1520 # Add comment
     
     * VSMONEY-1520 # Rename addServices -> updateSaleOnAddServices
     
     * VSMONEY-1520 # comment
  *  AUTORUBACK-137 holocron fixes: fixed compilation, removed archived, fixed tests, added tests, refactoring, unify stages (not finished)

  *  AUTORUBACK-137 holocron fixes: refactoring, fixed setArchived, fixed setTimestamp for deactivation events

  *  AUTORUBACK-137 holocron fixes: was_sent, last_sent_moment, holo_timestamp, refactoring

  *  AUTORUBACK-137 holocron fixes: extended and simple holocron separation continue, use feature with generation

  *  AUTORUBACK-137 holocron fixes: refactoring, extended and simple holocron separation

  *  AUTORUBACK-137 holocron fixes: workers queue and workers refactoring

  *  AUTORUBACK-137 holocron fixes: continue refactoring: worker started

  *  Merge branch 'master' into AUTORUBACK-137_holocron_fixes

  *  AUTORUBACK-137 holocron fixes: validate only if we going to send, send to kafka directly, inc change_version only if we sent, do not validate DEACTIVATE event

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 14 May 2020 17:36:43 +0300

## yandex-vos2-autoru-consumers:0.82.0 (Sun, 10 May 2020 22:33:25 +0300)

  *  AUTORUBACK-137 holocron fixes: validate only if we going to send, sen… (#537)
     
     * AUTORUBACK-137 holocron fixes: validate only if we going to send, send to kafka directly, inc change_version only if we sent, do not validate DEACTIVATE event
     
     * AUTORUBACK-137 holocron fixes: continue refactoring: worker started
     
     * AUTORUBACK-137 holocron fixes: workers queue and workers refactoring
     
     * AUTORUBACK-137 holocron fixes: updated stage, continue worker, not finished
     
     * AUTORUBACK-137 holocron fixes: refactoring, extended and simple holocron separation
     
     * AUTORUBACK-137 holocron fixes: extended and simple holocron separation continue, use feature with generation
     
     * AUTORUBACK-137 holocron fixes: was_sent, last_sent_moment, holo_timestamp, refactoring
     
     * AUTORUBACK-137 holocron fixes: refactoring, fixed setArchived, fixed setTimestamp for deactivation events
     
     * AUTORUBACK-137 holocron fixes: fixed compilation, removed archived, fixed tests, added tests, refactoring, unify stages (not finished)
     
     * AUTORUBACK-137 holocron fixes: unify stages finished
     
     * AUTORUBACK-137 holocron fixes: updated stage: check only non-zero feature generations, get holocron status if simple holocron status doesn't exist
     
     * AUTORUBACK-137 holocron fixes: fixed stage test
     
     * AUTORUBACK-137 holocron fixes: async process in stage
     
     * AUTORUBACK-137 holocron fixes: simple stage tests
     
     * AUTORUBACK-137 holocron fixes: unify workers
     
     * AUTORUBACK-137 holocron fixes: refactoring, more tests, holocron worrker tests started
     
     * AUTORUBACK-137 holocron fixes: holocron worrker tests
     
     * AUTORUBACK-137 holocron fixes: renamed fields, added worker tests
     
     * AUTORUBACK-137 holocron fixes: finished holocron worker tests
     
     * AUTORUBACK-137 holocron fixes: stage tests refactoring, added more stage tests
     
     * AUTORUBACK-137 holocron fixes: get previous changeVersion from last event, refactoring, added logs (not finished)
     
     * AUTORUBACK-137 holocron fixes: style
     
     * AUTORUBACK-137 holocron fixes: converters refactoring and tests
     
     * AUTORUBACK-137 holocron fixes: kafka enable.idempotence
     
     * AUTORUBACK-137 holocron fixes: added logs to holocron worker
     
     * AUTORUBACK-137 holocron fixes: refactoring, holocron stage name
     
     * AUTORUBACK-137 holocron fixes: converter setArchived test
     
     * AUTORUBACK-137 holocron fixes: inmemory queue tests
     
     * AUTORUBACK-137 holocron fixes: inmemory queue tests
     
     * AUTORUBACK-137 holocron fixes: inmemory queue tests, refactoring: dequeue2
     
     * AUTORUBACK-137 holocron fixes: fixed MeteredHolocronValidator, MaxLastEventsSize test
  *  CARFAX-682: send vin resolution to holocron (#539)
     
     * CARFAX-682: send vin resolution to holocron
     
     * schema-registry version bump
     
     * schema-registry version bump
  *  AUTORUBACK-309 updated StatusBanned text

  *  VSMONEY-1520 # Push ADD service to old database to change offer expire_date (#545)
     
     * Fix for VSMONEY-1520, VSMONEY-1523
     
     * fmt
     
     * fix test generator
     
     * VSMONEY-1520 # CodeReview fix
     
     * VSMONEY-1520 # FIX test
     
     * fmt
     
     * VSMONEY-1520 # Push add service to old db
     
     * VSMONEY-1520 # Unit  test
     
     * VSMONEY-1520 # Add comment
     
     * VSMONEY-1520 # Rename addServices -> updateSaleOnAddServices
     
     * VSMONEY-1520 # comment

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 10 May 2020 22:33:25 +0300

## yandex-vos2-autoru-consumers:0.81.0 (Wed, 06 May 2020 15:33:09 +0300)

  *  AUTORUBACK-300 chat headers (#546)
     
     * AUTORUBACK-300 chat headers
     
     * AUTORUBACK-300 chat headers: style
     
     * AUTORUBACK-300 chat headers: fixed test, updated schema-registry version
     
     * Revert "AUTORUBACK-300 chat headers: style"
     
     This reverts commit 4dafe247
     
     * AUTORUBACK-300 chat headers: set provided id for service notification
     
     * AUTORUBACK-300 chat headers: same provided id in idempotency key and provided id

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 06 May 2020 15:33:09 +0300

## yandex-vos2-autoru-consumers:0.80.1 (Wed, 06 May 2020 14:24:58 +0300)

  *  AUTORUBACK-297 online view (#543)
     
     * AUTORUBACK-297 online view model
     
     * AUTORUBACK-297 online view model: online_view_available
     
     * AUTORUBACK-297 online_view_available: updated all converters, set tag
     
     * AUTORUBACK-297 online_view_available: updated schema-registry version
     
     * AUTORUBACK-297 online_view_available: style
     
     * AUTORUBACK-297 online_view_available: style again
     
     * AUTORUBACK-297 online_view_available: alterTag, tag in constant
     
     * AUTORUBACK-297 online_view_available: minor changes
     
     * AUTORUBACK-297 online_view_available: style
  *  AUTORUBACK-278 always parse offer description for some time (#538)
     
     * AUTORUBACK-278 always parse offer description for some time
     
     * pr fix
  *  ActivationStage: fix expire_date for free offers + correct decrement promocode feature # VSMONEY-1520, VSMONEY-1523 (#540)
     
     * Fix for VSMONEY-1520, VSMONEY-1523
     
     * fmt
     
     * fix test generator
     
     * VSMONEY-1520 # CodeReview fix
     
     * VSMONEY-1520 # FIX test
     
     * fmt

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 06 May 2020 14:24:58 +0300

## yandex-vos2-autoru-consumers:0.80.0 (Sun, 03 May 2020 14:07:09 +0300)

  *  AUTORUBACK-278 always parse offer description for some time (#538)
     
     * AUTORUBACK-278 always parse offer description for some time
     
     * pr fix
  *  ActivationStage: fix expire_date for free offers + correct decrement promocode feature # VSMONEY-1520, VSMONEY-1523 (#540)
     
     * Fix for VSMONEY-1520, VSMONEY-1523
     
     * fmt
     
     * fix test generator
     
     * VSMONEY-1520 # CodeReview fix
     
     * VSMONEY-1520 # FIX test
     
     * fmt

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Sun, 03 May 2020 14:07:09 +0300

## yandex-vos2-autoru-consumers:0.79.0 (Tue, 28 Apr 2020 20:16:36 +0300)

  *  AUTORUBACK-219: fix predict request param (#536)
     

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-279 increased timeout to ocr for sts recognition

  *  AUTORUBACK-48: Add stats_from/stats_to params for listing endpoint (#532)
     
     * AUTORUBACK-48: Add stats_from/stats_to params for listing endpoint
  *  AUTORUBACK-219: Send a model=dealers to predict price (#523)
     
     * AUTORUBACK-219: Send a model=dealers to predict price

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 28 Apr 2020 20:16:36 +0300

## yandex-vos2-autoru-consumers:0.78.0 (Fri, 24 Apr 2020 13:13:45 +0300)

  *  AUTORUBACK-270 armored fix (#534)
     
     * AUTORUBACK-270 armored fix
     
     need to reparse description on offers with wrong armored equipment
     
     * format fix
  *  VSMONEY-1517 rm unneeded salesman_user_prices feature (#533)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 24 Apr 2020 13:13:45 +0300

## yandex-vos2-autoru-consumers:0.77.0 (Wed, 22 Apr 2020 16:14:30 +0300)

  *  AUTORUBACK-199 case about removing proven owner tag (#531)
     
     * #AUTORUBACK-199 Clean proven_owner state & tag when there is no metadata
     
     * #AUTORUBACK-199 Unnecessary new line
     
     * make fmt

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 22 Apr 2020 16:14:30 +0300

## yandex-vos2-autoru-consumers:0.76.0 (Wed, 22 Apr 2020 14:49:45 +0300)

  *  AUTORUBACK-261 fixed offer bans on user_reseller+mos_ru_validation: fixed test

  *  AUTORUBACK-261 fixed offer bans on user_reseller+mos_ru_validation: fixed test

  *  AUTORUBACK-261 fixed offer bans on user_reseller+mos_ru_validation

  *  AUTORUBACK-48: Return daily calls with offer listing (#529)
     
     * AUTORUBACK-48: Return daily calls with offer listing
  *  CARFAX-653 send has no license plate photo to idx (#530)
     

  *  CARFAX-653 no license plate on photo (#525)
     

  *  VSMONEY-1376 make uploadFeed() code clean (#526)
     
     * VSMONEY-1376 move task param to constructor
     
     * VSMONEY-1376 move things outside of uploadFeed()
     
     * move find feeds logging to findByFeedprocessorId()
     
     * move feedProcessorIdsToEntity to findByFeedprocessorId()
     
     * simplify richEntities() signature
     
     * move requestEntities to ctor params
     
     * move vosOffersByHash to private
     
     * simplify enriching with media data
     
     * move formWriteParams creation outside of uploadFeed()
     
     * extract update & insert methods
     
     * extract createResponseForBanned
     
     * extract buildResults()
     
     * simplify addFeedprocessorImagesInfoToOffers() signature
     
     * extract saveErrorCount()
     
     * rm redundant @author annotation
     
     * rename requestEntities -> offersToUpload
  *  fix expert-related formatting (#527)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 22 Apr 2020 14:49:45 +0300

## yandex-vos2-autoru-consumers:0.75.0 (Fri, 17 Apr 2020 15:36:01 +0300)

  *  renamed autoru_pro index table

  *  renamed autoru_pro -> autoru_expert

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 17 Apr 2020 15:36:01 +0300

## yandex-vos2-autoru-consumers:0.74.14 (Thu, 16 Apr 2020 18:40:44 +0300)

  *  Update Dockerfile
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  improved logging for sts photo upload

  *  Update CHANGELOG.md
  *  fixed compilation

  *  merge master

  *  improved logging for sts photo upload

  *  #AUTORUBACK-209 New .scalafmt.conf (#524)
     

  *  Autoruback 217 autoru pro limitations (#522)
     
     * #AUTORUBACK-217 autoru_pro limitations
     
     * #AUTORUBACK-217 make fmt
     
     * #AUTORUBACK-217 Spec fix
     
     * #AUTORUBACK-217 Review fixes
  *  #AUTORUBACK-199 Proven owner support (#519)
     
     * #AUTORUBACK-199 Proven owner support
     
     * #AUTORUBACK-199 make fmt
     
     * #AUTORUBACK-199 Typo
     
     * #AUTORUBACK-199 touch
     
     * #AUTORUBACK-199 touch
  *  VSMONEY-1395 don't allow moderation to update autoru_pro (#520)
     
     * VSMONEY-1395 don't allow moderation to update autoru_pro
     
     Есть два источника обновления офферов из фидов:
     1. Дилер его обновляет
     2. Модерация его обновляет
     
     Если модерация ничего не делала:
     1. Витальные поля изменились — старое объявление снимаем, новое добавляем
     2. Не изменились — обновляем старое
     
     Если модерация меняла какие-то поля, то же самое, просто эти изменённые поля не учитываем в сравнении витальных полей.
     
     Таким образом, если модерация обновит витальное поле autoru_pro, оно обновится в оффере, что неверно.
     
     Фикс: запрещаем модерации обновлять это поле, разрешаем только дилеру с ним работать.
     
     * improve comment
  *   AUTO-11424_stable_price_calc
     
      AUTO-11424_stable_price_calc
  *  AUTO-11406 add price diff to offer (#518)
     
     AUTO-11406 add price diff to offer (#518)
  *  VSMONEY-1380 add autoru_pro to vital fields (#516)
     
     * VSMONEY-1380 add autoru_pro to cars vital fields
     
     Теперь офферы с autoru_pro = true и autoru_pro = false:
     1. будут разными офферами
     2. не будут активированы одновременно
     
     Также, офферы с autoru_pro = false и непроставленным autoru_pro будут одинаковыми офферами. Иначе при получении из фида autoru_pro = false и непроставленном в базе autoru_pro был бы создан новый оффер, что неверно.
     
     * VSMONEY-1380 simplify equalField()
     
     * VSMONEY-1380 add autoru_pro to trucks vital fields
     
     * VSMONEY-1380 use master schema-registry version
  *  scalafmt arrows rule (#517)
     
     * scalafmt arrows rule
     
     * make fmt-full
  *  schema_drop update

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUAPI-6643 sts photo in drafts: added logging

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  VSPASSPORT-501: mos.ru validation: keep offer unbanned: fix

  *  AUTORUBACK-181 tags for price quality (#505)
     
     * AUTORUBACK-181 tags for price quality
  *  VSMONEY-1377 extract AutoruOffersRequestHandler methods (#513)
     
     * VSMONEY-1377 extract handleFailedOffers() to separate class
     
     * VSMONEY-1377 rm unused val
     
     * VSMONEY-1377 extract handleStreamEnd() to separate class
     
     * VSMONEY-1377 extract handleOffers() to separate class
  *  VSMONEY-1366 rm remove_offers_outside_feed feature (#508)
     

  *  VSMONEY-1051 add calls statistics (#502)
     
     * VSMONEY-1051 add calls statistics
     
     * fill calls count
     
     * trying to resolve strange protobuf compilation issues
     
     * that's why you shouldn't write code by night if you're not used to it'
     
     * format
     
     * finally (maybe)
  *  Scalafmt code (#512)
     
     * Scalafmt maven plugin
     
     * check_style.sh fix for teamcity job
     
     * Removing the scalasttyle plugin
     
     * scalafmt code formatting
  *  rm unused OfferFieldMerger (#509)
     

  *  VSMONEY-1363 rm protect_vital_fields feature (#506)
     

  *  
     
     AUTORUAPI-6610 do not generate empty notices
  *  
     
     AUTORUAPI-6610 and test fix
  *  
     
     AUTORUAPI-6610 description parsing empty notice fix
  *  VSPASSPORT-501: mos.ru validation: keep offer unbanned

  *  #AUTORUBACK-184 autoru_pro index support (#500)
     
     * #AUTORUBACK-184 autoru_pro index support
     
     * #AUTORUBACK-184 Review fix & handler spec
     
     * #AUTORUBACK-184 Review fix
  *  AUTO-11393 Add discounts for truck (#501)
     
     * AUTO-11393 Add discounts for truck
     
     * AUTO-11393 Add discounts for truck: add leasing
  *  AUTORUAPI-6610 enrich offer equipment from description in feed consumer (#497)
     
     * enrich offer equipment from description in feed consumer
     
     * tests and pr fixes
     
     * keep meta in scheduler postConvert
  *  VERTISQ-244 autoru pro support (#493)
     
     * VERTISQ-244 autoru pro support
     
     * AUTORUBACK-179 autoru_pro in api offer model: receive from form durion creation only
     
     * AUTORUBACK-179 autoru_pro in api offer model: added tests
  *  VOS-3287 (#494)
     
     * VOS-3287 enable/disable publication for external panorama
  *  VSMONEY-1329 reduce dealer proxy TTL (#496)
     

  *  sale geo id conversion minor fix

  *  Autoruback 133 call fix (#492)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Replace to protobuf format because Json.printToString can't transform proto.Timestamp
  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 16 Apr 2020 18:40:44 +0300

## yandex-vos2-autoru-consumers:0.74.13 (Wed, 15 Apr 2020 20:35:13 +0300)

  *  Update CHANGELOG.md
  *  fixed compilation

  *  merge master

  *  improved logging for sts photo upload

  *  #AUTORUBACK-209 New .scalafmt.conf (#524)
     

  *  Autoruback 217 autoru pro limitations (#522)
     
     * #AUTORUBACK-217 autoru_pro limitations
     
     * #AUTORUBACK-217 make fmt
     
     * #AUTORUBACK-217 Spec fix
     
     * #AUTORUBACK-217 Review fixes
  *  #AUTORUBACK-199 Proven owner support (#519)
     
     * #AUTORUBACK-199 Proven owner support
     
     * #AUTORUBACK-199 make fmt
     
     * #AUTORUBACK-199 Typo
     
     * #AUTORUBACK-199 touch
     
     * #AUTORUBACK-199 touch
  *  VSMONEY-1395 don't allow moderation to update autoru_pro (#520)
     
     * VSMONEY-1395 don't allow moderation to update autoru_pro
     
     Есть два источника обновления офферов из фидов:
     1. Дилер его обновляет
     2. Модерация его обновляет
     
     Если модерация ничего не делала:
     1. Витальные поля изменились — старое объявление снимаем, новое добавляем
     2. Не изменились — обновляем старое
     
     Если модерация меняла какие-то поля, то же самое, просто эти изменённые поля не учитываем в сравнении витальных полей.
     
     Таким образом, если модерация обновит витальное поле autoru_pro, оно обновится в оффере, что неверно.
     
     Фикс: запрещаем модерации обновлять это поле, разрешаем только дилеру с ним работать.
     
     * improve comment
  *   AUTO-11424_stable_price_calc
     
      AUTO-11424_stable_price_calc
  *  AUTO-11406 add price diff to offer (#518)
     
     AUTO-11406 add price diff to offer (#518)
  *  VSMONEY-1380 add autoru_pro to vital fields (#516)
     
     * VSMONEY-1380 add autoru_pro to cars vital fields
     
     Теперь офферы с autoru_pro = true и autoru_pro = false:
     1. будут разными офферами
     2. не будут активированы одновременно
     
     Также, офферы с autoru_pro = false и непроставленным autoru_pro будут одинаковыми офферами. Иначе при получении из фида autoru_pro = false и непроставленном в базе autoru_pro был бы создан новый оффер, что неверно.
     
     * VSMONEY-1380 simplify equalField()
     
     * VSMONEY-1380 add autoru_pro to trucks vital fields
     
     * VSMONEY-1380 use master schema-registry version
  *  scalafmt arrows rule (#517)
     
     * scalafmt arrows rule
     
     * make fmt-full
  *  schema_drop update

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUAPI-6643 sts photo in drafts: added logging

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  VSPASSPORT-501: mos.ru validation: keep offer unbanned: fix

  *  AUTORUBACK-181 tags for price quality (#505)
     
     * AUTORUBACK-181 tags for price quality
  *  VSMONEY-1377 extract AutoruOffersRequestHandler methods (#513)
     
     * VSMONEY-1377 extract handleFailedOffers() to separate class
     
     * VSMONEY-1377 rm unused val
     
     * VSMONEY-1377 extract handleStreamEnd() to separate class
     
     * VSMONEY-1377 extract handleOffers() to separate class
  *  VSMONEY-1366 rm remove_offers_outside_feed feature (#508)
     

  *  VSMONEY-1051 add calls statistics (#502)
     
     * VSMONEY-1051 add calls statistics
     
     * fill calls count
     
     * trying to resolve strange protobuf compilation issues
     
     * that's why you shouldn't write code by night if you're not used to it'
     
     * format
     
     * finally (maybe)
  *  Scalafmt code (#512)
     
     * Scalafmt maven plugin
     
     * check_style.sh fix for teamcity job
     
     * Removing the scalasttyle plugin
     
     * scalafmt code formatting
  *  rm unused OfferFieldMerger (#509)
     

  *  VSMONEY-1363 rm protect_vital_fields feature (#506)
     

  *  
     
     AUTORUAPI-6610 do not generate empty notices
  *  
     
     AUTORUAPI-6610 and test fix
  *  
     
     AUTORUAPI-6610 description parsing empty notice fix
  *  VSPASSPORT-501: mos.ru validation: keep offer unbanned

  *  #AUTORUBACK-184 autoru_pro index support (#500)
     
     * #AUTORUBACK-184 autoru_pro index support
     
     * #AUTORUBACK-184 Review fix & handler spec
     
     * #AUTORUBACK-184 Review fix
  *  AUTO-11393 Add discounts for truck (#501)
     
     * AUTO-11393 Add discounts for truck
     
     * AUTO-11393 Add discounts for truck: add leasing
  *  AUTORUAPI-6610 enrich offer equipment from description in feed consumer (#497)
     
     * enrich offer equipment from description in feed consumer
     
     * tests and pr fixes
     
     * keep meta in scheduler postConvert
  *  VERTISQ-244 autoru pro support (#493)
     
     * VERTISQ-244 autoru pro support
     
     * AUTORUBACK-179 autoru_pro in api offer model: receive from form durion creation only
     
     * AUTORUBACK-179 autoru_pro in api offer model: added tests
  *  VOS-3287 (#494)
     
     * VOS-3287 enable/disable publication for external panorama
  *  VSMONEY-1329 reduce dealer proxy TTL (#496)
     

  *  sale geo id conversion minor fix

  *  Autoruback 133 call fix (#492)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Replace to protobuf format because Json.printToString can't transform proto.Timestamp
  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 15 Apr 2020 20:35:13 +0300

## yandex-vos2-autoru-consumers:0.74.12 (Mon, 13 Apr 2020 10:31:52 +0300)

  *  up
  
## yandex-vos2-autoru-consumers:0.74.11 (Mon, 13 Apr 2020 10:31:52 +0300)

  *  VSMONEY-1380 add autoru_pro to vital fields (#516)
     
     * VSMONEY-1380 add autoru_pro to cars vital fields
     
     Теперь офферы с autoru_pro = true и autoru_pro = false:
     1. будут разными офферами
     2. не будут активированы одновременно
     
     Также, офферы с autoru_pro = false и непроставленным autoru_pro будут одинаковыми офферами. Иначе при получении из фида autoru_pro = false и непроставленном в базе autoru_pro был бы создан новый оффер, что неверно.
     
     * VSMONEY-1380 simplify equalField()
     
     * VSMONEY-1380 add autoru_pro to trucks vital fields
     
     * VSMONEY-1380 use master schema-registry version
  *  scalafmt arrows rule (#517)
     
     * scalafmt arrows rule
     
     * make fmt-full
  *  schema_drop update

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUAPI-6643 sts photo in drafts: added logging

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  VSPASSPORT-501: mos.ru validation: keep offer unbanned: fix

  *  AUTORUBACK-181 tags for price quality (#505)
     
     * AUTORUBACK-181 tags for price quality
  *  VSMONEY-1377 extract AutoruOffersRequestHandler methods (#513)
     
     * VSMONEY-1377 extract handleFailedOffers() to separate class
     
     * VSMONEY-1377 rm unused val
     
     * VSMONEY-1377 extract handleStreamEnd() to separate class
     
     * VSMONEY-1377 extract handleOffers() to separate class
  *  VSMONEY-1366 rm remove_offers_outside_feed feature (#508)
     

  *  VSMONEY-1051 add calls statistics (#502)
     
     * VSMONEY-1051 add calls statistics
     
     * fill calls count
     
     * trying to resolve strange protobuf compilation issues
     
     * that's why you shouldn't write code by night if you're not used to it'
     
     * format
     
     * finally (maybe)
  *  Scalafmt code (#512)
     
     * Scalafmt maven plugin
     
     * check_style.sh fix for teamcity job
     
     * Removing the scalasttyle plugin
     
     * scalafmt code formatting
  *  rm unused OfferFieldMerger (#509)
     

  *  VSMONEY-1363 rm protect_vital_fields feature (#506)
     

  *  
     
     AUTORUAPI-6610 do not generate empty notices
  *  
     
     AUTORUAPI-6610 and test fix
  *  
     
     AUTORUAPI-6610 description parsing empty notice fix
  *  VSPASSPORT-501: mos.ru validation: keep offer unbanned

  *  #AUTORUBACK-184 autoru_pro index support (#500)
     
     * #AUTORUBACK-184 autoru_pro index support
     
     * #AUTORUBACK-184 Review fix & handler spec
     
     * #AUTORUBACK-184 Review fix
  *  AUTO-11393 Add discounts for truck (#501)
     
     * AUTO-11393 Add discounts for truck
     
     * AUTO-11393 Add discounts for truck: add leasing
  *  AUTORUAPI-6610 enrich offer equipment from description in feed consumer (#497)
     
     * enrich offer equipment from description in feed consumer
     
     * tests and pr fixes
     
     * keep meta in scheduler postConvert
  *  VERTISQ-244 autoru pro support (#493)
     
     * VERTISQ-244 autoru pro support
     
     * AUTORUBACK-179 autoru_pro in api offer model: receive from form durion creation only
     
     * AUTORUBACK-179 autoru_pro in api offer model: added tests
  *  VOS-3287 (#494)
     
     * VOS-3287 enable/disable publication for external panorama
  *  VSMONEY-1329 reduce dealer proxy TTL (#496)
     

  *  sale geo id conversion minor fix

  *  Autoruback 133 call fix (#492)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Replace to protobuf format because Json.printToString can't transform proto.Timestamp
  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 13 Apr 2020 10:31:52 +0300

## yandex-vos2-autoru-consumers:0.74.10 (Thu, 09 Apr 2020 15:13:58 +0300)

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  VSPASSPORT-501: mos.ru validation: keep offer unbanned: fix

  *  AUTORUBACK-181 tags for price quality (#505)
     
     * AUTORUBACK-181 tags for price quality
  *  VSMONEY-1377 extract AutoruOffersRequestHandler methods (#513)
     
     * VSMONEY-1377 extract handleFailedOffers() to separate class
     
     * VSMONEY-1377 rm unused val
     
     * VSMONEY-1377 extract handleStreamEnd() to separate class
     
     * VSMONEY-1377 extract handleOffers() to separate class
  *  VSMONEY-1366 rm remove_offers_outside_feed feature (#508)
     

  *  VSMONEY-1051 add calls statistics (#502)
     
     * VSMONEY-1051 add calls statistics
     
     * fill calls count
     
     * trying to resolve strange protobuf compilation issues
     
     * that's why you shouldn't write code by night if you're not used to it'
     
     * format
     
     * finally (maybe)
  *  Scalafmt code (#512)
     
     * Scalafmt maven plugin
     
     * check_style.sh fix for teamcity job
     
     * Removing the scalasttyle plugin
     
     * scalafmt code formatting
  *  rm unused OfferFieldMerger (#509)
     

  *  VSMONEY-1363 rm protect_vital_fields feature (#506)
     

  *  
     
     AUTORUAPI-6610 do not generate empty notices
  *  
     
     AUTORUAPI-6610 and test fix
  *  
     
     AUTORUAPI-6610 description parsing empty notice fix
  *  VSPASSPORT-501: mos.ru validation: keep offer unbanned

  *  #AUTORUBACK-184 autoru_pro index support (#500)
     
     * #AUTORUBACK-184 autoru_pro index support
     
     * #AUTORUBACK-184 Review fix & handler spec
     
     * #AUTORUBACK-184 Review fix
  *  AUTO-11393 Add discounts for truck (#501)
     
     * AUTO-11393 Add discounts for truck
     
     * AUTO-11393 Add discounts for truck: add leasing
  *  AUTORUAPI-6610 enrich offer equipment from description in feed consumer (#497)
     
     * enrich offer equipment from description in feed consumer
     
     * tests and pr fixes
     
     * keep meta in scheduler postConvert
  *  VERTISQ-244 autoru pro support (#493)
     
     * VERTISQ-244 autoru pro support
     
     * AUTORUBACK-179 autoru_pro in api offer model: receive from form durion creation only
     
     * AUTORUBACK-179 autoru_pro in api offer model: added tests
  *  VOS-3287 (#494)
     
     * VOS-3287 enable/disable publication for external panorama
  *  VSMONEY-1329 reduce dealer proxy TTL (#496)
     

  *  sale geo id conversion minor fix

  *  Autoruback 133 call fix (#492)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Replace to protobuf format because Json.printToString can't transform proto.Timestamp
  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 09 Apr 2020 15:13:58 +0300

## yandex-vos2-autoru-consumers:0.74.9 (Wed, 08 Apr 2020 12:30:45 +0300)

  *  
     
     AUTORUAPI-6610 do not generate empty notices
  *  
     
     AUTORUAPI-6610 and test fix
  *  
     
     AUTORUAPI-6610 description parsing empty notice fix
  *  VSPASSPORT-501: mos.ru validation: keep offer unbanned

  *  #AUTORUBACK-184 autoru_pro index support (#500)
     
     * #AUTORUBACK-184 autoru_pro index support
     
     * #AUTORUBACK-184 Review fix & handler spec
     
     * #AUTORUBACK-184 Review fix
  *  AUTO-11393 Add discounts for truck (#501)
     
     * AUTO-11393 Add discounts for truck
     
     * AUTO-11393 Add discounts for truck: add leasing
  *  AUTORUAPI-6610 enrich offer equipment from description in feed consumer (#497)
     
     * enrich offer equipment from description in feed consumer
     
     * tests and pr fixes
     
     * keep meta in scheduler postConvert
  *  VERTISQ-244 autoru pro support (#493)
     
     * VERTISQ-244 autoru pro support
     
     * AUTORUBACK-179 autoru_pro in api offer model: receive from form durion creation only
     
     * AUTORUBACK-179 autoru_pro in api offer model: added tests
  *  VOS-3287 (#494)
     
     * VOS-3287 enable/disable publication for external panorama
  *  VSMONEY-1329 reduce dealer proxy TTL (#496)
     

  *  sale geo id conversion minor fix

  *  Autoruback 133 call fix (#492)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Replace to protobuf format because Json.printToString can't transform proto.Timestamp
  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 08 Apr 2020 12:30:45 +0300

## yandex-vos2-autoru-consumers:0.74.8 (Tue, 07 Apr 2020 12:37:26 +0300)

  *  
     
     AUTORUAPI-6610 and test fix
  *  
     
     AUTORUAPI-6610 description parsing empty notice fix
  *  VSPASSPORT-501: mos.ru validation: keep offer unbanned

  *  #AUTORUBACK-184 autoru_pro index support (#500)
     
     * #AUTORUBACK-184 autoru_pro index support
     
     * #AUTORUBACK-184 Review fix & handler spec
     
     * #AUTORUBACK-184 Review fix
  *  AUTO-11393 Add discounts for truck (#501)
     
     * AUTO-11393 Add discounts for truck
     
     * AUTO-11393 Add discounts for truck: add leasing
  *  AUTORUAPI-6610 enrich offer equipment from description in feed consumer (#497)
     
     * enrich offer equipment from description in feed consumer
     
     * tests and pr fixes
     
     * keep meta in scheduler postConvert
  *  VERTISQ-244 autoru pro support (#493)
     
     * VERTISQ-244 autoru pro support
     
     * AUTORUBACK-179 autoru_pro in api offer model: receive from form durion creation only
     
     * AUTORUBACK-179 autoru_pro in api offer model: added tests
  *  VOS-3287 (#494)
     
     * VOS-3287 enable/disable publication for external panorama
  *  VSMONEY-1329 reduce dealer proxy TTL (#496)
     

  *  sale geo id conversion minor fix

  *  Autoruback 133 call fix (#492)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Replace to protobuf format because Json.printToString can't transform proto.Timestamp
  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 07 Apr 2020 12:37:26 +0300

## yandex-vos2-autoru-consumers:0.74.7 (Mon, 06 Apr 2020 19:26:25 +0300)

  *  VSPASSPORT-501: mos.ru validation: keep offer unbanned

  *  #AUTORUBACK-184 autoru_pro index support (#500)
     
     * #AUTORUBACK-184 autoru_pro index support
     
     * #AUTORUBACK-184 Review fix & handler spec
     
     * #AUTORUBACK-184 Review fix
  *  AUTO-11393 Add discounts for truck (#501)
     
     * AUTO-11393 Add discounts for truck
     
     * AUTO-11393 Add discounts for truck: add leasing
  *  AUTORUAPI-6610 enrich offer equipment from description in feed consumer (#497)
     
     * enrich offer equipment from description in feed consumer
     
     * tests and pr fixes
     
     * keep meta in scheduler postConvert
  *  VERTISQ-244 autoru pro support (#493)
     
     * VERTISQ-244 autoru pro support
     
     * AUTORUBACK-179 autoru_pro in api offer model: receive from form durion creation only
     
     * AUTORUBACK-179 autoru_pro in api offer model: added tests
  *  VOS-3287 (#494)
     
     * VOS-3287 enable/disable publication for external panorama
  *  VSMONEY-1329 reduce dealer proxy TTL (#496)
     

  *  sale geo id conversion minor fix

  *  Autoruback 133 call fix (#492)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Replace to protobuf format because Json.printToString can't transform proto.Timestamp
  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 06 Apr 2020 19:26:25 +0300

## yandex-vos2-autoru-consumers:0.74.6 (Thu, 02 Apr 2020 19:16:00 +0300)

  *  AUTORUAPI-6610 enrich offer equipment from description in feed consumer (#497)
     
     * enrich offer equipment from description in feed consumer
     
     * tests and pr fixes
     
     * keep meta in scheduler postConvert
  *  VERTISQ-244 autoru pro support (#493)
     
     * VERTISQ-244 autoru pro support
     
     * AUTORUBACK-179 autoru_pro in api offer model: receive from form durion creation only
     
     * AUTORUBACK-179 autoru_pro in api offer model: added tests
  *  VOS-3287 (#494)
     
     * VOS-3287 enable/disable publication for external panorama
  *  VSMONEY-1329 reduce dealer proxy TTL (#496)
     

  *  sale geo id conversion minor fix

  *  Autoruback 133 call fix (#492)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Replace to protobuf format because Json.printToString can't transform proto.Timestamp
  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 02 Apr 2020 19:16:00 +0300

## yandex-vos2-autoru-consumers:0.74.5 (Thu, 02 Apr 2020 11:15:29 +0300)

  *  VERTISQ-244 autoru pro support (#493)
     
     * VERTISQ-244 autoru pro support
     
     * AUTORUBACK-179 autoru_pro in api offer model: receive from form durion creation only
     
     * AUTORUBACK-179 autoru_pro in api offer model: added tests
  *  VOS-3287 (#494)
     
     * VOS-3287 enable/disable publication for external panorama
  *  VSMONEY-1329 reduce dealer proxy TTL (#496)
     

  *  sale geo id conversion minor fix

  *  Autoruback 133 call fix (#492)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Replace to protobuf format because Json.printToString can't transform proto.Timestamp
  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 02 Apr 2020 11:15:29 +0300

## yandex-vos2-autoru-consumers:0.74.4 (Fri, 27 Mar 2020 21:36:26 +0300)

  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 27 Mar 2020 21:36:26 +0300

## yandex-vos2-autoru-consumers:0.74.3 (Fri, 27 Mar 2020 19:01:25 +0300)

  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 27 Mar 2020 19:01:25 +0300

## yandex-vos2-autoru-consumers:0.74.2 (Fri, 27 Mar 2020 17:45:09 +0300)

  *  Autoruback 133 Fix phone number format (#491)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Fix phone format
     
     * AUTORUBACK-133 Fix phone format
  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 27 Mar 2020 17:45:09 +0300

## yandex-vos2-autoru-consumers:0.74.1 (Fri, 27 Mar 2020 14:03:01 +0300)

  *  AUTORUBACK-133 Fix date-time conversion (#490)
     
     * AUTORUBACK-133 Fix date-time conversion
     
     * AUTORUBACK-133 Fix style
  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 27 Mar 2020 14:03:01 +0300

## yandex-vos2-autoru-consumers:0.74.0 (Fri, 27 Mar 2020 13:03:36 +0300)

  *  Autoruback 133 call info to chat (#487)
     
     * AUTORUBACK-133 Refactoring Telepony Consumer; add notification type in proto; up schema-registry version
     
     * AUTORUBACK-133 Extend Passport Client: add searching by phone Number
     
     * AUTORUBACK-133 Refactor publicAPI client; add render for call info
     
     * AUTORUBACK-133 Fix tests; try to calculate ids
     todo:
     - cut number
     - headers?
     - message for old version
     
     * AUTORUBACK-133 Fix according to code review
     todo: headers, check seconds
     
     * AUTORUBACK-133 Add headers for public API
     
     * AUTORUBACK-133 Format date; fix second-milliseconds divergence
     
     * AUTORUBACK-133 Fix according to code review
     
     * AUTORUBACK-133 Add feature call_info_message
     
     * AUTORUBACK-133 Duration as FiniteDuration; add tests;  pretty (and correct) print for duration
     
     * AUTORUBACK-133 Fix according to code review: minor chandes about feature name, logging, simplify code
     
     * AUTORUBACK-133 Fix according to code review: fix test, passport <=> autoru transformation
     
     * AUTORUBACK-133 fix test
     
     * AUTORUBACK-133 Add more feature
     
     * AUTORUBACK-133 Add new method offerChat for Notification
     
     * AUTORUBACK-133 Rename sendMessage... methods + add logging/monitoring for offer message
     
     * AUTORUBACK-133 Fix style
     
     * AUTORUBACK-133 Rename callNotification to sendToOfferChat
     
     Co-authored-by: a-sophie 
  *  AUTORUAPI-6643 sts photo upload (#489)
     
     * AUTORUAPI-6643: sts photo upload
     
     * AUTORUAPI-6643: sts photo upload: added some test
     
     * AUTORUAPI-6643: sts photo upload: updated tests
     
     * AUTORUAPI-6643: sts photo upload: fixed tests
  *  AUTORUAPI-6621 excluded I from valid vin symbols

  *  AUTORUBACK-144 remove tag external_panoramas (#482)
     
     * AUTORUBACK-144 remove tag external_panoramas

  *  AUTORUBACK-134 (#486)
     
     add setting name of mark in OfferMotoInfoConverter and OfferTrucksInfoConverter
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  AUTORUBACK-153 removed credit products save from form to offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 27 Mar 2020 13:03:36 +0300

## yandex-vos2-autoru-consumers:0.73.0 (Fri, 20 Mar 2020 17:43:45 +0300)

  *  AUTORUBACK-153 fixed credit products duplication

  *  AUTORUBACK-149 published as next (#485)
     
     * AUTORUBACK-149 add published panorama
  *  AUTORUBACK-149 add published panorama (#484)
     
     * AUTORUBACK-149 add published panorama
  *  AUTORUBACK-125 add federal subject id to holocron (#481)
     
     * switch version of schema-registry
     
     * add federalSubject in Cars, Extended Cars, Moto, Extended Moto, Trucks, Extended Trucks converters
     
     * change protobuf version
     
     * set regionTree from TestDataEngine in tests
     
     Co-authored-by: Suchkov Denis <suchkovdenis@yandex-team.ru>
  *  fix test

  *  better mds urls

  *  AUTORUAPI-6637 panoramas repair stage (#477)
     
     * AUTORUAPI-6637 hot fix for hidden panoramas
     
     * AUTORUAPI-6637 panoramas repair stage
  *  AUTORUAPI-6637 hot fix for hidden panoramas (#476)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 20 Mar 2020 17:43:45 +0300

## yandex-vos2-autoru-consumers:0.72.1 (Fri, 13 Mar 2020 13:37:58 +0300)

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUSUP-4967 losing original photos: another fix: check namespace before throw exception

  *  AUTORUSUP-4967 losing original photos: updated exception

  *  AUTORUBACK-138 added exclusion for feeds

  *  VSMONEY-1072 reset counters on refresh (#463)
     
     * reset counters on refresh
     
     * check if refresh is active and reset counters with correct now() date
     
     * refactoring
     
     * rename countersStartDate to setCountersStartDate
     
     * Set offer counters based on an activation date
     
     * Tests for Refresh
     
     Co-authored-by: Grigorii Ponomarev <gripon@yandex-team.ru>
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUSUP-4967 losing original photos: unexpected photos error

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 13 Mar 2020 13:37:58 +0300

## yandex-vos2-autoru-consumers:0.72.0 (Fri, 13 Mar 2020 13:24:13 +0300)

  *  AUTORUSUP-4967 losing original photos: updated exception

  *  AUTORUBACK-138 added exclusion for feeds

  *  VSMONEY-1072 reset counters on refresh (#463)
     
     * reset counters on refresh
     
     * check if refresh is active and reset counters with correct now() date
     
     * refactoring
     
     * rename countersStartDate to setCountersStartDate
     
     * Set offer counters based on an activation date
     
     * Tests for Refresh
     
     Co-authored-by: Grigorii Ponomarev <gripon@yandex-team.ru>
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUSUP-4967 losing original photos: unexpected photos error

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 13 Mar 2020 13:24:13 +0300

## yandex-vos2-autoru-consumers:0.71.0 (Thu, 12 Mar 2020 12:49:28 +0300)

  *  AUTORUBACK-100 push for completed panorama (#465)
     
     * AUTORUBACK-100 push for completed panorama
  *  VOS-3284 Do not send notification about licensePlate if offer is inactive (#472)
     
     * VOS-3284 fix render predicate
     
     * VOS-3284 remove unnecessary checks; rf tests

  *  AUTORUBACK-124 (#471)
     
     * AUTORUBACK-124 correct offers data for publishing draft
     
     * AUTORUBACK-124 fix convert panoram from form

  *  VOS-3224 Send to moderation nameplate_front & complectation_id (#470)
     
     * VOS-3224 send to moderation nameplate_front & complectation_id
     
     * VOS-3224 add test
     
     * VOS-3224 remove json-offer from test (fix)

  *  AUTORUBACK-124 correct offers data for publishing draft (#468)
     

  *  VSMONEY-1095 PhoneType=Mobile for offer numbers (#469)
     

  *  AUTORUSUP-4967 losing original photos: fixed tests

  *  AUTORUSUP-4967 losing original photos: fix for moderation photos

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUSUP-4967 losing original photos: added exception and updated logging

  *  AUTORUBACK-104 (#466)
     

  *  AUTORUAPI-6521 add leasing_discount, validate discount options for any but LCV (#464)
     
     * AUTORUAPI-6521 add leasing_discount, validate discount options for any but LCV

  *  CARFAX-607 change vin resolution notifications (#462)
     
     * CARFAX-607 change vin resolution notifications

  *  AUTORUBACK-118 fixed equipment codes duplication

  *  VSMONEY-1028 offer_id to telepony tag for calltracking (#460)
     

  *  New property in poi7 (#459)
     

  *  AUTORUBACK-104 (#458)
     
     * AUTORUBACK-104 fix for draft

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 12 Mar 2020 12:49:28 +0300

## yandex-vos2-autoru-consumers:0.70.2 (Tue, 18 Feb 2020 14:57:00 +0300)

  *  Autoruback 104 (#456)
     
     * AUTORUBACK-104 yt up

  *  AUTORUBACK-104 (#455)
     
     * AUTORUBACK-104 log

  *  AUTORUBACK-104 (#454)
     
     * AUTORUBACK-104 log
  *  fix tests

  *  clean log

  *  AUTORUSUP-4846 fixed license plate update: convert to cyrtillic on update (#453)
     

  *  set dprice fields

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 18 Feb 2020 14:57:00 +0300

## yandex-vos2-autoru-consumers:0.70.1 (Tue, 18 Feb 2020 13:26:43 +0300)

  *  AUTORUBACK-104 (#455)
     
     * AUTORUBACK-104 log

  *  AUTORUBACK-104 (#454)
     
     * AUTORUBACK-104 log
  *  fix tests

  *  clean log

  *  AUTORUSUP-4846 fixed license plate update: convert to cyrtillic on update (#453)
     

  *  set dprice fields

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 18 Feb 2020 13:26:43 +0300

## yandex-vos2-autoru-consumers:0.70.0 (Tue, 18 Feb 2020 13:03:22 +0300)

  *  AUTORUBACK-104 (#454)
     
     * AUTORUBACK-104 log
  *  fix tests

  *  clean log

  *  AUTORUSUP-4846 fixed license plate update: convert to cyrtillic on update (#453)
     

  *  set dprice fields

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 18 Feb 2020 13:03:22 +0300

## yandex-vos2-autoru-consumers:0.69.0 (Thu, 06 Feb 2020 14:16:22 +0300)

  *  AUTORUBACK-75 (#452)
     
     * AUTORUBACK-75 fix unpublished panoramas from feed

  *  AUTORUBACK-75 (#451)
     
     * AUTORUBACK-75 unpublished panoramas from feed
     * AUTORUBACK-75 skip panprramas for form

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 06 Feb 2020 14:16:22 +0300

## yandex-vos2-autoru-consumers:0.68.3 (Mon, 03 Feb 2020 16:11:21 +0300)

  *  AUTORUBACK-75 (#450)
     
     * AUTORUBACK-75 unpublished panoramas from feed

  *  AUTORUBACK-75 (#449)
     
     * AUTORUBACK-75 unpublished panoramas from feed

  *  AUTORUBACK-75 (#448)
     
     * AUTORUBACK-75 unpublished panoramas from feed
     * AUTORUBACK-75 logs

  *  AUTORUBACK-75 unpublished panoramas from feed (#447)
     

  *  AUTORUBACK-67 scheduler sharding (#444)
     
     * AUTORUBACK-67: scheduler sharding, not finished
     
     * AUTORUBACK-67: scheduler sharding
     
     * AUTORUBACK-67: scheduler sharding: pr fixes
     
     * AUTORUBACK-67: scheduler sharding: minor changes

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 03 Feb 2020 16:11:21 +0300

## yandex-vos2-autoru-consumers:0.68.2 (Mon, 03 Feb 2020 15:18:20 +0300)

  *  AUTORUBACK-75 (#449)
     
     * AUTORUBACK-75 unpublished panoramas from feed

  *  AUTORUBACK-75 (#448)
     
     * AUTORUBACK-75 unpublished panoramas from feed
     * AUTORUBACK-75 logs

  *  AUTORUBACK-75 unpublished panoramas from feed (#447)
     

  *  AUTORUBACK-67 scheduler sharding (#444)
     
     * AUTORUBACK-67: scheduler sharding, not finished
     
     * AUTORUBACK-67: scheduler sharding
     
     * AUTORUBACK-67: scheduler sharding: pr fixes
     
     * AUTORUBACK-67: scheduler sharding: minor changes

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 03 Feb 2020 15:18:20 +0300

## yandex-vos2-autoru-consumers:0.68.1 (Mon, 03 Feb 2020 13:41:30 +0300)

  *  AUTORUBACK-75 (#448)
     
     * AUTORUBACK-75 unpublished panoramas from feed
     * AUTORUBACK-75 logs

  *  AUTORUBACK-75 unpublished panoramas from feed (#447)
     

  *  AUTORUBACK-67 scheduler sharding (#444)
     
     * AUTORUBACK-67: scheduler sharding, not finished
     
     * AUTORUBACK-67: scheduler sharding
     
     * AUTORUBACK-67: scheduler sharding: pr fixes
     
     * AUTORUBACK-67: scheduler sharding: minor changes

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 03 Feb 2020 13:41:30 +0300

## yandex-vos2-autoru-consumers:0.68.0 (Mon, 03 Feb 2020 12:29:55 +0300)

  *  AUTORUBACK-75 unpublished panoramas from feed (#447)
     

  *  AUTORUBACK-67 scheduler sharding (#444)
     
     * AUTORUBACK-67: scheduler sharding, not finished
     
     * AUTORUBACK-67: scheduler sharding
     
     * AUTORUBACK-67: scheduler sharding: pr fixes
     
     * AUTORUBACK-67: scheduler sharding: minor changes

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 03 Feb 2020 12:29:55 +0300

## yandex-vos2-autoru-consumers:0.67.5 (Tue, 28 Jan 2020 17:36:00 +0300)

  *  VOS-3272: trucks and moto mark model in notifications: fixed tests

  *  VOS-3272: trucks and moto mark model in unban notifications and notifications about hide without phones

  *  Revert "db cache refactoring, moved to core, not finished"
     
     This reverts commit a325b382

  *  VOS-3280 fixed new price predict client response parsing

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-24 external panorama for idx (#442)
     
     * AUTORUBACK-24 extermal panorama for idx

  *  db cache refactoring, moved to core, not finished

  *  VOS-3271 Fix. Не вставляем марку/модель в смс для комтс/мото после звонка КЦ (#443)
     

  *  VOS-3171 revert previos changes from c5811fcd7fc677c2193ab77cd573e3d067a86a14 … (#441)
     
     * revert previos changes from c5811fcd7fc677c2193ab77cd573e3d067a86a14 and added feature for fast swap between old and new client for prediction
     
     * added 2 pricepredict clients: old and new. use feature for swap it. later you need to remove old client. tests only for new client
     
     * added same tests for old prediction client
     
     * fix requiredParams for new client
     
     * fix review

  *  VOS-3272 [Авто.ру] Начать слать нотификации о бане/разбане мото и комтс (#439)
     
     * VOS-3272 [Авто.ру] Начать слать нотификации о бане/разбане мото и комтс
     
     * FIx

  *  VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ (#437)
     
     * VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ
     
     * Fix trucks
     
     * Fix
     
     * Fix "Unspecified value parameters"
     
     * Fix ModerationBanRenderer creating

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  updated consumers: auto.offset.reset = earliest

  *  AUTORUAPI-6555 handler for list panoramas (#435)
     
     * AUTORUAPI-6555 handler for list panoramas

  *  updated consumers: do not commit offsets if skip records processing due to feature disabled

  *  increased zio session acquire timeout

  *  fix flaky test

  *  fix flaky test

  *  update ydb & zio versions (#402)
     

  *  VOS-3278 allow unknown equipment in drafts: generate notices and remove them, added test
     VOS-3265: license plate moderation protection fix: added test

  *  VOS-3265 licenseplate moderation protection fix: check licenseplates from offer and form both in upper case

  *  AUTORUAPI-6567 handler for add external panorama (#434)
     
     * AUTORUAPI-6567 handler for add and delete external panorama

  *  AUTORUAPI-6556 (#433)
     
     * AUTORUAPI-6556 fix publishedAt and clean logs

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 28 Jan 2020 17:36:00 +0300

## yandex-vos2-autoru-consumers:0.67.4 (Tue, 28 Jan 2020 16:39:26 +0300)

  *  VOS-3272: trucks and moto mark model in notifications: fixed tests

  *  VOS-3272: trucks and moto mark model in unban notifications and notifications about hide without phones

  *  Revert "db cache refactoring, moved to core, not finished"
     
     This reverts commit a325b382

  *  VOS-3280 fixed new price predict client response parsing

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUBACK-24 external panorama for idx (#442)
     
     * AUTORUBACK-24 extermal panorama for idx

  *  db cache refactoring, moved to core, not finished

  *  VOS-3271 Fix. Не вставляем марку/модель в смс для комтс/мото после звонка КЦ (#443)
     

  *  VOS-3171 revert previos changes from c5811fcd7fc677c2193ab77cd573e3d067a86a14 … (#441)
     
     * revert previos changes from c5811fcd7fc677c2193ab77cd573e3d067a86a14 and added feature for fast swap between old and new client for prediction
     
     * added 2 pricepredict clients: old and new. use feature for swap it. later you need to remove old client. tests only for new client
     
     * added same tests for old prediction client
     
     * fix requiredParams for new client
     
     * fix review

  *  VOS-3272 [Авто.ру] Начать слать нотификации о бане/разбане мото и комтс (#439)
     
     * VOS-3272 [Авто.ру] Начать слать нотификации о бане/разбане мото и комтс
     
     * FIx

  *  VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ (#437)
     
     * VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ
     
     * Fix trucks
     
     * Fix
     
     * Fix "Unspecified value parameters"
     
     * Fix ModerationBanRenderer creating

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  updated consumers: auto.offset.reset = earliest

  *  AUTORUAPI-6555 handler for list panoramas (#435)
     
     * AUTORUAPI-6555 handler for list panoramas

  *  updated consumers: do not commit offsets if skip records processing due to feature disabled

  *  increased zio session acquire timeout

  *  fix flaky test

  *  fix flaky test

  *  update ydb & zio versions (#402)
     

  *  VOS-3278 allow unknown equipment in drafts: generate notices and remove them, added test
     VOS-3265: license plate moderation protection fix: added test

  *  VOS-3265 licenseplate moderation protection fix: check licenseplates from offer and form both in upper case

  *  AUTORUAPI-6567 handler for add external panorama (#434)
     
     * AUTORUAPI-6567 handler for add and delete external panorama

  *  AUTORUAPI-6556 (#433)
     
     * AUTORUAPI-6556 fix publishedAt and clean logs

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 28 Jan 2020 16:39:26 +0300

## yandex-vos2-autoru-consumers:0.67.3 (Fri, 17 Jan 2020 19:48:36 +0300)

  *  VOS-3271 Fix. Не вставляем марку/модель в смс для комтс/мото после звонка КЦ (#443)
     

  *  VOS-3171 revert previos changes from c5811fcd7fc677c2193ab77cd573e3d067a86a14 … (#441)
     
     * revert previos changes from c5811fcd7fc677c2193ab77cd573e3d067a86a14 and added feature for fast swap between old and new client for prediction
     
     * added 2 pricepredict clients: old and new. use feature for swap it. later you need to remove old client. tests only for new client
     
     * added same tests for old prediction client
     
     * fix requiredParams for new client
     
     * fix review

  *  VOS-3272 [Авто.ру] Начать слать нотификации о бане/разбане мото и комтс (#439)
     
     * VOS-3272 [Авто.ру] Начать слать нотификации о бане/разбане мото и комтс
     
     * FIx

  *  VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ (#437)
     
     * VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ
     
     * Fix trucks
     
     * Fix
     
     * Fix "Unspecified value parameters"
     
     * Fix ModerationBanRenderer creating

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  updated consumers: auto.offset.reset = earliest

  *  AUTORUAPI-6555 handler for list panoramas (#435)
     
     * AUTORUAPI-6555 handler for list panoramas

  *  updated consumers: do not commit offsets if skip records processing due to feature disabled

  *  increased zio session acquire timeout

  *  fix flaky test

  *  fix flaky test

  *  update ydb & zio versions (#402)
     

  *  VOS-3278 allow unknown equipment in drafts: generate notices and remove them, added test
     VOS-3265: license plate moderation protection fix: added test

  *  VOS-3265 licenseplate moderation protection fix: check licenseplates from offer and form both in upper case

  *  AUTORUAPI-6567 handler for add external panorama (#434)
     
     * AUTORUAPI-6567 handler for add and delete external panorama

  *  AUTORUAPI-6556 (#433)
     
     * AUTORUAPI-6556 fix publishedAt and clean logs

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 17 Jan 2020 19:48:36 +0300

## yandex-vos2-autoru-consumers:0.67.2 (Fri, 17 Jan 2020 16:51:20 +0300)

  *  VOS-3271 Fix. Не вставляем марку/модель в смс для комтс/мото после звонка КЦ (#443)
     

  *  VOS-3171 revert previos changes from c5811fcd7fc677c2193ab77cd573e3d067a86a14 … (#441)
     
     * revert previos changes from c5811fcd7fc677c2193ab77cd573e3d067a86a14 and added feature for fast swap between old and new client for prediction
     
     * added 2 pricepredict clients: old and new. use feature for swap it. later you need to remove old client. tests only for new client
     
     * added same tests for old prediction client
     
     * fix requiredParams for new client
     
     * fix review

  *  VOS-3272 [Авто.ру] Начать слать нотификации о бане/разбане мото и комтс (#439)
     
     * VOS-3272 [Авто.ру] Начать слать нотификации о бане/разбане мото и комтс
     
     * FIx

  *  VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ (#437)
     
     * VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ
     
     * Fix trucks
     
     * Fix
     
     * Fix "Unspecified value parameters"
     
     * Fix ModerationBanRenderer creating

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  updated consumers: auto.offset.reset = earliest

  *  AUTORUAPI-6555 handler for list panoramas (#435)
     
     * AUTORUAPI-6555 handler for list panoramas

  *  updated consumers: do not commit offsets if skip records processing due to feature disabled

  *  increased zio session acquire timeout

  *  fix flaky test

  *  fix flaky test

  *  update ydb & zio versions (#402)
     

  *  VOS-3278 allow unknown equipment in drafts: generate notices and remove them, added test
     VOS-3265: license plate moderation protection fix: added test

  *  VOS-3265 licenseplate moderation protection fix: check licenseplates from offer and form both in upper case

  *  AUTORUAPI-6567 handler for add external panorama (#434)
     
     * AUTORUAPI-6567 handler for add and delete external panorama

  *  AUTORUAPI-6556 (#433)
     
     * AUTORUAPI-6556 fix publishedAt and clean logs

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 17 Jan 2020 16:51:20 +0300

## yandex-vos2-autoru-consumers:0.67.1 (Wed, 15 Jan 2020 20:08:24 +0300)

  *  VOS-3272 [Авто.ру] Начать слать нотификации о бане/разбане мото и комтс (#439)
     
     * VOS-3272 [Авто.ру] Начать слать нотификации о бане/разбане мото и комтс
     
     * FIx

  *  VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ (#437)
     
     * VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ
     
     * Fix trucks
     
     * Fix
     
     * Fix "Unspecified value parameters"
     
     * Fix ModerationBanRenderer creating

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  updated consumers: auto.offset.reset = earliest

  *  AUTORUAPI-6555 handler for list panoramas (#435)
     
     * AUTORUAPI-6555 handler for list panoramas

  *  updated consumers: do not commit offsets if skip records processing due to feature disabled

  *  increased zio session acquire timeout

  *  fix flaky test

  *  fix flaky test

  *  update ydb & zio versions (#402)
     

  *  VOS-3278 allow unknown equipment in drafts: generate notices and remove them, added test
     VOS-3265: license plate moderation protection fix: added test

  *  VOS-3265 licenseplate moderation protection fix: check licenseplates from offer and form both in upper case

  *  AUTORUAPI-6567 handler for add external panorama (#434)
     
     * AUTORUAPI-6567 handler for add and delete external panorama

  *  AUTORUAPI-6556 (#433)
     
     * AUTORUAPI-6556 fix publishedAt and clean logs

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 15 Jan 2020 20:08:24 +0300

## yandex-vos2-autoru-consumers:0.67.0 (Wed, 15 Jan 2020 15:25:14 +0300)

  *  VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ (#437)
     
     * VOS-3271 Не вставляем марку/модель в смс для комтс/мото после звонка КЦ
     
     * Fix trucks
     
     * Fix
     
     * Fix "Unspecified value parameters"
     
     * Fix ModerationBanRenderer creating

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  updated consumers: auto.offset.reset = earliest

  *  AUTORUAPI-6555 handler for list panoramas (#435)
     
     * AUTORUAPI-6555 handler for list panoramas

  *  updated consumers: do not commit offsets if skip records processing due to feature disabled

  *  increased zio session acquire timeout

  *  fix flaky test

  *  fix flaky test

  *  update ydb & zio versions (#402)
     

  *  VOS-3278 allow unknown equipment in drafts: generate notices and remove them, added test
     VOS-3265: license plate moderation protection fix: added test

  *  VOS-3265 licenseplate moderation protection fix: check licenseplates from offer and form both in upper case

  *  AUTORUAPI-6567 handler for add external panorama (#434)
     
     * AUTORUAPI-6567 handler for add and delete external panorama

  *  AUTORUAPI-6556 (#433)
     
     * AUTORUAPI-6556 fix publishedAt and clean logs

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 15 Jan 2020 15:25:14 +0300

## yandex-vos2-autoru-consumers:0.66.7 (Wed, 25 Dec 2019 16:24:37 +0300)
  *  AUTORUAPI-6556 logs
  *  Update CHANGELOG.md
  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#430)
  *  AUTORUAPI-6556 (#429)
  *  Deleted default sorting (#428)
  *  AUTORUAPI-6556 (#424)
  *  VOS-3276 Fix: [moderation] Подгонять забывчивых юзеров пушами и смс (#426)
  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#425)
  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#422)
  *  VSMONEY-594: get zero value too (#423)

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 25 Dec 2019 16:24:37 +0300

## yandex-vos2-autoru-consumers:0.66.6 (Wed, 25 Dec 2019 16:12:30 +0300)

  *  Update CHANGELOG.md
  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#430)
     

  *  AUTORUAPI-6556 (#429)
     
     * AUTORUAPI-6556 test & fix

  *  Deleted default sorting (#428)
     

  *  AUTORUAPI-6556 (#424)
     
     * AUTORUAPI-6556 add new panorama
     

  *  VOS-3276 Fix: [moderation] Подгонять забывчивых юзеров пушами и смс (#426)
     
     * VOS-3276 Fix: [moderation] Подгонять забывчивых юзеров пушами и смс
     
     * Fix condition

  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#425)
     

  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#422)
     
     * VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс
     
     * Remove autors
     
     * Fix timestamp
     
     * Fix unaply
     
     * FIx testts
     
     * update json from bunker
     
     * Исправления по ревью
     
     * Fix: "Первый раз шлём и смс, и пуш"
     
     * Try to fix linter (remove tabs from json)
     
     * Add features
     
     * Fix feature
     
     * Исправления по ревью
     
     * Fix reminders renders create
     
     * Try to fix tests
     
     * Fix scheduled send time
     
     * Format Seq
     
     * Fix conditions
     
     * Исправления
     
     * Fix timeToSend
     
     * Еще немного исправлений
     
     * Fix YDB back
     
     * Поправил чуток
     
     * minSentAtInFuture (опечатка)

  *  VSMONEY-594: get zero value too (#423)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 25 Dec 2019 16:12:30 +0300

## yandex-vos2-autoru-consumers:0.66.5 (Wed, 25 Dec 2019 13:05:41 +0300)

  *  Fake release
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 25 Dec 2019 13:05:41 +0300
 
 ## yandex-vos2-autoru-consumers:0.66.3 (Wed, 25 Dec 2019 13:05:41 +0300)

  *  AUTORUAPI-6556 (#424)
     
     * AUTORUAPI-6556 add new panorama
     

  *  VOS-3276 Fix: [moderation] Подгонять забывчивых юзеров пушами и смс (#426)
     
     * VOS-3276 Fix: [moderation] Подгонять забывчивых юзеров пушами и смс
     
     * Fix condition

  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#425)
     

  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#422)
     
     * VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс
     
     * Remove autors
     
     * Fix timestamp
     
     * Fix unaply
     
     * FIx testts
     
     * update json from bunker
     
     * Исправления по ревью
     
     * Fix: "Первый раз шлём и смс, и пуш"
     
     * Try to fix linter (remove tabs from json)
     
     * Add features
     
     * Fix feature
     
     * Исправления по ревью
     
     * Fix reminders renders create
     
     * Try to fix tests
     
     * Fix scheduled send time
     
     * Format Seq
     
     * Fix conditions
     
     * Исправления
     
     * Fix timeToSend
     
     * Еще немного исправлений
     
     * Fix YDB back
     
     * Поправил чуток
     
     * minSentAtInFuture (опечатка)

  *  VSMONEY-594: get zero value too (#423)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 25 Dec 2019 13:05:41 +0300

## yandex-vos2-autoru-consumers:0.66.2 (Tue, 24 Dec 2019 17:16:26 +0300)

  *  AUTORUAPI-6556 (#424)
     
     * AUTORUAPI-6556 add new panorama
     

  *  VOS-3276 Fix: [moderation] Подгонять забывчивых юзеров пушами и смс (#426)
     
     * VOS-3276 Fix: [moderation] Подгонять забывчивых юзеров пушами и смс
     
     * Fix condition

  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#425)
     

  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#422)
     
     * VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс
     
     * Remove autors
     
     * Fix timestamp
     
     * Fix unaply
     
     * FIx testts
     
     * update json from bunker
     
     * Исправления по ревью
     
     * Fix: "Первый раз шлём и смс, и пуш"
     
     * Try to fix linter (remove tabs from json)
     
     * Add features
     
     * Fix feature
     
     * Исправления по ревью
     
     * Fix reminders renders create
     
     * Try to fix tests
     
     * Fix scheduled send time
     
     * Format Seq
     
     * Fix conditions
     
     * Исправления
     
     * Fix timeToSend
     
     * Еще немного исправлений
     
     * Fix YDB back
     
     * Поправил чуток
     
     * minSentAtInFuture (опечатка)

  *  VSMONEY-594: get zero value too (#423)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 24 Dec 2019 17:16:26 +0300

## yandex-vos2-autoru-consumers:0.66.1 (Tue, 24 Dec 2019 13:51:59 +0300)

  *  VOS-3276 Fix: [moderation] Подгонять забывчивых юзеров пушами и смс (#426)
     
     * VOS-3276 Fix: [moderation] Подгонять забывчивых юзеров пушами и смс
     
     * Fix condition

  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#425)
     

  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#422)
     
     * VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс
     
     * Remove autors
     
     * Fix timestamp
     
     * Fix unaply
     
     * FIx testts
     
     * update json from bunker
     
     * Исправления по ревью
     
     * Fix: "Первый раз шлём и смс, и пуш"
     
     * Try to fix linter (remove tabs from json)
     
     * Add features
     
     * Fix feature
     
     * Исправления по ревью
     
     * Fix reminders renders create
     
     * Try to fix tests
     
     * Fix scheduled send time
     
     * Format Seq
     
     * Fix conditions
     
     * Исправления
     
     * Fix timeToSend
     
     * Еще немного исправлений
     
     * Fix YDB back
     
     * Поправил чуток
     
     * minSentAtInFuture (опечатка)

  *  VSMONEY-594: get zero value too (#423)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 24 Dec 2019 13:51:59 +0300

## yandex-vos2-autoru-consumers:0.66.0 (Tue, 24 Dec 2019 13:20:43 +0300)

  *  VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс (#422)
     
     * VOS-3276 [moderation] Подгонять забывчивых юзеров пушами и смс
     
     * Remove autors
     
     * Fix timestamp
     
     * Fix unaply
     
     * FIx testts
     
     * update json from bunker
     
     * Исправления по ревью
     
     * Fix: "Первый раз шлём и смс, и пуш"
     
     * Try to fix linter (remove tabs from json)
     
     * Add features
     
     * Fix feature
     
     * Исправления по ревью
     
     * Fix reminders renders create
     
     * Try to fix tests
     
     * Fix scheduled send time
     
     * Format Seq
     
     * Fix conditions
     
     * Исправления
     
     * Fix timeToSend
     
     * Еще немного исправлений
     
     * Fix YDB back
     
     * Поправил чуток
     
     * minSentAtInFuture (опечатка)

  *  VSMONEY-594: get zero value too (#423)
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 24 Dec 2019 13:20:43 +0300

## yandex-vos2-autoru-consumers:0.65.1 (Fri, 20 Dec 2019 14:32:54 +0300)

  *  disable compression with mysql

  *  Vsmoney 594 conversion sort (#418)
     
     * VSMONEY-594: conversion index
     
     * VSMONEY-594: conversion sort
     
     * VSMONEY-594: conversion -> cars_view_phone_show_conversion; phone_shows -> phone_show
     
     * VSMONEY-594: fix typo cars -> card
     
     * VSMONEY-594: endpoint for card_view_phone_show_conversion values
     
     * VSMONEY-594: review fixes
     
     * VSMONEY-594: review fix - use index table only
     
     * Revert "VSMONEY-594: review fix - use index table only"
     
     This reverts commit 02b0454fc5c1f4afa420148550e98adcc07fec5a.
     
     * Revert "VSMONEY-594: endpoint for card_view_phone_show_conversion values"
     
     This reverts commit 67fa1a68ee6f8b8dc030ff961dd3e391ae005e68.
     
     * VSMONEY-594: add conversion to response

  *  AUTORUAPI-6382 with_nds: fixed logic, fixed test

  *  VSMONEY-593: fetch conversion-related values from Statist (#416)
     
     * VSMONEY-593: fetch conversion-related values from Statist
     
     * VSMONEY-593: review fixes; client response parsing fix
     
     * release 0.204.2

  *  removed verba problems sender

  *  AUTORUAPI-6538 added autoru_exclusive_verified flag to full holocron cars model

  *  holocron validation: minor fixes

  *  VOS2 Scala 2.12 major version (#415)
     
     * Scala 2.12 major version
     
     * Update pom.xml
     
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  VSDATA-268: added typeKey conversion to extended holocron moto converter

  *  VOS-3240 commons sentry (#414)
     
     * Using commons sentry
     
     * Fixed dns string

  *  AUTORUAPI-6382 allow nds for privates in CARS

  *  AUTORUBACK-11 updated HttpChatClient.serviceNotification: TEXT_HTML

  *  switching to registry.yandex.net

  *  AUTORUAPI-6541 fixed license plate numbers recognition for dealers (#413)
     
     * AUTORUAPI-6541 fixed license plate numbers recognition for dealers, refactoring
     
     * AUTORUAPI-6541 fixed license plate numbers recognition for dealers: pr fixes

  *  VOS-3245 akka http (#384)
     
     * Added new utils handlers
     
     * OfferConvertHandler + matchersUtils
     
     * Clean up pingHandler
     
     * Added new v0 handler
     
     * Added utils facade
     
     * Draft manager
     
     * V1 handlers without actors
     
     * Added some model changes for inner responses and requests of api + added partitionHandler
     
     * Created and refactored api managers
     
     * Deleted partitioning handling
     
     * little code fixes
     
     * Added offersHandler
     
     * ModerationHandler and root
     
     * Added last handlers + swagger
     
     * Added some infrustructure for start using akka-http
     
     * Deleted old infrustructure in api
     
     * deleted spray from vos-core
     
     * Deleted spray from whole code + deleted NEW prefixes from classes that was rewritten using akka-http
     
     * api tests
     
     * Fix some tests
     
     * Fix some tests #2
     
     * Updated to commons 2+, used custom protobufsupport and fixed some tests
     
     * Using commons TracingSupport and directives + fixes
     
     * Changed mdc support + more fixing
     
     * Fixed new mdc support
     
     * Fixing swagger and consumers startup
     
     * Fixed last tests
     
     * fixed fixes
     
     * Fixes
     
     * Deleted redudant directive
     
     * executioner queue & added RejectedExecutionException handler
     
     * Fixing swagger

  *  Revert "VOS-3171 change prediction api host (#328)" (#412)
     
     This reverts commit e4e5003d7302abecd9cec2011d6acc21a602b46d.
  *  updated holocron validation logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 20 Dec 2019 14:32:54 +0300

## yandex-vos2-autoru-consumers:0.65.0 (Mon, 09 Dec 2019 18:29:53 +0300)

  *  VOS-3245 akka http (#384)
     
     * Added new utils handlers
     
     * OfferConvertHandler + matchersUtils
     
     * Clean up pingHandler
     
     * Added new v0 handler
     
     * Added utils facade
     
     * Draft manager
     
     * V1 handlers without actors
     
     * Added some model changes for inner responses and requests of api + added partitionHandler
     
     * Created and refactored api managers
     
     * Deleted partitioning handling
     
     * little code fixes
     
     * Added offersHandler
     
     * ModerationHandler and root
     
     * Added last handlers + swagger
     
     * Added some infrustructure for start using akka-http
     
     * Deleted old infrustructure in api
     
     * deleted spray from vos-core
     
     * Deleted spray from whole code + deleted NEW prefixes from classes that was rewritten using akka-http
     
     * api tests
     
     * Fix some tests
     
     * Fix some tests #2
     
     * Updated to commons 2+, used custom protobufsupport and fixed some tests
     
     * Using commons TracingSupport and directives + fixes
     
     * Changed mdc support + more fixing
     
     * Fixed new mdc support
     
     * Fixing swagger and consumers startup
     
     * Fixed last tests
     
     * fixed fixes
     
     * Fixes
     
     * Deleted redudant directive
     
     * executioner queue & added RejectedExecutionException handler
     
     * Fixing swagger

  *  Revert "VOS-3171 change prediction api host (#328)" (#412)
     
     This reverts commit e4e5003d7302abecd9cec2011d6acc21a602b46d.
  *  updated holocron validation logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 09 Dec 2019 18:29:53 +0300

## yandex-vos2-autoru-consumers:0.64.0 (Tue, 03 Dec 2019 18:27:01 +0300)

  *  VOS-3005 (#411)
     
     * VOS-3005 fix moto converter
  *  Vsdata 268 holocron moto comtrans converters (#397)
     
     * VSDATA-268: holocron moto comtrans converters: refactoring
     
     * VSDATA-268: holocron moto comtrans converters: simple converters
     
     * VSDATA-268: holocron moto comtrans converters: fixed simple converters
     
     * VSDATA-268: holocron moto comtrans converters: fixed simple converters
     
     * VSDATA-268: holocron moto comtrans converters: moto extended converter
     
     * VSDATA-268: holocron moto comtrans converters: removed certification set
     
     * VSDATA-268: holocron moto comtrans converters: trucks extended holocron converter
     
     * VSDATA-268: holocron moto comtrans converters: refactoring
     
     * VSDATA-268: holocron moto comtrans converters: cars converter refactoring
     
     * VSDATA-268: holocron moto comtrans converters: extended converters refactoring
     
     * VSDATA-268: holocron moto comtrans converters: send moto and comtrans data
     
     * VSDATA-268: holocron moto comtrans converters: removed HolocronSendData, fixed test
     
     * VSDATA-268: holocron moto comtrans converters: fixed compilation
     
     * VSDATA-268: holocron moto comtrans converters: fixed tests
     
     * VSDATA-268: holocron moto comtrans converters: refactoring, updated stage test, added trucks converter test
     
     * VSDATA-268: holocron moto comtrans converters: updated  trucks converter test, added moto converter test
     
     * VSDATA-268: holocron moto comtrans converters: updated tests, updated stage: always send extended model, updated stage test
     
     * VSDATA-268: holocron moto comtrans converters: added tests
     
     * VSDATA-268: holocron moto comtrans converters: added more category checks to stage, added features, updated tests
     
     * VSDATA-268: holocron moto comtrans converters: topics test
     
     * KafkaUtils refactoring
     
     * KafkaUtils refactoring
     
     * VSDATA-268: holocron moto comtrans converters: refactoring
     
     * VSDATA-268: holocron moto comtrans converters: set customs status
     
     * KafkaUtils refactoring
     
     * VSDATA-268: holocron moto comtrans converters: test refactoring
     
     * VSDATA-268: holocron moto comtrans converters: tests refactoring
     
     * VSDATA-268: holocron moto comtrans converters: tests refactoring: fixture

  *  Vos 3005 remove used  mark, model from old db  (#42)
     
     * VOS-3005 remove used  mark, model from old db

  *  VOS-3171 change prediction api host (#328)
     

  *  fix test env provider

  *  AUTO-11219 Send TeleponyInfo to indexer (#405)
     
     Нам нужна TeleponyInfo для того чтобы положить ее в CarAd индекс и потом в ЕДС в дилер-фетчере сходить в телепони за актуальным подменником
     
     У нас тут, в этой же самой точке, уже есть инфа по подменникам (в message Redirect) но эти номера могут протухнуть когда мы доберемся до фетчера, так что нам нет смысла передавать их в индексер

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 03 Dec 2019 18:27:01 +0300

## yandex-vos2-autoru-consumers:0.63.0 (Fri, 29 Nov 2019 17:38:21 +0300)

  *  VSMONEY-568: add equipment codes from Verba (#408)
     

  *  AUTORUAPI-6514 (#406)
     
     * AUTORUAPI-6514 save version panoramas

  *  AUTORUAPI-6514 save version panoramas (#404)
     
     * AUTORUAPI-6514 save version panoramas

  *  VOS-3250 add drafts cleaner (#396)
     
     

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 29 Nov 2019 17:38:21 +0300

## yandex-vos2-autoru-consumers:0.62.0 (Thu, 28 Nov 2019 14:20:28 +0300)

  *  AUTORUAPI-6515 remove doppel clusters and autoru_exclusive_verified for offers from section=new
     process non-exclusive offers with enough_data=false

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 28 Nov 2019 14:20:28 +0300

## yandex-vos2-autoru-consumers:0.61.0 (Thu, 28 Nov 2019 13:23:56 +0300)

  *  AUTORUAPI-6437 doppel clusters size fix (#401)
     

  *  discount price and options in cars extended holocron converter

  *  AUTORUAPI-6444 change minibus translation (#400)
     

  *  AUTORUAPI-6489 field preview (#398)
     
     * AUTORUAPI-6489 field preview

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 28 Nov 2019 13:23:56 +0300

## yandex-vos2-autoru-consumers:0.60.2 (Fri, 22 Nov 2019 19:16:44 +0300)

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: fixed migration again

  *  AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: fixed migration

  *  AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka (#393)
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: updated logging
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: check active status
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: enough data counter
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: updated results counter
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: save clusters to protobuf, refactoring
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: update data for all vos offers in cluster, added to launcher, refactoring
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: history limit
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: main id instead of key
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: fixed processing

  *  VOS-3032 telepony calls consumer: minor changes

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 22 Nov 2019 19:16:44 +0300

## yandex-vos2-autoru-consumers:0.60.1 (Fri, 22 Nov 2019 18:38:49 +0300)

  *  AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: fixed migration

  *  AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka (#393)
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: updated logging
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: check active status
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: enough data counter
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: updated results counter
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: save clusters to protobuf, refactoring
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: update data for all vos offers in cluster, added to launcher, refactoring
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: history limit
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: main id instead of key
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: fixed processing

  *  VOS-3032 telepony calls consumer: minor changes

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 22 Nov 2019 18:38:49 +0300

## yandex-vos2-autoru-consumers:0.60.0 (Fri, 22 Nov 2019 13:53:52 +0300)

  *  AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka (#393)
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: updated logging
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: check active status
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: enough data counter
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: updated results counter
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: save clusters to protobuf, refactoring
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: update data for all vos offers in cluster, added to launcher, refactoring
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: history limit
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: main id instead of key
     
     * AUTORUAPI-6437: autoru exclusive: doppel clusters from kafka: fixed processing

  *  VOS-3032 telepony calls consumer: minor changes

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 22 Nov 2019 13:53:52 +0300

## yandex-vos2-autoru-consumers:0.59.4 (Wed, 20 Nov 2019 16:44:27 +0300)

  *  VOS-3032 telepony topic (#390)
     
     * VOS-3032 telepony calls consumer
     
     * VOS-3032 telepony calls consumer: added engine, added feature
     
     * VOS-3032 telepony calls consumer: disabled PhoneCallLoader on feature
     
     * VOS-3032 telepony calls consumer: added metrics
     
     * VOS-3032 telepony calls consumer: pr fixes
     
     * VOS-3032 telepony calls consumer: pr fixes

  *  AUTORUAPI-6444 add new bodytypes (#391)
     
     * AUTORUAPI-6444 add new bodytypes
     
     * Update vos2-core/src/main/proto/autoru/autoru_model.proto
     
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>

  *  CARFAX-267: use separate sender templates (#392)
     
     * CARFAX-267: use separate sender templates (has history / without history)for good resolution arrival event

  *  AUTORUAPI-6225 Fix. Отправка писем для подтверждения мэйлов (#356)
     

  *  remove reseller flag from user

  *  VOS-3236 disable actions.can_edit for resellers

  *  bump changelog

  *  VOS-3236 unpaid reseller offer edit: added isModerator check (#348)
     

  *  VOS-3259 [auto] Секреты в репозитории (#382)
     

  *  VOS-3266 Сделать ручку в VOS для сохранения OfferBilling внутри Offer (#388)
     

  *  AUTORUAPI-6437: autoru exclusive: always verified feature: for tests (#389)
     
     * AUTORUAPI-6437: autoru exclusive: always verified feature: for tests
     
     * AUTORUAPI-6437: autoru exclusive: fixed compilation

  *  AUTO-11237 Add PanoramaAutoru to IdxStage (#386)
     
     * AUTO-11237 Add PanoramaAutoru to IdxStage
     
     * Remove unused import

  *  VOS-3263 ignore malformed work hours

  *  AUTORUAPI-6437 autoru_exclusive flags in vos (#379)
     
     * AUTORUAPI-6437 autoru_exclusive flags in vos
     
     * AUTORUAPI-6437 autoru_exclusive flags in vos: updated converters
     
     * AUTORUAPI-6437 autoru_exclusive flags in vos: stage
     
     * AUTORUAPI-6437 autoru_exclusive -> accepted_autoru_exclusive
     
     * AUTORUAPI-6437 autoru_exclusive flags in vos: stage refactoring
     
     * AUTORUAPI-6437 autoru_exclusive flags in vos: updated schema-registry version

  *  AUTORUAPI-6428 (#381)
     
     * AUTORUAPI-6428 panoramas stage
  *  AUTORUAPI-6428 (#380)
     
     * AUTORUAPI-6428 panoramas stage

  *  VOS-3250 api to read all drafts (#354)
     

  *  AUTORUAPI-6428 panoramas (#378)
     
     * AUTORUAPI-6428 panoramas stage
  *  remove debug logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 20 Nov 2019 16:44:27 +0300

## yandex-vos2-autoru-consumers:0.59.3 (Thu, 14 Nov 2019 17:07:18 +0300)

  *  bump changelog

  *  VOS-3236 unpaid reseller offer edit: added isModerator check (#348)
     

  *  VOS-3259 [auto] Секреты в репозитории (#382)
     

  *  VOS-3266 Сделать ручку в VOS для сохранения OfferBilling внутри Offer (#388)
     

  *  AUTORUAPI-6437: autoru exclusive: always verified feature: for tests (#389)
     
     * AUTORUAPI-6437: autoru exclusive: always verified feature: for tests
     
     * AUTORUAPI-6437: autoru exclusive: fixed compilation

  *  AUTO-11237 Add PanoramaAutoru to IdxStage (#386)
     
     * AUTO-11237 Add PanoramaAutoru to IdxStage
     
     * Remove unused import

  *  VOS-3263 ignore malformed work hours

  *  AUTORUAPI-6437 autoru_exclusive flags in vos (#379)
     
     * AUTORUAPI-6437 autoru_exclusive flags in vos
     
     * AUTORUAPI-6437 autoru_exclusive flags in vos: updated converters
     
     * AUTORUAPI-6437 autoru_exclusive flags in vos: stage
     
     * AUTORUAPI-6437 autoru_exclusive -> accepted_autoru_exclusive
     
     * AUTORUAPI-6437 autoru_exclusive flags in vos: stage refactoring
     
     * AUTORUAPI-6437 autoru_exclusive flags in vos: updated schema-registry version

  *  AUTORUAPI-6428 (#381)
     
     * AUTORUAPI-6428 panoramas stage
  *  AUTORUAPI-6428 (#380)
     
     * AUTORUAPI-6428 panoramas stage

  *  VOS-3250 api to read all drafts (#354)
     

  *  AUTORUAPI-6428 panoramas (#378)
     
     * AUTORUAPI-6428 panoramas stage
  *  remove debug logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 14 Nov 2019 17:07:18 +0300

## yandex-vos2-autoru-consumers:0.59.2 (Fri, 01 Nov 2019 18:21:40 +0300)
## yandex-vos2-autoru-consumers:0.59.1 (Fri, 01 Nov 2019 18:21:40 +0300)

  *  AUTORUAPI-6428 (#380)
     
     * AUTORUAPI-6428 panoramas stage

  *  VOS-3250 api to read all drafts (#354)
     

  *  AUTORUAPI-6428 panoramas (#378)
     
     * AUTORUAPI-6428 panoramas stage
  *  remove debug logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 01 Nov 2019 18:21:40 +0300

## yandex-vos2-autoru-consumers:0.59.0 (Fri, 01 Nov 2019 13:37:26 +0300)

  *  AUTORUAPI-6428 panoramas (#378)
     
     * AUTORUAPI-6428 panoramas stage
  *  remove debug logging

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 01 Nov 2019 13:37:26 +0300

## yandex-vos2-autoru-consumers:0.58.0 (Mon, 28 Oct 2019 19:27:27 +0300)

  *  VOS-3012 using common features (#372)
     
     * Using common features in autoru-core and autoru-api
     
     * Using common features in autoru-consumers
     
     * Using common features in autoru-scheduler
     
     * Using common features in autoru-workers
     
     * Using common features in autoru-mirror and a little bit more
     
     * Deleted old features
     
     * Fixing tests because of merge
     
     * fix tests
     
     * Created method for changing CategoryFeature value
     
     * pending teleperformance test

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 28 Oct 2019 19:27:27 +0300

## yandex-vos2-autoru-consumers:0.57.1 (Thu, 24 Oct 2019 17:14:34 +0300)

  *  Vos 3255 (#374)
     
     * VOS-3255 fix review
  *  AUTORUAPI-6381 withNds: updated micro-core and converters to send new field to indexer

  *  VOS-3248: pass vin resolution hiding reason (#369)
     
     * VOS-3248: pass vin resolution hiding reason
     
     * review fixes

  *  Vos 3255 fix moderation protection fields (#373)
     
     * VOS-3255 fix protected form
     
     * VOS-3255 test

  *  VOS-3012 fix features api (#371)
     
     * not so lazy features manager
     
     * Temporary test fix
     
     * fixed tests again!
     
     * Added features api fix
     
     * cleanup
     
     * Fix test entity type

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUAPI-6381 withNds: fixed converter, added tests

  *  not so lazy features manager (#368)
     

  *  Ydb session create timeout (#367)
     
     * raised timeout
     
     * raised timeout #2

  *  raised timeout (#366)
     

  *  AUTORUAPI-6382 with nds flag (#364)
     
     * AUTORUAPI-6382 with nds flag
     
     * AUTORUAPI-6382 with nds flag: updated converters
     
     * AUTORUAPI-6381 withNds = true if not set in NEW comtrans
     
     * AUTORUAPI-6381 withNds: fixed validation: forbidden to offer price with nds for private users in non-trucks categories, set withNds to true for new trucks for all kinds of users

  *  VOS-3012 adding common features (#365)
     
     * Added common-feature support
     
     * Added features duplicates
     
     * Fixing dependencies for tests
     
     * Fixing more tests
     
     * Delete useless code
     
     * little fixes
     
     * Added vos features with generation
     
     * Added test & fixed some code
     
     * delete useless manipulation
     
     * Fixed tests
     
     * Deleted implicit size
     
     * deleted useless imports

  *  VOS_3213 init ydb on start (#362)
     
     * Deleted lazy modificator from all places with ydb init
     
     * Fixing tests
     
     * Using force initialization
     
     * Added sessions pool init
     
     * fixed initSessionsPool use
     
     * Using existing runtime
     
     * Ydb force init

  *  AUTORUAPI-5325 added cabinet platform (#361)
     
     * Added cabinet platform
     
     * source fix
     
     * With fixing schema registry

  *  VSMONEY-141 # FIX calls_auction_available with cars-new offers (#360)
     
     * VSMONEY-141 Salesman call on redirect info generation
     
     * VSMONEY-141 Feature flag for telepony qualifier
     
     * VSMONEY-283 # Fix calls_auction_available only for cars-new, remove isCarsNew condition

  *  VOS-3251 Do not migrate invalid offers (#359)
     
     * comment
     
     * do not migrate sales from old db without corresponding offers in vos
     
     it will avoid creation of invalid offers (e.g. without car_info)
     
     * fix test

  *  ignore empty mark & model

  *  Revert "VSMONEY-141 Salesman call on redirect info generation (#331)" (#358)
     
     This reverts commit cc5988b7f17e1cfde7af0537a189abe22275cce4.
  *  reduce logging level

  *  VSMONEY-141 Salesman call on redirect info generation (#331)
     
     * VSMONEY-141 Salesman call on redirect info generation
     
     * VSMONEY-141 Feature flag for telepony qualifier

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 24 Oct 2019 17:14:34 +0300

## yandex-vos2-autoru-consumers:0.57.0 (Wed, 23 Oct 2019 16:53:13 +0300)

  *  Vos 3255 fix moderation protection fields (#373)
     
     * VOS-3255 fix protected form
     
     * VOS-3255 test

  *  VOS-3012 fix features api (#371)
     
     * not so lazy features manager
     
     * Temporary test fix
     
     * fixed tests again!
     
     * Added features api fix
     
     * cleanup
     
     * Fix test entity type

  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru

  *  AUTORUAPI-6381 withNds: fixed converter, added tests

  *  not so lazy features manager (#368)
     

  *  Ydb session create timeout (#367)
     
     * raised timeout
     
     * raised timeout #2

  *  raised timeout (#366)
     

  *  AUTORUAPI-6382 with nds flag (#364)
     
     * AUTORUAPI-6382 with nds flag
     
     * AUTORUAPI-6382 with nds flag: updated converters
     
     * AUTORUAPI-6381 withNds = true if not set in NEW comtrans
     
     * AUTORUAPI-6381 withNds: fixed validation: forbidden to offer price with nds for private users in non-trucks categories, set withNds to true for new trucks for all kinds of users

  *  VOS-3012 adding common features (#365)
     
     * Added common-feature support
     
     * Added features duplicates
     
     * Fixing dependencies for tests
     
     * Fixing more tests
     
     * Delete useless code
     
     * little fixes
     
     * Added vos features with generation
     
     * Added test & fixed some code
     
     * delete useless manipulation
     
     * Fixed tests
     
     * Deleted implicit size
     
     * deleted useless imports

  *  VOS_3213 init ydb on start (#362)
     
     * Deleted lazy modificator from all places with ydb init
     
     * Fixing tests
     
     * Using force initialization
     
     * Added sessions pool init
     
     * fixed initSessionsPool use
     
     * Using existing runtime
     
     * Ydb force init

  *  AUTORUAPI-5325 added cabinet platform (#361)
     
     * Added cabinet platform
     
     * source fix
     
     * With fixing schema registry

  *  VSMONEY-141 # FIX calls_auction_available with cars-new offers (#360)
     
     * VSMONEY-141 Salesman call on redirect info generation
     
     * VSMONEY-141 Feature flag for telepony qualifier
     
     * VSMONEY-283 # Fix calls_auction_available only for cars-new, remove isCarsNew condition

  *  VOS-3251 Do not migrate invalid offers (#359)
     
     * comment
     
     * do not migrate sales from old db without corresponding offers in vos
     
     it will avoid creation of invalid offers (e.g. without car_info)
     
     * fix test

  *  ignore empty mark & model

  *  Revert "VSMONEY-141 Salesman call on redirect info generation (#331)" (#358)
     
     This reverts commit cc5988b7f17e1cfde7af0537a189abe22275cce4.
  *  reduce logging level

  *  VSMONEY-141 Salesman call on redirect info generation (#331)
     
     * VSMONEY-141 Salesman call on redirect info generation
     
     * VSMONEY-141 Feature flag for telepony qualifier

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 23 Oct 2019 16:53:13 +0300

## yandex-vos2-autoru-consumers:0.56.0 (Fri, 11 Oct 2019 12:26:55 +0300)

  *  do not crash on empty mark & model

  *  test & minor changes

  *  AUTORUAPI-6391 (#357)
     

  *  Deleted unused code

  *  VOS-3228 using raw_moderation_bunker

  *  keep license_plate_moderation_state after migration

  *  VOS-3237 testcontainers for mysql test containers (#339)
     
     * Added testcontainer usage for mysql test containers
     
     * fix dependency convergence
     
     * Registered sql container in closer
     
     * Fixed tmpfs config
     
     * Updated testcontainers versions
     
     * Fixed dependencies
     
     * Using testcontainers for extracting container url
     
     * fixing jdbcUrl
     
     * fixing jdbcUrl #2
     
     * Fixing jdbcUrl #3
     
     * Added logs for check url
     
     * Debugging port values
     
     * Deleted debug status
     
     * Using MySQLContainer
     
     * Without signleContainer
     
     * Added more config
     
     * Container per db
     
     * Fixed
     
     * Back to singleGenericContainer + fixed test
     
     * Fix some tests local launch
     
     * Fixing tmpfs config
     
     * Fixing tmpfs #2
     
     * Fixing initDbs in Vos2ApiSuite
     
     * Fixed some remote and local tests
     
     * Fixing vos2-autoru-workers test dependencies
     
     * Little code clean up
     
     * poms clean up
     
     * Using waitStrategy
     
     * delete some debug code
     
     * Using wait.forListeningPort

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 11 Oct 2019 12:26:55 +0300

## yandex-vos2-autoru-consumers:0.55.1 (Tue, 08 Oct 2019 14:06:04 +0300)

  *  Cleanup (#353)
     
     * VOS-3242 remove autoru_finance
     * VOS-3243 remove price_history migration

  *  Delete unnecessary logs

  *  CARFAX-383: dont update reload time if resolution is empty yet

  *  VOS-3228 license plate moderation (#350)
     

  *  Merge pull request #349 from YandexClassifieds/VSMONEY-130_service_change_logs
     
     VSMONEY-130: more service change logs
  *  Merge remote-tracking branch 'origin/master'

  *  VSMONEY-130: more service change logs

  *  VOS-3236 reseller unpaid forbid edit: disabled check temporarily: disabled test for that

  *  VOS-3236 reseller unpaid forbid edit: disabled check temporarily

  *  VOS-3236 reseller unpaid forbid edit: fixed wrong field

  *  Merge remote-tracking branch 'origin/master'

  *  VOS-3241 filter out deleted photos from form when check protection

  *  VOS-3241 filter out deleted photos from form when check protection

  *  rename

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 08 Oct 2019 14:06:04 +0300

## yandex-vos2-autoru-consumers:0.55.0 (Fri, 04 Oct 2019 18:44:17 +0300)

  *  VOS-3228 license plate moderation (#350)
     

  *  Merge pull request #349 from YandexClassifieds/VSMONEY-130_service_change_logs
     
     VSMONEY-130: more service change logs
  *  Merge remote-tracking branch 'origin/master'

  *  VSMONEY-130: more service change logs

  *  VOS-3236 reseller unpaid forbid edit: disabled check temporarily: disabled test for that

  *  VOS-3236 reseller unpaid forbid edit: disabled check temporarily

  *  VOS-3236 reseller unpaid forbid edit: fixed wrong field

  *  Merge remote-tracking branch 'origin/master'

  *  VOS-3241 filter out deleted photos from form when check protection

  *  VOS-3241 filter out deleted photos from form when check protection

  *  rename

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 04 Oct 2019 18:44:17 +0300

## yandex-vos2-autoru-consumers:0.54.1 (Wed, 02 Oct 2019 18:12:50 +0300)

  *  Merge pull request #346 from YandexClassifieds/VOS-3220-options-parsing
     
     VOS-3220 Parse only new options
  *  fix naming

  *  Merge pull request #345 from YandexClassifieds/VOS-3236_reseller_unpaid_forbid_edit
     
     VOS-3236 forbid to edit unpaid offer for reseller
  *  Added metric label

  *  Fix compilation

  *  Parse only new options

  *  VOS-3236 forbid to edit unpaid offer for reseller

  *  cleanup

  *  VOS-3239 recognize lp on moderation photo

  *  Merge pull request #343 from YandexClassifieds/AUTORUAPI-6346_vin_license_number_required
     
     AUTORUAPI-6346 vin and license plate are required in all regions
  *  Merge pull request #342 from YandexClassifieds/VOS-3220-options-parsing
     
     VOS-3220 added logs
  *  AUTORUAPI-6346 vin and license plate are required in all regions except Far Eastern Federal District

  *  Merge pull request #341 from YandexClassifieds/VOS-3233_merge_internal
     
     VOS-3233 change moderation photos namespace url
  *  Merge branch 'master' into VOS-3220-options-parsing

  *  Additional logs

  *  VOS-3233 change moderation photos namespace url

  *  Merge pull request #340 from YandexClassifieds/VOS-3233_merge_internal
     
     VOS-3233 add moderation photos to common converter
  *  VOS-3233 add moderation photos to common converter

  *  Merge remote-tracking branch 'origin/master'

  *  unmark deleted photos in drafts

  *  Merge pull request #334 from YandexClassifieds/VOS-3233_merge_internal
     
     VOS-3233 moderation photos
  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUSUP-4789 remove `deleted` marker for photos added via external_url

  *  VOS-3233 moderation photos test

  *  VOS-3233 moderation photos test

  *  Merge remote-tracking branch 'origin/master' into VOS-3233_merge_internal

  *  VOS-3233 photos convert method refactoring

  *  VOS-3233 extract moderation photos convert method

  *  VOS-3233 remove is_internal from tests

  *  VOS-3233 remove is_internal from tests

  *  VOS-3233 recognize lp on moderation photos

  *  VOS-3233 add moderation photos

  *  VOS-3233 add moderation photos

  *  VOS-3233 merge internal photos

  *  VOS-3233 merge internal photos

  *  VOS-3233 merge internal photos

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 02 Oct 2019 18:12:50 +0300

## yandex-vos2-autoru-consumers:0.54.0 (Tue, 01 Oct 2019 21:47:19 +0300)

  *  Merge pull request #343 from YandexClassifieds/AUTORUAPI-6346_vin_license_number_required
     
     AUTORUAPI-6346 vin and license plate are required in all regions
  *  Merge pull request #342 from YandexClassifieds/VOS-3220-options-parsing
     
     VOS-3220 added logs
  *  AUTORUAPI-6346 vin and license plate are required in all regions except Far Eastern Federal District

  *  Merge pull request #341 from YandexClassifieds/VOS-3233_merge_internal
     
     VOS-3233 change moderation photos namespace url
  *  Merge branch 'master' into VOS-3220-options-parsing

  *  Additional logs

  *  VOS-3233 change moderation photos namespace url

  *  Merge pull request #340 from YandexClassifieds/VOS-3233_merge_internal
     
     VOS-3233 add moderation photos to common converter
  *  VOS-3233 add moderation photos to common converter

  *  Merge remote-tracking branch 'origin/master'

  *  unmark deleted photos in drafts

  *  Merge pull request #334 from YandexClassifieds/VOS-3233_merge_internal
     
     VOS-3233 moderation photos
  *  Merge remote-tracking branch 'origin/master'

  *  AUTORUSUP-4789 remove `deleted` marker for photos added via external_url

  *  VOS-3233 moderation photos test

  *  VOS-3233 moderation photos test

  *  Merge remote-tracking branch 'origin/master' into VOS-3233_merge_internal

  *  VOS-3233 photos convert method refactoring

  *  VOS-3233 extract moderation photos convert method

  *  VOS-3233 remove is_internal from tests

  *  VOS-3233 remove is_internal from tests

  *  VOS-3233 recognize lp on moderation photos

  *  VOS-3233 add moderation photos

  *  VOS-3233 add moderation photos

  *  VOS-3233 merge internal photos

  *  VOS-3233 merge internal photos

  *  VOS-3233 merge internal photos

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 01 Oct 2019 21:47:19 +0300

## yandex-vos2-autoru-consumers:0.53.2 (Mon, 30 Sep 2019 14:04:01 +0300)

  *  VOS-3143 new moderation opinion topic

  *  Merge remote-tracking branch 'origin/master'

  *  simplify

  *  Merge branch 'master' into VOS-3220-options-parsing

  *  Remove old catalog && fix tests (#336)
     

  *  add missing zero

  *  add was active to yt

  *  Merge pull request #325 from YandexClassifieds/AUTORUAPI-6298_eclipse_exclision
     
     AUTORUAPI-6298 exclude mitsubishi eclipse vin validation
  *  Merge branch 'master' into VOS-3220-options-parsing

  *  Changed verba equipment to verba options dictionary

  *  bugfix

  *  Merge remote-tracking branch 'origin/master'

  *  rename Generation -> Supergen & use fields from car_info if tech_param_id is not set

  *  better trace propagation (#327)
     

  *  use non-autoru gear_types

  *  revert gear_types

  *  gear types

  *  VOS-3232 dont index internal photo test

  *  VOS-3232 dont index internal photo

  *  AUTORUAPI-6298 exclude mitsubishi eclipse vin validation

  *  AUTORUAPI-6298 exclude mitsubishi eclipse vin validation

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 30 Sep 2019 14:04:01 +0300

## yandex-vos2-autoru-consumers:0.53.1 (Fri, 27 Sep 2019 17:21:00 +0300)

  *  Merge remote-tracking branch 'origin/master'

  *  simplify

  *  Merge branch 'master' into VOS-3220-options-parsing

  *  Remove old catalog && fix tests (#336)
     

  *  add missing zero

  *  add was active to yt

  *  Merge pull request #325 from YandexClassifieds/AUTORUAPI-6298_eclipse_exclision
     
     AUTORUAPI-6298 exclude mitsubishi eclipse vin validation
  *  Merge branch 'master' into VOS-3220-options-parsing

  *  Changed verba equipment to verba options dictionary

  *  bugfix

  *  Merge remote-tracking branch 'origin/master'

  *  rename Generation -> Supergen & use fields from car_info if tech_param_id is not set

  *  better trace propagation (#327)
     

  *  use non-autoru gear_types

  *  revert gear_types

  *  gear types

  *  VOS-3232 dont index internal photo test

  *  VOS-3232 dont index internal photo

  *  AUTORUAPI-6298 exclude mitsubishi eclipse vin validation

  *  AUTORUAPI-6298 exclude mitsubishi eclipse vin validation

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 27 Sep 2019 17:21:00 +0300

## yandex-vos2-autoru-consumers:0.53.0 (Tue, 24 Sep 2019 19:20:44 +0300)

  *  Remove old catalog && fix tests (#336)
     

  *  add missing zero

  *  add was active to yt

  *  Merge pull request #325 from YandexClassifieds/AUTORUAPI-6298_eclipse_exclision
     
     AUTORUAPI-6298 exclude mitsubishi eclipse vin validation
  *  bugfix

  *  Merge remote-tracking branch 'origin/master'

  *  rename Generation -> Supergen & use fields from car_info if tech_param_id is not set

  *  better trace propagation (#327)
     

  *  use non-autoru gear_types

  *  revert gear_types

  *  gear types

  *  VOS-3232 dont index internal photo test

  *  VOS-3232 dont index internal photo

  *  AUTORUAPI-6298 exclude mitsubishi eclipse vin validation

  *  AUTORUAPI-6298 exclude mitsubishi eclipse vin validation

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 24 Sep 2019 19:20:44 +0300

## yandex-vos2-autoru-consumers:0.52.2 (Wed, 18 Sep 2019 19:18:02 +0300)

  *  Merge pull request #323 from YandexClassifieds/VOS-3220-options-parsing
     VOS-3220 added parsing old offers
  *  AUTORUSUP-4781 do not migrate gear_type
  *  remove ALL_WHEEL_DRIVE dominance
  *  code cleanup
  *  Added parsing old offers description
  *  better logs
  *  better logs
  *  log expected & actual values in ModerationProtection errors
  *  more logs && save to vos is always required in FormWriter
  *  fill super_gen_id and configuration_id from catalog
  *  AUTORUSUP-4781 fill gear type from catalog
  *  more logs
  *  renamings
  *  Merge remote-tracking branch 'origin/master'
  *  simplify
  *  Offer options enriching fixed
  *  release 0.52.1
  *  VOS-3231 fix deleted flat convert
  *  new test
  *  style
  *  do not trace OfferFormConverter
  *  fix
  *  remove test
  *  Merge remote-tracking branch 'origin/master'
  *  ignore DO_NOT_EXIST for dealers
  *  better style
  *  Merge pull request #321 from YandexClassifieds/VOS-3225_internal_photo_again
     VOS-3225 internal photo again
  *  VOS-3225 internal photo again
  *  VOS-3225 internal photo again
  *  release 0.52.0
  *  Merge pull request #312 from YandexClassifieds/VOS-3220-options-parsing
     VOS-3220 options parsing fix
  *  very little fixes
  *  Little fixes
  *  Fixes
  *  Merge remote-tracking branch 'origin/master'
  *  do not catch throwables
  *  Merge pull request #313 from YandexClassifieds/VOS-3191_diff_fields
     VOS-3191 add diff fields
  *  little fix
  *  Fixed tests again
  *  Merge pull request #319 from YandexClassifieds/AUTORUAPI-6225_new_email_confirm_template
     AUTORUAPI-6225: email_confirm_offers template
  *  AUTORUAPI-6225: email_confirm_offers template
  *  VOS-3226 add original urls
  *  VOS-3226 add original urls
  *  VOS-3226 add original urls
  *  Merge remote-tracking branch 'origin/master' into VOS-3225_internal_photo
  *  Merge branch 'master' into VOS-3225_internal_photo
  *  Merge remote-tracking branch 'origin/master'
  *  fix tests
  *  VOS-3225 add original photos
  *  Merge pull request #315 from YandexClassifieds/VOS-3225_internal_photo
     VOS-3225 add original photos
  *  deduplicate metrics
  *  using default CollectorRegistry
  *  cleanup
  *  update ydb-wrapper version && metrics && update zio version
  *  VOS-3225 add original photos
  *  VOS-3191 diff fields
  *  VOS-3225 add original photos
  *  Fixed tests
  *  Merge branch 'master' into VOS-3220-options-parsing
  *  Merge remote-tracking branch 'origin/master'
  *  correct handling of "not found" images
  *  VOS-3225 add original photos
  *  More fixes!
  *  Merge remote-tracking branch 'origin/master' into VOS-3191_diff_fields
  *  VOS-3191 diff fields
  *  Fixes
  *  Merge pull request #314 from YandexClassifieds/VOS-3225_internal_photo
     VOS-3225 internal photo
  *  VOS-3225 internal photo
  *  Merge remote-tracking branch 'origin/master' into VOS-3191_diff_fields
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/offers/diff/DiffGenerator.scala
  *  VOS-3191 add diff fields
  *  Merge pull request #305 from YandexClassifieds/VOS-3225_internal_photo
     VOS-3225 internal photo
  *  fixed tests... ?
  *  Recovered parsing:
  *  Merged master hopefully
  *  Revert "Merge pull request #288 from YandexClassifieds/VOS-3220-options-parsing"
     This reverts commit f18943ca5cd19ca8bfb9262ea4dffbe1a896ded5.
  *  remove draft migration
  *  Deleted debug stuff
  *  Added descriptions parsing for dealers offers
  *  Fixed work with verba
  *  Merge pull request #306 from YandexClassifieds/VOS-3227
     VOS-3227 new method and test
  *  remove test for removed logic
  *  VOS-3183 add deleted & internal to PhotoInfo
  *  remove DO_NOT_EXISTS
  *  rewrite test for other field
  *  Merge remote-tracking branch 'origin/master' into VOS-3227
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/model/AutoruModelUtils.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3183 add deleted & internal to PhotoInfo
  *  remove not show
  *  move other reasons to rich utils
  *  VOS-3225 internal photo
  *  better test
  *  VOS-3225 internal photo
  *  fix test
  *  new method and test
  *  VOS-3225 internal photo
  *  VOS-3225 internal photo

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 18 Sep 2019 19:18:02 +0300

## yandex-vos2-autoru-consumers:0.52.1 (Tue, 17 Sep 2019 19:38:00 +0300)

  *  VOS-3231 fix deleted flat convert
  *  new test
  *  style
  *  do not trace OfferFormConverter
  *  fix
  *  remove test
  *  Merge remote-tracking branch 'origin/master'
  *  ignore DO_NOT_EXIST for dealers
  *  better style
  *  Merge pull request #321 from YandexClassifieds/VOS-3225_internal_photo_again
     VOS-3225 internal photo again
  *  VOS-3225 internal photo again
  *  VOS-3225 internal photo again
  *  release 0.52.0
  *  Merge pull request #312 from YandexClassifieds/VOS-3220-options-parsing
     VOS-3220 options parsing fix
  *  very little fixes
  *  Little fixes
  *  Fixes
  *  Merge remote-tracking branch 'origin/master'
  *  do not catch throwables
  *  Merge pull request #313 from YandexClassifieds/VOS-3191_diff_fields
     VOS-3191 add diff fields
  *  little fix
  *  Fixed tests again
  *  Merge pull request #319 from YandexClassifieds/AUTORUAPI-6225_new_email_confirm_template
     AUTORUAPI-6225: email_confirm_offers template
  *  AUTORUAPI-6225: email_confirm_offers template
  *  VOS-3226 add original urls
  *  VOS-3226 add original urls
  *  VOS-3226 add original urls
  *  Merge remote-tracking branch 'origin/master' into VOS-3225_internal_photo
  *  Merge branch 'master' into VOS-3225_internal_photo
  *  Merge remote-tracking branch 'origin/master'
  *  fix tests
  *  VOS-3225 add original photos
  *  Merge pull request #315 from YandexClassifieds/VOS-3225_internal_photo
     VOS-3225 add original photos
  *  deduplicate metrics
  *  using default CollectorRegistry
  *  cleanup
  *  update ydb-wrapper version && metrics && update zio version
  *  VOS-3225 add original photos
  *  VOS-3191 diff fields
  *  VOS-3225 add original photos
  *  Fixed tests
  *  Merge branch 'master' into VOS-3220-options-parsing
  *  Merge remote-tracking branch 'origin/master'
  *  correct handling of "not found" images
  *  VOS-3225 add original photos
  *  More fixes!
  *  Merge remote-tracking branch 'origin/master' into VOS-3191_diff_fields
  *  VOS-3191 diff fields
  *  Fixes
  *  Merge pull request #314 from YandexClassifieds/VOS-3225_internal_photo
     VOS-3225 internal photo
  *  VOS-3225 internal photo
  *  Merge remote-tracking branch 'origin/master' into VOS-3191_diff_fields
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/offers/diff/DiffGenerator.scala
  *  VOS-3191 add diff fields
  *  Merge pull request #305 from YandexClassifieds/VOS-3225_internal_photo
     VOS-3225 internal photo
  *  fixed tests... ?
  *  Recovered parsing:
  *  Merged master hopefully
  *  Revert "Merge pull request #288 from YandexClassifieds/VOS-3220-options-parsing"
     This reverts commit f18943ca5cd19ca8bfb9262ea4dffbe1a896ded5.
  *  remove draft migration
  *  Deleted debug stuff
  *  Added descriptions parsing for dealers offers
  *  Fixed work with verba
  *  Merge pull request #306 from YandexClassifieds/VOS-3227
     VOS-3227 new method and test
  *  remove test for removed logic
  *  VOS-3183 add deleted & internal to PhotoInfo
  *  remove DO_NOT_EXISTS
  *  rewrite test for other field
  *  Merge remote-tracking branch 'origin/master' into VOS-3227
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/model/AutoruModelUtils.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3183 add deleted & internal to PhotoInfo
  *  remove not show
  *  move other reasons to rich utils
  *  VOS-3225 internal photo
  *  better test
  *  VOS-3225 internal photo
  *  fix test
  *  new method and test
  *  VOS-3225 internal photo
  *  VOS-3225 internal photo

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 17 Sep 2019 19:38:00 +0300

## yandex-vos2-autoru-consumers:0.52.0 (Mon, 16 Sep 2019 18:29:01 +0300)

  *  Merge pull request #312 from YandexClassifieds/VOS-3220-options-parsing
     VOS-3220 options parsing fix
  *  very little fixes
  *  Little fixes
  *  Fixes
  *  Merge remote-tracking branch 'origin/master'
  *  do not catch throwables
  *  Merge pull request #313 from YandexClassifieds/VOS-3191_diff_fields
     VOS-3191 add diff fields
  *  little fix
  *  Fixed tests again
  *  Merge pull request #319 from YandexClassifieds/AUTORUAPI-6225_new_email_confirm_template
     AUTORUAPI-6225: email_confirm_offers template
  *  AUTORUAPI-6225: email_confirm_offers template
  *  VOS-3226 add original urls
  *  VOS-3226 add original urls
  *  VOS-3226 add original urls
  *  Merge remote-tracking branch 'origin/master' into VOS-3225_internal_photo
  *  Merge branch 'master' into VOS-3225_internal_photo
  *  Merge remote-tracking branch 'origin/master'
  *  fix tests
  *  VOS-3225 add original photos
  *  Merge pull request #315 from YandexClassifieds/VOS-3225_internal_photo
     VOS-3225 add original photos
  *  deduplicate metrics
  *  using default CollectorRegistry
  *  cleanup
  *  update ydb-wrapper version && metrics && update zio version
  *  VOS-3225 add original photos
  *  VOS-3191 diff fields
  *  VOS-3225 add original photos
  *  Fixed tests
  *  Merge branch 'master' into VOS-3220-options-parsing
  *  Merge remote-tracking branch 'origin/master'
  *  correct handling of "not found" images
  *  VOS-3225 add original photos
  *  More fixes!
  *  Merge remote-tracking branch 'origin/master' into VOS-3191_diff_fields
  *  VOS-3191 diff fields
  *  Fixes
  *  Merge pull request #314 from YandexClassifieds/VOS-3225_internal_photo
     VOS-3225 internal photo
  *  VOS-3225 internal photo
  *  Merge remote-tracking branch 'origin/master' into VOS-3191_diff_fields
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/offers/diff/DiffGenerator.scala
  *  VOS-3191 add diff fields
  *  Merge pull request #305 from YandexClassifieds/VOS-3225_internal_photo
     VOS-3225 internal photo
  *  fixed tests... ?
  *  Recovered parsing:
  *  Merged master hopefully
  *  Revert "Merge pull request #288 from YandexClassifieds/VOS-3220-options-parsing"
     This reverts commit f18943ca5cd19ca8bfb9262ea4dffbe1a896ded5.
  *  remove draft migration
  *  Deleted debug stuff
  *  Added descriptions parsing for dealers offers
  *  Fixed work with verba
  *  Merge pull request #306 from YandexClassifieds/VOS-3227
     VOS-3227 new method and test
  *  remove test for removed logic
  *  VOS-3183 add deleted & internal to PhotoInfo
  *  remove DO_NOT_EXISTS
  *  rewrite test for other field
  *  Merge remote-tracking branch 'origin/master' into VOS-3227
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/model/AutoruModelUtils.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3183 add deleted & internal to PhotoInfo
  *  remove not show
  *  move other reasons to rich utils
  *  VOS-3225 internal photo
  *  better test
  *  VOS-3225 internal photo
  *  fix test
  *  new method and test
  *  VOS-3225 internal photo
  *  VOS-3225 internal photo

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 16 Sep 2019 18:29:01 +0300

## yandex-vos2-autoru-consumers:0.51.0 (Tue, 10 Sep 2019 15:25:59 +0300)

  *  Merge pull request #307 from YandexClassifieds/VOS-3212_banned_but_editable
     VOS-3212: can edit banned offers with offer_editable flag
  *  VOS-3212: tests
  *  Merge branch 'master' into VOS-3220-options-parsing
  *  Fixed tests
  *  Revert "Merge pull request #304 from YandexClassifieds/VSMONEY-49"
     This reverts commit e77bd71d01cded35c4f63090018006117df8e122, reversing
     changes made to 26970538c5411f028c4503629053e8fc993f5f76.
  *  Merge pull request #304 from YandexClassifieds/VSMONEY-49
     VSMONEY-29 Use X-Yandex-Request-ID
  *  VOS-3212: can edit banned offers with offer_editable flag
  *  Merge branch 'master' into AUTORUAPI-6023_status
  *  
     a day may come when i make my tests work, but not today
  *  Added simple method for metrics accumulation
  *  VSMONEY-49 fix test
  *  Fixed optionsParser call & optionsParser working style
  *  fix imports
  *  VSMONEY-29 Use X-Yandex-Request-ID
  *  Added feature for metrics & deleted enriching
  *  update tag adding
  *  minor refactoring
  *  
     pr fixes
  *  
     more fixes
  *  
     tests and fixes
  *  
     restore last offer status after unban + removed all reduant ban workflows
  *  AUTORUAPI-4443 (#300)
     * AUTORUAPI-4443 rename body type
  *  VOS-3218 keep last 30 deleted photos && do not remove after 3 days (#299)
  *  Added metric support
  *  Renamed feature & code cleanup
  *  Merge branch 'master' into AUTORUAPI-6205_sms
  *  
     offer creation sms fixes
  *  Autoruapi 4443 Убрать лишний тип кузова (#109)
     AUTORUAPI-4443 replace bodyType
  *  Added feature & optionsParser usage
  *  Refactored methods + fixed tests
  *  VOS-3168 recall offer if placement deactivated (#296)
     * VOS-3168 recall offer if placement deactivated
     
  *  Merge pull request #294 from YandexClassifieds/VSMONEY-31_hotfix
     VSMONEY-31 hotfix prices from salesman
  *  Fixed list
  *  VSMONEY-31 ignore test for hotfix
  *  VSMONEY-31 hotfix prices from salesman
  *  Merge pull request #292 from YandexClassifieds/AUTORUAPI-6237_osago
     AUTORUAPI-6237 osago
  *  Throwed saving verba in memory & fixed returning mutable collections
  *  AUTORUAPI-6237 osago insurance
  *  AUTORUAPI-6237 osago insurance
  *  AUTORUAPI-6237 osago insurance
  *  Added tests for options parser + moved lowerCase logic into optionsParser
  *  Added options aliases checking in OptionsParser
  *  AUTORUAPI-6237 osago insurance
  *  VSMONEY-31 use trait Logging
  *  VSMONEY-31 logs for salesman prices
  *  Made parser more simplier and slower
  *  Added description parser
  *  VOS-3221 new error
  *  Added feature to block info update in offer
  *  Made memory optimization for searching simulars + fixed tests
  *  Added lazy query to db
  *  Optimized similar searching
  *  VOS-3192 change email via moderation_update
  *  Merge branch 'master' into VOS-3188_offer_validate_card
  *  Code cleanup + added feature
  *  Added stage to pipeline & little model naming fixes
  *  Merge pull request #278 from YandexClassifieds/AUTORUAPI-6237_osago
     AUTORUAPI-6237 osago
  *  Fixed certain field names in autoru offer model
  *  AUTORUAPI-6237 osago insurance
  *  AUTORUAPI-6237 osago insurance
  *  AUTORUAPI-6237 osago insurance
  *  AUTORUAPI-6237 osago insurance
  *  Added offer validation stage
  *  AUTORUAPI-6237 osago insurance
  *  fix compilation & provide operationalSupport
  *  always use ttl in pica-pica client
  *  better
  *  VOS-3216: add configuration and super_gen to vital-related fields
  *  Merge pull request #275 from YandexClassifieds/VOS-3215_use_orig
     VOS-3215:use orig for recognize numbers
  *  VOS-3215:use orig for recognize numbers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 10 Sep 2019 15:25:59 +0300

## yandex-vos2-autoru-consumers:0.50.2 (Thu, 15 Aug 2019 11:49:22 +0300)

  *  VOS-3208: preserve photo delete status
  *  VOS-3197 searcher index (#269)
     * VOS-3197 searcher
  *  Merge pull request #266 from YandexClassifieds/VOS-2958
     VOS-2958 Use salesman-user prices instead of octopus prices, under fe…
  *  VOS-2958 Rename SalesmanUserService to PriceService
  *  VOS-2958 Rename object, extract traced to method argument
  *  Merge branch 'VOS-2958' of https://github.com/YandexClassifieds/vos2-autoru into VOS-2958
  *  VOS-2985 SalesmanUserService
  *  release 0.50.1
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/services/salesman/HttpSalesmanUserClient.scala
     Co-Authored-By: Evgeny Veretennikov <vere10@yandex-team.ru>
  *  VOS-3208: photo protection
  *  Merge pull request #263 from YandexClassifieds/AUTORUAPI-6154_credit_product_to_index
     AUTORUAPI-6154 add credit product to indexer
  *  VOS-3203 allow empty vin for moderators (#267)
  *  remove obsolete files
  *  VOS-2958 Use salesman-user prices instead of octopus prices, under feature
  *  release 0.50.0
  *  Merge pull request #262 from YandexClassifieds/VOS-3034
     VOS-3034 Протащить видео в комтрансе и мото
  *  VOS-3197 флаг для запрета звонков продавцу (#261)
     * VOS-3197 field chat_only
  *  resolve namespace clash
  *  Merge branch 'master' into VOS-3034
     # Conflicts:
     #	vos2-autoru-core/src/test/scala/ru/yandex/vos2/autoru/services/idx/AutoruIdxRequestBuilderTest.scala
  *  cleanup
  *  VOS-3206 removed enum AutoruOffer.Category (#264)
  *  AUTORUAPI-6154 add credit product to indexer
  *  VOS-3167 Ydb drafts (#260)
  *  tests
  *  Merge pull request #259 from YandexClassifieds/VOS-3099_private_user_case
     VOS-3099: handle private and commercial users separately
  *  VOS-3099: handle private and commercial users separately
  *  comtrans to implement addAutoruPhotosBuilder

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 15 Aug 2019 11:49:22 +0300

## yandex-vos2-autoru-consumers:0.50.1 (Tue, 13 Aug 2019 11:35:10 +0300)

  *  VOS-3208: photo protection
  *  Merge pull request #263 from YandexClassifieds/AUTORUAPI-6154_credit_product_to_index
     AUTORUAPI-6154 add credit product to indexer
  *  VOS-3203 allow empty vin for moderators (#267)
  *  remove obsolete files
  *  release 0.50.0
  *  Merge pull request #262 from YandexClassifieds/VOS-3034
     VOS-3034 Протащить видео в комтрансе и мото
  *  VOS-3197 флаг для запрета звонков продавцу (#261)
     * VOS-3197 field chat_only
  *  resolve namespace clash
  *  Merge branch 'master' into VOS-3034
     # Conflicts:
     #	vos2-autoru-core/src/test/scala/ru/yandex/vos2/autoru/services/idx/AutoruIdxRequestBuilderTest.scala
  *  cleanup
  *  VOS-3206 removed enum AutoruOffer.Category (#264)
  *  AUTORUAPI-6154 add credit product to indexer
  *  VOS-3167 Ydb drafts (#260)
  *  tests
  *  Merge pull request #259 from YandexClassifieds/VOS-3099_private_user_case
     VOS-3099: handle private and commercial users separately
  *  VOS-3099: handle private and commercial users separately
  *  comtrans to implement addAutoruPhotosBuilder

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 13 Aug 2019 11:35:10 +0300

## yandex-vos2-autoru-consumers:0.50.0 (Mon, 12 Aug 2019 13:01:53 +0300)

  *  Merge pull request #262 from YandexClassifieds/VOS-3034
     VOS-3034 Протащить видео в комтрансе и мото
  *  VOS-3197 флаг для запрета звонков продавцу (#261)
     * VOS-3197 field chat_only
  *  resolve namespace clash
  *  Merge branch 'master' into VOS-3034
     # Conflicts:
     #	vos2-autoru-core/src/test/scala/ru/yandex/vos2/autoru/services/idx/AutoruIdxRequestBuilderTest.scala
  *  cleanup
  *  VOS-3206 removed enum AutoruOffer.Category (#264)
  *  VOS-3167 Ydb drafts (#260)
  *  tests
  *  Merge pull request #259 from YandexClassifieds/VOS-3099_private_user_case
     VOS-3099: handle private and commercial users separately
  *  VOS-3099: handle private and commercial users separately
  *  comtrans to implement addAutoruPhotosBuilder

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 12 Aug 2019 13:01:53 +0300

## yandex-vos2-autoru-consumers:0.49.1 (Wed, 07 Aug 2019 19:41:56 +0300)

  *  VOS-3099: automatically protect all vital and related fields
  *  VOS-3205 allow retries for mds
  *  better runtime exception
  *  do not throw FiberFailure
  *  add log around offer locks
  *  remove asserts: some offers exist only in vos
  *  disable logSlowQueries to avoid useless stack trace allocation
  *  release 0.49.0
  *  Merge pull request #257 from YandexClassifieds/VOS-3099_auto_tech_param_id
     VOS-3099: automaticallly set tech_param_id protection
  *  VOS-3204 use index_data in grouped-by-ban-reason (#258)
     * VOS-3204 use index_data in grouped-by-ban-reason
     
     * using unused parameter
     
     * return ban reasons in lowercase
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/moderation/ModerationProtection.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3099: automatically set tech_param_id protection
  *  remove old code
  *  remove dispatch dependency
  *  fix compilation
  *  removed obsolete parameter in FormWriteParams
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  AUTORUAPI-6153 set current timestamp in photos meta message to kafka: fixed test and code (TestsReallyHelped)
  *  ignore zero discount price
  *  fixed verba client: use page params in request
  *  ignore already deleted drafts
  *  bugfix
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-core/src/main/scala/ru/yandex/vos2/services/moderation/ModerationOpinionsConsumer.scala
  *  VOS-3167 using DraftsManager in api (#245)
  *  Merge remote-tracking branch 'origin/master'
  *  Merge remote-tracking branch 'origin/master'
  *  dont lose last_check_exist_timestamp update after update from form
  *  VOS-3170 added tests, minor fix (TestsReallyHelped)
  *  VOS-3170 added remote_id and remote_url form params
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
     # Conflicts:
     #	pom.xml
  *  VOS-3104 availability is optional
  *  Merge pull request #249 from YandexClassifieds/AUTORUAPI-6154_credit_programs
     AUTORUAPI-6154 credit products
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  VOS-3170 carsCatalog.getCardByTechParamId is optional for holocron conversion
  *  VOS-3170 verba pagination: read full verba dictionary
  *  Merge pull request #251 from YandexClassifieds/feature/VOS-3193
     Added feature validate_offers_send_email to turn off emailing reports by default
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  VOS-3104 fixed complectation_id, engine_type, body_type validation
  *  Merge branch 'master' into feature/VOS-3193
  *  VOS-3193: added feature validate_offers_send_email to turn off email sending by default. Updated email template. Updated field names for Statface report
  *  AUTORUAPI-4853: don't send not found photo to moderation
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  AUTORUAPI-6154 credit products
  *  AUTORUAPI-6154 credit products
  *  AUTORUAPI-6154 credit products
  *  AUTORUAPI-6154 credit products
  *  Merge pull request #239 from YandexClassifieds/feature/VOS-3193
     VOS-3193: first version of ValidateOffers
  *  refactoring (#246)
  *  imports
  *  VOS-3199 fix license plate stage (#244)
  *  remove token from local config
  *  VOS-3099: remove salon getter/setter methods from field modifiers
  *  ignore fresh_date = 0
  *  fix fresh_date
  *  VOS-3150 save valid form (#243)
  *  VOS-3170 merge master
  *  VOS-3193: YqlClient use JdbcTemplate under the hood
  *  Merge branch 'master' into feature/VOS-3193
  *  VOS-3193: refactored YqlClient and ValidateOffers
  *  VOS-3193: improvemens in ValidateOffers. Added email sending.
  *  VOS-3193: first version of ValidateOffers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 07 Aug 2019 19:41:56 +0300

## yandex-vos2-autoru-consumers:0.49.0 (Wed, 07 Aug 2019 15:20:29 +0300)

  *  Merge pull request #257 from YandexClassifieds/VOS-3099_auto_tech_param_id
     VOS-3099: automaticallly set tech_param_id protection
  *  VOS-3204 use index_data in grouped-by-ban-reason (#258)
     * VOS-3204 use index_data in grouped-by-ban-reason
     
     * using unused parameter
     
     * return ban reasons in lowercase
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/moderation/ModerationProtection.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3099: automatically set tech_param_id protection
  *  remove old code
  *  remove dispatch dependency
  *  fix compilation
  *  removed obsolete parameter in FormWriteParams
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  AUTORUAPI-6153 set current timestamp in photos meta message to kafka: fixed test and code (TestsReallyHelped)
  *  ignore zero discount price
  *  fixed verba client: use page params in request
  *  ignore already deleted drafts
  *  bugfix
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-core/src/main/scala/ru/yandex/vos2/services/moderation/ModerationOpinionsConsumer.scala
  *  VOS-3167 using DraftsManager in api (#245)
  *  Merge remote-tracking branch 'origin/master'
  *  Merge remote-tracking branch 'origin/master'
  *  dont lose last_check_exist_timestamp update after update from form
  *  VOS-3170 added tests, minor fix (TestsReallyHelped)
  *  VOS-3170 added remote_id and remote_url form params
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
     # Conflicts:
     #	pom.xml
  *  VOS-3104 availability is optional
  *  Merge pull request #249 from YandexClassifieds/AUTORUAPI-6154_credit_programs
     AUTORUAPI-6154 credit products
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  VOS-3170 carsCatalog.getCardByTechParamId is optional for holocron conversion
  *  VOS-3170 verba pagination: read full verba dictionary
  *  Merge pull request #251 from YandexClassifieds/feature/VOS-3193
     Added feature validate_offers_send_email to turn off emailing reports by default
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  VOS-3104 fixed complectation_id, engine_type, body_type validation
  *  Merge branch 'master' into feature/VOS-3193
  *  VOS-3193: added feature validate_offers_send_email to turn off email sending by default. Updated email template. Updated field names for Statface report
  *  AUTORUAPI-4853: don't send not found photo to moderation
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  AUTORUAPI-6154 credit products
  *  AUTORUAPI-6154 credit products
  *  AUTORUAPI-6154 credit products
  *  AUTORUAPI-6154 credit products
  *  Merge pull request #239 from YandexClassifieds/feature/VOS-3193
     VOS-3193: first version of ValidateOffers
  *  refactoring (#246)
  *  imports
  *  VOS-3199 fix license plate stage (#244)
  *  remove token from local config
  *  VOS-3099: remove salon getter/setter methods from field modifiers
  *  ignore fresh_date = 0
  *  fix fresh_date
  *  VOS-3150 save valid form (#243)
  *  VOS-3170 merge master
  *  VOS-3193: YqlClient use JdbcTemplate under the hood
  *  Merge branch 'master' into feature/VOS-3193
  *  VOS-3193: refactored YqlClient and ValidateOffers
  *  VOS-3193: improvemens in ValidateOffers. Added email sending.
  *  VOS-3193: first version of ValidateOffers

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 07 Aug 2019 15:20:29 +0300

## yandex-vos2-autoru-consumers:0.48.3 (Wed, 31 Jul 2019 15:54:20 +0300)

  *  VOS-3099: simplify select logic
  *  release 0.48.2
  *  Merge pull request #242 from YandexClassifieds/VOS-3099_dont_dublicate_on_vital_field_edit
     Vos 3099 dont dublicate on vital field edit
  *  Merge remote-tracking branch 'origin/master'
  *  VOS-3187: mark 410 and 400 as not found
  *  review fixes
  *  VOS-3196 fix badges to Indexer converter
  *  VOS-3196 fix badges to Indexer converter
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  VOS-3104 fixed configuration_id field set
  *  release 0.48.1
  *  VOS-3196 do not write to sales_services for privates (#238)
  *  VOS-3099: fix protected fields check
  *  VOS-3099: select most similar offer between multiple variants with equal VIN/unique_id
  *  Revert "VOS-3176: remove extra offer mergers (moderation rules)"
     rename nonModifiedFields -> protectVitalFields
     This reverts commit 2661b7964b975cbaf32eb8d921b65006581ae317.
  *  Merge pull request #241 from YandexClassifieds/VOS-3179_names
     VOS-3179 mark/model names in offer form converter
  *  
     unit tests fix
  *  
     mark/model names in offer form converter
  *  AUTORUSUP-4709: fix namespace for undo blur
  *  fixed compilation
  *  fixed compilation
  *  VOS-3104 fixed delivery regions set
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  AUTORUAPI-6127 delivery regions in holocron
  *  fix test
  *  VOS-3104 extended holocron validation fixes
  *  disable UserIndex watcher
  *  VOS-3167 drafts manager wip (#231)
  *  VOS-3194: use check exist cache to detect not found images
  *  VOS-3194: don't send photo with namespace autoru-orig to indexer
  *  VOS-3187: fix npe
  *  VOS-3187: fix limiter
  *  Merge pull request #235 from YandexClassifieds/AUTORUAPI-4853_mark_not_found_in_mds
     VOS-3187: mark not found
  *  AUTORUAPI-4853: fix typo
  *  AUTORUAPI-4853: fix test
  *  AUTORUAPI-4853: use check exist photo cache in mds uploader client
  *  AUTORUAPI-4853: change model
  *  reverted local props
  *  VOS-3187: small fix
  *  VOS-3187: fix bugs & refactoring
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  metrics for holocron validation errors
  *  VOS-3187: mark not found
  *  release 0.48.0
  *  protect fields not_registered_in_russia & availability
  *  release 0.47.0
  *  published letter: send archives

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 31 Jul 2019 15:54:20 +0300

## yandex-vos2-autoru-consumers:0.48.2 (Wed, 31 Jul 2019 14:18:25 +0300)

  *  Merge pull request #242 from YandexClassifieds/VOS-3099_dont_dublicate_on_vital_field_edit
     Vos 3099 dont dublicate on vital field edit
  *  Merge remote-tracking branch 'origin/master'
  *  VOS-3187: mark 410 and 400 as not found
  *  review fixes
  *  VOS-3196 fix badges to Indexer converter
  *  VOS-3196 fix badges to Indexer converter
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  VOS-3104 fixed configuration_id field set
  *  release 0.48.1
  *  VOS-3196 do not write to sales_services for privates (#238)
  *  VOS-3099: fix protected fields check
  *  VOS-3099: select most similar offer between multiple variants with equal VIN/unique_id
  *  Revert "VOS-3176: remove extra offer mergers (moderation rules)"
     rename nonModifiedFields -> protectVitalFields
     This reverts commit 2661b7964b975cbaf32eb8d921b65006581ae317.
  *  Merge pull request #241 from YandexClassifieds/VOS-3179_names
     VOS-3179 mark/model names in offer form converter
  *  
     unit tests fix
  *  
     mark/model names in offer form converter
  *  AUTORUSUP-4709: fix namespace for undo blur
  *  fixed compilation
  *  fixed compilation
  *  VOS-3104 fixed delivery regions set
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  AUTORUAPI-6127 delivery regions in holocron
  *  fix test
  *  VOS-3104 extended holocron validation fixes
  *  disable UserIndex watcher
  *  VOS-3167 drafts manager wip (#231)
  *  VOS-3194: use check exist cache to detect not found images
  *  VOS-3194: don't send photo with namespace autoru-orig to indexer
  *  VOS-3187: fix npe
  *  VOS-3187: fix limiter
  *  Merge pull request #235 from YandexClassifieds/AUTORUAPI-4853_mark_not_found_in_mds
     VOS-3187: mark not found
  *  AUTORUAPI-4853: fix typo
  *  AUTORUAPI-4853: fix test
  *  AUTORUAPI-4853: use check exist photo cache in mds uploader client
  *  AUTORUAPI-4853: change model
  *  reverted local props
  *  VOS-3187: small fix
  *  VOS-3187: fix bugs & refactoring
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  metrics for holocron validation errors
  *  VOS-3187: mark not found
  *  release 0.48.0
  *  protect fields not_registered_in_russia & availability
  *  release 0.47.0
  *  published letter: send archives

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 31 Jul 2019 14:18:25 +0300

## yandex-vos2-autoru-consumers:0.48.1 (Tue, 30 Jul 2019 16:49:59 +0300)

  *  VOS-3196 do not write to sales_services for privates (#238)
  *  Merge pull request #241 from YandexClassifieds/VOS-3179_names
     VOS-3179 mark/model names in offer form converter
  *  
     unit tests fix
  *  
     mark/model names in offer form converter
  *  AUTORUSUP-4709: fix namespace for undo blur
  *  fixed compilation
  *  fixed compilation
  *  VOS-3104 fixed delivery regions set
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  AUTORUAPI-6127 delivery regions in holocron
  *  fix test
  *  VOS-3104 extended holocron validation fixes
  *  disable UserIndex watcher
  *  VOS-3167 drafts manager wip (#231)
  *  VOS-3194: use check exist cache to detect not found images
  *  VOS-3194: don't send photo with namespace autoru-orig to indexer
  *  VOS-3187: fix npe
  *  VOS-3187: fix limiter
  *  Merge pull request #235 from YandexClassifieds/AUTORUAPI-4853_mark_not_found_in_mds
     VOS-3187: mark not found
  *  AUTORUAPI-4853: fix typo
  *  AUTORUAPI-4853: fix test
  *  AUTORUAPI-4853: use check exist photo cache in mds uploader client
  *  AUTORUAPI-4853: change model
  *  reverted local props
  *  VOS-3187: small fix
  *  VOS-3187: fix bugs & refactoring
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  metrics for holocron validation errors
  *  VOS-3187: mark not found
  *  release 0.48.0
  *  protect fields not_registered_in_russia & availability
  *  release 0.47.0
  *  published letter: send archives

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 30 Jul 2019 16:49:59 +0300

## yandex-vos2-autoru-consumers:0.48.0 (Fri, 19 Jul 2019 16:37:21 +0300)

  *  protect fields not_registered_in_russia & availability
  *  release 0.47.0

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 19 Jul 2019 16:37:21 +0300

## yandex-vos2-autoru-consumers:0.47.0 (Fri, 19 Jul 2019 12:48:55 +0300)

  *  VOS-3184 do not recall dealer offer with reason SOLD (#234)
  *  AUTORUAPI-4853: tryTransformAction
  *  AUTORUAPI-4853: fix restore orig
  *  VOS-3161 VOS-3162 new fields (#232)
  *  always set isCallCenter to some value
  *  VOS-3104 fixed wheel drive set
  *  VOS-3104 do not validate is_source field presence: it always would be VOS
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  VOS-3104 updated created field in photo in holocron extended converter
  *  Merge pull request #230 from YandexClassifieds/VOS-3180
     VOS-3180 allow 6 digit frame numbers
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  minor changes
  *  better trace
  *  allow 6 digit frame numbers
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  VOS-3104 fixed holocron extended converter
  *  zio dependency && DraftsManager(#218)

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 19 Jul 2019 12:48:55 +0300

## yandex-vos2-autoru-consumers:0.46.1 (Fri, 12 Jul 2019 19:25:02 +0300)

  *  VOS-3163 Поддержать замену номера телефона на * в описании (#229)
     * VOS-3163 update offer description for opinion of moderation with PHONE_IN_DESC
     
  *  connect scheduler to sentry
  *  remove obsolete dependencies
  *  remove review datatypes
  *  bugfix
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  fixed test
  *  optimize imports
  *  AUTORUSUP-4689 fix sinpcarDataDef
  *  fixed compilation
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  VOS-3104 updated schema registry to fix validation errors, updated holocron extended converter for new model
  *  release 0.46.0
  *  register in ext data service only dataTypes we need instead of all data types
     (cherry picked from commit 7d5e450)
  *  Merge pull request #228 from YandexClassifieds/VOS-3176_rm_additional_offer_mergers
     VOS-3176: remove extra offer mergers (moderation rules)
  *  VOS-3176: remove extra offer mergers (moderation rules)
  *  ignore empty emails from cabinet
  *  better
  *  VOS-3104 fixed color conversion for holocron extended model
  *  VOS-3156 copy from ftp to s3 (#226)
     * VOS-3156 copy from ftp to s3
  *  VOS-3099: notification fixes
  *  VOS-3132 many emails in notification (#224)
  *  Merge pull request #221 from YandexClassifieds/VOS-3099_handle_moder_protect_err
     VOS-3099: new moderation protection error type
  *  compilation fix
  *  VOS-3099: new moderation protection error type

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 12 Jul 2019 19:25:02 +0300

## yandex-vos2-autoru-consumers:0.46.0 (Fri, 12 Jul 2019 12:56:57 +0300)

  *  Merge pull request #228 from YandexClassifieds/VOS-3176_rm_additional_offer_mergers
     VOS-3176: remove extra offer mergers (moderation rules)
  *  VOS-3176: remove extra offer mergers (moderation rules)
  *  ignore empty emails from cabinet
  *  better
  *  VOS-3104 fixed color conversion for holocron extended model
  *  VOS-3156 copy from ftp to s3 (#226)
     * VOS-3156 copy from ftp to s3
  *  VOS-3099: notification fixes
  *  VOS-3132 many emails in notification (#224)
  *  Merge pull request #221 from YandexClassifieds/VOS-3099_handle_moder_protect_err
     VOS-3099: new moderation protection error type
  *  compilation fix
  *  VOS-3099: new moderation protection error type

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 12 Jul 2019 12:56:57 +0300

## yandex-vos2-autoru-consumers:0.45.1 (Tue, 09 Jul 2019 16:47:53 +0300)

  *  removed comment
  *  added enriching with federalSubjectId
  *  Merge pull request #222 from YandexClassifieds/VOS-3116.2
     VOS-3116 Fix. Более надежный механизм обновления пользователя
  *  fix metrics for InstrumentedThreadPool
  *  cleanup
  *  Reformat code
  *  VOS-3116 Более надежный механизм обновления пользователя
  *  cleanup
  *  cleanup
  *  cleanup
  *  refactoring
  *  refactoring
  *  refactoring
  *  Merge pull request #219 from YandexClassifieds/VOS-3099_reliable_feed_check
     VOS-3099: reliable check about feed
  *  VOS-3099: fix test
  *  release 0.45.0
  *  Revert "Revert "VOS-3151 sold inactive""
  *  VOS-3099: reliable check about feed
  *  remove ydb-wrapper code

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 09 Jul 2019 16:47:53 +0300

## yandex-vos2-autoru-consumers:0.45.0 (Mon, 08 Jul 2019 18:19:20 +0300)

  *  Revert "Revert "VOS-3151 sold inactive""
  *  remove ydb-wrapper code

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 08 Jul 2019 18:19:20 +0300

## yandex-vos2-autoru-consumers:0.44.3 (Fri, 05 Jul 2019 18:06:12 +0300)

  *  AUTORUAPI-6083 new body type for trucks (#217)
  *  release 0.44.2
  *  Merge pull request #216 from YandexClassifieds/VOS-3099_fields_info
     VOS-3099: unite geo related fields to one
  *  clean
  *  fix tests
  *  switch to separate ydb-wrapper module
  *  better toString
  *  cleanup
  *  Merge branch 'master' into VOS-3099_fields_info
  *  VOS-3099: unite geo related fields to one
  *  release 0.44.1
  *  VOS-3167 Ydb drafts storage (#204)
  *  Merge pull request #214 from YandexClassifieds/VOS-3099_fields_info
     VOS-3099: correct field names in error description
  *  VOS-3099: correct field names in error description
  *  Изменил текущие маркеры
  *  AUTORUAPI-6078 [vos2] Починить мониторинг DefaultPassportClient.getUser
  *  Merge pull request #212 from YandexClassifieds/_fix_logging
     Явное логирование в DefaultPassportClient.getUser
  *  Merge pull request #206 from YandexClassifieds/AUTORUAPI-5852_update_coordinates
     AUTORUAPI-5852 update coordinates
  *  Убрал лишние скобки
  *  Явное логирование в DefaultPassportClient.getUser
  *  AUTORUAPI-5852 remove duplicate option
  *  AUTORUAPI-5852 remove duplicate option
  *  Revert "AUTORUAPI-5852 fix tests"
     This reverts commit ad60fb18
  *  Merge pull request #200 from YandexClassifieds/VOS-3099_form_moder_protection_list
     VOS-3099: moderation protection list in form
  *  AUTORUAPI-5852 fix tests
  *  VOS-3166 remove MessageTemplate (#209)
  *  VOS-3116 Fix. Более надежный механизм обновления пользователя
  *  Merge branch 'master' into VOS-3099_form_moder_protection_list
  *  Merge pull request #189 from YandexClassifieds/VOS-3116
     VOS-3116 Более надежный механизм обновления пользователя
  *  fix for AUTORUAPI-5691
  *  Autoruapi 6040 (#207)
     * AUTORUAPI-6040 add template parameter for new_email
  *  Rename updateUser def
  *  AUTORUAPI-5852 remove duplicate option
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-5852_update_coordinates
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/validators/CommonFormValidator.scala
  *  AUTORUAPI-5852 validate coordinates
  *  release 0.44.0
  *  AUTORUAPI-5691 send changed fields to chat
  *  Merge pull request #203 from YandexClassifieds/VOS-3099_user_exceptions
     VOS-3099: user exceptions for moderation protection
  *  AUTORUAPI-6040 check email (#205)
     * AUTORUAPI-6040 check email
  *  Merge branch 'master' into VOS-3099_form_moder_protection_list
  *  rm unused function
  *  VOS-3099: write moder prot. fields to form
  *  VOS-3099: moderation protection list in form
  *  VOS-3099: user exceptions for moderation protection
  *  Change log message
  *  Fix consumers
  *  Move writers to new package
  *  VOS-3116 Более надежный механизм обновления пользователя

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 05 Jul 2019 18:06:12 +0300

## yandex-vos2-autoru-consumers:0.44.2 (Fri, 05 Jul 2019 14:50:53 +0300)

  *  Merge pull request #216 from YandexClassifieds/VOS-3099_fields_info
     VOS-3099: unite geo related fields to one
  *  clean
  *  fix tests
  *  switch to separate ydb-wrapper module
  *  better toString
  *  cleanup
  *  Merge branch 'master' into VOS-3099_fields_info
  *  VOS-3099: unite geo related fields to one
  *  release 0.44.1
  *  VOS-3167 Ydb drafts storage (#204)
  *  Merge pull request #214 from YandexClassifieds/VOS-3099_fields_info
     VOS-3099: correct field names in error description
  *  VOS-3099: correct field names in error description
  *  Изменил текущие маркеры
  *  AUTORUAPI-6078 [vos2] Починить мониторинг DefaultPassportClient.getUser
  *  Merge pull request #212 from YandexClassifieds/_fix_logging
     Явное логирование в DefaultPassportClient.getUser
  *  Merge pull request #206 from YandexClassifieds/AUTORUAPI-5852_update_coordinates
     AUTORUAPI-5852 update coordinates
  *  Убрал лишние скобки
  *  Явное логирование в DefaultPassportClient.getUser
  *  AUTORUAPI-5852 remove duplicate option
  *  AUTORUAPI-5852 remove duplicate option
  *  Revert "AUTORUAPI-5852 fix tests"
     This reverts commit ad60fb18
  *  Merge pull request #200 from YandexClassifieds/VOS-3099_form_moder_protection_list
     VOS-3099: moderation protection list in form
  *  AUTORUAPI-5852 fix tests
  *  VOS-3166 remove MessageTemplate (#209)
  *  VOS-3116 Fix. Более надежный механизм обновления пользователя
  *  Merge branch 'master' into VOS-3099_form_moder_protection_list
  *  Merge pull request #189 from YandexClassifieds/VOS-3116
     VOS-3116 Более надежный механизм обновления пользователя
  *  fix for AUTORUAPI-5691
  *  Autoruapi 6040 (#207)
     * AUTORUAPI-6040 add template parameter for new_email
  *  Rename updateUser def
  *  AUTORUAPI-5852 remove duplicate option
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-5852_update_coordinates
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/validators/CommonFormValidator.scala
  *  AUTORUAPI-5852 validate coordinates
  *  release 0.44.0
  *  AUTORUAPI-5691 send changed fields to chat
  *  Merge pull request #203 from YandexClassifieds/VOS-3099_user_exceptions
     VOS-3099: user exceptions for moderation protection
  *  AUTORUAPI-6040 check email (#205)
     * AUTORUAPI-6040 check email
  *  Merge branch 'master' into VOS-3099_form_moder_protection_list
  *  rm unused function
  *  VOS-3099: write moder prot. fields to form
  *  VOS-3099: moderation protection list in form
  *  VOS-3099: user exceptions for moderation protection
  *  Change log message
  *  Fix consumers
  *  Move writers to new package
  *  VOS-3116 Более надежный механизм обновления пользователя

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 05 Jul 2019 14:50:53 +0300

## yandex-vos2-autoru-consumers:0.44.1 (Thu, 04 Jul 2019 18:27:54 +0300)

  *  VOS-3167 Ydb drafts storage (#204)
  *  Merge pull request #214 from YandexClassifieds/VOS-3099_fields_info
     VOS-3099: correct field names in error description
  *  VOS-3099: correct field names in error description
  *  Изменил текущие маркеры
  *  AUTORUAPI-6078 [vos2] Починить мониторинг DefaultPassportClient.getUser
  *  Merge pull request #212 from YandexClassifieds/_fix_logging
     Явное логирование в DefaultPassportClient.getUser
  *  Merge pull request #206 from YandexClassifieds/AUTORUAPI-5852_update_coordinates
     AUTORUAPI-5852 update coordinates
  *  Убрал лишние скобки
  *  Явное логирование в DefaultPassportClient.getUser
  *  AUTORUAPI-5852 remove duplicate option
  *  AUTORUAPI-5852 remove duplicate option
  *  Revert "AUTORUAPI-5852 fix tests"
     This reverts commit ad60fb18
  *  Merge pull request #200 from YandexClassifieds/VOS-3099_form_moder_protection_list
     VOS-3099: moderation protection list in form
  *  AUTORUAPI-5852 fix tests
  *  VOS-3166 remove MessageTemplate (#209)
  *  VOS-3116 Fix. Более надежный механизм обновления пользователя
  *  Merge branch 'master' into VOS-3099_form_moder_protection_list
  *  Merge pull request #189 from YandexClassifieds/VOS-3116
     VOS-3116 Более надежный механизм обновления пользователя
  *  fix for AUTORUAPI-5691
  *  Autoruapi 6040 (#207)
     * AUTORUAPI-6040 add template parameter for new_email
  *  Rename updateUser def
  *  AUTORUAPI-5852 remove duplicate option
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-5852_update_coordinates
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/validators/CommonFormValidator.scala
  *  AUTORUAPI-5852 validate coordinates
  *  release 0.44.0
  *  AUTORUAPI-5691 send changed fields to chat
  *  Merge pull request #203 from YandexClassifieds/VOS-3099_user_exceptions
     VOS-3099: user exceptions for moderation protection
  *  AUTORUAPI-6040 check email (#205)
     * AUTORUAPI-6040 check email
  *  Merge branch 'master' into VOS-3099_form_moder_protection_list
  *  rm unused function
  *  VOS-3099: write moder prot. fields to form
  *  VOS-3099: moderation protection list in form
  *  VOS-3099: user exceptions for moderation protection
  *  Change log message
  *  Fix consumers
  *  Move writers to new package
  *  VOS-3116 Более надежный механизм обновления пользователя

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 04 Jul 2019 18:27:54 +0300

## yandex-vos2-autoru-consumers:0.44.0 (Tue, 02 Jul 2019 19:25:40 +0300)

  *  AUTORUAPI-5691 send changed fields to chat
  *  Merge pull request #203 from YandexClassifieds/VOS-3099_user_exceptions
     VOS-3099: user exceptions for moderation protection
  *  AUTORUAPI-6040 check email (#205)
     * AUTORUAPI-6040 check email
  *  rm unused function
  *  VOS-3099: user exceptions for moderation protection

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 02 Jul 2019 19:25:40 +0300

## yandex-vos2-autoru-consumers:0.43.1 (Mon, 01 Jul 2019 19:52:59 +0300)

  *  AUTORUAPI-6056 remove RegionInfo (#202)
  *  release 0.43.0
  *  AUTORUAPI-6056 RegionInfo (#201)

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 01 Jul 2019 19:52:59 +0300

## yandex-vos2-autoru-consumers:0.43.0 (Mon, 01 Jul 2019 19:34:54 +0300)

  *  AUTORUAPI-6056 RegionInfo (#201)

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 01 Jul 2019 19:34:54 +0300

## yandex-vos2-autoru-consumers:0.42.8 (Mon, 01 Jul 2019 18:50:24 +0300)

  *  Merge pull request #196 from YandexClassifieds/AUTORUAPI-5852_update_coordinates
     AUTORUAPI-5852  moderation update coordinates
  *  cleanup in UserRef classes
  *  remove fields from User
  *  clean imports
  *  fix typo
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-5852_update_coordinates
     # Conflicts:
     #	pom.xml
  *  release 0.42.7
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  VOS-3104 another extended holocron converter fixes after model update
  *  AUTORUAPI-6056 remove DeliveryInfo logic (#197)
  *  AUTORUAPI-5852 filed modifiers equals for coondinates
  *  release 0.42.6
  *  Merge pull request #195 from YandexClassifieds/VOS-3158
     VOS-3158 move to s3edr client
  *  AUTORUAPI-5852 filed modifiers for coondinates
  *  AUTORUAPI-5852 delete useless Salon modifications
  *  AUTORUAPI-5852 add FieldModifiers for coordinates
  *  VOS-3158 added properties for local run
  *  AUTORUAPI-5852  moderation update coordinates
  *  AUTORUAPI-6040 (#194)
     * AUTORUAPI-6040 offer form confirm email
  *  VOS-3158 move to s3edr client
  *  VOS-3104 extended holocron converter fixes
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  fixed offer-to-form converter: set remoteUrl from parse url
  *  release 0.42.5
  *  Revert "VOS-3151 sold inactive"
  *  release 0.42.4
  *  Merge pull request #191 from YandexClassifieds/VOS-3151_sold_incative
     VOS-3151 sold inactive
  *  release 0.42.3
  *  Merge branch 'master' into VOS-3099_getter_exception
  *  VOS-3099: test and code fixes
  *  VOS-3151 sold and docs_sale simultaneously test
  *  Merge remote-tracking branch 'origin/VOS-3138_recognized_lp'
     # Conflicts:
     #	pom.xml
  *  VOS-3138: added feature
  *  remove old class
  *  Merge remote-tracking branch 'origin/master'
  *  AUTORUAPI-4853: added 120x90 resize
  *  VOS-3151 sold inactive
  *  VOS-3157 do not ping mysql in /ping
  *  VOS-3109 moderation deleted photos (#190)
  *  VOS-3099: option in any enums with nonequal sizes
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  do not require photos from moderators
  *  update ydb version
  *  fixed test
  *  updated holocron extended converter
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  AUTORUAPI-3138: delete moderation-micro-core
  *  VOS-3138: set empty license plate if there are not recognized numbers on photo
  *  AUTORUAPI-6040 do not send emails to unconfirmed email
  *  lazy val
  *  fix rur_price conversion
  *  fix test
  *  full rur_price in forms
  *  VOS-3138: only active photo
  *  VOS-3138: hash independent from order
  *  VOS-3138: refactoring & tests
  *  VOS-3138: most frequent license plate
  *  VOS-3138: choose best recognized license plate
  *  AUTORUAPI-6004 is_callcenter from request params (#185)
     * add isCallcenter parameter to RequestInfo
     * move simplifiedValidation to FormWriterParams
     * do not log OfferNotFound in Database
  *  VOS-3104 extended holocron data: fixed message key for extended messages
  *  Merge pull request #186 from YandexClassifieds/VOS-3104_extended_holocron_offer
     VOS-3104 extended holocron converter
  *  VOS-3104 extended holocron data: updated cert data in converter
  *  release 0.42.2
  *  fix changelog
  *  VOS-3104 extended holocron data: updated stage test, fixed big queue sender
  *  Merge branch 'master' into VOS-3104_extended_holocron_offer
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/components/DefaultAutoruCoreComponents.scala
  *  VOS-3104 extended holocron data: fixed config for tests
  *  Merge pull request #168 from YandexClassifieds/VOS-3099_moderation_protection
     Vos 3099 moderation protection
  *  consumer dev config
  *  VOS-3104 extended holocron data: updated holocron stage and sender
  *  VOS-3104 extended holocron converter
  *  VOS-3099: remove auto adding of protected fields
  *  VOS-3099: review fixes
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/FormWriter.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3099: blocking code in separate thread
  *  VOS-3099: fix wrong source skip
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  VOS-3099: modifier test, fix found bugs
  *  
     and compilation fix
  *  
     i am ashamed of my previous commit
  *  
     random test form generator should generate valid steering wheel
  *  
     logs in tests
  *  Merge branch 'master' into AUTORUAPI-5961_steering_wheel
  *  
     tests and fixes
  *  Merge pull request #184 from YandexClassifieds/AUTORUOFFICE-5724-region-id-for-delivery-region-location
     AUTORUOFFICE-5724 rename region_id to federal_subject_id
  *  VOS-3099: fix typos
  *  rename region_id to federal_subject_id
  *  AUTORUAPI-4853: debug logs
  *  rename region id field
  *  added region id to delivery region location
  *  Merge remote-tracking branch 'origin/master'
  *  fix teleperformance metrics
  *  AUTORUAPI-6000 (#180)
     * cleanup
     
     * AUTORUAPI-6000 enable promocodes in 3 new regions
  *  
     validate steering wheel by tech param id
  *  VOS-3099: handle fields with message type
  *  AUTORUAPI-4853: support 1200x900 for autoru-orig
  *  AUTORUAPI-4853: debug logs
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/PhotoUtils.scala
  *  AUTORUAPI-4853: debug logs
  *  VOS-3099: some getters and modifiers implementation
  *  Merge pull request #178 from YandexClassifieds/AUTORUAPI-5982_fix_photo_id_format
     AUTORUAPI-5982: public photo_id format
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: delete version 1 filter
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-5929_redemption_enable
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/properties.conf
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/features/AutoruFeatures.scala
  *  AUTORUAPI-5929: fix password
  *  restore size 456x342
  *  AUTORUAPI-5961 fix npe
  *  VOS-3099: protected field REST API
  *  VOS-3099: move application-specific code from DAO to OfferWriter
  *  AUTORUAPI-5961 move under feature
  *  AUTORUAPI-5961 fix
  *  AUTORUAPI-5961 steering wheel validation
  *  VOS-3099: introduce feature, catch possible exceptions from field getters
  *  Fix shard2 port in local conf (#174)
  *  fix password
  *  VOS-3099: protection hooks in api handlers
  *  VOS-3099 use enum fields instead of strings
  *  AUTORUAPI-4853: fix read url for original photo
  *  temporarily pending integration test
  *  VOS-3136: fix url for original photo
  *  VOS-3136: fix tests
  *  send not blurred photo to moderation
  *  Vos 3141 Обрабатывать резолюцию "Недозвон" от колл-центра (#170)
     * VOS-3141 support NO_ANSWER
  *  AUTORUAPI-5929: fix tests
  *  AUTORUAPI-5929: redemption come back
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  extract youtube request from mutator function
  *  Merge pull request #166 from YandexClassifieds/AUTORUAPI-5970
     AUTORUAPI-5970 add options mapping to converter
  *  Merge remote-tracking branch 'origin/master'
  *  optimize imports
  *  VOS-3099: moderation protection and validation
  *  VOS-3099: change get/has method params to offerOrBuilder
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into AUTORUOFFICE-5600-add-filter-by-delivery-region
  *  refactored tests + fixed tags list modification
  *  update zk dev address
  *  AUTORUAPI-5970 fix error
  *  AUTORUAPI-5970 add options mapping to converter
  *  VOS-3099: field gettter/setter draft
  *  added new tag for offer which will be created if deliveryInfo is not empty and removed is one is empty
  *  Vos 3022 AVAILABILITY (#164)
     * VOS-3022 Availability
  *  update zk dev address
  *  Merge pull request #159 from YandexClassifieds/CARFAX-238
     CARFAX-238 change reload stage behaviour and  add test
  *  release 0.42.0
  *  Merge pull request #157 from YandexClassifieds/AUTORUAPI-4853_switch_private_users_to_new_namespaces
     AUTORUAPI-4853: added namespace to form photo name
  *  Merge pull request #162 from YandexClassifieds/AUTORUOFFICE-5682-save-region-info
     AUTORUOFFICE-5682 save region info
  *  release 0.41.7
  *  added regionInfo to offer response model.
  *  added regionInfo to delivery region location.
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: refactoring and fix tests
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_switch_private_users_to_new_namespaces
     # Conflicts:
     #	vos2-autoru-api/src/test/scala/ru/yandex/vos2/autoru/api/v1/draft/DraftHandlerPhotosTest.scala
  *  AUTORUAPI-4853: refactoring
  *  change behaviour and  add test
  *  VOS-3136: added original and process original
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: added namespace to form photo name
  *  VOS-3099: mv to another package
  *  VOS-3099: moderation protection hooks draft

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 01 Jul 2019 18:50:24 +0300

## yandex-vos2-autoru-consumers:0.42.7 (Fri, 28 Jun 2019 18:22:35 +0300)

  *  AUTORUAPI-6056 remove DeliveryInfo logic (#197)
  *  release 0.42.6
  *  Merge pull request #195 from YandexClassifieds/VOS-3158
     VOS-3158 move to s3edr client
  *  VOS-3158 added properties for local run
  *  AUTORUAPI-6040 (#194)
     * AUTORUAPI-6040 offer form confirm email
  *  VOS-3158 move to s3edr client
  *  VOS-3104 extended holocron converter fixes
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  fixed offer-to-form converter: set remoteUrl from parse url
  *  release 0.42.5
  *  Revert "VOS-3151 sold inactive"
  *  release 0.42.4
  *  Merge pull request #191 from YandexClassifieds/VOS-3151_sold_incative
     VOS-3151 sold inactive
  *  release 0.42.3
  *  Merge branch 'master' into VOS-3099_getter_exception
  *  VOS-3099: test and code fixes
  *  VOS-3151 sold and docs_sale simultaneously test
  *  Merge remote-tracking branch 'origin/VOS-3138_recognized_lp'
     # Conflicts:
     #	pom.xml
  *  VOS-3138: added feature
  *  remove old class
  *  Merge remote-tracking branch 'origin/master'
  *  AUTORUAPI-4853: added 120x90 resize
  *  VOS-3151 sold inactive
  *  VOS-3157 do not ping mysql in /ping
  *  VOS-3109 moderation deleted photos (#190)
  *  VOS-3099: option in any enums with nonequal sizes
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  do not require photos from moderators
  *  update ydb version
  *  fixed test
  *  updated holocron extended converter
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  AUTORUAPI-3138: delete moderation-micro-core
  *  VOS-3138: set empty license plate if there are not recognized numbers on photo
  *  AUTORUAPI-6040 do not send emails to unconfirmed email
  *  lazy val
  *  fix rur_price conversion
  *  fix test
  *  full rur_price in forms
  *  VOS-3138: only active photo
  *  VOS-3138: hash independent from order
  *  VOS-3138: refactoring & tests
  *  VOS-3138: most frequent license plate
  *  VOS-3138: choose best recognized license plate
  *  AUTORUAPI-6004 is_callcenter from request params (#185)
     * add isCallcenter parameter to RequestInfo
     * move simplifiedValidation to FormWriterParams
     * do not log OfferNotFound in Database
  *  VOS-3104 extended holocron data: fixed message key for extended messages
  *  Merge pull request #186 from YandexClassifieds/VOS-3104_extended_holocron_offer
     VOS-3104 extended holocron converter
  *  VOS-3104 extended holocron data: updated cert data in converter
  *  release 0.42.2
  *  fix changelog
  *  VOS-3104 extended holocron data: updated stage test, fixed big queue sender
  *  Merge branch 'master' into VOS-3104_extended_holocron_offer
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/components/DefaultAutoruCoreComponents.scala
  *  VOS-3104 extended holocron data: fixed config for tests
  *  Merge pull request #168 from YandexClassifieds/VOS-3099_moderation_protection
     Vos 3099 moderation protection
  *  consumer dev config
  *  VOS-3104 extended holocron data: updated holocron stage and sender
  *  VOS-3104 extended holocron converter
  *  VOS-3099: remove auto adding of protected fields
  *  VOS-3099: review fixes
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/FormWriter.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3099: blocking code in separate thread
  *  VOS-3099: fix wrong source skip
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  VOS-3099: modifier test, fix found bugs
  *  
     and compilation fix
  *  
     i am ashamed of my previous commit
  *  
     random test form generator should generate valid steering wheel
  *  
     logs in tests
  *  Merge branch 'master' into AUTORUAPI-5961_steering_wheel
  *  
     tests and fixes
  *  Merge pull request #184 from YandexClassifieds/AUTORUOFFICE-5724-region-id-for-delivery-region-location
     AUTORUOFFICE-5724 rename region_id to federal_subject_id
  *  VOS-3099: fix typos
  *  rename region_id to federal_subject_id
  *  AUTORUAPI-4853: debug logs
  *  rename region id field
  *  added region id to delivery region location
  *  Merge remote-tracking branch 'origin/master'
  *  fix teleperformance metrics
  *  AUTORUAPI-6000 (#180)
     * cleanup
     
     * AUTORUAPI-6000 enable promocodes in 3 new regions
  *  
     validate steering wheel by tech param id
  *  VOS-3099: handle fields with message type
  *  AUTORUAPI-4853: support 1200x900 for autoru-orig
  *  AUTORUAPI-4853: debug logs
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/PhotoUtils.scala
  *  AUTORUAPI-4853: debug logs
  *  VOS-3099: some getters and modifiers implementation
  *  Merge pull request #178 from YandexClassifieds/AUTORUAPI-5982_fix_photo_id_format
     AUTORUAPI-5982: public photo_id format
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: delete version 1 filter
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-5929_redemption_enable
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/properties.conf
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/features/AutoruFeatures.scala
  *  AUTORUAPI-5929: fix password
  *  restore size 456x342
  *  AUTORUAPI-5961 fix npe
  *  VOS-3099: protected field REST API
  *  VOS-3099: move application-specific code from DAO to OfferWriter
  *  AUTORUAPI-5961 move under feature
  *  AUTORUAPI-5961 fix
  *  AUTORUAPI-5961 steering wheel validation
  *  VOS-3099: introduce feature, catch possible exceptions from field getters
  *  Fix shard2 port in local conf (#174)
  *  fix password
  *  VOS-3099: protection hooks in api handlers
  *  VOS-3099 use enum fields instead of strings
  *  AUTORUAPI-4853: fix read url for original photo
  *  temporarily pending integration test
  *  VOS-3136: fix url for original photo
  *  VOS-3136: fix tests
  *  send not blurred photo to moderation
  *  Vos 3141 Обрабатывать резолюцию "Недозвон" от колл-центра (#170)
     * VOS-3141 support NO_ANSWER
  *  AUTORUAPI-5929: fix tests
  *  AUTORUAPI-5929: redemption come back
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  extract youtube request from mutator function
  *  Merge pull request #166 from YandexClassifieds/AUTORUAPI-5970
     AUTORUAPI-5970 add options mapping to converter
  *  Merge remote-tracking branch 'origin/master'
  *  optimize imports
  *  VOS-3099: moderation protection and validation
  *  VOS-3099: change get/has method params to offerOrBuilder
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into AUTORUOFFICE-5600-add-filter-by-delivery-region
  *  refactored tests + fixed tags list modification
  *  update zk dev address
  *  AUTORUAPI-5970 fix error
  *  AUTORUAPI-5970 add options mapping to converter
  *  VOS-3099: field gettter/setter draft
  *  added new tag for offer which will be created if deliveryInfo is not empty and removed is one is empty
  *  Vos 3022 AVAILABILITY (#164)
     * VOS-3022 Availability
  *  update zk dev address
  *  Merge pull request #159 from YandexClassifieds/CARFAX-238
     CARFAX-238 change reload stage behaviour and  add test
  *  release 0.42.0
  *  Merge pull request #157 from YandexClassifieds/AUTORUAPI-4853_switch_private_users_to_new_namespaces
     AUTORUAPI-4853: added namespace to form photo name
  *  Merge pull request #162 from YandexClassifieds/AUTORUOFFICE-5682-save-region-info
     AUTORUOFFICE-5682 save region info
  *  release 0.41.7
  *  added regionInfo to offer response model.
  *  added regionInfo to delivery region location.
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: refactoring and fix tests
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_switch_private_users_to_new_namespaces
     # Conflicts:
     #	vos2-autoru-api/src/test/scala/ru/yandex/vos2/autoru/api/v1/draft/DraftHandlerPhotosTest.scala
  *  AUTORUAPI-4853: refactoring
  *  change behaviour and  add test
  *  VOS-3136: added original and process original
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: added namespace to form photo name
  *  VOS-3099: mv to another package
  *  VOS-3099: moderation protection hooks draft

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 28 Jun 2019 18:22:35 +0300

## yandex-vos2-autoru-consumers:0.42.6 (Fri, 28 Jun 2019 17:21:18 +0300)

  *  Merge pull request #195 from YandexClassifieds/VOS-3158
     VOS-3158 move to s3edr client
  *  VOS-3158 added properties for local run
  *  AUTORUAPI-6040 (#194)
     * AUTORUAPI-6040 offer form confirm email
  *  VOS-3158 move to s3edr client
  *  VOS-3104 extended holocron converter fixes
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru
  *  fixed offer-to-form converter: set remoteUrl from parse url
  *  release 0.42.5
  *  Revert "VOS-3151 sold inactive"
  *  release 0.42.4
  *  Merge pull request #191 from YandexClassifieds/VOS-3151_sold_incative
     VOS-3151 sold inactive
  *  release 0.42.3
  *  Merge branch 'master' into VOS-3099_getter_exception
  *  VOS-3099: test and code fixes
  *  VOS-3151 sold and docs_sale simultaneously test
  *  Merge remote-tracking branch 'origin/VOS-3138_recognized_lp'
     # Conflicts:
     #	pom.xml
  *  VOS-3138: added feature
  *  remove old class
  *  Merge remote-tracking branch 'origin/master'
  *  AUTORUAPI-4853: added 120x90 resize
  *  VOS-3151 sold inactive
  *  VOS-3157 do not ping mysql in /ping
  *  VOS-3109 moderation deleted photos (#190)
  *  VOS-3099: option in any enums with nonequal sizes
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  do not require photos from moderators
  *  update ydb version
  *  fixed test
  *  updated holocron extended converter
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  AUTORUAPI-3138: delete moderation-micro-core
  *  VOS-3138: set empty license plate if there are not recognized numbers on photo
  *  AUTORUAPI-6040 do not send emails to unconfirmed email
  *  lazy val
  *  fix rur_price conversion
  *  fix test
  *  full rur_price in forms
  *  VOS-3138: only active photo
  *  VOS-3138: hash independent from order
  *  VOS-3138: refactoring & tests
  *  VOS-3138: most frequent license plate
  *  VOS-3138: choose best recognized license plate
  *  AUTORUAPI-6004 is_callcenter from request params (#185)
     * add isCallcenter parameter to RequestInfo
     * move simplifiedValidation to FormWriterParams
     * do not log OfferNotFound in Database
  *  VOS-3104 extended holocron data: fixed message key for extended messages
  *  Merge pull request #186 from YandexClassifieds/VOS-3104_extended_holocron_offer
     VOS-3104 extended holocron converter
  *  VOS-3104 extended holocron data: updated cert data in converter
  *  release 0.42.2
  *  fix changelog
  *  VOS-3104 extended holocron data: updated stage test, fixed big queue sender
  *  Merge branch 'master' into VOS-3104_extended_holocron_offer
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/components/DefaultAutoruCoreComponents.scala
  *  VOS-3104 extended holocron data: fixed config for tests
  *  Merge pull request #168 from YandexClassifieds/VOS-3099_moderation_protection
     Vos 3099 moderation protection
  *  consumer dev config
  *  VOS-3104 extended holocron data: updated holocron stage and sender
  *  VOS-3104 extended holocron converter
  *  VOS-3099: remove auto adding of protected fields
  *  VOS-3099: review fixes
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/FormWriter.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3099: blocking code in separate thread
  *  VOS-3099: fix wrong source skip
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  VOS-3099: modifier test, fix found bugs
  *  
     and compilation fix
  *  
     i am ashamed of my previous commit
  *  
     random test form generator should generate valid steering wheel
  *  
     logs in tests
  *  Merge branch 'master' into AUTORUAPI-5961_steering_wheel
  *  
     tests and fixes
  *  Merge pull request #184 from YandexClassifieds/AUTORUOFFICE-5724-region-id-for-delivery-region-location
     AUTORUOFFICE-5724 rename region_id to federal_subject_id
  *  VOS-3099: fix typos
  *  rename region_id to federal_subject_id
  *  AUTORUAPI-4853: debug logs
  *  rename region id field
  *  added region id to delivery region location
  *  Merge remote-tracking branch 'origin/master'
  *  fix teleperformance metrics
  *  AUTORUAPI-6000 (#180)
     * cleanup
     
     * AUTORUAPI-6000 enable promocodes in 3 new regions
  *  
     validate steering wheel by tech param id
  *  VOS-3099: handle fields with message type
  *  AUTORUAPI-4853: support 1200x900 for autoru-orig
  *  AUTORUAPI-4853: debug logs
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/PhotoUtils.scala
  *  AUTORUAPI-4853: debug logs
  *  VOS-3099: some getters and modifiers implementation
  *  Merge pull request #178 from YandexClassifieds/AUTORUAPI-5982_fix_photo_id_format
     AUTORUAPI-5982: public photo_id format
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: delete version 1 filter
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-5929_redemption_enable
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/properties.conf
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/features/AutoruFeatures.scala
  *  AUTORUAPI-5929: fix password
  *  restore size 456x342
  *  AUTORUAPI-5961 fix npe
  *  VOS-3099: protected field REST API
  *  VOS-3099: move application-specific code from DAO to OfferWriter
  *  AUTORUAPI-5961 move under feature
  *  AUTORUAPI-5961 fix
  *  AUTORUAPI-5961 steering wheel validation
  *  VOS-3099: introduce feature, catch possible exceptions from field getters
  *  Fix shard2 port in local conf (#174)
  *  fix password
  *  VOS-3099: protection hooks in api handlers
  *  VOS-3099 use enum fields instead of strings
  *  AUTORUAPI-4853: fix read url for original photo
  *  temporarily pending integration test
  *  VOS-3136: fix url for original photo
  *  VOS-3136: fix tests
  *  send not blurred photo to moderation
  *  Vos 3141 Обрабатывать резолюцию "Недозвон" от колл-центра (#170)
     * VOS-3141 support NO_ANSWER
  *  AUTORUAPI-5929: fix tests
  *  AUTORUAPI-5929: redemption come back
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  extract youtube request from mutator function
  *  Merge pull request #166 from YandexClassifieds/AUTORUAPI-5970
     AUTORUAPI-5970 add options mapping to converter
  *  Merge remote-tracking branch 'origin/master'
  *  optimize imports
  *  VOS-3099: moderation protection and validation
  *  VOS-3099: change get/has method params to offerOrBuilder
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into AUTORUOFFICE-5600-add-filter-by-delivery-region
  *  refactored tests + fixed tags list modification
  *  update zk dev address
  *  AUTORUAPI-5970 fix error
  *  AUTORUAPI-5970 add options mapping to converter
  *  VOS-3099: field gettter/setter draft
  *  added new tag for offer which will be created if deliveryInfo is not empty and removed is one is empty
  *  Vos 3022 AVAILABILITY (#164)
     * VOS-3022 Availability
  *  update zk dev address
  *  Merge pull request #159 from YandexClassifieds/CARFAX-238
     CARFAX-238 change reload stage behaviour and  add test
  *  release 0.42.0
  *  Merge pull request #157 from YandexClassifieds/AUTORUAPI-4853_switch_private_users_to_new_namespaces
     AUTORUAPI-4853: added namespace to form photo name
  *  Merge pull request #162 from YandexClassifieds/AUTORUOFFICE-5682-save-region-info
     AUTORUOFFICE-5682 save region info
  *  release 0.41.7
  *  added regionInfo to offer response model.
  *  added regionInfo to delivery region location.
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: refactoring and fix tests
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_switch_private_users_to_new_namespaces
     # Conflicts:
     #	vos2-autoru-api/src/test/scala/ru/yandex/vos2/autoru/api/v1/draft/DraftHandlerPhotosTest.scala
  *  AUTORUAPI-4853: refactoring
  *  change behaviour and  add test
  *  VOS-3136: added original and process original
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: added namespace to form photo name
  *  VOS-3099: mv to another package
  *  VOS-3099: moderation protection hooks draft

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 28 Jun 2019 17:21:18 +0300

## yandex-vos2-autoru-consumers:0.42.5 (Thu, 27 Jun 2019 15:35:20 +0300)

  *  Revert "VOS-3151 sold inactive"
  *  release 0.42.4
  *  Merge pull request #191 from YandexClassifieds/VOS-3151_sold_incative
     VOS-3151 sold inactive
  *  release 0.42.3
  *  Merge branch 'master' into VOS-3099_getter_exception
  *  VOS-3099: test and code fixes
  *  VOS-3151 sold and docs_sale simultaneously test
  *  Merge remote-tracking branch 'origin/VOS-3138_recognized_lp'
     # Conflicts:
     #	pom.xml
  *  VOS-3138: added feature
  *  remove old class
  *  Merge remote-tracking branch 'origin/master'
  *  AUTORUAPI-4853: added 120x90 resize
  *  VOS-3151 sold inactive
  *  VOS-3157 do not ping mysql in /ping
  *  VOS-3109 moderation deleted photos (#190)
  *  VOS-3099: option in any enums with nonequal sizes
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  do not require photos from moderators
  *  update ydb version
  *  fixed test
  *  updated holocron extended converter
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  AUTORUAPI-3138: delete moderation-micro-core
  *  VOS-3138: set empty license plate if there are not recognized numbers on photo
  *  AUTORUAPI-6040 do not send emails to unconfirmed email
  *  lazy val
  *  fix rur_price conversion
  *  fix test
  *  full rur_price in forms
  *  VOS-3138: only active photo
  *  VOS-3138: hash independent from order
  *  VOS-3138: refactoring & tests
  *  VOS-3138: most frequent license plate
  *  VOS-3138: choose best recognized license plate
  *  AUTORUAPI-6004 is_callcenter from request params (#185)
     * add isCallcenter parameter to RequestInfo
     * move simplifiedValidation to FormWriterParams
     * do not log OfferNotFound in Database
  *  VOS-3104 extended holocron data: fixed message key for extended messages
  *  Merge pull request #186 from YandexClassifieds/VOS-3104_extended_holocron_offer
     VOS-3104 extended holocron converter
  *  VOS-3104 extended holocron data: updated cert data in converter
  *  release 0.42.2
  *  fix changelog
  *  VOS-3104 extended holocron data: updated stage test, fixed big queue sender
  *  Merge branch 'master' into VOS-3104_extended_holocron_offer
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/components/DefaultAutoruCoreComponents.scala
  *  VOS-3104 extended holocron data: fixed config for tests
  *  Merge pull request #168 from YandexClassifieds/VOS-3099_moderation_protection
     Vos 3099 moderation protection
  *  consumer dev config
  *  VOS-3104 extended holocron data: updated holocron stage and sender
  *  VOS-3104 extended holocron converter
  *  VOS-3099: remove auto adding of protected fields
  *  VOS-3099: review fixes
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/FormWriter.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3099: blocking code in separate thread
  *  VOS-3099: fix wrong source skip
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  VOS-3099: modifier test, fix found bugs
  *  
     and compilation fix
  *  
     i am ashamed of my previous commit
  *  
     random test form generator should generate valid steering wheel
  *  
     logs in tests
  *  Merge branch 'master' into AUTORUAPI-5961_steering_wheel
  *  
     tests and fixes
  *  Merge pull request #184 from YandexClassifieds/AUTORUOFFICE-5724-region-id-for-delivery-region-location
     AUTORUOFFICE-5724 rename region_id to federal_subject_id
  *  VOS-3099: fix typos
  *  rename region_id to federal_subject_id
  *  AUTORUAPI-4853: debug logs
  *  rename region id field
  *  added region id to delivery region location
  *  Merge remote-tracking branch 'origin/master'
  *  fix teleperformance metrics
  *  AUTORUAPI-6000 (#180)
     * cleanup
     
     * AUTORUAPI-6000 enable promocodes in 3 new regions
  *  
     validate steering wheel by tech param id
  *  VOS-3099: handle fields with message type
  *  AUTORUAPI-4853: support 1200x900 for autoru-orig
  *  AUTORUAPI-4853: debug logs
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/PhotoUtils.scala
  *  AUTORUAPI-4853: debug logs
  *  VOS-3099: some getters and modifiers implementation
  *  Merge pull request #178 from YandexClassifieds/AUTORUAPI-5982_fix_photo_id_format
     AUTORUAPI-5982: public photo_id format
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: delete version 1 filter
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-5929_redemption_enable
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/properties.conf
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/features/AutoruFeatures.scala
  *  AUTORUAPI-5929: fix password
  *  restore size 456x342
  *  AUTORUAPI-5961 fix npe
  *  VOS-3099: protected field REST API
  *  VOS-3099: move application-specific code from DAO to OfferWriter
  *  AUTORUAPI-5961 move under feature
  *  AUTORUAPI-5961 fix
  *  AUTORUAPI-5961 steering wheel validation
  *  VOS-3099: introduce feature, catch possible exceptions from field getters
  *  Fix shard2 port in local conf (#174)
  *  fix password
  *  VOS-3099: protection hooks in api handlers
  *  VOS-3099 use enum fields instead of strings
  *  AUTORUAPI-4853: fix read url for original photo
  *  temporarily pending integration test
  *  VOS-3136: fix url for original photo
  *  VOS-3136: fix tests
  *  send not blurred photo to moderation
  *  Vos 3141 Обрабатывать резолюцию "Недозвон" от колл-центра (#170)
     * VOS-3141 support NO_ANSWER
  *  AUTORUAPI-5929: fix tests
  *  AUTORUAPI-5929: redemption come back
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  extract youtube request from mutator function
  *  Merge pull request #166 from YandexClassifieds/AUTORUAPI-5970
     AUTORUAPI-5970 add options mapping to converter
  *  Merge remote-tracking branch 'origin/master'
  *  optimize imports
  *  VOS-3099: moderation protection and validation
  *  VOS-3099: change get/has method params to offerOrBuilder
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into AUTORUOFFICE-5600-add-filter-by-delivery-region
  *  refactored tests + fixed tags list modification
  *  update zk dev address
  *  AUTORUAPI-5970 fix error
  *  AUTORUAPI-5970 add options mapping to converter
  *  VOS-3099: field gettter/setter draft
  *  added new tag for offer which will be created if deliveryInfo is not empty and removed is one is empty
  *  Vos 3022 AVAILABILITY (#164)
     * VOS-3022 Availability
  *  update zk dev address
  *  Merge pull request #159 from YandexClassifieds/CARFAX-238
     CARFAX-238 change reload stage behaviour and  add test
  *  release 0.42.0
  *  Merge pull request #157 from YandexClassifieds/AUTORUAPI-4853_switch_private_users_to_new_namespaces
     AUTORUAPI-4853: added namespace to form photo name
  *  Merge pull request #162 from YandexClassifieds/AUTORUOFFICE-5682-save-region-info
     AUTORUOFFICE-5682 save region info
  *  release 0.41.7
  *  added regionInfo to offer response model.
  *  added regionInfo to delivery region location.
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: refactoring and fix tests
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_switch_private_users_to_new_namespaces
     # Conflicts:
     #	vos2-autoru-api/src/test/scala/ru/yandex/vos2/autoru/api/v1/draft/DraftHandlerPhotosTest.scala
  *  AUTORUAPI-4853: refactoring
  *  change behaviour and  add test
  *  VOS-3136: added original and process original
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: added namespace to form photo name
  *  VOS-3099: mv to another package
  *  VOS-3099: moderation protection hooks draft

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 27 Jun 2019 15:35:20 +0300

## yandex-vos2-autoru-consumers:0.42.4 (Thu, 27 Jun 2019 13:11:23 +0300)

  *  Merge pull request #191 from YandexClassifieds/VOS-3151_sold_incative
     VOS-3151 sold inactive
  *  release 0.42.3
  *  Merge branch 'master' into VOS-3099_getter_exception
  *  VOS-3099: test and code fixes
  *  VOS-3151 sold and docs_sale simultaneously test
  *  Merge remote-tracking branch 'origin/VOS-3138_recognized_lp'
     # Conflicts:
     #	pom.xml
  *  VOS-3138: added feature
  *  remove old class
  *  Merge remote-tracking branch 'origin/master'
  *  AUTORUAPI-4853: added 120x90 resize
  *  VOS-3151 sold inactive
  *  VOS-3157 do not ping mysql in /ping
  *  VOS-3109 moderation deleted photos (#190)
  *  VOS-3099: option in any enums with nonequal sizes
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  do not require photos from moderators
  *  update ydb version
  *  fixed test
  *  updated holocron extended converter
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  AUTORUAPI-3138: delete moderation-micro-core
  *  VOS-3138: set empty license plate if there are not recognized numbers on photo
  *  AUTORUAPI-6040 do not send emails to unconfirmed email
  *  lazy val
  *  fix rur_price conversion
  *  fix test
  *  full rur_price in forms
  *  VOS-3138: only active photo
  *  VOS-3138: hash independent from order
  *  VOS-3138: refactoring & tests
  *  VOS-3138: most frequent license plate
  *  VOS-3138: choose best recognized license plate
  *  AUTORUAPI-6004 is_callcenter from request params (#185)
     * add isCallcenter parameter to RequestInfo
     * move simplifiedValidation to FormWriterParams
     * do not log OfferNotFound in Database
  *  VOS-3104 extended holocron data: fixed message key for extended messages
  *  Merge pull request #186 from YandexClassifieds/VOS-3104_extended_holocron_offer
     VOS-3104 extended holocron converter
  *  VOS-3104 extended holocron data: updated cert data in converter
  *  release 0.42.2
  *  fix changelog
  *  VOS-3104 extended holocron data: updated stage test, fixed big queue sender
  *  Merge branch 'master' into VOS-3104_extended_holocron_offer
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/components/DefaultAutoruCoreComponents.scala
  *  VOS-3104 extended holocron data: fixed config for tests
  *  Merge pull request #168 from YandexClassifieds/VOS-3099_moderation_protection
     Vos 3099 moderation protection
  *  consumer dev config
  *  VOS-3104 extended holocron data: updated holocron stage and sender
  *  VOS-3104 extended holocron converter
  *  VOS-3099: remove auto adding of protected fields
  *  VOS-3099: review fixes
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/FormWriter.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3099: blocking code in separate thread
  *  VOS-3099: fix wrong source skip
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  VOS-3099: modifier test, fix found bugs
  *  
     and compilation fix
  *  
     i am ashamed of my previous commit
  *  
     random test form generator should generate valid steering wheel
  *  
     logs in tests
  *  Merge branch 'master' into AUTORUAPI-5961_steering_wheel
  *  
     tests and fixes
  *  Merge pull request #184 from YandexClassifieds/AUTORUOFFICE-5724-region-id-for-delivery-region-location
     AUTORUOFFICE-5724 rename region_id to federal_subject_id
  *  VOS-3099: fix typos
  *  rename region_id to federal_subject_id
  *  AUTORUAPI-4853: debug logs
  *  rename region id field
  *  added region id to delivery region location
  *  Merge remote-tracking branch 'origin/master'
  *  fix teleperformance metrics
  *  AUTORUAPI-6000 (#180)
     * cleanup
     
     * AUTORUAPI-6000 enable promocodes in 3 new regions
  *  
     validate steering wheel by tech param id
  *  VOS-3099: handle fields with message type
  *  AUTORUAPI-4853: support 1200x900 for autoru-orig
  *  AUTORUAPI-4853: debug logs
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/PhotoUtils.scala
  *  AUTORUAPI-4853: debug logs
  *  VOS-3099: some getters and modifiers implementation
  *  Merge pull request #178 from YandexClassifieds/AUTORUAPI-5982_fix_photo_id_format
     AUTORUAPI-5982: public photo_id format
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: delete version 1 filter
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-5929_redemption_enable
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/properties.conf
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/features/AutoruFeatures.scala
  *  AUTORUAPI-5929: fix password
  *  restore size 456x342
  *  AUTORUAPI-5961 fix npe
  *  VOS-3099: protected field REST API
  *  VOS-3099: move application-specific code from DAO to OfferWriter
  *  AUTORUAPI-5961 move under feature
  *  AUTORUAPI-5961 fix
  *  AUTORUAPI-5961 steering wheel validation
  *  VOS-3099: introduce feature, catch possible exceptions from field getters
  *  Fix shard2 port in local conf (#174)
  *  fix password
  *  VOS-3099: protection hooks in api handlers
  *  VOS-3099 use enum fields instead of strings
  *  AUTORUAPI-4853: fix read url for original photo
  *  temporarily pending integration test
  *  VOS-3136: fix url for original photo
  *  VOS-3136: fix tests
  *  send not blurred photo to moderation
  *  Vos 3141 Обрабатывать резолюцию "Недозвон" от колл-центра (#170)
     * VOS-3141 support NO_ANSWER
  *  AUTORUAPI-5929: fix tests
  *  AUTORUAPI-5929: redemption come back
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  extract youtube request from mutator function
  *  Merge pull request #166 from YandexClassifieds/AUTORUAPI-5970
     AUTORUAPI-5970 add options mapping to converter
  *  Merge remote-tracking branch 'origin/master'
  *  optimize imports
  *  VOS-3099: moderation protection and validation
  *  VOS-3099: change get/has method params to offerOrBuilder
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into AUTORUOFFICE-5600-add-filter-by-delivery-region
  *  refactored tests + fixed tags list modification
  *  update zk dev address
  *  AUTORUAPI-5970 fix error
  *  AUTORUAPI-5970 add options mapping to converter
  *  VOS-3099: field gettter/setter draft
  *  added new tag for offer which will be created if deliveryInfo is not empty and removed is one is empty
  *  Vos 3022 AVAILABILITY (#164)
     * VOS-3022 Availability
  *  update zk dev address
  *  Merge pull request #159 from YandexClassifieds/CARFAX-238
     CARFAX-238 change reload stage behaviour and  add test
  *  release 0.42.0
  *  Merge pull request #157 from YandexClassifieds/AUTORUAPI-4853_switch_private_users_to_new_namespaces
     AUTORUAPI-4853: added namespace to form photo name
  *  Merge pull request #162 from YandexClassifieds/AUTORUOFFICE-5682-save-region-info
     AUTORUOFFICE-5682 save region info
  *  release 0.41.7
  *  added regionInfo to offer response model.
  *  added regionInfo to delivery region location.
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: refactoring and fix tests
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_switch_private_users_to_new_namespaces
     # Conflicts:
     #	vos2-autoru-api/src/test/scala/ru/yandex/vos2/autoru/api/v1/draft/DraftHandlerPhotosTest.scala
  *  AUTORUAPI-4853: refactoring
  *  change behaviour and  add test
  *  VOS-3136: added original and process original
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: added namespace to form photo name
  *  VOS-3099: mv to another package
  *  VOS-3099: moderation protection hooks draft

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 27 Jun 2019 13:11:23 +0300

## yandex-vos2-autoru-consumers:0.42.3 (Wed, 26 Jun 2019 20:19:45 +0300)

  *  Merge branch 'master' into VOS-3099_getter_exception
  *  VOS-3099: test and code fixes
  *  Merge remote-tracking branch 'origin/VOS-3138_recognized_lp'
     # Conflicts:
     #	pom.xml
  *  VOS-3138: added feature
  *  remove old class
  *  Merge remote-tracking branch 'origin/master'
  *  AUTORUAPI-4853: added 120x90 resize
  *  VOS-3157 do not ping mysql in /ping
  *  VOS-3109 moderation deleted photos (#190)
  *  VOS-3099: option in any enums with nonequal sizes
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  do not require photos from moderators
  *  update ydb version
  *  fixed test
  *  updated holocron extended converter
  *  Merge remote-tracking branch 'origin/master' into VOS-3138_recognized_lp
     # Conflicts:
     #	pom.xml
  *  AUTORUAPI-3138: delete moderation-micro-core
  *  VOS-3138: set empty license plate if there are not recognized numbers on photo
  *  AUTORUAPI-6040 do not send emails to unconfirmed email
  *  lazy val
  *  fix rur_price conversion
  *  fix test
  *  full rur_price in forms
  *  VOS-3138: only active photo
  *  VOS-3138: hash independent from order
  *  VOS-3138: refactoring & tests
  *  VOS-3138: most frequent license plate
  *  VOS-3138: choose best recognized license plate
  *  AUTORUAPI-6004 is_callcenter from request params (#185)
     * add isCallcenter parameter to RequestInfo
     * move simplifiedValidation to FormWriterParams
     * do not log OfferNotFound in Database
  *  VOS-3104 extended holocron data: fixed message key for extended messages
  *  Merge pull request #186 from YandexClassifieds/VOS-3104_extended_holocron_offer
     VOS-3104 extended holocron converter
  *  VOS-3104 extended holocron data: updated cert data in converter
  *  release 0.42.2
  *  fix changelog
  *  VOS-3104 extended holocron data: updated stage test, fixed big queue sender
  *  Merge branch 'master' into VOS-3104_extended_holocron_offer
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/components/DefaultAutoruCoreComponents.scala
  *  VOS-3104 extended holocron data: fixed config for tests
  *  Merge pull request #168 from YandexClassifieds/VOS-3099_moderation_protection
     Vos 3099 moderation protection
  *  consumer dev config
  *  VOS-3104 extended holocron data: updated holocron stage and sender
  *  VOS-3104 extended holocron converter
  *  VOS-3099: remove auto adding of protected fields
  *  VOS-3099: review fixes
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/FormWriter.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3099: blocking code in separate thread
  *  VOS-3099: fix wrong source skip
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  VOS-3099: modifier test, fix found bugs
  *  
     and compilation fix
  *  
     i am ashamed of my previous commit
  *  
     random test form generator should generate valid steering wheel
  *  
     logs in tests
  *  Merge branch 'master' into AUTORUAPI-5961_steering_wheel
  *  
     tests and fixes
  *  Merge pull request #184 from YandexClassifieds/AUTORUOFFICE-5724-region-id-for-delivery-region-location
     AUTORUOFFICE-5724 rename region_id to federal_subject_id
  *  VOS-3099: fix typos
  *  rename region_id to federal_subject_id
  *  AUTORUAPI-4853: debug logs
  *  rename region id field
  *  added region id to delivery region location
  *  Merge remote-tracking branch 'origin/master'
  *  fix teleperformance metrics
  *  AUTORUAPI-6000 (#180)
     * cleanup
     
     * AUTORUAPI-6000 enable promocodes in 3 new regions
  *  
     validate steering wheel by tech param id
  *  VOS-3099: handle fields with message type
  *  AUTORUAPI-4853: support 1200x900 for autoru-orig
  *  AUTORUAPI-4853: debug logs
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/PhotoUtils.scala
  *  AUTORUAPI-4853: debug logs
  *  VOS-3099: some getters and modifiers implementation
  *  Merge pull request #178 from YandexClassifieds/AUTORUAPI-5982_fix_photo_id_format
     AUTORUAPI-5982: public photo_id format
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: delete version 1 filter
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-5929_redemption_enable
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/properties.conf
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/features/AutoruFeatures.scala
  *  AUTORUAPI-5929: fix password
  *  restore size 456x342
  *  AUTORUAPI-5961 fix npe
  *  VOS-3099: protected field REST API
  *  VOS-3099: move application-specific code from DAO to OfferWriter
  *  AUTORUAPI-5961 move under feature
  *  AUTORUAPI-5961 fix
  *  AUTORUAPI-5961 steering wheel validation
  *  VOS-3099: introduce feature, catch possible exceptions from field getters
  *  Fix shard2 port in local conf (#174)
  *  fix password
  *  VOS-3099: protection hooks in api handlers
  *  VOS-3099 use enum fields instead of strings
  *  AUTORUAPI-4853: fix read url for original photo
  *  temporarily pending integration test
  *  VOS-3136: fix url for original photo
  *  VOS-3136: fix tests
  *  send not blurred photo to moderation
  *  Vos 3141 Обрабатывать резолюцию "Недозвон" от колл-центра (#170)
     * VOS-3141 support NO_ANSWER
  *  AUTORUAPI-5929: fix tests
  *  AUTORUAPI-5929: redemption come back
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  extract youtube request from mutator function
  *  Merge pull request #166 from YandexClassifieds/AUTORUAPI-5970
     AUTORUAPI-5970 add options mapping to converter
  *  Merge remote-tracking branch 'origin/master'
  *  optimize imports
  *  VOS-3099: moderation protection and validation
  *  VOS-3099: change get/has method params to offerOrBuilder
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into AUTORUOFFICE-5600-add-filter-by-delivery-region
  *  refactored tests + fixed tags list modification
  *  update zk dev address
  *  AUTORUAPI-5970 fix error
  *  AUTORUAPI-5970 add options mapping to converter
  *  VOS-3099: field gettter/setter draft
  *  added new tag for offer which will be created if deliveryInfo is not empty and removed is one is empty
  *  Vos 3022 AVAILABILITY (#164)
     * VOS-3022 Availability
  *  update zk dev address
  *  Merge pull request #159 from YandexClassifieds/CARFAX-238
     CARFAX-238 change reload stage behaviour and  add test
  *  release 0.42.0
  *  Merge pull request #157 from YandexClassifieds/AUTORUAPI-4853_switch_private_users_to_new_namespaces
     AUTORUAPI-4853: added namespace to form photo name
  *  Merge pull request #162 from YandexClassifieds/AUTORUOFFICE-5682-save-region-info
     AUTORUOFFICE-5682 save region info
  *  release 0.41.7
  *  added regionInfo to offer response model.
  *  added regionInfo to delivery region location.
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: refactoring and fix tests
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_switch_private_users_to_new_namespaces
     # Conflicts:
     #	vos2-autoru-api/src/test/scala/ru/yandex/vos2/autoru/api/v1/draft/DraftHandlerPhotosTest.scala
  *  AUTORUAPI-4853: refactoring
  *  change behaviour and  add test
  *  VOS-3136: added original and process original
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: added namespace to form photo name
  *  VOS-3099: mv to another package
  *  VOS-3099: moderation protection hooks draft

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 26 Jun 2019 20:19:45 +0300

## yandex-vos2-autoru-consumers:0.42.2 (Thu, 20 Jun 2019 20:21:31 +0300)

  *  fix changelog
  *  Merge pull request #168 from YandexClassifieds/VOS-3099_moderation_protection
     Vos 3099 moderation protection
  *  consumer dev config
  *  VOS-3099: remove auto adding of protected fields
  *  VOS-3099: review fixes
  *  Update vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/proxy/FormWriter.scala
     Co-Authored-By: Vladislav Dolbilov <darl@yandex-team.ru>
  *  VOS-3099: blocking code in separate thread
  *  VOS-3099: fix wrong source skip
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  VOS-3099: modifier test, fix found bugs
  *  
     and compilation fix
  *  
     i am ashamed of my previous commit
  *  
     random test form generator should generate valid steering wheel
  *  
     logs in tests
  *  Merge branch 'master' into AUTORUAPI-5961_steering_wheel
  *  
     tests and fixes
  *  Merge pull request #184 from YandexClassifieds/AUTORUOFFICE-5724-region-id-for-delivery-region-location
     AUTORUOFFICE-5724 rename region_id to federal_subject_id
  *  VOS-3099: fix typos
  *  rename region_id to federal_subject_id
  *  AUTORUAPI-4853: debug logs
  *  rename region id field
  *  added region id to delivery region location
  *  Merge remote-tracking branch 'origin/master'
  *  fix teleperformance metrics
  *  AUTORUAPI-6000 (#180)
     * cleanup
     
     * AUTORUAPI-6000 enable promocodes in 3 new regions
  *  
     validate steering wheel by tech param id
  *  VOS-3099: handle fields with message type
  *  AUTORUAPI-4853: support 1200x900 for autoru-orig
  *  AUTORUAPI-4853: debug logs
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/utils/PhotoUtils.scala
  *  AUTORUAPI-4853: debug logs
  *  VOS-3099: some getters and modifiers implementation
  *  Merge pull request #178 from YandexClassifieds/AUTORUAPI-5982_fix_photo_id_format
     AUTORUAPI-5982: public photo_id format
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: refactoring
  *  AUTORUAPI-5929: delete version 1 filter
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-5929_redemption_enable
     # Conflicts:
     #	vos2-autoru-core/src/main/resources/properties.conf
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/features/AutoruFeatures.scala
  *  AUTORUAPI-5929: fix password
  *  restore size 456x342
  *  AUTORUAPI-5961 fix npe
  *  VOS-3099: protected field REST API
  *  VOS-3099: move application-specific code from DAO to OfferWriter
  *  AUTORUAPI-5961 move under feature
  *  AUTORUAPI-5961 fix
  *  AUTORUAPI-5961 steering wheel validation
  *  VOS-3099: introduce feature, catch possible exceptions from field getters
  *  Fix shard2 port in local conf (#174)
  *  fix password
  *  VOS-3099: protection hooks in api handlers
  *  VOS-3099 use enum fields instead of strings
  *  AUTORUAPI-4853: fix read url for original photo
  *  temporarily pending integration test
  *  VOS-3136: fix url for original photo
  *  VOS-3136: fix tests
  *  send not blurred photo to moderation
  *  Vos 3141 Обрабатывать резолюцию "Недозвон" от колл-центра (#170)
     * VOS-3141 support NO_ANSWER
  *  AUTORUAPI-5929: fix tests
  *  AUTORUAPI-5929: redemption come back
  *  Merge branch 'master' into VOS-3099_moderation_protection
  *  extract youtube request from mutator function
  *  Merge pull request #166 from YandexClassifieds/AUTORUAPI-5970
     AUTORUAPI-5970 add options mapping to converter
  *  Merge remote-tracking branch 'origin/master'
  *  optimize imports
  *  VOS-3099: moderation protection and validation
  *  VOS-3099: change get/has method params to offerOrBuilder
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into AUTORUOFFICE-5600-add-filter-by-delivery-region
  *  refactored tests + fixed tags list modification
  *  update zk dev address
  *  AUTORUAPI-5970 fix error
  *  AUTORUAPI-5970 add options mapping to converter
  *  VOS-3099: field gettter/setter draft
  *  added new tag for offer which will be created if deliveryInfo is not empty and removed is one is empty
  *  Vos 3022 AVAILABILITY (#164)
     * VOS-3022 Availability
  *  update zk dev address
  *  Merge pull request #159 from YandexClassifieds/CARFAX-238
     CARFAX-238 change reload stage behaviour and  add test
  *  release 0.42.0
  *  Merge pull request #157 from YandexClassifieds/AUTORUAPI-4853_switch_private_users_to_new_namespaces
     AUTORUAPI-4853: added namespace to form photo name
  *  Merge pull request #162 from YandexClassifieds/AUTORUOFFICE-5682-save-region-info
     AUTORUOFFICE-5682 save region info
  *  release 0.41.7
  *  added regionInfo to offer response model.
  *  added regionInfo to delivery region location.
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: refactoring and fix tests
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_switch_private_users_to_new_namespaces
     # Conflicts:
     #	vos2-autoru-api/src/test/scala/ru/yandex/vos2/autoru/api/v1/draft/DraftHandlerPhotosTest.scala
  *  AUTORUAPI-4853: refactoring
  *  change behaviour and  add test
  *  VOS-3136: added original and process original
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: added namespace to form photo name
  *  VOS-3099: mv to another package
  *  VOS-3099: moderation protection hooks draft

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 20 Jun 2019 20:21:31 +0300

## yandex-vos2-autoru-consumers:0.42.1 (Tue, 04 Jun 2019 17:06:22 +0300)
  *  build from branch

-- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 04 Jun 2019 17:06:22 +0300

## yandex-vos2-autoru-consumers:0.42.0 (Tue, 04 Jun 2019 17:06:22 +0300)

  *  Merge pull request #157 from YandexClassifieds/AUTORUAPI-4853_switch_private_users_to_new_namespaces
     AUTORUAPI-4853: added namespace to form photo name
  *  Merge pull request #162 from YandexClassifieds/AUTORUOFFICE-5682-save-region-info
     AUTORUOFFICE-5682 save region info
  *  release 0.41.7
  *  added regionInfo to offer response model.
  *  added regionInfo to delivery region location.
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: refactoring and fix tests
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_switch_private_users_to_new_namespaces
     # Conflicts:
     #	vos2-autoru-api/src/test/scala/ru/yandex/vos2/autoru/api/v1/draft/DraftHandlerPhotosTest.scala
  *  AUTORUAPI-4853: refactoring
  *  VOS-3136: added original and process original
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: added namespace to form photo name

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 04 Jun 2019 17:06:22 +0300

## yandex-vos2-autoru-consumers:0.41.7 (Mon, 03 Jun 2019 19:19:25 +0300)

  *  Autoruapi 5935 (#161)
     * AUTORUAPI-5935 Delivery Info
  *  YDB (#153)
  *  release 0.41.6
  *  VOS-3119 added deliveryInfo to indexing model
  *  AUTORUAPI-4853: revert
  *  VOS-3133 flag for create notification if edit moderator (#156)
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: save blurred photo to autoru-vos, new photo to autoru-orig
  *  AUTORUSUP-4591 allow photos for comtrans offers from callcenter
  *  minor
  *  Revert "Vos 3119 add delivery to indexing"
  *  CARFAX-204: change vin-decoder url
  *  release 0.41.5
  *  Merge pull request #140 from YandexClassifieds/VOS-3119-add-delivery-to-indexing
     Vos 3119 add delivery to indexing
  *  cleanup (#152)
  *  AUTORUAPI-4853: fix transform history for blurred photo without number
  *  Merge remote-tracking branch 'origin/master'
  *  AUTORUAPI-4853: don't include photo from autoru-orig namespace in api response
  *  VOS-3126 strcit holocron validation
  *  AUTORUAPI-4853: fix transform history & added test & shouldRevisitSoon
  *  Merge pull request #150 from YandexClassifieds/AUTORUAPI-4853_migrate_namespace_stage
     AUTORUAPI-4853
  *  AUTORUAPI-4853: migrate to autoru-vos namespace stage & meta stage refactoring
  *  release 0.41.4
  *  remove old vin exclusions
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into VOS-3119-add-delivery-to-indexing
  *  release 0.41.3
  *  save numbers in from offer converter
  *  release 0.41.2
  *  Merge pull request #143 from YandexClassifieds/AUTORUAPI-5656
     AUTORUAPI-5656
  *  Merge branch 'master' into AUTORUAPI-5656
  *  move all the VIN-related `year` into VinUtils
  *  added async-profiler
  *  release 0.41.1
  *  Merge pull request #126 from YandexClassifieds/VOS-3112-add-delivery-to-offer
     VOS-3112 added DeliveryInfo in AutoruOffer
  *  Merge pull request #135 from YandexClassifieds/VOS-3188
     VOS-3188
  *  Cleanup (#142)
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 add test eds data
  *  release 0.41.0
  *  Merge pull request #146 from YandexClassifieds/AUTORUAPI-5837_required_photo
     AUTORUAPI-5837 required photo
  *  AUTORUAPI-5837: fix typo
  *  AUTORUAPI-5837: added test
  *  save hide_license_plate in FormOfferConverter
  *  AUTORUAPI-5837: required photo for all private besides call center
  *  AUTORUAPI-5820: required vin + grz for all private besides call center
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 review fixes
  *  Merge branch 'master' into AUTORUAPI-5656
  *  condition test
  *  update year condition
  *  VOS-3119 added deliveryInfo to indexing model
  *  VOS-3112 made mapping more 'scala-like'
  *  VOS-3119 added enriching of auto model with delivery info
  *  VOS-3112 moved model mapping to different objects
  *  VOS-3112 added delivery info to card form read
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into VOS-3112-add-delivery-to-offer
  *  VOS-3085 fixes
  *  VOS-3118 add stage
  *  VOS-3118 remove searcher equipments
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3138 fixes
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3118 init commit
  *  VOS-3112 simplified delivery update with builder, removed empty line, replaced proto models mapping from byte array with .map
  *  VOS-3112 added DeliveryInfo for AutoruOffer
  *  VOS-3085 review fixes
  *  VOS-3085 car options from verba

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 03 Jun 2019 19:19:25 +0300

## yandex-vos2-autoru-consumers:0.41.6 (Fri, 31 May 2019 14:56:06 +0300)

  *  VOS-3119 added deliveryInfo to indexing model
  *  AUTORUAPI-4853: revert
  *  VOS-3133 flag for create notification if edit moderator (#156)
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: fix tests
  *  AUTORUAPI-4853: save blurred photo to autoru-vos, new photo to autoru-orig
  *  AUTORUSUP-4591 allow photos for comtrans offers from callcenter
  *  minor
  *  Revert "Vos 3119 add delivery to indexing"
  *  CARFAX-204: change vin-decoder url
  *  release 0.41.5
  *  Merge pull request #140 from YandexClassifieds/VOS-3119-add-delivery-to-indexing
     Vos 3119 add delivery to indexing
  *  cleanup (#152)
  *  AUTORUAPI-4853: fix transform history for blurred photo without number
  *  Merge remote-tracking branch 'origin/master'
  *  AUTORUAPI-4853: don't include photo from autoru-orig namespace in api response
  *  VOS-3126 strcit holocron validation
  *  AUTORUAPI-4853: fix transform history & added test & shouldRevisitSoon
  *  Merge pull request #150 from YandexClassifieds/AUTORUAPI-4853_migrate_namespace_stage
     AUTORUAPI-4853
  *  AUTORUAPI-4853: migrate to autoru-vos namespace stage & meta stage refactoring
  *  release 0.41.4
  *  remove old vin exclusions
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into VOS-3119-add-delivery-to-indexing
  *  release 0.41.3
  *  save numbers in from offer converter
  *  release 0.41.2
  *  Merge pull request #143 from YandexClassifieds/AUTORUAPI-5656
     AUTORUAPI-5656
  *  Merge branch 'master' into AUTORUAPI-5656
  *  move all the VIN-related `year` into VinUtils
  *  added async-profiler
  *  release 0.41.1
  *  Merge pull request #126 from YandexClassifieds/VOS-3112-add-delivery-to-offer
     VOS-3112 added DeliveryInfo in AutoruOffer
  *  Merge pull request #135 from YandexClassifieds/VOS-3188
     VOS-3188
  *  Cleanup (#142)
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 add test eds data
  *  release 0.41.0
  *  Merge pull request #146 from YandexClassifieds/AUTORUAPI-5837_required_photo
     AUTORUAPI-5837 required photo
  *  AUTORUAPI-5837: fix typo
  *  AUTORUAPI-5837: added test
  *  save hide_license_plate in FormOfferConverter
  *  AUTORUAPI-5837: required photo for all private besides call center
  *  AUTORUAPI-5820: required vin + grz for all private besides call center
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 review fixes
  *  Merge branch 'master' into AUTORUAPI-5656
  *  condition test
  *  update year condition
  *  VOS-3119 added deliveryInfo to indexing model
  *  VOS-3112 made mapping more 'scala-like'
  *  VOS-3119 added enriching of auto model with delivery info
  *  VOS-3112 moved model mapping to different objects
  *  VOS-3112 added delivery info to card form read
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into VOS-3112-add-delivery-to-offer
  *  VOS-3085 fixes
  *  VOS-3118 add stage
  *  VOS-3118 remove searcher equipments
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3138 fixes
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3118 init commit
  *  VOS-3112 simplified delivery update with builder, removed empty line, replaced proto models mapping from byte array with .map
  *  VOS-3112 added DeliveryInfo for AutoruOffer
  *  VOS-3085 review fixes
  *  VOS-3085 car options from verba

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 31 May 2019 14:56:06 +0300

## yandex-vos2-autoru-consumers:0.41.5 (Mon, 27 May 2019 09:32:21 +0300)

  *  Merge pull request #140 from YandexClassifieds/VOS-3119-add-delivery-to-indexing
     Vos 3119 add delivery to indexing
  *  cleanup (#152)
  *  AUTORUAPI-4853: fix transform history for blurred photo without number
  *  Merge remote-tracking branch 'origin/master'
  *  AUTORUAPI-4853: don't include photo from autoru-orig namespace in api response
  *  VOS-3126 strcit holocron validation
  *  AUTORUAPI-4853: fix transform history & added test & shouldRevisitSoon
  *  Merge pull request #150 from YandexClassifieds/AUTORUAPI-4853_migrate_namespace_stage
     AUTORUAPI-4853
  *  AUTORUAPI-4853: migrate to autoru-vos namespace stage & meta stage refactoring
  *  release 0.41.4
  *  remove old vin exclusions
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into VOS-3119-add-delivery-to-indexing
  *  release 0.41.3
  *  save numbers in from offer converter
  *  release 0.41.2
  *  Merge pull request #143 from YandexClassifieds/AUTORUAPI-5656
     AUTORUAPI-5656
  *  Merge branch 'master' into AUTORUAPI-5656
  *  move all the VIN-related `year` into VinUtils
  *  added async-profiler
  *  release 0.41.1
  *  Merge pull request #126 from YandexClassifieds/VOS-3112-add-delivery-to-offer
     VOS-3112 added DeliveryInfo in AutoruOffer
  *  Merge pull request #135 from YandexClassifieds/VOS-3188
     VOS-3188
  *  Cleanup (#142)
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 add test eds data
  *  release 0.41.0
  *  Merge pull request #146 from YandexClassifieds/AUTORUAPI-5837_required_photo
     AUTORUAPI-5837 required photo
  *  AUTORUAPI-5837: fix typo
  *  AUTORUAPI-5837: added test
  *  save hide_license_plate in FormOfferConverter
  *  AUTORUAPI-5837: required photo for all private besides call center
  *  AUTORUAPI-5820: required vin + grz for all private besides call center
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 review fixes
  *  Merge branch 'master' into AUTORUAPI-5656
  *  condition test
  *  update year condition
  *  VOS-3119 added deliveryInfo to indexing model
  *  VOS-3112 made mapping more 'scala-like'
  *  VOS-3119 added enriching of auto model with delivery info
  *  VOS-3112 moved model mapping to different objects
  *  VOS-3112 added delivery info to card form read
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into VOS-3112-add-delivery-to-offer
  *  VOS-3085 fixes
  *  VOS-3118 add stage
  *  VOS-3118 remove searcher equipments
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3138 fixes
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3118 init commit
  *  VOS-3112 simplified delivery update with builder, removed empty line, replaced proto models mapping from byte array with .map
  *  VOS-3112 added DeliveryInfo for AutoruOffer
  *  VOS-3085 review fixes
  *  VOS-3085 car options from verba

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 27 May 2019 09:32:21 +0300

## yandex-vos2-autoru-consumers:0.41.4 (Thu, 23 May 2019 16:02:40 +0300)

  *  remove old vin exclusions
  *  release 0.41.3
  *  save numbers in from offer converter
  *  release 0.41.2
  *  Merge pull request #143 from YandexClassifieds/AUTORUAPI-5656
     AUTORUAPI-5656
  *  Merge branch 'master' into AUTORUAPI-5656
  *  move all the VIN-related `year` into VinUtils
  *  added async-profiler
  *  release 0.41.1
  *  Merge pull request #126 from YandexClassifieds/VOS-3112-add-delivery-to-offer
     VOS-3112 added DeliveryInfo in AutoruOffer
  *  Merge pull request #135 from YandexClassifieds/VOS-3188
     VOS-3188
  *  Cleanup (#142)
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 add test eds data
  *  release 0.41.0
  *  Merge pull request #146 from YandexClassifieds/AUTORUAPI-5837_required_photo
     AUTORUAPI-5837 required photo
  *  AUTORUAPI-5837: fix typo
  *  AUTORUAPI-5837: added test
  *  save hide_license_plate in FormOfferConverter
  *  AUTORUAPI-5837: required photo for all private besides call center
  *  AUTORUAPI-5820: required vin + grz for all private besides call center
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 review fixes
  *  Merge branch 'master' into AUTORUAPI-5656
  *  condition test
  *  update year condition
  *  VOS-3112 made mapping more 'scala-like'
  *  VOS-3112 moved model mapping to different objects
  *  VOS-3112 added delivery info to card form read
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into VOS-3112-add-delivery-to-offer
  *  VOS-3085 fixes
  *  VOS-3118 add stage
  *  VOS-3118 remove searcher equipments
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3138 fixes
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3118 init commit
  *  VOS-3112 simplified delivery update with builder, removed empty line, replaced proto models mapping from byte array with .map
  *  VOS-3112 added DeliveryInfo for AutoruOffer
  *  VOS-3085 review fixes
  *  VOS-3085 car options from verba

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 23 May 2019 16:02:40 +0300

## yandex-vos2-autoru-consumers:0.41.3 (Thu, 23 May 2019 13:04:55 +0300)

  *  save numbers in from offer converter
  *  release 0.41.2
  *  Merge pull request #143 from YandexClassifieds/AUTORUAPI-5656
     AUTORUAPI-5656
  *  Merge branch 'master' into AUTORUAPI-5656
  *  move all the VIN-related `year` into VinUtils
  *  added async-profiler
  *  release 0.41.1
  *  Merge pull request #126 from YandexClassifieds/VOS-3112-add-delivery-to-offer
     VOS-3112 added DeliveryInfo in AutoruOffer
  *  Merge pull request #135 from YandexClassifieds/VOS-3188
     VOS-3188
  *  Cleanup (#142)
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 add test eds data
  *  release 0.41.0
  *  Merge pull request #146 from YandexClassifieds/AUTORUAPI-5837_required_photo
     AUTORUAPI-5837 required photo
  *  AUTORUAPI-5837: fix typo
  *  AUTORUAPI-5837: added test
  *  save hide_license_plate in FormOfferConverter
  *  AUTORUAPI-5837: required photo for all private besides call center
  *  AUTORUAPI-5820: required vin + grz for all private besides call center
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 review fixes
  *  Merge branch 'master' into AUTORUAPI-5656
  *  condition test
  *  update year condition
  *  VOS-3112 made mapping more 'scala-like'
  *  VOS-3112 moved model mapping to different objects
  *  VOS-3112 added delivery info to card form read
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into VOS-3112-add-delivery-to-offer
  *  VOS-3085 fixes
  *  VOS-3118 add stage
  *  VOS-3118 remove searcher equipments
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3138 fixes
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3118 init commit
  *  VOS-3112 simplified delivery update with builder, removed empty line, replaced proto models mapping from byte array with .map
  *  VOS-3112 added DeliveryInfo for AutoruOffer
  *  VOS-3085 review fixes
  *  VOS-3085 car options from verba

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 23 May 2019 13:04:55 +0300

## yandex-vos2-autoru-consumers:0.41.2 (Wed, 22 May 2019 14:18:43 +0300)

  *  Merge pull request #143 from YandexClassifieds/AUTORUAPI-5656
     AUTORUAPI-5656
  *  Merge branch 'master' into AUTORUAPI-5656
  *  move all the VIN-related `year` into VinUtils
  *  added async-profiler
  *  release 0.41.1
  *  Merge pull request #126 from YandexClassifieds/VOS-3112-add-delivery-to-offer
     VOS-3112 added DeliveryInfo in AutoruOffer
  *  Merge pull request #135 from YandexClassifieds/VOS-3188
     VOS-3188
  *  Cleanup (#142)
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 add test eds data
  *  release 0.41.0
  *  Merge pull request #146 from YandexClassifieds/AUTORUAPI-5837_required_photo
     AUTORUAPI-5837 required photo
  *  AUTORUAPI-5837: fix typo
  *  AUTORUAPI-5837: added test
  *  save hide_license_plate in FormOfferConverter
  *  AUTORUAPI-5837: required photo for all private besides call center
  *  AUTORUAPI-5820: required vin + grz for all private besides call center
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 review fixes
  *  Merge branch 'master' into AUTORUAPI-5656
  *  condition test
  *  update year condition
  *  VOS-3112 made mapping more 'scala-like'
  *  VOS-3112 moved model mapping to different objects
  *  VOS-3112 added delivery info to card form read
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into VOS-3112-add-delivery-to-offer
  *  VOS-3085 fixes
  *  VOS-3118 add stage
  *  VOS-3118 remove searcher equipments
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3138 fixes
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3118 init commit
  *  VOS-3112 simplified delivery update with builder, removed empty line, replaced proto models mapping from byte array with .map
  *  VOS-3112 added DeliveryInfo for AutoruOffer
  *  VOS-3085 review fixes
  *  VOS-3085 car options from verba

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 22 May 2019 14:18:43 +0300

## yandex-vos2-autoru-consumers:0.41.1 (Tue, 21 May 2019 16:54:20 +0300)

  *  Merge pull request #126 from YandexClassifieds/VOS-3112-add-delivery-to-offer
     VOS-3112 added DeliveryInfo in AutoruOffer
  *  Merge pull request #135 from YandexClassifieds/VOS-3188
     VOS-3188
  *  Cleanup (#142)
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 add test eds data
  *  release 0.41.0
  *  Merge pull request #146 from YandexClassifieds/AUTORUAPI-5837_required_photo
     AUTORUAPI-5837 required photo
  *  AUTORUAPI-5837: fix typo
  *  AUTORUAPI-5837: added test
  *  save hide_license_plate in FormOfferConverter
  *  AUTORUAPI-5837: required photo for all private besides call center
  *  AUTORUAPI-5820: required vin + grz for all private besides call center
  *  Merge remote-tracking branch 'origin/master' into VOS-3188
  *  VOS-3118 review fixes
  *  VOS-3112 made mapping more 'scala-like'
  *  VOS-3112 moved model mapping to different objects
  *  VOS-3112 added delivery info to card form read
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2-autoru into VOS-3112-add-delivery-to-offer
  *  VOS-3085 fixes
  *  VOS-3118 add stage
  *  VOS-3118 remove searcher equipments
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3138 fixes
  *  Merge remote-tracking branch 'origin/master' into VOS-3085
  *  VOS-3118 init commit
  *  VOS-3112 simplified delivery update with builder, removed empty line, replaced proto models mapping from byte array with .map
  *  VOS-3112 added DeliveryInfo for AutoruOffer
  *  VOS-3085 review fixes
  *  VOS-3085 car options from verba

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 21 May 2019 16:54:20 +0300

## yandex-vos2-autoru-consumers:0.41.0 (Mon, 20 May 2019 16:08:16 +0300)

  *  Merge pull request #146 from YandexClassifieds/AUTORUAPI-5837_required_photo
     AUTORUAPI-5837 required photo
  *  AUTORUAPI-5837: fix typo
  *  AUTORUAPI-5837: added test
  *  save hide_license_plate in FormOfferConverter
  *  AUTORUAPI-5837: required photo for all private besides call center
  *  AUTORUAPI-5820: required vin + grz for all private besides call center

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 20 May 2019 16:08:16 +0300

## yandex-vos2-autoru-consumers:0.40.0 (Fri, 17 May 2019 20:33:11 +0300)

  *  enable debug logs for kafka

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 17 May 2019 20:33:11 +0300

## yandex-vos2-autoru-consumers:0.39.0 (Fri, 17 May 2019 19:32:48 +0300)

  *  do not update user if not changed
  *  parallel consuming
  *  bettr logs
  *  bettr logs
  *  VOS-3070
  *  delete debug logs
  *  Merge remote-tracking branch 'origin/master'
  *  debug logs

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 17 May 2019 19:32:48 +0300

## yandex-vos2-autoru-consumers:0.38.1 (Thu, 16 May 2019 14:07:41 +0300)

  *  AUTORUSUP-4564 catch errors in AutoruOffersRequestHandler
  *  Merge pull request #138 from YandexClassifieds/namespace_in_parsing_response
     AUTORUAPI-4853: mds namespace in parsing response
  *  release 0.38.0
  *  more logs in consumers
  *  JsonPatch_FIX (#139)
  *  Merge pull request #137 from YandexClassifieds/AUTORUAPI-5871
     AUTORUAPI-5871
  *  AUTORUAPI-4853: refactoring
  *  AUTORUAPI-4853: refactoring
  *  AUTORUAPI-4853: mds namespace in parsing response
  *  Merge branch 'master' into AUTORUAPI-5871
  *  spincar id extraction got fixed

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 16 May 2019 14:07:41 +0300

## yandex-vos2-autoru-consumers:0.38.0 (Wed, 15 May 2019 18:39:15 +0300)

  *  more logs in consumers
  *  JsonPatch_FIX (#139)
  *  Merge pull request #137 from YandexClassifieds/AUTORUAPI-5871
     AUTORUAPI-5871
  *  Merge branch 'master' into AUTORUAPI-5871
  *  spincar id extraction got fixed

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 15 May 2019 18:39:15 +0300

## yandex-vos2-autoru-consumers:0.37.1 (Wed, 15 May 2019 16:47:35 +0300)

  *  AUTORUAPI-4853: fix start script
  *  Merge pull request #134 from YandexClassifieds/AUTORUAPI-4853_photo_migration
     AUTORUAPI-4853: photo-migration module
  *  AUTORUAPI-4853: more tests
  *  AUTORUAPI-4853: photo-migration module. init commit
  *  AUTO-11009 updated metrics observe
  *  AUTO-11009 pr fix
  *  Merge branch 'master' into AUTO-11009_photo_meta_send
     # Conflicts:
     #	pom.xml
     #	vos2-core/src/main/scala/ru/yandex/vos2/services/mds/MdsPhotoUtils.scala
  *  Merge branch 'master' into AUTO-11009_photo_meta_send
     # Conflicts:
     #	pom.xml
     #	vos2-core/src/main/scala/ru/yandex/vos2/services/mds/MdsPhotoUtils.scala
  *  AUTO-11009 pr fixes
  *  release 0.37.0
  *  AUTO-11009 updated meta model: added category, fixed mark and model set
  *  AUTORUAPI-4853: refactoring
  *  AUTO-11009 pr fixes
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_photo_refactoring
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/export/writer/AdwordsCsvExportWriter.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/export/writer/AutoruXmlExportWriter.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/export/writer/CarPriceXmlExportWriter.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/export/writer/CriteoTrucksCsvExportWriter.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/export/writer/FacebookExportWriter.scala
  *  AUTORUAPI-4853: added tests
  *  VOS-3122 allow activation of old offers (#131)
  *  AUTORUAPI-4853: fix change namespace in PhotoUtils
  *  AUTO-11009 added SendMetaWorkerTest, refactoring
  *  AUTORUAPI-4853: move photo from autoru-orig to autoru-vos in PicaResultStage
  *  AUTO-11009 kafka configs
  *  AUTO-11009 refactoring
  *  AUTO-11009 send photo meta from vos to kafka, updated creation code, fixed compilation
  *  AUTO-11009 send photo meta from vos to kafka, logs and metrics
  *  AUTO-11009 send photo meta from vos to kafka
  *  AUTORUAPI-4853: pica pica refactoring and tests
  *  AUTORUAPI-4853: fix form offer images convert
  *  AUTORUAPI-4853: migrate to new namespace method
  *  AUTORUAPI-4853: save orig namespace for new photo
  *  AUTORUAPI-4853: save namespace and orig namespace
  *  AUTORUAPI-4853: fix compilation
  *  refactoring
  *  refactoring MdsPhotoUtils
  *  delete redundant & refactoring
  *  delete redundant
  *  delete redundant
  *  fix tests
  *  namespace in converters
  *  fix tests
  *  added namespace to photo proto
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_photo_refactoring
  *  added namespace to proto

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 15 May 2019 16:47:35 +0300

## yandex-vos2-autoru-consumers:0.37.0 (Wed, 08 May 2019 19:00:40 +0300)

  *  AUTORUAPI-4853: refactoring
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_photo_refactoring
     # Conflicts:
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/export/writer/AdwordsCsvExportWriter.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/export/writer/AutoruXmlExportWriter.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/export/writer/CarPriceXmlExportWriter.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/export/writer/CriteoTrucksCsvExportWriter.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/export/writer/FacebookExportWriter.scala
  *  AUTORUAPI-4853: added tests
  *  VOS-3122 allow activation of old offers (#131)
  *  AUTORUAPI-4853: fix change namespace in PhotoUtils
  *  AUTORUAPI-4853: move photo from autoru-orig to autoru-vos in PicaResultStage
  *  AUTORUAPI-4853: pica pica refactoring and tests
  *  AUTORUAPI-4853: fix form offer images convert
  *  AUTORUAPI-4853: migrate to new namespace method
  *  AUTORUAPI-4853: save orig namespace for new photo
  *  AUTORUAPI-4853: save namespace and orig namespace
  *  AUTORUAPI-4853: fix compilation
  *  refactoring
  *  refactoring MdsPhotoUtils
  *  delete redundant & refactoring
  *  delete redundant
  *  delete redundant
  *  fix tests
  *  namespace in converters
  *  fix tests
  *  added namespace to photo proto
  *  Merge remote-tracking branch 'origin/master' into AUTORUAPI-4853_photo_refactoring
  *  added namespace to proto

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 08 May 2019 19:00:40 +0300

## yandex-vos2-autoru-consumers:0.36.1 (Wed, 08 May 2019 12:07:37 +0300)

  *  VOS-3050 json-patch for offers (#128)
     * VOS-3050 json-patch for offers
  *  fixed promocode
  *  AUTORUAPI-5787 create and apply promocode (#127)
  *  Merge pull request #22 from YandexClassifieds/VOS-2990_discount_tag_stage
     VOS-2990 discount tag stage
  *  release 0.36.0
  *  delete redundant
  *  Merge pull request #122 from YandexClassifieds/AUTORUSUP-4423_illegal_offer_removing
     AUTORUSUP-4423: fix illegal offer removing in case of short db problem
  *  VOS-3117 autoprolongation for callcenter
  *   AUTORUSUP-4423: logging abouit seek
  *  AUTORUSUP-4423: fix illegal offer removing in case of short db problem
  *  Merge remote-tracking branch 'origin/master' into VOS-2990_discount_tag_stage
  *  VOS-3117 infinity prolongation in all regions
  *  simplify
  *  release 0.35.0
  *  Merge remote-tracking branch 'origin/master'
  *  delete vos2-autoru-cv
  *  Merge remote-tracking branch 'origin/master' into VOS-2990_discount_tag_stage
  *  Merge branch 'master' into VOS-2990_discount_tag_stage
  *  VOS-2990 discount tag stage feature
  *  Merge branch 'master' into VOS-2990_discount_tag_stage
  *  Merge branch 'master' into VOS-2990_discount_tag_stage

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 08 May 2019 12:07:37 +0300

## yandex-vos2-autoru-consumers:0.36.0 (Fri, 26 Apr 2019 18:20:54 +0300)

  *  delete redundant
  *  Merge pull request #122 from YandexClassifieds/AUTORUSUP-4423_illegal_offer_removing
     AUTORUSUP-4423: fix illegal offer removing in case of short db problem
  *  VOS-3117 autoprolongation for callcenter
  *   AUTORUSUP-4423: logging abouit seek
  *  AUTORUSUP-4423: fix illegal offer removing in case of short db problem
  *  VOS-3117 infinity prolongation in all regions
  *  simplify
  *  release 0.35.0
  *  Merge remote-tracking branch 'origin/master'
  *  delete vos2-autoru-cv

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 26 Apr 2019 18:20:54 +0300

## yandex-vos2-autoru-consumers:0.35.0 (Thu, 25 Apr 2019 16:06:33 +0300)

  *  Merge pull request #121 from YandexClassifieds/VOS-3111_save_parsed_photos_as_deleted
     VOS-3111 save parsed photos as deleted
  *  refactoring
  *  Vos 3113 remove flag (#120)
     * VOS-3113 mileage history
  *  VOS-3114 set displacement for holocron, fixed tests
  *  VOS-3114 set displacement for holocron, fixed tests
  *  VOS-3111 save parsed photos as deleted: added tests, fixes
  *  VOS-3111 save parsed photos as deleted, keep last 30 deleted photos
  *  VOS-3113 mileage history (#119)
     * VOS-3113 mileage history
  *  VOS-3114 set displacement for holocron

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 25 Apr 2019 16:06:33 +0300

## yandex-vos2-autoru-consumers:0.34.1 (Mon, 22 Apr 2019 19:16:10 +0300)

  *  Merge remote-tracking branch 'origin/index_refactoring'
  *  temp method
  *  remove timestamp any update
  *  increase partitions & more logs
  *  group by partition
  *  fix create batch
  *  Merge pull request #118 from YandexClassifieds/index_refactoring
     index refactoring
  *  index refactoring
  *  release 0.34.0
  *  VOS-3108 new equipments
  *  fix sender parameter
  *  VOS-3106 fix tests
  *  VOS-3106 add tests
  *  VOS-3106 add original price
  *  drop obsolete tests
  *  remove barrier for avito photos
  *  fix json obj
  *  fix sender arguments
  *  Merge pull request #110 from YandexClassifieds/AUTORUAPI-5779_bot_tag
     AUTORUAPI-5779 AvailableForCheckup tag
  *  AvailableForCheckup tag
  *  Clean proto model (#107)
     * remove realty model
     
     * remove realty model
     
     * cleanup
     
     * cleanup
  *  AUTORUAPI-5785 remove test
  *  AUTORUAPI-5785 sms with link on all regions (for offers from callcenter)
  *  added UploadParsedPhotosTrucks feature to disable truck photos upload and UploadParsedPhotos to disable the whole stage
  *  VOS-3043 fix sender template name
  *  ignore ImageNotFound exception in metric
  *  do not threat callback exception as failure in MdsUploader

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 22 Apr 2019 19:16:10 +0300

## yandex-vos2-autoru-consumers:0.34.0 (Tue, 16 Apr 2019 18:40:49 +0300)

  *  VOS-3108 new equipments
  *  fix sender parameter
  *  VOS-3106 fix tests
  *  VOS-3106 add tests
  *  VOS-3106 add original price
  *  drop obsolete tests
  *  remove barrier for avito photos
  *  fix json obj
  *  fix sender arguments
  *  Merge pull request #110 from YandexClassifieds/AUTORUAPI-5779_bot_tag
     AUTORUAPI-5779 AvailableForCheckup tag
  *  AvailableForCheckup tag
  *  Clean proto model (#107)
     * remove realty model
     
     * remove realty model
     
     * cleanup
     
     * cleanup
  *  AUTORUAPI-5785 remove test
  *  AUTORUAPI-5785 sms with link on all regions (for offers from callcenter)
  *  added UploadParsedPhotosTrucks feature to disable truck photos upload and UploadParsedPhotos to disable the whole stage
  *  VOS-3043 fix sender template name
  *  ignore ImageNotFound exception in metric
  *  do not threat callback exception as failure in MdsUploader

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 16 Apr 2019 18:40:49 +0300

## yandex-vos2-autoru-consumers:0.33.2 (Thu, 04 Apr 2019 11:34:09 +0300)

  *  Merge remote-tracking branch 'origin/master'
  *  short notification interval for testing
  *  release 0.33.1
  *  fix build duplicate offer info
  *  release 0.33.0
  *  Merge pull request #106 from YandexClassifieds/AUTORUAPI-5576_ban_duplicate
     AUTORUAPI-5576 get duplicate offer info from offer
  *  fix test
  *  get duplicate offer info from offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 04 Apr 2019 11:34:09 +0300

## yandex-vos2-autoru-consumers:0.33.1 (Thu, 04 Apr 2019 11:00:35 +0300)

  *  fix build duplicate offer info
  *  release 0.33.0
  *  Merge pull request #106 from YandexClassifieds/AUTORUAPI-5576_ban_duplicate
     AUTORUAPI-5576 get duplicate offer info from offer
  *  fix test
  *  get duplicate offer info from offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 04 Apr 2019 11:00:35 +0300

## yandex-vos2-autoru-consumers:0.33.0 (Wed, 03 Apr 2019 21:18:20 +0300)

  *  Merge pull request #106 from YandexClassifieds/AUTORUAPI-5576_ban_duplicate
     AUTORUAPI-5576 get duplicate offer info from offer
  *  fix test
  *  get duplicate offer info from offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 03 Apr 2019 21:18:20 +0300

## yandex-vos2-autoru-consumers:0.32.0 (Wed, 03 Apr 2019 15:56:01 +0300)

  *  VOS-3101 remove deleted images (#104)
  *  get mark/model from banned offer instead of original offer for duplicate ban renderer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 03 Apr 2019 15:56:01 +0300

## yandex-vos2-autoru-consumers:0.31.2 (Tue, 02 Apr 2019 18:17:28 +0300)

  *  refactoring
  *  fix users notification dao
  *  Merge remote-tracking branch 'origin/master'
  *  debug logs
  *  release 0.31.1
  *  universal X-Autoru-Operator-Uid for cabinet client
  *  Merge pull request #103 from YandexClassifieds/VOS-3043_fix_migration_user_origin
     VOS-3043 save user origin
  *  fix save user origin
  *  fix testcontainers versions
  *  force ipv6 in http client
  *  fix notification dao
  *  logs
  *  release 0.31.0
  *  feature
  *  Merge remote-tracking branch 'origin/master' into VOS-3043_user_batch_notifications
  *  VOS-3079 disable prolongation on expire (#101)
     * VOS-3079 disable prolongation on expire
     
     * VOS-3079 update test
  *  Cleanup (#100)
     * remove cetelem & other obsolete stuff
     
     * remove passport stage
     
     * report failed tests after run
     
     * fix tests
  *  fix type for custom coordinates (its compatible change)
     https://developers.google.com/protocol-buffers/docs/proto#updating
  *  remove custom coordinates on blur removal
  *  allow photo removal
  *  refactoring
  *  try catch to worker process
  *  get origin from db
  *  fix test
  *  Merge remote-tracking branch 'origin/master' into VOS-3043_user_batch_notifications
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/letters/renderers/VinResolutionRenderer.scala
  *  refactoring
  *  added token distribution
  *  refactoring
  *  notify manager refactoring
  *  init commit

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 02 Apr 2019 18:17:28 +0300

## yandex-vos2-autoru-consumers:0.31.1 (Tue, 02 Apr 2019 13:19:08 +0300)

  *  Merge pull request #103 from YandexClassifieds/VOS-3043_fix_migration_user_origin
     VOS-3043 save user origin
  *  fix save user origin
  *  fix testcontainers versions
  *  force ipv6 in http client
  *  fix notification dao
  *  logs
  *  release 0.31.0
  *  feature
  *  Merge remote-tracking branch 'origin/master' into VOS-3043_user_batch_notifications
  *  VOS-3079 disable prolongation on expire (#101)
     * VOS-3079 disable prolongation on expire
     
     * VOS-3079 update test
  *  Cleanup (#100)
     * remove cetelem & other obsolete stuff
     
     * remove passport stage
     
     * report failed tests after run
     
     * fix tests
  *  fix type for custom coordinates (its compatible change)
     https://developers.google.com/protocol-buffers/docs/proto#updating
  *  remove custom coordinates on blur removal
  *  allow photo removal
  *  refactoring
  *  try catch to worker process
  *  get origin from db
  *  fix test
  *  Merge remote-tracking branch 'origin/master' into VOS-3043_user_batch_notifications
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/letters/renderers/VinResolutionRenderer.scala
  *  refactoring
  *  added token distribution
  *  refactoring
  *  notify manager refactoring
  *  init commit

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 02 Apr 2019 13:19:08 +0300

## yandex-vos2-autoru-consumers:0.31.0 (Fri, 29 Mar 2019 19:16:40 +0300)

  *  feature
  *  Merge remote-tracking branch 'origin/master' into VOS-3043_user_batch_notifications
  *  VOS-3079 disable prolongation on expire (#101)
     * VOS-3079 disable prolongation on expire
     
     * VOS-3079 update test
  *  Cleanup (#100)
     * remove cetelem & other obsolete stuff
     
     * remove passport stage
     
     * report failed tests after run
     
     * fix tests
  *  fix type for custom coordinates (its compatible change)
     https://developers.google.com/protocol-buffers/docs/proto#updating
  *  remove custom coordinates on blur removal
  *  allow photo removal
  *  refactoring
  *  try catch to worker process
  *  get origin from db
  *  fix test
  *  Merge remote-tracking branch 'origin/master' into VOS-3043_user_batch_notifications
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/letters/renderers/VinResolutionRenderer.scala
  *  refactoring
  *  added token distribution
  *  refactoring
  *  notify manager refactoring
  *  init commit

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 29 Mar 2019 19:16:40 +0300

## yandex-vos2-autoru-consumers:0.30.0 (Thu, 28 Mar 2019 00:21:34 +0300)

  *  do not update offer if opinions not changed offer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Thu, 28 Mar 2019 00:21:34 +0300

## yandex-vos2-autoru-consumers:0.29.0 (Wed, 27 Mar 2019 23:34:07 +0300)

  *  small batches in ModerationOpinionConsumer

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 27 Mar 2019 23:34:07 +0300

## yandex-vos2-autoru-consumers:0.28.0 (Wed, 27 Mar 2019 20:58:53 +0300)

  *  include_remove = true for recall methods in all dao
  *  include remove in recall method
  *  remove monitoring for LicensePlateBlur client
  *  AUTORUAPI-5577 hide_license_plate for dealers (#97)
     * AUTORUAPI-5577 hide_license_plate parameter
     
     * AUTORUAPI-5577 blur photos for dealers
     
     * AUTORUAPI-5577 more tests
     
     * fix test data
     
     * rename variable

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 27 Mar 2019 20:58:53 +0300

## yandex-vos2-autoru-consumers:0.27.1 (Mon, 25 Mar 2019 20:19:07 +0300)

  *  Merge remote-tracking branch 'origin/master'
  *  save user hash in form offer converter
  *  release 0.27.0
  *  debug logs
  *  VOS-3089: holocron new model
  *  fix dictionary
  *  fix migration detaield ban reasons
  *  Revert "VOS-3088: разрешил редактировать объявления модератором вне зависимости от причины бана"
     This reverts commit 6a8c2a3bdd39331a6421b0899a816c43c96b952b.
  *  VOS-3088: разрешил редактировать объявления модератором вне зависимости от причины бана
  *  Revert "VOS-3088: разрешил редактировать объявления модератором вне зависимости от причины бана"
     This reverts commit bde675b8c9d128b8f015d55dcd1a1180ec0b2a3c.
  *  VOS-3088: разрешил редактировать объявления модератором вне зависимости от причины бана
  *  CARFAX-186: add mark/model/hasHistory to template params
  *  release 0.26.0

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 25 Mar 2019 20:19:07 +0300

## yandex-vos2-autoru-consumers:0.27.0 (Mon, 25 Mar 2019 19:26:54 +0300)

  *  debug logs
  *  VOS-3089: holocron new model
  *  fix dictionary
  *  fix migration detaield ban reasons
  *  Revert "VOS-3088: разрешил редактировать объявления модератором вне зависимости от причины бана"
     This reverts commit 6a8c2a3bdd39331a6421b0899a816c43c96b952b.
  *  VOS-3088: разрешил редактировать объявления модератором вне зависимости от причины бана
  *  Revert "VOS-3088: разрешил редактировать объявления модератором вне зависимости от причины бана"
     This reverts commit bde675b8c9d128b8f015d55dcd1a1180ec0b2a3c.
  *  VOS-3088: разрешил редактировать объявления модератором вне зависимости от причины бана
  *  CARFAX-186: add mark/model/hasHistory to template params
  *  release 0.26.0

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 25 Mar 2019 19:26:54 +0300

## yandex-vos2-autoru-consumers:0.26.0 (Mon, 18 Mar 2019 14:58:57 +0300)

  *  VOS-3075 new engine type (#89)
  *  save user index hash after migration
  *  delete sleep test
  *  Merge remote-tracking branch 'origin/master' into VOS-3073_scalatest
  *  2 seconds
  *  test data
  *  Merge remote-tracking branch 'origin/master' into VOS-3073_scalatest
  *  fix tests
  *  before all for all tests with init databases
  *  before all
  *  fork never
  *  tests
  *  moderation ban renderer test
  *  fix tests
  *  delete spincar client
  *  scalatest

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Mon, 18 Mar 2019 14:58:57 +0300

## yandex-vos2-autoru-consumers:0.25.5 (Fri, 15 Mar 2019 16:59:35 +0300)

  *  debug logs
  *  Merge pull request #88 from YandexClassifieds/CARFAX-184_revert
     CARFAX-184 hide under feature
  *  unsophisticate
  *  remove unused
  *  hide under feature
  *  VOS-3082 do not send to holocron deleted photos
  *  Merge pull request #87 from YandexClassifieds/CARFAX-184_revert
     CARFAX-184 revert
  *  release 0.25.4
  *  sender template fix
  *  VOS-3065 remove body type for old db (#85)
     * VOS-3065 remove body type for old db
  *  test
  *  revert send all
  *  VERTISMETA-168 disable parsing photos upload for more regions, send different sms there
  *  fix photo coordinates rotation; add tests
  *  release 0.25.3
  *  fix test
  *  Merge remote-tracking branch 'origin/master'
  *  added timestamp any update to index
  *  release 0.25.2
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-autoru-consumers/src/test/scala/ru/yandex/vos2/autoru/moderation/OpinionWriterTest.scala
  *  feature for duplicate ban notification
  *  release 0.25.1
  *  VOS-3064 blur photo by custom coordinates with cv (#82)
  *  logs
  *  release 0.25.0
  *  Merge pull request #80 from YandexClassifieds/AUTORUAPI-5576_ban_duplicate
     AUTORUAPI-5576 change ban notification logic
  *  original offer id
  *  Merge pull request #83 from YandexClassifieds/VOS-2929_offers_list_sort
     VOS-2929 sort fix
  *  tests
  *  VOS-3072 reduced keep-alive connection ttl
  *  sort fix
  *  refactoring
  *  remove dead code (#48)
     remove sales_certification db
  *  VOS-3066 better licenseplate monitorings; removed obsolete code (#81)
     * VOS-3066 better licenseplate monitorings; removed obsolete code
     
     * fix style
     
     * fix compilation
  *  change ban notification logic
  *  Merge pull request #68 from YandexClassifieds/CARFAX-162_send_all
     CARFAX-162 alternative way
  *  added args size
  *  debug logs
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  update big queue batch size
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  shining new 1mb batch
  *  fix compilation
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  play with kafka batch
  *  temp fix test
  *  alternative way

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 15 Mar 2019 16:59:35 +0300

## yandex-vos2-autoru-consumers:0.25.4 (Fri, 15 Mar 2019 13:45:53 +0300)

  *  sender template fix
  *  VOS-3065 remove body type for old db (#85)
     * VOS-3065 remove body type for old db
  *  VERTISMETA-168 disable parsing photos upload for more regions, send different sms there
  *  fix photo coordinates rotation; add tests
  *  release 0.25.3
  *  fix test
  *  Merge remote-tracking branch 'origin/master'
  *  added timestamp any update to index
  *  release 0.25.2
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-autoru-consumers/src/test/scala/ru/yandex/vos2/autoru/moderation/OpinionWriterTest.scala
  *  feature for duplicate ban notification
  *  release 0.25.1
  *  VOS-3064 blur photo by custom coordinates with cv (#82)
  *  logs
  *  release 0.25.0
  *  Merge pull request #80 from YandexClassifieds/AUTORUAPI-5576_ban_duplicate
     AUTORUAPI-5576 change ban notification logic
  *  original offer id
  *  Merge pull request #83 from YandexClassifieds/VOS-2929_offers_list_sort
     VOS-2929 sort fix
  *  tests
  *  VOS-3072 reduced keep-alive connection ttl
  *  sort fix
  *  refactoring
  *  remove dead code (#48)
     remove sales_certification db
  *  VOS-3066 better licenseplate monitorings; removed obsolete code (#81)
     * VOS-3066 better licenseplate monitorings; removed obsolete code
     
     * fix style
     
     * fix compilation
  *  change ban notification logic
  *  Merge pull request #68 from YandexClassifieds/CARFAX-162_send_all
     CARFAX-162 alternative way
  *  added args size
  *  debug logs
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  update big queue batch size
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  shining new 1mb batch
  *  fix compilation
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  play with kafka batch
  *  temp fix test
  *  alternative way

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Fri, 15 Mar 2019 13:45:53 +0300

## yandex-vos2-autoru-consumers:0.25.3 (Wed, 13 Mar 2019 14:10:03 +0300)

  *  Merge remote-tracking branch 'origin/master'
  *  added timestamp any update to index
  *  release 0.25.2
  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-autoru-consumers/src/test/scala/ru/yandex/vos2/autoru/moderation/OpinionWriterTest.scala
  *  feature for duplicate ban notification
  *  release 0.25.1
  *  VOS-3064 blur photo by custom coordinates with cv (#82)
  *  logs
  *  release 0.25.0
  *  Merge pull request #80 from YandexClassifieds/AUTORUAPI-5576_ban_duplicate
     AUTORUAPI-5576 change ban notification logic
  *  original offer id
  *  Merge pull request #83 from YandexClassifieds/VOS-2929_offers_list_sort
     VOS-2929 sort fix
  *  tests
  *  VOS-3072 reduced keep-alive connection ttl
  *  sort fix
  *  refactoring
  *  remove dead code (#48)
     remove sales_certification db
  *  VOS-3066 better licenseplate monitorings; removed obsolete code (#81)
     * VOS-3066 better licenseplate monitorings; removed obsolete code
     
     * fix style
     
     * fix compilation
  *  change ban notification logic
  *  Merge pull request #68 from YandexClassifieds/CARFAX-162_send_all
     CARFAX-162 alternative way
  *  added args size
  *  debug logs
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  update big queue batch size
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  shining new 1mb batch
  *  fix compilation
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  play with kafka batch
  *  temp fix test
  *  alternative way

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 13 Mar 2019 14:10:03 +0300

## yandex-vos2-autoru-consumers:0.25.2 (Wed, 13 Mar 2019 08:15:45 +0300)

  *  Merge remote-tracking branch 'origin/master'
     # Conflicts:
     #	vos2-autoru-consumers/src/test/scala/ru/yandex/vos2/autoru/moderation/OpinionWriterTest.scala
  *  feature for duplicate ban notification
  *  release 0.25.1
  *  VOS-3064 blur photo by custom coordinates with cv (#82)
  *  logs
  *  release 0.25.0
  *  Merge pull request #80 from YandexClassifieds/AUTORUAPI-5576_ban_duplicate
     AUTORUAPI-5576 change ban notification logic
  *  original offer id
  *  Merge pull request #83 from YandexClassifieds/VOS-2929_offers_list_sort
     VOS-2929 sort fix
  *  tests
  *  VOS-3072 reduced keep-alive connection ttl
  *  sort fix
  *  refactoring
  *  remove dead code (#48)
     remove sales_certification db
  *  VOS-3066 better licenseplate monitorings; removed obsolete code (#81)
     * VOS-3066 better licenseplate monitorings; removed obsolete code
     
     * fix style
     
     * fix compilation
  *  change ban notification logic
  *  Merge pull request #68 from YandexClassifieds/CARFAX-162_send_all
     CARFAX-162 alternative way
  *  added args size
  *  debug logs
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  update big queue batch size
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  shining new 1mb batch
  *  fix compilation
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  play with kafka batch
  *  temp fix test
  *  alternative way

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 13 Mar 2019 08:15:45 +0300

## yandex-vos2-autoru-consumers:0.25.1 (Wed, 13 Mar 2019 07:48:32 +0300)

  *  VOS-3064 blur photo by custom coordinates with cv (#82)
  *  logs
  *  release 0.25.0
  *  Merge pull request #80 from YandexClassifieds/AUTORUAPI-5576_ban_duplicate
     AUTORUAPI-5576 change ban notification logic
  *  original offer id
  *  Merge pull request #83 from YandexClassifieds/VOS-2929_offers_list_sort
     VOS-2929 sort fix
  *  tests
  *  VOS-3072 reduced keep-alive connection ttl
  *  sort fix
  *  refactoring
  *  remove dead code (#48)
     remove sales_certification db
  *  VOS-3066 better licenseplate monitorings; removed obsolete code (#81)
     * VOS-3066 better licenseplate monitorings; removed obsolete code
     
     * fix style
     
     * fix compilation
  *  change ban notification logic
  *  Merge pull request #68 from YandexClassifieds/CARFAX-162_send_all
     CARFAX-162 alternative way
  *  added args size
  *  debug logs
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  update big queue batch size
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  shining new 1mb batch
  *  fix compilation
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  play with kafka batch
  *  temp fix test
  *  alternative way

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Wed, 13 Mar 2019 07:48:32 +0300

## yandex-vos2-autoru-consumers:0.25.0 (Tue, 12 Mar 2019 17:38:43 +0300)

  *  Merge pull request #80 from YandexClassifieds/AUTORUAPI-5576_ban_duplicate
     AUTORUAPI-5576 change ban notification logic
  *  original offer id
  *  Merge pull request #83 from YandexClassifieds/VOS-2929_offers_list_sort
     VOS-2929 sort fix
  *  tests
  *  VOS-3072 reduced keep-alive connection ttl
  *  sort fix
  *  refactoring
  *  remove dead code (#48)
     remove sales_certification db
  *  VOS-3066 better licenseplate monitorings; removed obsolete code (#81)
     * VOS-3066 better licenseplate monitorings; removed obsolete code
     
     * fix style
     
     * fix compilation
  *  change ban notification logic
  *  Merge pull request #68 from YandexClassifieds/CARFAX-162_send_all
     CARFAX-162 alternative way
  *  added args size
  *  debug logs
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  update big queue batch size
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  shining new 1mb batch
  *  fix compilation
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  Merge remote-tracking branch 'origin/master' into CARFAX-162_send_all
  *  play with kafka batch
  *  temp fix test
  *  alternative way

 -- robot-vertis-repo <robot-vertis-repo@yandex-team.ru>  Tue, 12 Mar 2019 17:38:43 +0300

## yandex-vos2-autoru-consumers:0.24.2 (Thu, 07 Mar 2019 17:34:05 +0300)

  *  refactoring
  *  fix timer
  *  batch settings
  *  more debug logs
  *  fix compilation
  *  added comment
  *  Merge remote-tracking branch 'origin/master'
  *  optimize batch update
  *  fix create index method
  *  optimize filters
  *  Merge remote-tracking branch 'origin/AUTORUAPI-5427_vin_suggest'
     # Conflicts:
     #	pom.xml
  *  Vos 2648 Добавить новые типы двигателя для комм. транса (#69)
     VOS-2648 add new engine type for trucks
  *  fix table name
  *  fix PR
  *  Merge pull request #67 from YandexClassifieds/VOS-3056
     VOS-3056 search tag white list
  *  add parse test
  *  Merge remote-tracking branch 'origin/master' into VOS-3056
  *  refactoring
  *  swagger
  *  added routing
  *  use custom in correct test
  *  use custom in test
  *  logic and test
  *  create data def
  *  added response model and dao
  *  init commit

 -- teamcity <teamcity@yandex-team.ru>  Thu, 07 Mar 2019 17:34:05 +0300

## yandex-vos2-autoru-consumers:0.24.1 (Wed, 06 Mar 2019 18:21:07 +0300)

  *  fix create index method
  *  optimize filters
  *  Merge remote-tracking branch 'origin/AUTORUAPI-5427_vin_suggest'
     # Conflicts:
     #	pom.xml
  *  Vos 2648 Добавить новые типы двигателя для комм. транса (#69)
     VOS-2648 add new engine type for trucks
  *  fix table name
  *  fix PR
  *  Merge pull request #67 from YandexClassifieds/VOS-3056
     VOS-3056 search tag white list
  *  add parse test
  *  Merge remote-tracking branch 'origin/master' into VOS-3056
  *  refactoring
  *  swagger
  *  added routing
  *  use custom in correct test
  *  use custom in test
  *  logic and test
  *  create data def
  *  added response model and dao
  *  init commit

 -- teamcity <teamcity@yandex-team.ru>  Wed, 06 Mar 2019 18:21:07 +0300

## yandex-vos2-autoru-consumers:0.24.0 (Tue, 05 Mar 2019 18:20:53 +0300)

  *  Merge remote-tracking branch 'origin/AUTORUAPI-5427_vin_suggest'
     # Conflicts:
     #	pom.xml
  *  Vos 2648 Добавить новые типы двигателя для комм. транса (#69)
     VOS-2648 add new engine type for trucks
  *  fix table name
  *  fix PR
  *  Merge pull request #67 from YandexClassifieds/VOS-3056
     VOS-3056 search tag white list
  *  add parse test
  *  Merge remote-tracking branch 'origin/master' into VOS-3056
  *  refactoring
  *  swagger
  *  added routing
  *  use custom in correct test
  *  use custom in test
  *  logic and test
  *  create data def
  *  added response model and dao
  *  init commit

 -- teamcity <teamcity@yandex-team.ru>  Tue, 05 Mar 2019 18:20:53 +0300

## yandex-vos2-autoru-consumers:0.23.0 (Tue, 05 Mar 2019 12:15:15 +0300)



 -- teamcity <teamcity@yandex-team.ru>  Tue, 05 Mar 2019 12:15:15 +0300

## yandex-vos2-autoru-consumers:0.22.7 (Mon, 04 Mar 2019 13:34:23 +0300)

  *  AUTORUAPI-5367: compilation fix
  *  AUTORUAPI-5367: hotfix, merge function try-catch
  *  Merge remote-tracking branch 'origin/VOS-2929_index_update'
  *  batch size metric
  *  revisit api
     refactoring deduplication
  *  Revert "Revert "VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sende…""
  *  deduplication cache logic fix
  *  VOS-3054 new regions
  *  Revert "VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sende…"
  *  Merge pull request #57 from YandexClassifieds/VOS-3044
     VOS-3044 add fields to offer change event
  *  refactoring debug logs
  *  VOS-3044 merge with master
  *  Merge remote-tracking branch 'origin/master'
  *  debug logs
  *  Merge pull request #52 from YandexClassifieds/VOS-3020
     VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sende…
  *  VOS-3044 up schema version
  *  Vos 3053 Оторвать миграцию двигателя в/из старой базы (#63)
     * VOS-3053 remove engine type for old db
  *  Fix type mismatch
  *  added transaction read committed
  *  Merge remote-tracking branch 'origin/master'
  *  added debug logs
  *  Merge remote-tracking branch 'origin/VOS-2929_index_update'
  *  fix deduplication
  *  Merge pull request #61 from YandexClassifieds/VOS-2929_index_update
     VOS-2929 index update
  *  Исправления по ревью.
  *  return pending tests
  *  fix aggregate key; fix update feature; filter draft and anon.
  *  pending tests (temp)
  *  fix changelog [2]
  *  don't include user index in watchers if feature not enabled (temp)
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/offers/AutoruOfferWatchers.scala
  *  fix deduplication and tests
  *  partitions support
  *  fixIndex param and refactoring
  *  added feature
     added test
     fix save
  *  added tests for user index table
  *  VOS-3044 review fix
  *  added tests
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
  *  fix delete
  *  VOS-3044 add fields to offer change event
  *  added user index watcher
  *  added aggregate watchers
  *  read + scheduler update
  *  VOS-3020  Исправления
  *  VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sender_template

 -- teamcity <teamcity@yandex-team.ru>  Mon, 04 Mar 2019 13:34:23 +0300

## yandex-vos2-autoru-consumers:0.22.6 (Fri, 01 Mar 2019 16:25:44 +0300)

  *  Merge remote-tracking branch 'origin/VOS-2929_index_update'
  *  batch size metric
  *  revisit api
     refactoring deduplication
  *  Revert "Revert "VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sende…""
  *  deduplication cache logic fix
  *  VOS-3054 new regions
  *  Revert "VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sende…"
  *  Merge pull request #57 from YandexClassifieds/VOS-3044
     VOS-3044 add fields to offer change event
  *  refactoring debug logs
  *  VOS-3044 merge with master
  *  Merge remote-tracking branch 'origin/master'
  *  debug logs
  *  Merge pull request #52 from YandexClassifieds/VOS-3020
     VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sende…
  *  VOS-3044 up schema version
  *  Vos 3053 Оторвать миграцию двигателя в/из старой базы (#63)
     * VOS-3053 remove engine type for old db
  *  Fix type mismatch
  *  added transaction read committed
  *  Merge remote-tracking branch 'origin/master'
  *  added debug logs
  *  Merge remote-tracking branch 'origin/VOS-2929_index_update'
  *  fix deduplication
  *  Merge pull request #61 from YandexClassifieds/VOS-2929_index_update
     VOS-2929 index update
  *  Исправления по ревью.
  *  return pending tests
  *  fix aggregate key; fix update feature; filter draft and anon.
  *  pending tests (temp)
  *  fix changelog [2]
  *  don't include user index in watchers if feature not enabled (temp)
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/offers/AutoruOfferWatchers.scala
  *  fix deduplication and tests
  *  partitions support
  *  fixIndex param and refactoring
  *  added feature
     added test
     fix save
  *  added tests for user index table
  *  VOS-3044 review fix
  *  added tests
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
  *  fix delete
  *  VOS-3044 add fields to offer change event
  *  added user index watcher
  *  added aggregate watchers
  *  read + scheduler update
  *  VOS-3020  Исправления
  *  VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sender_template

 -- teamcity <teamcity@yandex-team.ru>  Fri, 01 Mar 2019 16:25:44 +0300

## yandex-vos2-autoru-consumers:0.22.5 (Fri, 01 Mar 2019 10:29:46 +0300)

  *  deduplication cache logic fix
  *  VOS-3054 new regions
  *  Revert "VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sende…"
  *  Merge pull request #57 from YandexClassifieds/VOS-3044
     VOS-3044 add fields to offer change event
  *  refactoring debug logs
  *  VOS-3044 merge with master
  *  Merge remote-tracking branch 'origin/master'
  *  debug logs
  *  Merge pull request #52 from YandexClassifieds/VOS-3020
     VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sende…
  *  VOS-3044 up schema version
  *  Vos 3053 Оторвать миграцию двигателя в/из старой базы (#63)
     * VOS-3053 remove engine type for old db
  *  Fix type mismatch
  *  added transaction read committed
  *  Merge remote-tracking branch 'origin/master'
  *  added debug logs
  *  Merge remote-tracking branch 'origin/VOS-2929_index_update'
  *  fix deduplication
  *  Merge pull request #61 from YandexClassifieds/VOS-2929_index_update
     VOS-2929 index update
  *  Исправления по ревью.
  *  return pending tests
  *  fix aggregate key; fix update feature; filter draft and anon.
  *  pending tests (temp)
  *  fix changelog [2]
  *  don't include user index in watchers if feature not enabled (temp)
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/offers/AutoruOfferWatchers.scala
  *  fix deduplication and tests
  *  partitions support
  *  fixIndex param and refactoring
  *  added feature
     added test
     fix save
  *  added tests for user index table
  *  VOS-3044 review fix
  *  added tests
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
  *  fix delete
  *  VOS-3044 add fields to offer change event
  *  added user index watcher
  *  added aggregate watchers
  *  read + scheduler update
  *  VOS-3020  Исправления
  *  VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sender_template

 -- teamcity <teamcity@yandex-team.ru>  Fri, 01 Mar 2019 10:29:46 +0300

## yandex-vos2-autoru-consumers:0.22.4 (Thu, 28 Feb 2019 16:44:09 +0300)

  *  Merge pull request #57 from YandexClassifieds/VOS-3044
     VOS-3044 add fields to offer change event
  *  refactoring debug logs
  *  VOS-3044 merge with master
  *  Merge remote-tracking branch 'origin/master'
  *  debug logs
  *  Merge pull request #52 from YandexClassifieds/VOS-3020
     VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sende…
  *  VOS-3044 up schema version
  *  Vos 3053 Оторвать миграцию двигателя в/из старой базы (#63)
     * VOS-3053 remove engine type for old db
  *  Fix type mismatch
  *  added transaction read committed
  *  Merge remote-tracking branch 'origin/master'
  *  added debug logs
  *  Merge remote-tracking branch 'origin/VOS-2929_index_update'
  *  fix deduplication
  *  Merge pull request #61 from YandexClassifieds/VOS-2929_index_update
     VOS-2929 index update
  *  Исправления по ревью.
  *  return pending tests
  *  fix aggregate key; fix update feature; filter draft and anon.
  *  pending tests (temp)
  *  fix changelog [2]
  *  don't include user index in watchers if feature not enabled (temp)
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/offers/AutoruOfferWatchers.scala
  *  fix deduplication and tests
  *  partitions support
  *  fixIndex param and refactoring
  *  added feature
     added test
     fix save
  *  added tests for user index table
  *  VOS-3044 review fix
  *  added tests
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
  *  fix delete
  *  VOS-3044 add fields to offer change event
  *  added user index watcher
  *  added aggregate watchers
  *  read + scheduler update
  *  VOS-3020  Исправления
  *  VOS-3020 [vos2-autoru] Обрабатывать опинионы, к которых нет vos_sender_template

 -- teamcity <teamcity@yandex-team.ru>  Thu, 28 Feb 2019 16:44:09 +0300

## yandex-vos2-autoru-consumers:0.22.3 (Thu, 28 Feb 2019 12:11:45 +0300)

  *  added transaction read committed
  *  Merge remote-tracking branch 'origin/master'
  *  added debug logs
  *  Merge remote-tracking branch 'origin/VOS-2929_index_update'
  *  fix deduplication
  *  Merge pull request #61 from YandexClassifieds/VOS-2929_index_update
     VOS-2929 index update
  *  return pending tests
  *  fix aggregate key; fix update feature; filter draft and anon.
  *  pending tests (temp)
  *  fix changelog [2]
  *  don't include user index in watchers if feature not enabled (temp)
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/offers/AutoruOfferWatchers.scala
  *  fix deduplication and tests
  *  partitions support
  *  fixIndex param and refactoring
  *  added feature
     added test
     fix save
  *  added tests for user index table
  *  added tests
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
  *  fix delete
  *  added user index watcher
  *  added aggregate watchers
  *  read + scheduler update

 -- teamcity <teamcity@yandex-team.ru>  Thu, 28 Feb 2019 12:11:45 +0300

## yandex-vos2-autoru-consumers:0.22.2 (Wed, 27 Feb 2019 18:55:48 +0300)

  *  Merge remote-tracking branch 'origin/VOS-2929_index_update'
  *  fix deduplication
  *  Merge pull request #61 from YandexClassifieds/VOS-2929_index_update
     VOS-2929 index update
  *  return pending tests
  *  fix aggregate key; fix update feature; filter draft and anon.
  *  pending tests (temp)
  *  fix changelog [2]
  *  don't include user index in watchers if feature not enabled (temp)
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/offers/AutoruOfferWatchers.scala
  *  fix deduplication and tests
  *  partitions support
  *  fixIndex param and refactoring
  *  added feature
     added test
     fix save
  *  added tests for user index table
  *  added tests
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
  *  fix delete
  *  added user index watcher
  *  added aggregate watchers
  *  read + scheduler update

 -- teamcity <teamcity@yandex-team.ru>  Wed, 27 Feb 2019 18:55:48 +0300

## yandex-vos2-autoru-consumers:0.22.1 (Wed, 27 Feb 2019 14:56:46 +0300)

  *  Merge pull request #61 from YandexClassifieds/VOS-2929_index_update
     VOS-2929 index update
  *  return pending tests
  *  fix aggregate key; fix update feature; filter draft and anon.
  *  pending tests (temp)
  *  fix changelog [2]
  *  don't include user index in watchers if feature not enabled (temp)
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/offers/AutoruOfferWatchers.scala
  *  fix deduplication and tests
  *  partitions support
  *  fixIndex param and refactoring
  *  added feature
     added test
     fix save
  *  added tests for user index table
  *  added tests
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
  *  fix delete
  *  added user index watcher
  *  added aggregate watchers
  *  read + scheduler update

 -- teamcity <teamcity@yandex-team.ru>  Wed, 27 Feb 2019 14:56:46 +0300

## yandex-vos2-autoru-consumers:0.22.0 (Wed, 27 Feb 2019 08:10:49 +0300)

  *  pending tests (temp)
  *  fix changelog [2]
  *  don't include user index in watchers if feature not enabled (temp)
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/dao/offers/AutoruOfferWatchers.scala
  *  fix deduplication and tests
  *  partitions support
  *  fixIndex param and refactoring
  *  added feature
     added test
     fix save
  *  added tests for user index table
  *  added tests
  *  Merge remote-tracking branch 'origin/master' into VOS-2929_index_update
  *  fix delete
  *  added user index watcher
  *  added aggregate watchers
  *  read + scheduler update

 -- teamcity <teamcity@yandex-team.ru>  Wed, 27 Feb 2019 08:10:49 +0300

## yandex-vos2-autoru-consumers:0.21.2 (Mon, 25 Feb 2019 19:54:20 +0300)

  *  AUTORUAPI-5367: wheel & geartype merge fix
  *  VOS-2983 config
  *  AUTORUAPI-5527 reduce dns cache ttl
  *  AUTORUAPI-5527 reduce dns cache ttl
  *  add all reasons to OpinionWriter status change
  *  AUTORUAPI-5367: rm verbose logging
  *  Merge pull request #49 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_4
     Autoruapi 5367 non modified tech and color 4
  *  AUTORUAPI-5367: review case simplification
  *  AUTORUAPI-5367: new functionality tests
  *  AUTORUAPI-5367: review fixes
  *  AUTORUAPI-5367: fix tests & OfferMerger tests
  *  AUTORUAPI-5367: fix tests
  *  AUTORUAPI-5509 fix save equipment
  *  AUTORUAPI-5367: more only moderation-editable fields, code refactroing
  *  Revert "Revert "Merge pull request #2 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_2""
     This reverts commit 20b4456117d5001a72d32f41c0f5238cef19f886.
  *  AUTORUAPI-5391 add feature for increased price
  *  SALESMAN-481 # Offer.CountersStartDate
  *  Merge pull request #31 from YandexClassifieds/VOS-3015
     VOS-3015 Выпилить миграцию и сохранение sales_images для комтс и мото
  *  Merge branch 'master' into VOS-3015
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/services/OfferConverterCommon.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ParsingPhotosUploadStageTest.scala
  *  Remove all.sale_images / all7.sales_images DB insert's for tests and fix tests
  *  Fix offer converter
  *  VOS-3015 Выпилить миграцию и сохранение sales_images для комтс и мото

 -- teamcity <teamcity@yandex-team.ru>  Mon, 25 Feb 2019 19:54:20 +0300

## yandex-vos2-autoru-consumers:0.21.1 (Thu, 21 Feb 2019 17:04:53 +0300)

  *  AUTORUAPI-5367: rm verbose logging
  *  Merge pull request #49 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_4
     Autoruapi 5367 non modified tech and color 4
  *  AUTORUAPI-5367: review case simplification
  *  AUTORUAPI-5367: new functionality tests
  *  AUTORUAPI-5367: review fixes
  *  AUTORUAPI-5367: fix tests & OfferMerger tests
  *  AUTORUAPI-5367: fix tests
  *  AUTORUAPI-5509 fix save equipment
  *  AUTORUAPI-5367: more only moderation-editable fields, code refactroing
  *  Revert "Revert "Merge pull request #2 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_2""
     This reverts commit 20b4456117d5001a72d32f41c0f5238cef19f886.
  *  AUTORUAPI-5391 add feature for increased price
  *  SALESMAN-481 # Offer.CountersStartDate
  *  Merge pull request #31 from YandexClassifieds/VOS-3015
     VOS-3015 Выпилить миграцию и сохранение sales_images для комтс и мото
  *  Merge branch 'master' into VOS-3015
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/services/OfferConverterCommon.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ParsingPhotosUploadStageTest.scala
  *  Remove all.sale_images / all7.sales_images DB insert's for tests and fix tests
  *  Fix offer converter
  *  VOS-3015 Выпилить миграцию и сохранение sales_images для комтс и мото

 -- teamcity <teamcity@yandex-team.ru>  Thu, 21 Feb 2019 17:04:53 +0300

## yandex-vos2-autoru-consumers:0.21.0 (Thu, 21 Feb 2019 15:24:59 +0300)

  *  Merge pull request #49 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_4
     Autoruapi 5367 non modified tech and color 4
  *  AUTORUAPI-5367: review case simplification
  *  AUTORUAPI-5367: new functionality tests
  *  AUTORUAPI-5367: review fixes
  *  AUTORUAPI-5367: fix tests & OfferMerger tests
  *  AUTORUAPI-5367: fix tests
  *  AUTORUAPI-5509 fix save equipment
  *  AUTORUAPI-5367: more only moderation-editable fields, code refactroing
  *  Revert "Revert "Merge pull request #2 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_2""
     This reverts commit 20b4456117d5001a72d32f41c0f5238cef19f886.
  *  AUTORUAPI-5391 add feature for increased price
  *  SALESMAN-481 # Offer.CountersStartDate
  *  Merge pull request #31 from YandexClassifieds/VOS-3015
     VOS-3015 Выпилить миграцию и сохранение sales_images для комтс и мото
  *  Merge branch 'master' into VOS-3015
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/services/OfferConverterCommon.scala
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/ParsingPhotosUploadStageTest.scala
  *  Remove all.sale_images / all7.sales_images DB insert's for tests and fix tests
  *  Fix offer converter
  *  VOS-3015 Выпилить миграцию и сохранение sales_images для комтс и мото

 -- teamcity <teamcity@yandex-team.ru>  Thu, 21 Feb 2019 15:24:59 +0300

## yandex-vos2-autoru-consumers:0.20.1 (Fri, 15 Feb 2019 15:37:43 +0300)

  *  Merge pull request #41 from YandexClassifieds/VOS-3019
     VOS-3019 mark all feedprocessor images
  *  Merge pull request #36 from YandexClassifieds/VOS-3028
     VOS-3028 Не мигрировать sales_damage
  *  Merge pull request #40 from YandexClassifieds/VOS-3038
     VOS-3038 ignore images not found in mds
  *  VOS-3028 Не мигрировать sales_damage
  *  VOS-3038 ignore images not found in mds
  *  
     VOS-2995 forgotten req entity
  *  mark all feedprocessor images
  *  
     VOS-2995 log on unexpected passport response
  *  add reserved
  *  VOS-3035 remove old autocode
  *  Merge pull request #38 from YandexClassifieds/VOS-3036_moderation_factors
     VOS-3036 remove moderation factors
  *  VOS-3037 fixed order
  *  VOS-3037 sort by category before other fields
  *  VOS-3036 remove moderation factors
  *  Merge pull request #33 from YandexClassifieds/VOS-2995_sms
     VOS-2995 userRef -> user
  *  
     test fix
  *  
     refactoring
  *  
     use UserRef to passport uuid convertation
  *  AUTORUSUP-4407: increase kafka read/write timeout 1 second -> 10 seconds
  *  
     unused import
  *  
     userRef -> userId
  *  Merge pull request #29 from YandexClassifieds/AUTORUAPI-5417_celebrity_alert
     AUTORUAPI-5417 celebrity alert
  *  AUTORUAPI-5417 replace, filter, lower case
  *  Merge branch 'master' into AUTORUAPI-5417_celebrity_alert
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/features/AutoruFeatures.scala
  *  AUTORUAPI-5417 celebrity alert

 -- teamcity <teamcity@yandex-team.ru>  Fri, 15 Feb 2019 15:37:43 +0300

## yandex-vos2-autoru-consumers:0.20.0 (Fri, 15 Feb 2019 13:59:32 +0300)

  *  add reserved
  *  VOS-3035 remove old autocode
  *  Merge pull request #38 from YandexClassifieds/VOS-3036_moderation_factors
     VOS-3036 remove moderation factors
  *  VOS-3037 fixed order
  *  VOS-3037 sort by category before other fields
  *  VOS-3036 remove moderation factors
  *  Merge pull request #33 from YandexClassifieds/VOS-2995_sms
     VOS-2995 userRef -> user
  *  
     test fix
  *  
     refactoring
  *  
     use UserRef to passport uuid convertation
  *  AUTORUSUP-4407: increase kafka read/write timeout 1 second -> 10 seconds
  *  
     unused import
  *  
     userRef -> userId
  *  Merge pull request #29 from YandexClassifieds/AUTORUAPI-5417_celebrity_alert
     AUTORUAPI-5417 celebrity alert
  *  AUTORUAPI-5417 replace, filter, lower case
  *  Merge branch 'master' into AUTORUAPI-5417_celebrity_alert
     # Conflicts:
     #	vos2-autoru-core/src/main/scala/ru/yandex/vos2/autoru/features/AutoruFeatures.scala
  *  AUTORUAPI-5417 celebrity alert

 -- teamcity <teamcity@yandex-team.ru>  Fri, 15 Feb 2019 13:59:32 +0300

## yandex-vos2-autoru-consumers:0.19.3 (Thu, 14 Feb 2019 14:59:38 +0300)

  *  Vos 3002 remove extras for old db (#26)
     VOS-3002 remove sale option from old db
  *  Merge pull request #23 from YandexClassifieds/VOS-3027_remove_description
     VOS-3027 remove saving offer description to old db
  *  
     exp sms != razyan sms
  *  VOS-3021 fixing oom
  *  Revert "Merge pull request #2 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_2"
     This reverts commit 7f4803977080adc8d55287104c95dd51a8d3a2fc, reversing
     changes made to 8177a098962a1abde5f4157de0ec0fea6a446b16.
  *  Merge pull request #27 from YandexClassifieds/AUTORUAPI-5458
     AUTORUAPI-5458 увеличил значение для валидации высоты подъема автопог…
  *  AUTORUAPI-5458 увеличил значение для валидации высоты подъема автопогрузчика
  *  Merge branch 'master' into VOS-2995_sms
  *  Revert "VOS-3021 fix OOM caused by YoctoCarsCatalog"
     This reverts commit 1e1d9034672b735896ec158689e139ee95719c3e.
  *  Merge branch 'master' into VOS-2995_sms
  *  
     exp sms feature
  *  VOS-3021 fix OOM caused by YoctoCarsCatalog
  *  Merge pull request #2 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_2
     AUTORUAPI-5367: ignore tech_param, color modification from feed
  *  VOS-3027 fix tests
  *  AUTORUAPI-5466 separate errors for vin & license plate requirments
  *  VOS-3027 remove saving offer description to old db
  *  minor style fixes
  *  Merge pull request #21 from YandexClassifieds/VOS-2747_remove_compression
     VOS-2747 remove compression
  *  another cleanup
  *  remove compression logic
  *  fix delete teleperformance
  *  remove MdsPhotoTypes
  *  cleanup data
  *  AUTORUAPI-5367: review fix
  *  Merge branch 'master' into AUTORUAPI-5367_non_modified_tech_and_color_2
  *  
     offer creation exp sms
  *  AUTORUAPI-5367: color fix
  *  AUTORUAPI-5367: code simplification, tests
  *  AUTORUAPI-5367: non modified field notices
  *  AUTORUAPI-5367: ignore tech_param, color modification from feed

 -- teamcity <teamcity@yandex-team.ru>  Thu, 14 Feb 2019 14:59:38 +0300

## yandex-vos2-autoru-consumers:0.19.2 (Thu, 14 Feb 2019 12:12:49 +0300)

  *  Merge pull request #23 from YandexClassifieds/VOS-3027_remove_description
     VOS-3027 remove saving offer description to old db
  *  
     exp sms != razyan sms
  *  VOS-3021 fixing oom
  *  Revert "Merge pull request #2 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_2"
     This reverts commit 7f4803977080adc8d55287104c95dd51a8d3a2fc, reversing
     changes made to 8177a098962a1abde5f4157de0ec0fea6a446b16.
  *  Merge pull request #27 from YandexClassifieds/AUTORUAPI-5458
     AUTORUAPI-5458 увеличил значение для валидации высоты подъема автопог…
  *  AUTORUAPI-5458 увеличил значение для валидации высоты подъема автопогрузчика
  *  Merge branch 'master' into VOS-2995_sms
  *  Revert "VOS-3021 fix OOM caused by YoctoCarsCatalog"
     This reverts commit 1e1d9034672b735896ec158689e139ee95719c3e.
  *  Merge branch 'master' into VOS-2995_sms
  *  
     exp sms feature
  *  VOS-3021 fix OOM caused by YoctoCarsCatalog
  *  Merge pull request #2 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_2
     AUTORUAPI-5367: ignore tech_param, color modification from feed
  *  VOS-3027 fix tests
  *  AUTORUAPI-5466 separate errors for vin & license plate requirments
  *  VOS-3027 remove saving offer description to old db
  *  minor style fixes
  *  Merge pull request #21 from YandexClassifieds/VOS-2747_remove_compression
     VOS-2747 remove compression
  *  another cleanup
  *  remove compression logic
  *  fix delete teleperformance
  *  remove MdsPhotoTypes
  *  cleanup data
  *  AUTORUAPI-5367: review fix
  *  Merge branch 'master' into AUTORUAPI-5367_non_modified_tech_and_color_2
  *  
     offer creation exp sms
  *  AUTORUAPI-5367: color fix
  *  AUTORUAPI-5367: code simplification, tests
  *  AUTORUAPI-5367: non modified field notices
  *  AUTORUAPI-5367: ignore tech_param, color modification from feed

 -- teamcity <teamcity@yandex-team.ru>  Thu, 14 Feb 2019 12:12:49 +0300

## yandex-vos2-autoru-consumers:0.19.1 (Wed, 13 Feb 2019 20:42:23 +0300)

  *  VOS-3021 fixing oom
  *  Revert "Merge pull request #2 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_2"
     This reverts commit 7f4803977080adc8d55287104c95dd51a8d3a2fc, reversing
     changes made to 8177a098962a1abde5f4157de0ec0fea6a446b16.
  *  Merge pull request #27 from YandexClassifieds/AUTORUAPI-5458
     AUTORUAPI-5458 увеличил значение для валидации высоты подъема автопог…
  *  AUTORUAPI-5458 увеличил значение для валидации высоты подъема автопогрузчика
  *  Merge branch 'master' into VOS-2995_sms
  *  Revert "VOS-3021 fix OOM caused by YoctoCarsCatalog"
     This reverts commit 1e1d9034672b735896ec158689e139ee95719c3e.
  *  Merge branch 'master' into VOS-2995_sms
  *  
     exp sms feature
  *  VOS-3021 fix OOM caused by YoctoCarsCatalog
  *  Merge pull request #2 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_2
     AUTORUAPI-5367: ignore tech_param, color modification from feed
  *  AUTORUAPI-5466 separate errors for vin & license plate requirments
  *  minor style fixes
  *  Merge pull request #21 from YandexClassifieds/VOS-2747_remove_compression
     VOS-2747 remove compression
  *  another cleanup
  *  remove compression logic
  *  fix delete teleperformance
  *  remove MdsPhotoTypes
  *  cleanup data
  *  AUTORUAPI-5367: review fix
  *  Merge branch 'master' into AUTORUAPI-5367_non_modified_tech_and_color_2
  *  
     offer creation exp sms
  *  AUTORUAPI-5367: color fix
  *  AUTORUAPI-5367: code simplification, tests
  *  AUTORUAPI-5367: non modified field notices
  *  AUTORUAPI-5367: ignore tech_param, color modification from feed

 -- teamcity <teamcity@yandex-team.ru>  Wed, 13 Feb 2019 20:42:23 +0300

## yandex-vos2-autoru-consumers:0.19.0 (Tue, 12 Feb 2019 19:25:54 +0300)

  *  Merge pull request #2 from YandexClassifieds/AUTORUAPI-5367_non_modified_tech_and_color_2
     AUTORUAPI-5367: ignore tech_param, color modification from feed
  *  AUTORUAPI-5466 separate errors for vin & license plate requirments
  *  minor style fixes
  *  Merge pull request #21 from YandexClassifieds/VOS-2747_remove_compression
     VOS-2747 remove compression
  *  another cleanup
  *  remove compression logic
  *  fix delete teleperformance
  *  remove MdsPhotoTypes
  *  cleanup data
  *  AUTORUAPI-5367: review fix
  *  Merge branch 'master' into AUTORUAPI-5367_non_modified_tech_and_color_2
  *  AUTORUAPI-5367: color fix
  *  AUTORUAPI-5367: code simplification, tests
  *  AUTORUAPI-5367: non modified field notices
  *  AUTORUAPI-5367: ignore tech_param, color modification from feed

 -- teamcity <teamcity@yandex-team.ru>  Tue, 12 Feb 2019 19:25:54 +0300

## yandex-vos2-autoru-consumers:0.18.0 (Fri, 08 Feb 2019 13:45:03 +0300)

  *  fix converter and components
  *  delete teleperformance from vos
  *  Merge pull request #18 from YandexClassifieds/REVIEWS-4717_review_promo2
     REVIEWS-4717 review promo 2
  *  REVIEWS-4717 review promo 2

 -- teamcity <teamcity@yandex-team.ru>  Fri, 08 Feb 2019 13:45:03 +0300

## yandex-vos2-autoru-consumers:0.17.0 (Wed, 06 Feb 2019 20:04:18 +0300)

  *  fix PR
  *  fix label for local logback
  *  fix typo
  *  Merge remote-tracking branch 'origin/master' into VOS-3011_json_logs
     # Conflicts:
     #	vos2-autoru-consumers/CHANGELOG.md
  *  added json appender

 -- teamcity <teamcity@yandex-team.ru>  Wed, 06 Feb 2019 20:04:18 +0300

## yandex-vos2-autoru-consumers:0.16.1 (Wed, 06 Feb 2019 14:49:08 +0300)

  *  Merge branch 'master' into AUTORUAPI-5337_vin_grz_required
  *  AUTORUAPI-5337 change validation error
  *  Merge pull request #8 from YandexClassifieds/revert-733-revert-726-VOS-2980_sales_images
     VOS-2980 ignore photos from all7.sales_images in migration
  *  Merge pull request #5 from YandexClassifieds/AUTORUAPI-5387
     AUTORUAPI-5387
  *  Merge pull request #9 from YandexClassifieds/AUTORUAPI-5337_vin_grz_required
     AUTORUAPI-5337 vin and license plate are required both
  *  Merge branch 'master' into revert-733-revert-726-VOS-2980_sales_images
  *  Merge branch 'master' into revert-733-revert-726-VOS-2980_sales_images
     # Conflicts:
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/PhotoSmartOrderSyncStageTest.scala
  *  mode debug logs
  *  allow only uniqeue photo name in photo migration
  *  fix photo migration
  *  refactoring
  *  added debug stage
  *  AUTORUAPI-5407 provide published phones
  *  Merge pull request #747 from YandexClassifieds/VOS-3008_skip_non_checked_photos
     VOS-3008 skip sending non-checked photos
  *  another fixes
  *  fix
  *  blurred photos in test
  *  AUTORUAPI-5387 fix tests and doc
  *  typo
  *  update test
  *  fix env
  *  log slow query = false in vos2-autoru-scheduler (experiment)
  *  VOS-3008 skip sending non-checked photos
  *  AUTORUAPI-5387 fix tests
  *  Merge pull request #744 from YandexClassifieds/VOS-3001_ryazan_kc
     VOS-3001 skip photos from Ryazan call center && change sms
  *  AUTORUAPI-5387 move all offer publish under db lock
  *  AUTORUAPI-5337 noLicensePlateSupport test
  *  AUTORUAPI-5337 fix noLicensePlateSupport support
  *  VOS-3001 fix test
  *  VOS-3001 test & fix build
  *  VOS-3001 skip photos from Ryazan call center && change sms
  *  db connection acquire timer; replace proxy implementation
  *  increase frame buffer size
  *  AUTORUAPI-5337 parse regions from bunker data type
  *  AUTORUAPI-5337 move homeless extdata models to special extdata package
  *  AUTORUAPI-5337 required vin and license plate test
  *  fix order
  *  refactoring
  *  Merge remote-tracking branch 'origin/master'
  *  alloc analyze
  *  Merge pull request #742 from YandexClassifieds/feature/REALTYBACK-438
     Feature/realtyback 438, 0 is now considered absent value in Metro::timeOnFoot and Metro::timeOnTransport
  *  fix path
  *  more profiling experiments
  *  60 seconds cpu profiling
  *  AUTORUAPI-5337 required vin and license plate
  *  feature/REALTYBACK-438: Done
  *  -e itimer
  *  Merge remote-tracking branch 'origin/async_profiler'
     # Conflicts:
     #	vos2-autoru-cv/CHANGELOG.md
  *  added profiler files to container
  *  Realty. Added force_revisits_count to storage model
  *  Merge remote-tracking branch 'origin/master'
  *  fix path
  *  Merge pull request #741 from YandexClassifieds/VOS-2972
     VOS-2972 fix inf duration
  *  VOS-2972 fix inf duration
  *  delete resources
  *  added profiler to resources
  *  async sampling profiler
  *  Merge pull request #722 from YandexClassifieds/VOS-2972
     VOS-2972 offer revisit
  *  Merge pull request #740 from YandexClassifieds/AUTORUAPI-5336_registered_in_russia
     AUTORUAPI-5336 not_registered_in_russia in moto & trucks
  *  AUTORUAPI-5336 not_registered_in_russia in moto & trucks
  *  Merge pull request #739 from YandexClassifieds/AUTORUAPI-5336_registered_in_russia
     AUTORUAPI-5336 NOT_registered_in_russia
  *  VOS-2972 add helper method
  *  AUTORUAPI-5336 NOT_registered_in_russia
  *  VOS-2972 merge with master
  *  AUTORUAPI-5336 registered_in_russia default true
  *  added additional metrics for migration
  *  Merge pull request #737 from YandexClassifieds/AUTORUAPI-5336_registered_in_russia
     AUTORUAPI-5336 registered in Russia
  *  AUTORUAPI-5336 tests & OfferConverterCommon
  *  AUTORUAPI-5336 registered in Russia
  *  VOS-2972 add metrics
  *  Merge remote-tracking branch 'origin/master' into VOS-2972
  *  Revert "Revert "VOS-2980 ignore photos from all7.sales_images in migration""
  *  VOS-2972 remove unused methods
  *  Merge remote-tracking branch 'origin/master' into VOS-2972
  *  VOS-2972 offer revisit

 -- teamcity <teamcity@yandex-team.ru>  Wed, 06 Feb 2019 14:49:08 +0300

## yandex-vos2-autoru-consumers:0.16.0 (Wed, 06 Feb 2019 12:05:42 +0300)

  *  Merge pull request #8 from YandexClassifieds/revert-733-revert-726-VOS-2980_sales_images
     VOS-2980 ignore photos from all7.sales_images in migration
  *  Merge pull request #5 from YandexClassifieds/AUTORUAPI-5387
     AUTORUAPI-5387
  *  Merge pull request #9 from YandexClassifieds/AUTORUAPI-5337_vin_grz_required
     AUTORUAPI-5337 vin and license plate are required both
  *  Merge branch 'master' into revert-733-revert-726-VOS-2980_sales_images
  *  Merge branch 'master' into revert-733-revert-726-VOS-2980_sales_images
     # Conflicts:
     #	vos2-autoru-scheduler/src/test/scala/ru/yandex/vos2/autoru/watching/stages/PhotoSmartOrderSyncStageTest.scala
  *  mode debug logs
  *  allow only uniqeue photo name in photo migration
  *  fix photo migration
  *  refactoring
  *  added debug stage
  *  AUTORUAPI-5407 provide published phones
  *  Merge pull request #747 from YandexClassifieds/VOS-3008_skip_non_checked_photos
     VOS-3008 skip sending non-checked photos
  *  another fixes
  *  fix
  *  blurred photos in test
  *  AUTORUAPI-5387 fix tests and doc
  *  typo
  *  update test
  *  fix env
  *  log slow query = false in vos2-autoru-scheduler (experiment)
  *  VOS-3008 skip sending non-checked photos
  *  AUTORUAPI-5387 fix tests
  *  Merge pull request #744 from YandexClassifieds/VOS-3001_ryazan_kc
     VOS-3001 skip photos from Ryazan call center && change sms
  *  AUTORUAPI-5387 move all offer publish under db lock
  *  AUTORUAPI-5337 noLicensePlateSupport test
  *  AUTORUAPI-5337 fix noLicensePlateSupport support
  *  VOS-3001 fix test
  *  VOS-3001 test & fix build
  *  VOS-3001 skip photos from Ryazan call center && change sms
  *  db connection acquire timer; replace proxy implementation
  *  increase frame buffer size
  *  AUTORUAPI-5337 parse regions from bunker data type
  *  AUTORUAPI-5337 move homeless extdata models to special extdata package
  *  AUTORUAPI-5337 required vin and license plate test
  *  fix order
  *  refactoring
  *  Merge remote-tracking branch 'origin/master'
  *  alloc analyze
  *  Merge pull request #742 from YandexClassifieds/feature/REALTYBACK-438
     Feature/realtyback 438, 0 is now considered absent value in Metro::timeOnFoot and Metro::timeOnTransport
  *  fix path
  *  more profiling experiments
  *  60 seconds cpu profiling
  *  AUTORUAPI-5337 required vin and license plate
  *  feature/REALTYBACK-438: Done
  *  -e itimer
  *  Merge remote-tracking branch 'origin/async_profiler'
     # Conflicts:
     #	vos2-autoru-cv/CHANGELOG.md
  *  added profiler files to container
  *  Realty. Added force_revisits_count to storage model
  *  Merge remote-tracking branch 'origin/master'
  *  fix path
  *  Merge pull request #741 from YandexClassifieds/VOS-2972
     VOS-2972 fix inf duration
  *  VOS-2972 fix inf duration
  *  delete resources
  *  added profiler to resources
  *  async sampling profiler
  *  Merge pull request #722 from YandexClassifieds/VOS-2972
     VOS-2972 offer revisit
  *  Merge pull request #740 from YandexClassifieds/AUTORUAPI-5336_registered_in_russia
     AUTORUAPI-5336 not_registered_in_russia in moto & trucks
  *  AUTORUAPI-5336 not_registered_in_russia in moto & trucks
  *  Merge pull request #739 from YandexClassifieds/AUTORUAPI-5336_registered_in_russia
     AUTORUAPI-5336 NOT_registered_in_russia
  *  VOS-2972 add helper method
  *  AUTORUAPI-5336 NOT_registered_in_russia
  *  VOS-2972 merge with master
  *  AUTORUAPI-5336 registered_in_russia default true
  *  added additional metrics for migration
  *  Merge pull request #737 from YandexClassifieds/AUTORUAPI-5336_registered_in_russia
     AUTORUAPI-5336 registered in Russia
  *  AUTORUAPI-5336 tests & OfferConverterCommon
  *  AUTORUAPI-5336 registered in Russia
  *  VOS-2972 add metrics
  *  Merge remote-tracking branch 'origin/master' into VOS-2972
  *  Revert "Revert "VOS-2980 ignore photos from all7.sales_images in migration""
  *  VOS-2972 remove unused methods
  *  Merge remote-tracking branch 'origin/master' into VOS-2972
  *  VOS-2972 offer revisit

 -- teamcity <teamcity@yandex-team.ru>  Wed, 06 Feb 2019 12:05:42 +0300

## yandex-vos2-autoru-consumers:0.15.0 (Mon, 28 Jan 2019 17:46:39 +0300)

  *  
     compilation fix
  *  
     moderation metrics
  *  VOS-2988 handle error 400 incorrect_params from parsing, fixed empty json case
  *  Realty consumer. Small refactoring
  *  Merge pull request #736 from YandexClassifieds/AUTORUAPI-5348
     AUTORUAPI-5348 fill source info for searcher
  *  AUTORUAPI-5348 add tests
  *  Merge pull request #732 from YandexClassifieds/CARFAX-127
     CARFAX-127: drop unnecessary tests
  *  AUTORUAPI-5348 fill source info for searcher
  *  CARFAX-127: fix tests
  *  VOS-2977 PhotoUtils tests fix
     (cherry picked from commit f823b3b196f170cb75d9b8f1917f909f3d36c789)
  *  Revert "VOS-2980 ignore photos from all7.sales_images in migration"
  *  Merge pull request #731 from YandexClassifieds/http_blocking
     added blocking to common http client
  *  Merge pull request #730 from YandexClassifieds/CARFAX-127
     CARFAX-127: don't mark unofficial programs
  *  added blocking to common http client
  *  review fixes
  *  Merge pull request #726 from YandexClassifieds/VOS-2980_sales_images
     VOS-2980 ignore photos from all7.sales_images in migration
  *  VOS-2988 handle error 400 incorrect_params from parsing, refactoring
  *  VOS-2988 handle error 400 incorrect_params from parsing, refactoring
  *  VOS-2988 handle error 400 incorrect_params from parsing
  *  allow points outside of image in custom blur
  *  fix
  *  Revert "Revert "delete autoru certifications""
     This reverts commit 91512e0
  *  Revert "delete autoru certifications"
     This reverts commit 82c1886
  *  Revert "temp pending photo utils test"
     This reverts commit 5f373d8
  *  Revert "fix and temp pending photo utils test"
     This reverts commit 167bb1e
  *  Revert "temp pending photo DraftHandlerPhotoTest"
     This reverts commit 62024c5
  *  Revert "return pending tests"
     This reverts commit 54a9def
  *  return pending tests
  *  temp pending photo DraftHandlerPhotoTest
  *  fix and temp pending photo utils test
  *  temp pending photo utils test
  *  delete autoru certifications
  *  more fixes
  *  more fixes
  *  another fix
  *  fixing tests
  *  cleanup
  *  VOS-2977 PhotoUtils tests fix
  *  VOS-2980 ignore photos from all7.sales_images in migration
  *  Merge pull request #724 from YandexClassifieds/AUTORUAPI-5348
     AUTORUAPI-5348 add is_callcanter to source info
  *  fix name length
  *  AUTORUAPI-5348 add is_callcanter to source info

 -- teamcity <teamcity@yandex-team.ru>  Mon, 28 Jan 2019 17:46:39 +0300

## yandex-vos2-autoru-consumers:0.14.0 (Tue, 22 Jan 2019 14:10:57 +0300)

  *  VOS-2976 multiple opinions apply (#723)
     * multiple opinions apply
     
     * pr fixes
  *  fix OfferNotFound in OffersWriter.addPhotoQuality
  *  Merge pull request #720 from YandexClassifieds/AUTORUAPI-5340_leave_damage_data
     AUTORUAPI-5340: leave damage data fo offers from feedprocessor
  *  added logs
  *  refactoring
  *  redemption criteria to bunker
  *  AUTORUAPI-5340: leave damage data fo offers from feedprocessor
  *  debug logs
  *  Realty API. Anon draft transfer to user fixed
  *  added vos2-autoru-cv process feature
  *  local properties
  *  Merge pull request #716 from YandexClassifieds/VOS-2934
     VOS-2934 add more props to change event
  *  Merge pull request #694 from YandexClassifieds/REVIEWS-4691_review_to_yt
     REVIEWS-4691 reviews to yt
  *  VOS-2934 rename prop
  *  VOS-2934 more converters
  *  VOS_2934 add more props to change event
  *  AUTORUAPI-4661 added feedprocessor unique id to convert
  *  REALTYBACK-231: Indexing errors duplicates fix
  *  AUTORUAPI-5304 fixed parsing photos stage: save car images to sales db
  *  rename properties.development.conf -> properties.local.conf
  *  Merge pull request #708 from YandexClassifieds/VOS-2957-limit-images-when-send-to-moderation
     VOS-2957: take first 100 images when send to moderation
  *  return hardcode
  *  delete redundant
  *  Merge remote-tracking branch 'origin/VOS-2970_bunker_blacklist'
  *  delete redundant
  *  Merge remote-tracking branch 'origin/VOS-2777_teleperformance_ds'
  *  teleperformance datasources
  *  Merge pull request #704 from YandexClassifieds/AUTORUAPI-5294
     Update AutoruIdxRequestBuilder.scala
  *  update format
  *  REALTYBACK-232: Send updates to indexer via Kafka (#705)
  *  fill data
  *  added validation error: WrongFrameNumberFormat
  *  delete redundant code
  *  refactoring
  *  added phone to black list
  *  fix checkstyle error
  *  get call center data from bunker
  *  Update ComtransIdxRequestBuilder.scala
  *  Update AutoruIdxRequestBuilder.scala
  *  addef feature
  *  allow custom blured photos from callcenter
  *  autorotate before blur; new test
  *  Merge branch 'master' into REVIEWS-4691_review_to_yt
  *  REALTYBACK-294: Implement consistent slicing in offers DAO. Metering.
  *  Merge pull request #702 from YandexClassifieds/VOS-2941.2
     VOS-2941 Fix: Представляться при отправке sms от Авто.ру
  *  VOS-2941 Fix: Представляться при отправке sms от Авто.ру
  *  REALTYBACK-294: Implement consistent slicing in offers DAO (#700)
     * REALTYBACK-294: Implement consistent slicing in offers DAO
  *  Merge remote-tracking branch 'origin/dealer_udpate_fix'
  *  Fix new ModerationBan in test
  *  VOS-2941 Представляться при отправке sms от Авто.ру
  *  filter events from cabinet which don't change user in vos db
  *  REVIEWS-4691 unfinished
  *  Merge pull request #698 from YandexClassifieds/VOS-2941
     VOS-2941 Представляться при отправке sms от Авто.ру
  *  Merge branch 'master' into REVIEWS-4691_review_to_yt
     # Conflicts:
     #	vos2-reviews-scheduler/CHANGELOG.md
  *  new test case
  *  better sortCoordinates algorithm
  *  better sortCoordinates algorithm
  *  allow empty DiscountPriceStatus
  *  keep remove_blur field
  *  keep custom coordinates after edit
  *  update sortCoordinates algorithm
  *  Merge pull request #697 from YandexClassifieds/AUTORUAPI-5168_ab_test_part1
     AUTORUAPI-5168 random template
  *  VOS-2941 Представляться при отправке sms от Авто.ру
  *  updated sortCoordinates algorithm
  *  allow orig name in /photo-quality
  *  sort coordinates before blur
  *  clean custom coordinates in converter
  *  clear old custom coordinates on new coordinates
  *  AUTORUAPI-5168 random template
  *  Merge remote-tracking branch 'origin/AUTORUAPI-4981_blur_old_offers'
  *  
     VOS-2935 options enrich feature in migration
  *  VOS-2935 options enrichment stage (#696)
     * options enrichment stage
     
     * pr fixes
  *  temporarily hardcode phone black list for redemption
  *  REVIEWS-4691 pom properties
  *  added statuses to mysql workers queue
  *  REVIEWS-4691 fix jar conflicts
  *  Merge branch 'master' into REVIEWS-4691_review_to_yt
  *  REVIEWS-4691 yt export writer
  *  Merge branch 'master' into REVIEWS-4691_review_to_yt

 -- teamcity <teamcity@yandex-team.ru>  Tue, 22 Jan 2019 14:10:57 +0300

## yandex-vos2-autoru-consumers:0.13.0 (Mon, 24 Dec 2018 15:27:43 +0300)

  *  AUTORUSUP-4333: fix feed photo deferred loading
  *  Merge remote-tracking branch 'origin/master'
  *  Merge pull request #688 from YandexClassifieds/AUTORUAPI-4981_blur_old_offers
     AUTORUAPI-4981 blur old offers
  *  merge master
  *  ParsingPhotosUploadStage: refactoring and test fix
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  updated parsingClient: added category to mdsName api
     fixed ParsingPhotosUploadStage: exclude offers with nonExternal photos
  *  AUTORUAPI-5267 upload parsed photos for cars if feature is enabled
  *  Realty. Try to push logs to YT
  *  updated validation error: removed mailto
  *  Merge pull request #684 from YandexClassifieds/VOS-2883
     VOS-2883 prolong infinity offers
  *  Merge pull request #648 from YandexClassifieds/CARFAX-95-bunker
     CARFAX-95: vin resolution push messages from bunker
  *  
     better partition label in moderation consumer metrics
  *  AUTORUAPPS-9084 form -> offer image convert (#682)
     * request annotation option
     
     * pr fixes
     
     * accurate form offer image convert
     
     * pr fix

 -- teamcity <teamcity@yandex-team.ru>  Mon, 24 Dec 2018 15:27:43 +0300

## yandex-vos2-autoru-consumers:0.12.0 (Tue, 18 Dec 2018 18:01:55 +0300)

  *  Merge pull request #683 from YandexClassifieds/feedprocessor_images_bug
     fix
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2

 -- teamcity <teamcity@yandex-team.ru>  Tue, 18 Dec 2018 18:01:55 +0300

## yandex-vos2-autoru-consumers:0.11.1 (Tue, 18 Dec 2018 16:12:42 +0300)

  *  Merge pull request #681 from YandexClassifieds/VOS-2956
     VOS-2956
  *  Merge pull request #679 from YandexClassifieds/VOS-2953_same_offer_draft
     VOS-2953 added sameoffer method for draft api
  *  Merge pull request #680 from YandexClassifieds/CARFAX-113-region-info-offer-form-converter
     CARFAX-113: send region info to kafka diff queue
  *  AUTORUAPPS-9084 request annotation option (#678)
     * request annotation option
     
     * pr fixes
  *  REALTYBACK-349: Renewals for packages (#676)
  *  Merge pull request #675 from YandexClassifieds/AUTO-10696
     AUTO-10696
  *  
     VOS-2947 typo fix
  *  VOS-2947 complectation (#673)
     * complectation validation
     
     * typo fix
     
     * removed some bad tech params from test data
     
     * updated more test for new catalog
     
     * some more fixes
     
     * different offer in notification tests
     
     * only for new cars !!!
  *  VOS-2947 complectation validation (#668)
     * complectation validation
     
     * typo fix
     
     * removed some bad tech params from test data
     
     * updated more test for new catalog
     
     * some more fixes
     
     * different offer in notification tests
  *  Merge pull request #672 from YandexClassifieds/AUTORUAPI-5246_blured_photo_in_index
     AUTORUAPI-5246 blured photo in index
  *  another fix
  *  Merge pull request #667 from YandexClassifieds/VOS-2950_activate_removed_on_push
     VOS-2950 activate removed offer on all_sale_activate push
  *  Merge pull request #665 from YandexClassifieds/AUTORUAPI-5220
     AUTORUAPI-5220 do not add photo with same external url
  *  parse raw meta from mds
  *  Merge pull request #663 from YandexClassifieds/VOS-2950_hashed_include_removed
     VOS-2950 include_removed param in GET /hashed
  *  REALTYBACK-230: New VOS-to-Indexer model (#639)
     * REALTYBACK-230: New VOS-to-Indexer model
  *  Merge pull request #660 from YandexClassifieds/AUTORUSUP-4302
     AUTORUSUP-4302
  *  Merge pull request #661 from YandexClassifieds/VOS-2949_redundant_stages
     VOS-2949 redundant stages

 -- teamcity <teamcity@yandex-team.ru>  Tue, 18 Dec 2018 16:12:42 +0300

## yandex-vos2-autoru-consumers:0.11.0 (Mon, 17 Dec 2018 13:14:01 +0300)

  *  REALTYBACK-349: Renewals for packages (#676)
  *  Merge pull request #675 from YandexClassifieds/AUTO-10696
     AUTO-10696
  *  
     VOS-2947 typo fix
  *  VOS-2947 complectation (#673)
     * complectation validation
     
     * typo fix
     
     * removed some bad tech params from test data
     
     * updated more test for new catalog
     
     * some more fixes
     
     * different offer in notification tests
     
     * only for new cars !!!
  *  VOS-2947 complectation validation (#668)
     * complectation validation
     
     * typo fix
     
     * removed some bad tech params from test data
     
     * updated more test for new catalog
     
     * some more fixes
     
     * different offer in notification tests
  *  Merge pull request #672 from YandexClassifieds/AUTORUAPI-5246_blured_photo_in_index
     AUTORUAPI-5246 blured photo in index
  *  another fix
  *  Merge pull request #667 from YandexClassifieds/VOS-2950_activate_removed_on_push
     VOS-2950 activate removed offer on all_sale_activate push
  *  Merge pull request #665 from YandexClassifieds/AUTORUAPI-5220
     AUTORUAPI-5220 do not add photo with same external url
  *  parse raw meta from mds
  *  Merge pull request #663 from YandexClassifieds/VOS-2950_hashed_include_removed
     VOS-2950 include_removed param in GET /hashed
  *  REALTYBACK-230: New VOS-to-Indexer model (#639)
     * REALTYBACK-230: New VOS-to-Indexer model
  *  Merge pull request #660 from YandexClassifieds/AUTORUSUP-4302
     AUTORUSUP-4302
  *  Merge pull request #661 from YandexClassifieds/VOS-2949_redundant_stages
     VOS-2949 redundant stages

 -- teamcity <teamcity@yandex-team.ru>  Mon, 17 Dec 2018 13:14:01 +0300

## yandex-vos2-autoru-consumers:0.10.1 (Mon, 10 Dec 2018 20:08:37 +0300)

  *  Merge pull request #657 from YandexClassifieds/CARFAX-105
     CARFAX-105: reload vin resolution with legal problems after publicati…
  *  Merge pull request #659 from YandexClassifieds/VOS-2946_delete_vos2_auto_mirror
     VOS-2946 delete code
  *  Merge pull request #658 from YandexClassifieds/VOS-2945_spincar_delete_redudant
     VOS-2945 delete all redundant spincar validation code
  *  Merge pull request #643 from YandexClassifieds/AUTORUAPI-5183_photo_disappear
     AUTORUAPI-5183 fix photo disappears
  *  Merge pull request #654 from YandexClassifieds/VOS-2942_blur_all_photos
     VOS-2942 blur all photos
  *  simplify validation geobase_id change for moderation update
  *  Merge pull request #650 from YandexClassifieds/AUTORUAPI-5158_was_active_field
     AUTORUAPI-5158 set was_active field
  *  fix CompositeStatus in status history
  *  Merge pull request #634 from YandexClassifieds/VOS-2902_disable_region_change
     VOS-2902 forbidden edit geo id
  *  Merge pull request #649 from YandexClassifieds/AUTORUAPI-4738
     AUTORUAPI-4738 add credit tag

 -- teamcity <teamcity@yandex-team.ru>  Mon, 10 Dec 2018 20:08:37 +0300

## yandex-vos2-autoru-consumers:0.10.0 (Mon, 10 Dec 2018 18:42:33 +0300)

  *  Merge pull request #658 from YandexClassifieds/VOS-2945_spincar_delete_redudant
     VOS-2945 delete all redundant spincar validation code
  *  Merge pull request #643 from YandexClassifieds/AUTORUAPI-5183_photo_disappear
     AUTORUAPI-5183 fix photo disappears
  *  Merge pull request #654 from YandexClassifieds/VOS-2942_blur_all_photos
     VOS-2942 blur all photos
  *  simplify validation geobase_id change for moderation update
  *  Merge pull request #650 from YandexClassifieds/AUTORUAPI-5158_was_active_field
     AUTORUAPI-5158 set was_active field
  *  fix CompositeStatus in status history
  *  Merge pull request #634 from YandexClassifieds/VOS-2902_disable_region_change
     VOS-2902 forbidden edit geo id
  *  Merge pull request #649 from YandexClassifieds/AUTORUAPI-4738
     AUTORUAPI-4738 add credit tag

 -- teamcity <teamcity@yandex-team.ru>  Mon, 10 Dec 2018 18:42:33 +0300

## yandex-vos2-autoru-consumers:0.9.0 (Wed, 05 Dec 2018 21:24:11 +0300)

  *  Merge pull request #647 from YandexClassifieds/AUTORUAPI-5167_half_price_check
     Autoruapi 5167 half price check

 -- teamcity <teamcity@yandex-team.ru>  Wed, 05 Dec 2018 21:24:11 +0300

## yandex-vos2-autoru-consumers:0.8.0 (Tue, 04 Dec 2018 18:11:54 +0300)

  *  increase autoru-consumer memory
  *  Merge remote-tracking branch 'origin/master'
  *  data def
  *  added spincar data type
  *  VOS-2932 replace schema-registry submodule with artifact (#642)
  *  status history in opinions consumer (#641)
  *  VOS-2926: fix status code checking
  *  fixed picapica port
  *  VOS-2924 use transmission from verba cars catalog during migration: fixed getTransmission method
  *  Merge pull request #633 from YandexClassifieds/AUTORUAPI-5155-fix-call-history
     AUTORUAPI-5155: the ability to always return telepony info
  *  Merge pull request #632 from YandexClassifieds/VOS-2926_pica_client
     VOS-2926: pica client
  *  REALTYBACK-235: Use experiment flags in renewals (#628)
     * REALTYBACK-235: Use experiment flags in renewals
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  fixed hash check in getOldDao: don't check hash if category is defined
  *  VOS-2924 use transmission from verba cars catalog during migration
  *  merge master, updated schema-registry to use new holocron model; holocron setMileage update
  *  VOS-2890 updated holocron converter: setWheelDrive fix
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  VOS-2915 fixed revisit api: include_removed=true
  *  VOS-2890 updated holocron converter: setPrice fix
  *  mds uploader more errors
  *  VOS-2890 updated holocron converter: fallback for price, configuration_id, steering_wheel conversions
  *  Merge remote-tracking branch 'origin/master'
  *  Merge remote-tracking branch 'origin/VOS-2904_spincar_batch_validation'
  *  telephony fix monitoring
  *  Merge remote-tracking branch 'origin/master'
  *  fix logs
  *  error logs for teleperformance
  *  increase allow errors fro teleperformance
  *  fix teleperformance proxy
  *  Merge remote-tracking branch 'origin/VOS-2863_monitored_http_client'
  *  fix eds addresses
  *  Merge pull request #606 from YandexClassifieds/VOS-2882_search_by_vin
     VOS-2882 search by vin
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2

 -- teamcity <teamcity@yandex-team.ru>  Tue, 04 Dec 2018 18:11:54 +0300

## yandex-vos2-autoru-consumers:0.7.0 (Fri, 09 Nov 2018 19:49:35 +0300)

  *  fix photo preview converting (form -> offer)
     added test
  *  VOS-2895 fix time intervals
  *  VOS-2895 teleperformance time intervals
  *  Merge remote-tracking branch 'origin/master'
  *  handle teleperformance 400 bad request
  *  monitored fix for blur client
  *  Merge remote-tracking branch 'origin/VOS-2816_photo_preview_worker'
  *  Merge remote-tracking branch 'origin/VOS-2816_teleperformance_worker'
  *  AUTORUAPI-5039 updated setArchive
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  AUTORUAPI-5039 updated deletion method: feedprocessor can restore deleted offer for seven days if it was created by feedprocessor or its a dealers section=new offer
  *  resolve
  *  Merge remote-tracking branch 'origin/master' into ap-master
     # Conflicts:
     #	pom.xml
     #	vos2-autoparts-scheduler/src/main/scala/ru/yandex/vos2/autoparts/watching/subscriptions/letters/AutopartsEmailNotificationRenderer.scala
     #	vos2-autoru-scheduler/src/main/scala/ru/yandex/vos2/autoru/config/DefaultAutoruSchedulerComponents.scala
     #	vos2-core/src/main/scala/ru/yandex/vos2/services/sender/HttpSenderClient.scala
     #	vos2-scheduler-core/src/main/scala/ru/yandex/vos2/watching/subscriptions/NotificationEngine.scala
  *  VOS-2707 some fixes for low funds notification processing (#594)
     * VOS-2707
     
     * VOS-2707
     
     * VOS-2707 fix scheduling
     
     * VOS-2707 fix scheduling and deploy vos-ap
     
     * VOS-2707 add some logs
     
     * VOS-2707 fix
  *  VOS-2707 low funds. fix some issues (#585)
     * VOS-2707 low funds. fix some issues
     
     * VOS-2707 low funds. fix some issues
  *  VOS-2707 reduce silence interval for low funds notifications
  *  VOS-2838: fix a case for two users with same cabinet client ids
  *  Vos 2707 funds ends emails (#523)
     * VOS-2707 funds ends emails
     
     * VOS-2707 funds ends emails spec
     
     * VOS-2707 low funds pr fixes
     
     * VOS-2707 fix
     
     * VOS-2707 fix
     
     * VOS-2707 WIP waiting for spray protobuf support in scala-common
     
     * VOS-2707 fix
     
     * VOS-2707 fix
     
     * VOS-2707 up scala_common, schema-registry

 -- teamcity <teamcity@yandex-team.ru>  Fri, 09 Nov 2018 19:49:35 +0300

## yandex-vos2-autoru-consumers:0.6.0 (Fri, 02 Nov 2018 16:32:51 +0300)

  *  fix sql
  *  Merge remote-tracking branch 'origin/master' into VOS-2798_additional_data_loader
  *  fix tests [2]
  *  fix tests
  *  vos user in additional data
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  VOS-2885 use TimestampCheck as car.updated instead of TimestampAnyUpdate
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2

 -- teamcity <teamcity@yandex-team.ru>  Fri, 02 Nov 2018 16:32:51 +0300

## yandex-vos2-autoru-consumers:0.5.0 (Wed, 31 Oct 2018 17:06:48 +0300)

  *  Merge remote-tracking branch 'origin/master'
  *  user UserModerationStatusChange insetead of UserBanned/UserUnbanned in passport consumer
  *  dealers sync stage
  *  save autoru dealer status in offers
  *  Merge pull request #608 from YandexClassifieds/AUTORUAPI-4945_fyuse_panorama
     AUTORUAPI-4945 up auto micro core

 -- teamcity <teamcity@yandex-team.ru>  Wed, 31 Oct 2018 17:06:48 +0300

## yandex-vos2-autoru-consumers:0.4.1 (Tue, 30 Oct 2018 15:10:25 +0300)

  *  
     fixed my dumbest error so far
  *  Merge remote-tracking branch 'origin/AUTORUAPI-4913_cabinet_consumer'
  *  sync suspension chassis proto models
  *  Merge pull request #604 from YandexClassifieds/VOS-2828
     VOS-2828 fixes

 -- teamcity <teamcity@yandex-team.ru>  Tue, 30 Oct 2018 15:10:25 +0300

## yandex-vos2-autoru-consumers:0.4.0 (Tue, 30 Oct 2018 14:39:49 +0300)

  *  Merge remote-tracking branch 'origin/AUTORUAPI-4913_cabinet_consumer'
  *  sync suspension chassis proto models
  *  Merge pull request #604 from YandexClassifieds/VOS-2828
     VOS-2828 fixes

 -- teamcity <teamcity@yandex-team.ru>  Tue, 30 Oct 2018 14:39:49 +0300

## yandex-vos2-autoru-consumers:0.3.0 (Mon, 29 Oct 2018 18:45:42 +0300)

  *  VOS-2251 do not ignore batch update errors and single offer update errors(stable) (#603)
     * do not ignore batch update errors and single offer update errors(stable)
     
     * compute last update time right before moderation request
     
     * better flow control
  *  added test for color
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  fixed color set for holocron
  *  updated holocron converter for new holocron schema
  *  AUTORUAPI-4971 extracted offer precomputed status function (#600)
     * extracted offer precomputed status function
     
     * better looking
     
     * even better looking

 -- teamcity <teamcity@yandex-team.ru>  Mon, 29 Oct 2018 18:45:42 +0300

## yandex-vos2-autoru-consumers:0.2.1 (Fri, 26 Oct 2018 15:46:39 +0300)

  *  don't restore deleted hand uploaded photos
  *  Merge pull request #595 from YandexClassifieds/VOS-2872-ext-parking-type
     VOS-2872 add new values 'OPEN' and 'CLOSED' to ParkingType
  *  VOS-2878: Reduce SMS aggregation type to 30 minutes
  *  Merge pull request #591 from YandexClassifieds/VSINFR-3443_holo_validation
     Added proto validation
  *  Merge remote-tracking branch 'origin/AUTORUAPI-4913_cabinet_consumer'
  *  fix convert not found flag
  *  Merge remote-tracking branch 'origin/master'
  *  fix request
  *  better log
  *  Merge remote-tracking branch 'origin/master'
  *  mds meta check stage
  *  WRONG_VIN editable again
  *  Merge pull request #586 from YandexClassifieds/VOS-2866
     VOS-2866 set attributes for yt table
  *  Merge remote-tracking branch 'origin/telepony_handle_449'
  *  Merge pull request #584 from YandexClassifieds/VOS-2864
     VOS-2864 logs
  *  Merge pull request #571 from YandexClassifieds/AUTORUAPI-4898_allow_one_vin_update
     AUTORUAPI-4898 allow 1 VIN edit

 -- teamcity <teamcity@yandex-team.ru>  Fri, 26 Oct 2018 15:46:39 +0300

## yandex-vos2-autoru-consumers:0.2.0 (Wed, 24 Oct 2018 16:08:21 +0300)

  *  Merge remote-tracking branch 'origin/AUTORUAPI-4913_cabinet_consumer'
  *  fix convert not found flag
  *  Merge remote-tracking branch 'origin/master'
  *  fix request
  *  better log
  *  Merge remote-tracking branch 'origin/master'
  *  mds meta check stage
  *  WRONG_VIN editable again
  *  Merge pull request #586 from YandexClassifieds/VOS-2866
     VOS-2866 set attributes for yt table
  *  Merge remote-tracking branch 'origin/telepony_handle_449'
  *  Merge pull request #584 from YandexClassifieds/VOS-2864
     VOS-2864 logs
  *  Merge pull request #571 from YandexClassifieds/AUTORUAPI-4898_allow_one_vin_update
     AUTORUAPI-4898 allow 1 VIN edit

 -- teamcity <teamcity@yandex-team.ru>  Wed, 24 Oct 2018 16:08:21 +0300

## yandex-vos2-autoru-consumers:0.1.1 (Wed, 17 Oct 2018 14:38:11 +0300)

  *  VOS-2251 filter autoru opinions by context (#581)
     * filter autoru opinions by context
     
     * moved custom filter to custom consumer
  *  AUTORUAPI-4948 skip notexist.pts and notexist.owners validation for scooters
  *  Merge remote-tracking branch 'origin/VOS-2860_not_found_in_mds'
  *  separate thread pool for parallel collections in license plate blur worker
  *  Merge pull request #583 from YandexClassifieds/VOS-2861
     VOS-2861 check size line of YSON
  *  Realty. Some legacy code removed
  *  Merge pull request #552 from YandexClassifieds/AUTORUOFFICE-5087
     AUTORUOFFICE-5087 # Sync offer expire_date with placement service
  *  Merge pull request #580 from YandexClassifieds/VOS-2828
     VOS-2828 remove draft events
  *  Merge pull request #572 from YandexClassifieds/AUTORUAPI-4783_preserver_smart_order
     AUTORUAPI-4783: preserve smart order after feedprocessing update
  *  added nomad_alloc_id and timestamp to heap dump file name
  *  change add goods api try(unit) -> try(boolean)
  *  Merge remote-tracking branch 'origin/fix_salesman_client'
  *  Merge pull request #579 from YandexClassifieds/fix_salesman_client
     fix salesman client
  *  Merge pull request #578 from YandexClassifieds/VOS-2828
     VOS-2828
  *  Merge pull request #577 from YandexClassifieds/CARFAX-61
     CARFAX-61 change url
  *  Merge pull request #575 from YandexClassifieds/VOS-2828
     VOS-2828
  *  commercial activation fixes (#576)
  *  AUTORUAPI-4882 can I activate my offer check (#574)
     * can i publish my draft check
     
     * Revert "can i publish my draft check"
     
     This reverts commit 2cfdf26a3e313ec0771b6fb935c676ce67a4d88b.
     
     * activation status request
     
     * fixes and test
  *  Merge remote-tracking branch 'origin/master'
  *  Merge remote-tracking branch 'origin/master'
  *  Merge remote-tracking branch 'origin/VOS-2816_blur_photo_separate_thread'
  *  updated kafka settings for holocron and disabled waiting records tobe sent
  *  VOS-2824: Renewals SMS changed (#551)
  *  Merge pull request #565 from YandexClassifieds/VOS-2828
     VOS-2828 save user actions for offer
  *  forbid vin change
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  Merge branch 'realty-master'
  *  AUTORUAPI-4900 order (#563)
     * apply new order on update
     
     * typo fix
  *  Fix DuplicateKeys on subscription update/create
  *  Merge branch 'subscriptions_duplicate_keys_fix'
  *  Merge branch 'realty-master'
  *  fix
  *  move data path to env variable
  *  Merge remote-tracking branch 'origin/master'
  *  move data path to datasources
  *  fix tests
  *  Merge remote-tracking branch 'origin/master'
  *  eds to ephemeral disk
  *  VOS-2831 save big queue files to ephemeral disk
  *  Merge remote-tracking branch 'origin/master'
  *  change preCommitHook
     better metrics
  *  Merge remote-tracking branch 'origin/VOS-2798_passport_consumer'
  *  Merge remote-tracking branch 'origin/master'
  *  retrun proxy to teleperformance
  *  fix to status method
  *  Merge remote-tracking branch 'origin/teleperformance_refactoring'
  *  Merge remote-tracking branch 'origin/VOS-2798_passport_consumer'
  *  AUTORUAPI-4784 schema update

 -- teamcity <teamcity@yandex-team.ru>  Wed, 17 Oct 2018 14:38:11 +0300

## yandex-vos2-autoru-consumers:0.1.0 (Tue, 16 Oct 2018 18:03:50 +0300)

  *  AUTORUAPI-4948 skip notexist.pts and notexist.owners validation for scooters
  *  Merge remote-tracking branch 'origin/VOS-2860_not_found_in_mds'
  *  separate thread pool for parallel collections in license plate blur worker
  *  Merge pull request #583 from YandexClassifieds/VOS-2861
     VOS-2861 check size line of YSON
  *  Realty. Some legacy code removed
  *  Merge pull request #552 from YandexClassifieds/AUTORUOFFICE-5087
     AUTORUOFFICE-5087 # Sync offer expire_date with placement service
  *  Merge pull request #580 from YandexClassifieds/VOS-2828
     VOS-2828 remove draft events
  *  Merge pull request #572 from YandexClassifieds/AUTORUAPI-4783_preserver_smart_order
     AUTORUAPI-4783: preserve smart order after feedprocessing update
  *  added nomad_alloc_id and timestamp to heap dump file name
  *  change add goods api try(unit) -> try(boolean)
  *  Merge remote-tracking branch 'origin/fix_salesman_client'
  *  Merge pull request #579 from YandexClassifieds/fix_salesman_client
     fix salesman client
  *  Merge pull request #578 from YandexClassifieds/VOS-2828
     VOS-2828
  *  Merge pull request #577 from YandexClassifieds/CARFAX-61
     CARFAX-61 change url
  *  Merge pull request #575 from YandexClassifieds/VOS-2828
     VOS-2828
  *  commercial activation fixes (#576)
  *  AUTORUAPI-4882 can I activate my offer check (#574)
     * can i publish my draft check
     
     * Revert "can i publish my draft check"
     
     This reverts commit 2cfdf26a3e313ec0771b6fb935c676ce67a4d88b.
     
     * activation status request
     
     * fixes and test
  *  Merge remote-tracking branch 'origin/master'
  *  Merge remote-tracking branch 'origin/master'
  *  Merge remote-tracking branch 'origin/VOS-2816_blur_photo_separate_thread'
  *  updated kafka settings for holocron and disabled waiting records tobe sent
  *  VOS-2824: Renewals SMS changed (#551)
  *  Merge pull request #565 from YandexClassifieds/VOS-2828
     VOS-2828 save user actions for offer
  *  forbid vin change
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  Merge branch 'realty-master'
  *  AUTORUAPI-4900 order (#563)
     * apply new order on update
     
     * typo fix
  *  Fix DuplicateKeys on subscription update/create
  *  Merge branch 'subscriptions_duplicate_keys_fix'
  *  Merge branch 'realty-master'
  *  fix
  *  move data path to env variable
  *  Merge remote-tracking branch 'origin/master'
  *  move data path to datasources
  *  fix tests
  *  Merge remote-tracking branch 'origin/master'
  *  eds to ephemeral disk
  *  VOS-2831 save big queue files to ephemeral disk
  *  Merge remote-tracking branch 'origin/master'
  *  change preCommitHook
     better metrics
  *  Merge remote-tracking branch 'origin/VOS-2798_passport_consumer'
  *  Merge remote-tracking branch 'origin/master'
  *  retrun proxy to teleperformance
  *  fix to status method
  *  Merge remote-tracking branch 'origin/teleperformance_refactoring'
  *  Merge remote-tracking branch 'origin/VOS-2798_passport_consumer'
  *  AUTORUAPI-4784 schema update

 -- teamcity <teamcity@yandex-team.ru>  Tue, 16 Oct 2018 18:03:50 +0300

## yandex-vos2-autoru-consumers:0.0.54 (Wed, 03 Oct 2018 22:04:42 +0300)

  *  VOS-2831 save big queue files to ephemeral disk

 -- teamcity <teamcity@yandex-team.ru>  Wed, 03 Oct 2018 22:04:42 +0300

## yandex-vos2-autoru-consumers:0.0.53 (Wed, 03 Oct 2018 19:56:56 +0300)

  *  Merge remote-tracking branch 'origin/master'
  *  change preCommitHook
     better metrics

 -- teamcity <teamcity@yandex-team.ru>  Wed, 03 Oct 2018 19:56:56 +0300

## yandex-vos2-autoru-consumers:0.0.52 (Wed, 03 Oct 2018 18:42:16 +0300)

  *  Merge remote-tracking branch 'origin/VOS-2798_passport_consumer'
  *  Merge remote-tracking branch 'origin/master'

 -- teamcity <teamcity@yandex-team.ru>  Wed, 03 Oct 2018 18:42:16 +0300

## yandex-vos2-autoru-consumers:0.0.51 (Wed, 03 Oct 2018 14:51:01 +0300)

  *  VOS-2817  better consumers logging (#559)
     * better consumers logging
     
     * removed typo
  *  retrun proxy to teleperformance
  *  fix to status method
  *  Merge remote-tracking branch 'origin/teleperformance_refactoring'
  *  Merge remote-tracking branch 'origin/VOS-2798_passport_consumer'
  *  AUTORUAPI-4784 schema update

 -- teamcity <teamcity@yandex-team.ru>  Wed, 03 Oct 2018 14:51:01 +0300

## yandex-vos2-autoru-consumers:0.0.50 (Mon, 01 Oct 2018 17:02:24 +0300)

  *  AUTORUAPI-4869: allow removing of offers outside feed for non-CAR categories
  *  added additional metrics to teleperformance client
  *  AUTORUAPI-4784 schema update
  *  delete redundant gauge
  *  Merge remote-tracking branch 'origin/master'
  *  don't send drafts to kafka (diff topic)

 -- teamcity <teamcity@yandex-team.ru>  Mon, 01 Oct 2018 17:02:24 +0300

## yandex-vos2-autoru-consumers:0.0.49 (Fri, 28 Sep 2018 12:25:45 +0300)

  *  send photo_preview to shard
  *  change prometheus prefix for vos2-autoru-consumers

 -- teamcity <teamcity@yandex-team.ru>  Fri, 28 Sep 2018 12:25:45 +0300

## yandex-vos2-autoru-consumers:0.0.48 (Fri, 28 Sep 2018 10:48:42 +0300)

  *  Merge remote-tracking branch 'origin/VOS-2809_teleperformans_additional'
  *  Merge remote-tracking branch 'origin/VOS-2809_teleperformans_additional'
  *  Merge pull request #550 from YandexClassifieds/VOS-2827
     VOS-2827 Вынести scheme для рассылятора в data sources
  *  Merge remote-tracking branch 'origin/master'
  *  upgrade debug logs
  *  added 0.9 quantile to next processing delay metric
  *  fix debug logs
  *  Merge remote-tracking branch 'origin/master'
  *  added debug logs
  *  added debug metrics for watching
  *  added debug log
  *  Merge remote-tracking branch 'origin/master'
  *  user histogram instead of summary for batch process metrics
  *  comment debug logs
  *  Merge pull request #547 from YandexClassifieds/AUTORUAPI-4633
     AUTORUAPI-4633 added new mark for vin decoder
  *  VOS-2251 batch process opinions + include removed offers for process (#546)
     * batch process opinions + include removed offers for process
     
     * tests fix
  *  Merge remote-tracking branch 'origin/master'
  *  added parametr noout=1 for recognize number request
  *  Merge remote-tracking branch 'origin/VOS-2816_scheduler_throughput'

 -- teamcity <teamcity@yandex-team.ru>  Fri, 28 Sep 2018 10:48:42 +0300

## yandex-vos2-autoru-consumers:0.0.47 (Thu, 20 Sep 2018 00:08:39 +0300)

  *  added debug logs for feedprocessor consumer
  *  Merge pull request #545 from YandexClassifieds/VOS-2805
     VOS-2805 ipv4 proxy
  *  better metrics
  *  VSINFR-3434 set RawJson, update previousState only if sent, exclude changeVersion from hash calculation
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  VSINFR-3434 updated holocron converter and test
  *  Merge pull request #542 from YandexClassifieds/VSINFR-3434_holocron-auto-cars
     VSINFR-3434 holocron auto cars
  *  added more buckets for timing metrics
  *  delete redundant quantile
  *  added debug logs
  *  fix moderation update email
  *  Merge branch 'ap-master'
  *  delete debug logs and experiment with jvm options
  *  Added debug logs for information about high timing in vos-autoru-api
  *  fix max phone test
  *  fix compilation
  *  fix parse moderation ban reasons json (push title) and delete test feature
  *  AUTORUAPI-4769 fix replace {mark} and {model} for moderation ban push
  *  Merge remote-tracking branch 'origin/master'
  *  AUTORUAPI-4769 fix push text
  *  added push notification to moderation ban
  *  REALTY-16714: email with stats (#505)
     * VOS-2764: JDBC metrics. Prometeus metrics refactored
     
     * VOS-2764: Env properties fix
     
     * VOS-2764: MySQL URLs from environment variables
     
     * email with stats
     
     * email with stats
     
     * refactor
     
     * refactor
     
     * user selection for stat emails
     
     * fix schema registry
     
     * fixes
     
     * fixes
     
     * fix build
     
     * spammer support
     
     * add spammer support
     
     * remove unused code
     
     * add https scheme on port 443
     
     * update schema-registry
     
     * fix scheduling
     
     * fix scheduling
     
     * fix scheduling
     
     * add correct spammer path
     
     * deploy scheduler
     
     * fix import
     
     * deploy
     
     * fix day of week
     
     * fixes for pr
     
     * fixes for pr
     
     * fixes for pr
     
     * fixes for pr
     
     * refactor
     
     * fix metric name
  *  Merge pull request #517 from YandexClassifieds/VOS-2729
     Vos 2729 Offers to YT
  *  Merge pull request #531 from YandexClassifieds/VOS-2802
     VOS-2802 Починить OfferConverterTest
  *  added client ac_7806 favorite motors for spincar validation
  *  Merge remote-tracking branch 'origin/master'

 -- teamcity <teamcity@yandex-team.ru>  Thu, 20 Sep 2018 00:08:39 +0300

## yandex-vos2-autoru-consumers:0.0.46 (Tue, 04 Sep 2018 19:54:48 +0300)

  *  Merge remote-tracking branch 'origin/VOS-2789_prometheus_metrics'

 -- teamcity <teamcity@yandex-team.ru>  Tue, 04 Sep 2018 19:54:48 +0300

## yandex-vos2-autoru-consumers:0.0.45 (Tue, 04 Sep 2018 16:42:35 +0300)

  *  replace vos2-autoru-feedprocessor -> vos2-autoru-consumers

 -- teamcity <teamcity@yandex-team.ru>  Tue, 04 Sep 2018 16:42:35 +0300

## yandex-vos2-autoru-consumers:0.0.44 (Tue, 04 Sep 2018 16:02:52 +0300)

  *  return back old monitored values for blur client
  *  delete redundant logs

 -- teamcity <teamcity@yandex-team.ru>  Tue, 04 Sep 2018 16:02:52 +0300

## yandex-vos2-autoru-consumers:0.0.43 (Mon, 03 Sep 2018 16:34:22 +0300)

  *  rename docker image

 -- teamcity <teamcity@yandex-team.ru>  Mon, 03 Sep 2018 16:34:22 +0300

## yandex-vos2-autoru-feedprocessor:0.0.43 (Mon, 03 Sep 2018 16:34:22 +0300)

  *  skip OfferNotFoundException for opinions processing (#516)

 -- teamcity <teamcity@yandex-team.ru>  Mon, 03 Sep 2018 16:34:22 +0300

## yandex-vos2-autoru-feedprocessor:0.0.42 (Mon, 03 Sep 2018 13:55:49 +0300)

  *  Merge remote-tracking branch 'origin/master'
  *  fix init error

 -- teamcity <teamcity@yandex-team.ru>  Mon, 03 Sep 2018 13:55:49 +0300

## yandex-vos2-autoru-feedprocessor:0.0.41 (Mon, 03 Sep 2018 13:36:32 +0300)

  *  fix component name [2]
  *  Merge remote-tracking branch 'origin/master'
  *  revert

 -- teamcity <teamcity@yandex-team.ru>  Mon, 03 Sep 2018 13:36:32 +0300

## yandex-vos2-autoru-feedprocessor:0.0.40 (Mon, 03 Sep 2018 12:52:39 +0300)

  *  Merge remote-tracking branch 'origin/master'
  *  fix component name
  *  delete validation error ForbiddenChangeLicensePlate for moderation update
  *  Merge remote-tracking branch 'origin/master'
  *  added upt-get update
  *  Added logs for archive from moderation opinion stage
  *  Merge remote-tracking branch 'origin/VOS-2765_new_moderation_reasons'
     # Conflicts:
     #	vos2-autoru-scheduler/CHANGELOG.md
  *  added imagemagick to scheduler dockerfile
  *  added logging blur exception to master
  *  update schema registry
  *  Merge remote-tracking branch 'origin/VOS-2785_edit_license_plate'
  *  release 0.0.23
  *  Merge pull request #509 from YandexClassifieds/VOS-2690-2
     VOS-2690 Переехать в яндексовый s3 из амазона
  *  Merge pull request #513 from YandexClassifieds/VOS-2787
     VOS-2787 Выпилить фид gm-export.xml.gz
  *  release 0.31.3
  *  release 0.0.22
  *  added metrics to amazon s3 client
  *  release 0.0.21
  *  Merge pull request #512 from YandexClassifieds/VOS-2740-7
     VOS-2786 Починить маркер low_price в фиде критео
  *  release 0.0.20
  *  Merge pull request #510 from YandexClassifieds/VOS-2740-5
     VOS-2740 Fix: Добавить в фид Критео новые колонки
  *  release 0.0.19
  *  Merge remote-tracking branch 'origin/master'
  *  added ipv4 proxy to amazon s3 client
  *  Merge remote-tracking branch 'origin/prometheus_alert'
  *   VOS-2783: Ablity to get all drafts for anon user
  *  Merge branch 'VOS-2783_anon_draft_search'
  *  Realty. Changed DB
  *  Realty consumer. Added some fatal SQL exceptions
  *  release 0.0.17
  *  logging ipv6 support
  *  REALTY-16758: SQL issue fix
  *  release 0.0.16
  *  Merge pull request #500 from YandexClassifieds/VOS-2615-2
     VOS-2615 [autoru] Добавляем статус "удаленности" к картинке в объявление
  *  VOS-2770: Do not store drafts in mirror fix
  *  realty-api changelogs
  *  Merge branch 'VOS-2782_not_execute_renewal_on_inactive_offer'
  *  release 0.0.15
  *  added debug logs to scheduler
  *  release 0.0.14
  *  Merge pull request #508 from YandexClassifieds/VOS-2773
     VOS-2773 DeleteDraftStage: обрабатывать вариант с некорректным именем…
  *  release 0.0.13
  *  release 0.53.9
  *  Merge pull request #506 from YandexClassifieds/VOS-2740
     VOS-2740 Добавить в фид Критео новые колонки
  *  delete redundant logs
  *  added changelog
  *  fix debug logs
  *  Merge remote-tracking branch 'origin/master'
  *  added debug logs
  *  Merge remote-tracking branch 'origin/VOS-2774_offer_low_rating_broken_push'
  *  VOS-2770: Do not store drafts in mirror
  *  VOS-2764: From master
  *  VOS-2764 Realty to Docker (#498)
  *  release 0.0.11
  *  Merge remote-tracking branch 'origin/master'
  *  hardcode login and password for teleperformance
  *  Merge remote-tracking branch 'origin/master'
  *  return old teleperformance user/password
  *  delete overriden to status from common remote client
  *  Merge remote-tracking branch 'origin/master'
  *  fix common remote client and teleperformance datasources
  *  fix tests
  *  Merge remote-tracking branch 'origin/master'
  *  get teleperformance data from datasources
  *  Merge remote-tracking branch 'origin/master'
  *  fix prometheus metrics in CommonRemoteClient
  *  override toStatus method for promerheus metrics in CommonRemoteClient
  *  release 0.0.5
  *  fix typo in push offer low rating
  *  added proxy for teleperformance http client
  *  release 0.53.8
  *  release 0.0.4
  *  Merge remote-tracking branch 'origin/master'
  *  Added MonrunExport
  *  fix vos2-autoru-api pom
  *  Merge remote-tracking branch 'origin/master'
  *  changelog
  *  Merge remote-tracking branch 'origin/VOS-2591_docker_autoru_vos'
  *  Merge branch 'REALTY-16721_drafts_user_ip'
  *  Merge pull request #502 from YandexClassifieds/ap-webhooks
     ap-webhooks
  *  changelog without typo
  *  release 0.0.74
  *  update scala-common from 0.0.108 to 0.0.131
  *  AUTORUAPI-4654: check authorized dealers
  *  deactivate brand certificatas updated more than 3 days ago
  *  release 0.53.4
  *  fix offer updating in async stage
  *  fix json parsing
  *  print error
  *  release 0.31.2
  *  Merge pull request #499 from YandexClassifieds/VOS-2766_mod_update_notify_fix
     VOS-2766 moderation update notify fix
  *  release 0.0.73
  *  release 0.0.72
  *  release 0.31.1
  *  Added .hubfile.yml
  *  release 0.53.3
  *  release 0.31.0
  *  Merge pull request #493 from YandexClassifieds/AUTORUAPI-4654_certification
     AUTORUAPI-4654: brand certification update stage
  *  release 0.30.1
  *  Merge pull request #497 from YandexClassifieds/AUTORUAPI-4698_forbid_mileage_decrease
     AUTORUAPI-4698 forbid to decrease mileage for private users for car offers
  *  release 0.0.71
  *  release 0.0.70
  *  release 0.0.69
  *  release 0.0.68
  *  release 0.0.67
  *  release 0.0.66
  *  release 0.0.65
  *  release 0.53.2
  *  release 0.0.64
  *  Merge pull request #496 from YandexClassifieds/remove_old_unused_diff_gen
     CLEANUP remove unused code
  *  release 0.0.63
  *  release 0.0.62
  *  release 0.0.61
  *  release 0.0.60
  *  release 0.0.59
  *  release 0.0.58
  *  release 0.0.57
  *  release 0.0.56
  *  release 0.0.55
  *  release 0.0.54
  *  release 0.0.53
  *  release 0.0.52
  *  release 0.0.51
  *  release 0.0.50
  *  release 0.0.49
  *  release 0.0.48
  *  release 0.0.47
  *  release 0.0.46
  *  release 0.0.45
  *  release 0.0.44
  *  release 0.0.43
  *  release 0.0.42
  *  release 0.0.41
  *  release 0.0.40
  *  release 0.0.39
  *  release 0.0.38
  *  release 0.0.37
  *  release 0.0.36
  *  release 0.0.35
  *  release 0.0.34
  *  release 0.0.33
  *  release 0.0.32
  *  release 0.0.31
  *  release 0.0.30
  *  release 0.0.29
  *  release 0.0.28
  *  release 0.0.27
  *  release 0.0.26
  *  release 0.0.25
  *  release 0.0.24
  *  release 0.0.23
  *  release 0.0.22
  *  release 0.0.21
  *  release 0.0.20
  *  release 0.0.19
  *  release 0.0.18
  *  release 0.0.17
  *  release 0.0.16
  *  release 0.0.15
  *  release 0.0.14
  *  release 0.0.13
  *  release 0.0.12
  *  release 0.0.11
  *  release 0.0.10
  *  release 0.0.9
  *  release 0.53.1
  *  release 0.0.8
  *  Merge remote-tracking branch 'origin/VOS-2591_autoru_api_docker'
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  VOS-2767: Get rid of HOUSE_WITH_LOT
  *  Merge remote-tracking branch 'origin/master'
  *  REVIEWS changelog
  *  Merge remote-tracking branch 'origin/master'
  *  changelog
  *  simplify validation warranty expire for moderation update
  *  changelog [sync with master]
  *  changelog [delete debug code]
  *  delete debug code
  *  changelog [2]
  *  changelog
  *  setSanitize false
  *  hardcode cetelem and octopus host for test [changelog]
  *  hardcode cetelem and octopus host for test
  *  print all configs readed from consul
  *  added debug logs [2]
  *  added debug logs
  *  changelog from branch
  *  changelog from branch
  *  changelog
  *  release 0.53.0
  *  take datasources from consul
  *  changelog
  *  fix schema registry
  *  Merge remote-tracking branch 'origin/master'
  *  fix ops port
  *  change max thread pool values
  *  added separately thread pool for OfferStatusesActor
  *  fix test
  *  AUTORUAPI-4662 commercial activation stage (#491)
     * commercial activation stage
     
     * commercial activation to async stage
  *  release 0.52.10
  *  better
  *  remove cyrillicName usage
  *  normal mark_model names for OfferCreation event
  *  
     VOS-2714 Editor migration
  *  VOS-2761: New storage schema fix
     VOS-2762: Apartments for rooms
     VOS-2763: Shower and toilet
  *  release 0.52.9
  *  release 0.28.5
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  VOS-2755 fixed set ban by inheritance in stage
  *  VOS-2755 set ban by inheritance from current offer during migration: added test
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  VOS-2755 set ban by inheritance from current offer during migration
  *  VOS-2755 added again inheritance check
  *  release 0.52.5
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  VOS-2755 removed inheritance check, updated OpinionWriter to send notification on unban too
  *  Merge pull request #486 from YandexClassifieds/VOS-2755_send_notifications_to_techsupport
     VOS-2755 send notifications to techsupport
  *  Merge pull request #485 from YandexClassifieds/VOS-2737-fix_proto
     VOS-2737 add parent regions to moderation
  *  Merge pull request #489 from YandexClassifieds/VSMODERATION-2340
     VSMODERATION-2340 fixed ModerationUserConverte
  *  Merge pull request #488 from YandexClassifieds/REVIEWS-4661_new_comment_notify
     REVIEWS-4661 new comment notify
  *  release 0.28.3
  *  Merge remote-tracking branch 'origin/VOS-2591_autoru_api_docker'
  *  
     typo fix
  *  
     fixed scheduler compilation
  *  fix tests
  *  release 0.28.2
  *  fix dev conf for shard
  *  fix operational init
  *  VOS-2251 last moderation update timestamp usage (#482)
     * moderation opinion consumer
     
     * pr fixes + some metrics
     
     * different features for push and poll moderation
     
     * last moderation update timestamp usage
     
     * fixed log message for skipped offers
  *  release 0.28.1
  *  Merge pull request #483 from YandexClassifieds/VOS-2737-fix_proto
     fix test
  *  release 0.52.3
  *  pom
  *  changelog
  *  release 0.52.2
  *  Merge remote-tracking branch 'origin/master'
  *  fix OfferModerationTest
  *  Merge remote-tracking branch 'origin/VOS-2591_autoru_api_docker'
  *  changelog
  *  Merge pull request #481 from YandexClassifieds/VOS-2737-fix_proto
     VOS-2737 remove duplicate moderation-proto generation
  *  VOS-2757: Filter by address. Address unification
  *  Merge pull request #474 from YandexClassifieds/VERTISTRAF-53
     VERTISTRAF-53 Sitemap for mobile urls
  *  VOS-2757: Filter by address fixed
  *  release 0.52.1
  *  Merge remote-tracking branch 'origin/VOS-2591_autoru_api_docker'
  *  release 0.52.0
  *  Merge branch 'VOS-2591_autoru_api_docker'
  *  Merge pull request #480 from YandexClassifieds/REVIEWS-4658_write_addition
     REVIEWS-4658 write addition
  *  Merge remote-tracking branch 'origin/VOS-2591_autoru_api_docker'
  *  VOS-2757: Filter by address
  *  release 0.51.1
  *  VERTISADMIN-19825: account time window right corner
  *  Merge pull request #468 from YandexClassifieds/AUTORUAPI-4503
     AUTORUAPI-4503: Поддержать wizard в offer
  *  release 0.51.0
  *  VERTISADMIN-19825: don't process too fresh offers
  *  VOS-2743: Get rid of StartRaisingWithoutPromotionStage: everything is activated
  *  release 0.50.9
  *  Merge remote-tracking branch 'origin/master'
  *  fix metric name
  *  Merge pull request #479 from YandexClassifieds/VOS-2752_fix_repeat_notifications
     VOS-2752 remove bad requirement
  *  Merge remote-tracking branch 'origin/VOS-2591_autoru_api_docker'
  *  Merge pull request #478 from YandexClassifieds/VOS-2752_fix_repeat_notifications
     VOS-2752 send offer creation immediately
  *  Merge remote-tracking branch 'origin/VOS-2591_autoru_api_docker'
  *  release 0.50.7
  *  Merge remote-tracking branch 'origin/VOS-2591_autoru_api_docker'
  *  release 0.50.6
  *  Merge pull request #477 from YandexClassifieds/VOS-2752_fix_repeat_notifications
     VOS-2752 compare threads instead of names
  *  release 0.50.5
  *  Merge pull request #475 from YandexClassifieds/VOS-2752_fix_repeat_notifications
     VOS-2752 update pending notifications
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  Merge branch 'realty-master'
  *  Merge branch 'realty-master'
  *  fix TelephonyClient tests
  *  Merge remote-tracking branch 'origin/master'
  *  common remote client metrics
  *  fix watching queue size metrics
  *  release 0.50.2
  *  updated async state logging
     (cherry picked from commit 04fbb7e)
  *  Merge remote-tracking branch 'origin/master'
  *  added watching queue size metrics
  *  fix consumers env provider
  *  Merge remote-tracking branch 'origin/VOS-2591_autoru_api_docker'
  *  release 0.50.0
  *  refactoring
  *  fix tests
  *  Merge remote-tracking branch 'origin/master'
  *  refactoring
  *  Merge remote-tracking branch 'origin/master'
  *  added prometheus stage metrics
  *  added named and metered stage to vos2-scheduler-cre
  *  added logs for 4xx response from teleperformance
  *  return old monrun connect timeout for scheduler
  *  release 0.27.1
  *  Get rid of Sentry
  *  Merge remote-tracking branch 'origin/master'
  *  return back graphite metrics for vos-api
  *  Merge remote-tracking branch 'origin/master'
  *  fix mon run port, return back graphite metrics
  *  Merge remote-tracking branch 'origin/master'
  *  try to increase connect time out for conductor
  *  delete stage metrics because of error
  *  Merge remote-tracking branch 'origin/master'
  *  fix pom
  *  Merge remote-tracking branch 'origin/master'
  *  fix pom
  *  merge some prometheus metrics
  *  Merge remote-tracking branch 'origin/VOS-2591_autoru_api_docker'
     # Conflicts:
     #	schema-registry
  *  Merge pull request #470 from YandexClassifieds/schema_registry_v0.0.401
     schema_registry_v0.0.401
  *  VOS-2743: Fix price2
  *  Merge pull request #469 from YandexClassifieds/REVIEWS_zen_deleted_img
     REVIEWS zen deleted img
  *  VOS-2743: Turn on raising renewals without promotion
  *  VOS-2743: Turn on raising renewals without promotion (#467)
     * VOS-2743: Turn on raising renewals without promotion
     * VOS-2743: Turn on raising with CONDITIONS_CHANGED later than 2018-07-23
  *  VOS-2714 moderation editor update (#465)
     * moderation update editor poll and push
     
     * moderation update tests
  *  new enum values for auto mirror
  *  fix metrics with infinite delay
  *  release 0.26.4
  *  Merge pull request #464 from YandexClassifieds/VOS-2739-vins
     VOS-2739 get offers vin by offer ids
  *  VOS-2745: Added electricity_included for garage
  *  release 0.48.4
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  updated notify logging
  *  Merge pull request #458 from YandexClassifieds/VOS-2711_ban_to_chat_service_notification
     VOS-2711 ban notification to tech support room
  *  Realty 2.12 initial
  *  Merge branch 'realty-master'
  *  release 0.48.2
  *  Merge pull request #462 from YandexClassifieds/update_auto_micro_core-0.12.81
     update auto-micro-core 0.12.81
  *  Merge pull request #457 from YandexClassifieds/VSMODERATION-2285_vin_resolution_update
     VSMODERATION-2285 added VinIndexResolution.updated to resolution hash…
  *  release 0.48.1
  *  fix import
  *  Merge remote-tracking branch 'origin/master'
  *  added next processing metric
  *  schema registry fix
  *  added new metrics
  *  AUTORUAPI-4574: remove soft checking for some feed tags
  *  VOS-2717: Realty 2.11 integration
  *  Merge pull request #455 from YandexClassifieds/back_to_v0.0.384
     fix schema-registry
  *  request id in healthchecks (#454)
  *  release 0.26.2
  *  test fix
  *  Merge remote-tracking branch 'origin/master'
  *  VOS-2738 fixed wrong mark-models counters, added test
  *  fixed opinions test
  *  Merge branch 'master' of github.com:YandexClassifieds/vos2
  *  VOS-2738 fixed wrong mark-models counters
  *  VOS-2643: fix salesman client
  *  release 0.23.0
  *  Merge pull request #432 from YandexClassifieds/VOS-2716
     VOS-2716 дефолтный сурс - Partner
  *  Merge pull request #433 from YandexClassifieds/AUTORUAPI-4422-extended
     AUTORUAPI-4422 revert update requisites
  *  Merge pull request #430 from YandexClassifieds/_fix_feedprocessor
     Fix: Could not find the selected project in the reactor: vos2-autoru-…
  *  release 0.22.7
  *  Merge pull request #429 from YandexClassifieds/AUTORUAPI-4422-extended
     Autoruapi 4422 extended
  *  release 0.43.6
  *  VOS-2643: fix truck->trucks in salesman client
  *  release 0.43.5
  *  VOS-2643: temporary comment monitoring notify
  *  VOS-2643: check services using timestamps and activity status
  *  release 0.22.6
  *  release 0.43.4
  *  Merge remote-tracking branch 'origin/master'
  *  
     import and tests fixes
  *  VOS-2715 default description for offers with empty description
  *  better
  *  Realty 2.11 initial
  *  
     changelog
  *  VOS-2251  different features for push and poll moderation (#428)
     * moderation opinion consumer
     
     * pr fixes + some metrics
     
     * different features for push and poll moderation
  *  VOS-2686: Fix patches premoderation status
  *  Status apply logging
  *  schema registry v0.0.367
  *  schema registry v0.0.366
  *  DAO method useOnShard for external ids fixed
  *  release 0.22.4
  *  release 0.43.2

 -- teamcity <teamcity@yandex-team.ru>  Mon, 03 Sep 2018 12:52:39 +0300

## yandex-vos2-autoru-feedprocessor:0.0.39 (Fri, 20 Jul 2018 19:30:06 +0300)

  * AUTORUSUP-4038: upper case VIN

## yandex-vos2-autoru-feedprocessor:0.0.38 (Fri, 20 Jul 2018 18:32:53 +0300)

  * VOS-2677: allow any max_discount value except greater than price

## yandex-vos2-autoru-feedprocessor:0.0.37 (Tue, 17 Jul 2018 19:50:30 +0300)

  * VOS-2701: save offer in transaction

## yandex-vos2-autoru-feedprocessor:0.0.36 (Tue, 17 Jul 2018 18:25:02 +0300)

  * VOS-2701: change index tables execute order

## yandex-vos2-autoru-feedprocessor:0.0.35 (Mon, 16 Jul 2018 18:00:12 +0300)

  * VOS-2677: validate discount options

## yandex-vos2-autoru-feedprocessor:0.0.34 (Mon, 16 Jul 2018 15:44:25 +0300)

  * VOS-2670: always involve section in matching hashes

## yandex-vos2-autoru-feedprocessor:0.0.33 (Thu, 12 Jul 2018 11:17:43 +0300)

  * AUTORUAPI-4411: hide exception messages from clients

## yandex-vos2-autoru-feedprocessor:0.0.32 (Mon, 09 Jul 2018 15:36:43 +0300)

  * VOS-2670: учитывать Section при составления hash-ей матчинга офферов

## yandex-vos2-autoru-feedprocessor:0.0.31 (Mon, 09 Jul 2018 11:29:06 +0300)

  * VOS-2677: max_discount setting

## yandex-vos2-autoru-feedprocessor:0.0.30 (Fri, 06 Jul 2018 11:54:17 +0300)

  * AUTORUSUP-4064: vin FZJ800130253

## yandex-vos2-autoru-feedprocessor:0.0.29 (Wed, 27 Jun 2018 11:11:15 +0300)

  * VOS-2326: stop usage of old index tables

## yandex-vos2-autoru-feedprocessor:0.0.28 (Fri, 15 Jun 2018 18:49:33 +0300)

  * fix key not found exception

## yandex-vos2-autoru-feedprocessor:0.0.27 (Fri, 08 Jun 2018 11:56:37 +0300)

  * VOS-2326: compare unified vin versions if feature enabled

## yandex-vos2-autoru-feedprocessor:0.0.26 (Thu, 07 Jun 2018 19:55:43 +0300)

  * VOS-2326: matching by unified vin

## yandex-vos2-autoru-feedprocessor:0.0.25 (Wed, 06 Jun 2018 19:34:59 +0300)

  * VOS-2625 save sales_vin 

## yandex-vos2-autoru-feedprocessor:0.0.24 (Tue, 05 Jun 2018 13:03:11 +0300)

  * VOS-2612: don't ignore exceptions of saving in VOS

## yandex-vos2-autoru-feedprocessor:0.0.23 (Tue, 29 May 2018 18:00:08 +0300)

  * AUTORUAPI-4271 parition label for messages_counter metrics

## yandex-vos2-autoru-feedprocessor:0.0.22 (Tue, 29 May 2018 13:12:38 +0300)

  * calculate feedId independently in VOS 

## yandex-vos2-autoru-feedprocessor:0.0.21 (Thu, 24 May 2018 13:31:08 +0300)

  * VOS-2525 tasks race 

## yandex-vos2-autoru-feedprocessor:0.0.20 (Wed, 23 May 2018 14:03:45 +0300)

  * batch commit offset 

## yandex-vos2-autoru-feedprocessor:0.0.19 (Mon, 21 May 2018 18:20:48 +0300)

  * remove all cars outside of feed (not only used)

## yandex-vos2-autoru-feedprocessor:0.0.18 (Mon, 21 May 2018 14:42:46 +0300)

  * AUTORUAPI-4103 don't add feedprocessor images to offer if all photo already loaded 

## yandex-vos2-autoru-feedprocessor:0.0.17 (Fri, 18 May 2018 15:31:43 +0300)

  * AUTORUAPI-4089: touch and don't delete invalid offers in VOS

## yandex-vos2-autoru-feedprocessor:0.0.16 (Fri, 18 May 2018 11:45:05 +0300)

  * rename metrics 

## yandex-vos2-autoru-feedprocessor:0.0.15 (Thu, 17 May 2018 15:47:15 +0300)

  * added _ to end of prometheus prefix 

## yandex-vos2-autoru-feedprocessor:0.0.14 (Thu, 17 May 2018 13:03:29 +0300)

  * added prometheus prefix for metrics (vos2-autoru-feedprocessor) 

## yandex-vos2-autoru-feedprocessor:0.0.13 (Tue, 15 May 2018 11:16:59 +0300)

  * use latest offset for feedloader

## yandex-vos2-autoru-feedprocessor:0.0.12 (Mon, 14 May 2018 20:46:43 +0300)

  * AUTORUAPI-4089: remove offers outside feed feature

## yandex-vos2-autoru-feedprocessor:0.0.11 (Mon, 14 May 2018 17:34:43 +0300)

  * AUTORUAPI-4089: touch failed offers

## yandex-vos2-autoru-feedprocessor:0.0.10 (Mon, 14 May 2018 10:32:42 +0300)

  * AUTORUSUP-3673 fix compile error

## yandex-vos2-autoru-feedprocessor:0.0.9 (Fri, 11 May 2018 19:52:45 +0300)

  * AUTORUSUP-3673 don't delete hand uploaded images 

## yandex-vos2-autoru-feedprocessor:0.0.8 (Tue, 08 May 2018 12:00:51 +0300)

  * log system property java.io.tmpdir 

## yandex-vos2-autoru-feedprocessor:0.0.7 (Tue, 08 May 2018 11:21:30 +0300)

  * use less xmx and xms (512 m) 

## yandex-vos2-autoru-feedprocessor:0.0.6 (Mon, 07 May 2018 19:03:58 +0300)

  * added directories for extdata 

## yandex-vos2-autoru-feedprocessor:0.0.5 (Mon, 07 May 2018 17:59:36 +0300)

  * get props from consul 

## yandex-vos2-autoru-feedprocessor:0.0.4 (Mon, 07 May 2018 16:30:03 +0300)

  * get host.name from ENV HOSTNAME if exists 

## yandex-vos2-autoru-feedprocessor:0.0.3 (Mon, 07 May 2018 14:53:26 +0300)

  * fix create logs directory 

## yandex-vos2-autoru-feedprocessor:0.0.2 (Sat, 05 May 2018 15:34:04 +0300)

  * AUTORUAPI-3902 delete hardcode DEBUG_PORT and JMX_PORT from start.sh 

## yandex-vos2-autoru-feedprocessor:0.0.1 (Wed, 25 Apr 2018 18:38:20 +0300)

  * AUTORUAPI-3902 create vos2-autoru-feedprocessor subproject in VOS 
