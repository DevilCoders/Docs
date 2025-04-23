| library | note |
| ------- | ---- |
| `agg` | Arcadized. Used in `maps/renderer`. Not present in `contrib` |
| `freeimage` | Arcadized. Used in `maps/libs/imageutils`. Not present in `contrib`. |
| `fribidi` | Arcadized. Used in `maps/renderer`. Not present in `contrib` |
| `harfbuzz` | Arcadized. Used in `maps/renderer`. Not present in `contrib` |
| `heatmap` | Not arcadized. Used in `maps/carparks`. Not present in `contrib` |
| `lua-resty-http` | Arcadized version of lua driver for OpenResty. Is dependent by `packages/yandex-maps-ratelimiter2-agent` |
| `pylibs` | Contrib libraries for python |
| `rapidjson` | Used in `maps/renderer`. Should be removed in favor of `maps/libs/json` / `contrib/libs/rapidjson` |
| `succinct` | Yet another succint data structures implementation (taken from [ot/succinct](https://github.com/ot/succinct)). Arcadized and used in `maps/routing`. Logically duplicates `library/cpp/succinct_arrays`, yet built bitstreams are binary incompatible |
| `swagger` | Not arcadized, yet looks useful |
| `unionfs-fuse` | Not arcadized. Used to build unionfs-fuse module (used in yandex-maps-build / yandex-maps-sanebuild) |
| `xmlwrapp` | Arcadized, used in `maps/renderer`. Not present in `contrib` |
