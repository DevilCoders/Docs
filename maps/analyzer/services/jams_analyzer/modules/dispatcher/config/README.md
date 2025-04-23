How it works

Hosts configs: `dispatcher-hosts.conf.*` (selected by environment type)
    see [testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_testing/endpoint_sets/) or [stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_analyzer_stable/endpoint_sets/) endpoints

Dispatcher config:
 - COMMON config = dispatcher.conf.common
 - CUSTOM config = dispatcher.conf.* (except common)

Dispatcher takes union of `<allowed_clids>`, `<allowed_osm_regions>`, `<miids_whitelist_disabled_regions>` and `<fingerprints>` from both CUSTOM and COMMON configs, CUSTOM clid entries for `<allowed_clids>` override COMMON.
Single clid is not allowed to appear in multiple entires or multiple times in same entry of single config file, in this case dispatcher will fail to load config and start.
`<path_to_hosts_config>`, `<actual_time>` and `<loggers>` from CUSTOM config _overwrites_ corresponding COMMON sections.
