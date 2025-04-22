A tool to automate QUASAR-7440 data flow
========================================

How to use:
```
ya make && ./burn_data --help
```


General info:
-------------------
This tool is created to manage data for provisioning the secrets for yandexstation_2 and device_id generating for all platforms.

Three main modes are recognized:
* factory provision (normal mode)
* local provision (a.k.a. rework)
* OTA provision (a.k.a. OTA rework)

Device lifecycle is, at most:
1. create new device_id via `add_new_devices`
2. obtain widevine and hdcp_14 per-device keys
3. upload them via `decode_XXX`
4. prepare factory data via `rebuild_burn_data`
5. (rework) move device to a designated quasmodrom group
6. (rework) prepare rework data via `prepare_rework_tarball`
7. (ota) re-upload hdcp_14 and widevine keys via `ota_decode_XXX` (this is required because OTA provision uses different key set for wrapping)
8. (ota) add device to ota rework source table
9. (ota) prepare ota data for backend via `rebuild_ota_rework_data`

Commands
-------------------
See `./burn_data --help` for exact description.

See `./burn_data <some_command> --help` for particular command help.
