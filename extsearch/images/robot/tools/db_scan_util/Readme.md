## This is set of tools to scan some images robot yt bases

## Documentation
https://wiki.yandex-team.ru/YandexImages/Robot/dbscanutils/

## Here are some launch examples

./db_scan_util ImageDBScanCrcsThumbIds --input-file ./input_for_test_0 --output-file  ./output_of_test_0 --server arnold --imagedb-state=head --imagedb-prefix //home/images

./db_scan_util SemidupsPublicStateScanCrcs --input-file ./input_for_test_1 --output-file ./output_of_test_1 --semidups-state 20190131-082744 --server arnold --semidups-prefix //home/cvdup/semidups/public/production

./db_scan_util UrlDBScanUrlsForCrcs --input-file ./input_for_test_2 --output-file ./output_of_test_2 --urldb-state=head --server arnold --urldb-prefix //home/images --urldb-shard-count 5

./db_scan_util ImageDBScanCrcsForFeatures --input-file ./input_for_test_3 --output-file ./output_of_test_3 --chunk-name TFeaturesChunkVer6 --layer-name FEAT_I2T_200 --imagedb-state=head --server arnold --imagedb-prefix //home/images

./db_scan_util MetaDocScanDocIds --input-file ./input_for_test_4 --output-file ./output_of_test_4 --index-prefix //home/images --index-state 20190205-090237 --server arnold --index-shard-count 10

