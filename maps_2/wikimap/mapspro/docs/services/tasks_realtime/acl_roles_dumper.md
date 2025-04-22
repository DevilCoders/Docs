ACL Roles Dumper
================
ACL Roles Dumper periodically (once a day) dumps information about users' roles. This dump is shipped to YT by LogBroker.

Note. The application dumps all roles but `common`. The `common` role is not dumped because almost every user has this role. A dump with the `common` role bigger on several orders of magnitude than a dump without it.

Usage
-----
The application does not support any command line arguments and must be executed as is.

For establishing connections towards the DB, configuration files from `maps/wikimap/mapspro/cfg/services` are used (by means of `maps/wikimap/mapspro/libs/common/include/yandex/maps/wiki/common/default_config.h`).
