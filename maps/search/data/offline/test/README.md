This tool is used to build test data for offline search integration tests. It consists of two packages:

* `yandex-maps-offline-search-test-data` (`source` folder) is used to place indexes' source files to corresponding folders on filesystem
* `yandex-mapsmobi-offline-search-test-data` (`binary` folder) is used to build actual offline search indexes from source files provided by previous package

== `yandex-maps-offline-search-test-data` usage

* Place source data for offline business indexer into `source/offline-search-test-data/business/`
* Place source data for offline geocoder indexer into `source/offline-search-test-data/geocoder/`
* Run `make deb` in `source` folder
* Dupload resulting package to MAPSCORE repository and use it in `yandex-mapsmobi-offline-search-test-data` package

== `yandex-mapsmobi-offline-search-test-data` usage

* Run `make deb` in `binary` folder
* Dupload resulting package to MAPSMOBI repository and use it in corresponding packages (`yandex-mapsmobi-libs-mapkit-offline-search-geocoder`,  `yandex-mapsmobi-libs-mapkit-offline-search-business`, etc.)