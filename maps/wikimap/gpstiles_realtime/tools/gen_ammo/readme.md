## gpstiles_realtime ammo generator
Generates URI-style ammo file of randomized /tiles queries with specified parameters.
See
 - https://yandextank.readthedocs.io/en/latest/tutorial.html#uri-style-uris-in-file - for more info on ammo file format
 - https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/gpstiles_realtime/fastcgi/swagger_api.yaml - API schema for /tiles query
## usage
```bash
    python gen_ammo.py --host=gpstiles-realtime.maps.yandex.ru --req_params=moscow_z15_1hour.yaml --size=100000 > ammo_moscow_1hour.txt
```
where
- `host` - hostname to use in queries (will be written as `[Host: <host>]`  in ammo file).
- `req_params` - path to yaml config. This config provides bbox of region of interest, zoom range and time interval duration (*since_shift - till_shift*). Random `/tiles` queries satisfying these parameters will be generated. See existing `*.yaml` files for examples.
- `size` - ammo length (number of queries to gen). 
Writes output to `stdout`.
## notes
[04.05.2018] Currently cannot be built with `ya make` as `maps/libs/tileutils/lib/pymod` is not properly arcadized (osgeo missing).
