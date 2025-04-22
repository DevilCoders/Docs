# Gar to YT import

Importing GAR objects to YT.

import_gar.sh -- Entry point. Imports all regions from gar.zip archive except listed in "regions_to_skip.lst" to YT.
import_region.sh -- Imports one specified region to YT.
regions_to_skip.lst -- List of technical/empty regions that should not be imported.
gar_xml_to_yt -- A binary for importing one xml (toponym, house, hierarchy or house_parameters)

## HowTo run

Write your OAUTH YT TOKEN to ~/.yt/token

Run:
```bash
ya make -r
./import_gar.sh path/to/gar.zip //path/to/yt/folder ./regions_to_skip.lst
```

This will create some tables with toponyms, houses, hierarchy and house parameters (for postal codes import) in provided YT folder.
