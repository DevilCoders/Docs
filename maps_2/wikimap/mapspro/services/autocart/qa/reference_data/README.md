pgsql2shp -f out/bld1.shp -h garden-pgm-rus01h.tst.maps.yandex.ru -p 5432  -u mapsgarden -P gardenTst garden "select bld_id, shape from ymapsdf_yandex_and_tr_20180226_010977_37_8479371.bld_geom where shape && st_makeenvelope(29.776712,40.711542, 29.798603,40.727759, 4326)";


$ pgsql2shp -f out/bld2.shp -h garden-pgm-rus01h.tst.maps.yandex.ru -p 5432  -u mapsgarden -P gardenTst garden "select bld_id, shape from ymapsdf_yandex_and_tr_20180226_010977_37_8479371.bld_geom where shape && st_makeenvelope(29.951769,40.772453,29.965440,40.781147, 4326)";
Initializing...
Done (postgis major version: 2).
Output shape: Polygon
Dumping: XXXXXXXXXXXXXXXXXXXX [1994 rows].
quoter@pollux:~/devel/arcadia/maps/wikimap/mapspro/services/autocart/qa/reference_data$ pgsql2shp -f out/bld3.shp -h garden-pgm-rus01h.tst.maps.yandex.ru -p 5432  -u mapsgarden -P gardenTst garden "select bld_id, shape from ymapsdf_yandex_and_tr_20180226_010977_37_8479371.bld_geom where shape && st_makeenvelope(29.051176,40.177976,29.072333,40.193196, 4326)";
Initializing...
Done (postgis major version: 2).
Output shape: Polygon
Dumping: XXXXXXXXXXXXXXXXXX [1756 rows].
quoter@pollux:~/devel/arcadia/maps/wikimap/mapspro/services/autocart/qa/reference_data$ pgsql2shp -f out/bld4.shp -h garden-pgm-rus01h.tst.maps.yandex.ru -p 5432  -u mapsgarden -P gardenTst garden "select bld_id, shape from ymapsdf_yandex_and_tr_20180226_010977_37_8479371.bld_geom where shape && st_makeenvelope(30.680496,36.886977,30.695263,36.898760, 4326)";
Initializing...
Done (postgis major version: 2).
Output shape: Polygon
Dumping: XXXXXXXXXXXXXXXX [1509 rows].

Reference data was saved to https://proxy.sandbox.yandex-team.ru/521715468
