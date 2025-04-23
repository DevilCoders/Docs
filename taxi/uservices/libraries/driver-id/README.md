# Driver id helper library
This library provides strongly typed dbid and uuid types (based on std::string)
and several helpers classes:
1. ::driver_id::DriverUuidView, ::driver_id::DriverDbidView - typedefs over
   string_view over dbid/uuid respecively
2. ::driver_id::DriverIdView - pair of vies over dbid and uuid
3. ::driver_id::DriverDbidUndscrUuid - suitable for working with geobus, this
   classs incapsulates dbid and uuid in form of ${dbid}\_${uuid} and provides
   views over those two
4. ::driver_id::DriverId - basic class, simply stores dbid and uuid. It is more
    expensive to copy than ::driver::DriverDbidUndscrUuid.
5. ::driver_id::DriverIdPrehashed - class that internally stores calculated hash value.
6. ::driver_id::DriverIdViewStorage - class that stores given
   ::driver_id::DriverDbidUndscrUuid internally and provides view over them.
   It also provides effective hasher and equal_to implementation for those
   views.
6. ::driver_id::Shared - This templates can wrap any driver id type from above
   as shared_ptr. It provides hashing, comparison and other necessary methods.

Provided types support serialization to/from json/bson/yaml by standard means.
