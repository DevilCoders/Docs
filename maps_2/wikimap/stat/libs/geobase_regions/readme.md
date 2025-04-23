Geobase Regions
===============

This `PY23_LIBRARY` provides an easy-to-use way to map frequent geospatial data types onto `region_id`-s.

Geodata intialization
---------------------
Conversion to `region_id` requires geodata. There are three initialization methods:
1. `init_geodata_from_resource` is designed to be used in tests.
   * Geodata is not changing over time. Therefore, returned `region_id`-s do not change from run to run.
   * Does not require any external connections during runtime.
   * Requires `RESOURCE(sbr: )` in target's _ya.make_.
2. `init_geodata_from_yt_copy` is designed for local runs.
   * Geodata is expected to be frequently updated. Returned `region_id`-s can change from run to run.
   * Requires connection to _hahn_ yt cluster during runtime. Fetches geodata from `//statbox/statbox-dict-last/geodata5.bin`.
3. Initialization by default is designed for usage in _nile_ operations.
   * Geodata is expected to be frequently updated. Returned `region_id`-s can change from run to run.
   * Geodata will be fetched during first conversion to `region_id`.
   * Can not run locally as `ArcGeobase` qb2 resource will not be available.
   * Options `files=GEOBASE_FILES, memory_limit=GEOBASE_JOB_MEMORY_LIMIT_MB` should be specified for the according _nile_ operation.
