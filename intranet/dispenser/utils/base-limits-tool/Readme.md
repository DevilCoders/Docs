# About
This is a tool to update base resource limits in Dispenser.

Supported parameters are:
````
base-limits-tool
   --get-all <campaign_key> <provider_key> <output_file>
   --put-all <campaign_key> <provider_key> <input_file>
   --get-one <campaign_key> <base_resource_key>
   --put-one <campaign_key> <base_resource_key> <value> <unit>
   --test
````

Usage:
````
base-limits-tool --get-all feb2021 yp output.json
base-limits-tool --get-one aug2021 yp:cpu:man:default --test
````

Supported units ensembles are:
````
BPS, KBPS, MBPS, GBPS, TBPS
BINARY_BPS, KIBPS, MIBPS, GIBPS, TIBPS
MPS, KMPS, MMPS, GMPS
BYTE, KIBIBYTE, MEBIBYTE, GIBIBYTE, TEBIBYTE
PERMILLE, PERCENT, COUNT, KILO, MEGA, GIGA
PERMILLE_CORES, PERCENT_CORES, CORES, KILO_CORES, MEGA_CORES, GIGA_CORES
GIBIBYTE_BASE, TEBIBYTE_BASE, PEBIBYTE_BASE, EXBIBYTE_BASE
````
How to install:
- Setup Arcadia using this [guide](https://docs.yandex-team.ru/devtools/).
- Execute ``ya make`` in ``${ARCADIA_ROOT}/intranet/dispenser/utils/base-limits-tool``
- SSH key needs to be registered on Staff, this key is required to get an OAuth token
- Run the tool
