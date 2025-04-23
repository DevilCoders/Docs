### How to run
  
1. Build executables: `./gradlew :assemble`  
2. Goto `cd ./build/bin/[macos|linux|mingw]x64/releaseExecutable/`  
3. Run `./kn-tanker-utils.kexe job --params...`  
  
#### Remote jobs  
  
1. `copyKeys` — copies filtered keys from source keyset to target keyset;  
   e.g. `./kn-tanker-utils.kexe copyKeys --oauth=AQAD-* --source=taximetre/driver --target=taxi/testnew --filter=filter.txt`    
   Parameters:  
- `--oauth` — nuff said, goto https://nda.ya.ru/3SjQY7 for personal key  
- `--target` — "project-id/keyset" in Tanker to move keys from  
- `--source` — "project-id/keyset" to create and fill  
- `--force` — forces to create new keyset without old info  
- `--filter` — path to file with keys to explicitly include into the new keyset  
- `--only-languages` — copies only selected languages  
  
2. `resetStatus` — filter keys and reset status to selected one;  
   e.g. `./kn-tanker-utils.kexe resetStatus --oauth=AQAD-* --source=taximetre/driver --new-status=expired --filter=filter.txt --exclude-languages=ru,en,he`  
   Parameters:  
- `--oauth` — nuff said, goto https://nda.ya.ru/3SjQY7 for personal key  
- `--target` — "project-id/keyset" in Tanker to work with keys in  
- `--new-status` — target status to change keys to  
- `--filter` — path to file with keys to explicitly include into the new keyset  
- `--exclude-languages` — coma separated languages' iso codes to filter status change in
  
3. `deleteKeys` — filter keys and remove them from target keyset;
   e.g. `./kn-tanker-utils.kexe deleteKeys --oauth=AQAD-* --target=taximetre/driver --filter=filter.txt --method=blacklist`
   Parameters:  
- `--oauth` — nuff said, goto https://nda.ya.ru/3SjQY7 for personal key  
- `--target` — "project-id/keyset" in Tanker to work with keys in  
- `--filter` — path to file with keys to rm keys from target keyset  
- `--method` — select between rm methods: `blacklist` is not supporting by API for now, `whitelist` have different mechanics (underground we have to say what keys should be left in keyset, others will be deleted)  

Filter file should looks like (each key on a new line without any whitespaces):  
```
DriverPromocodes_12h
DriverPromocodes_168h_7d
DriverPromocodes_1h
DriverPromocodes_3h
DriverPromocodes_3h_description
DriverPromocodes_kaz_brand_parttime_description
DriverPromocodes_kaz_retention_sept_description
```
