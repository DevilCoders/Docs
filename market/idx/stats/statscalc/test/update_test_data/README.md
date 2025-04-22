# Test data update manual

1. Build ```arcadia/market/indexer/vcluster_pictures_merger/vcluster_pictures_merger```
2. Find name of current index generation in testing planeshift (ps01ht.market.yandex.net) (e.g. 20170320_0441)
3. Run ```./update_test_data.sh <generation>``` (```./update_test_data.sh 20170320_0441```)
4. Upload test_data dir to sandbox ```ya upload test_data --ttl inf```
5. Update sanbox resource id in ```arcadia/market/idx/stats/statscalc/test/ya.make```
