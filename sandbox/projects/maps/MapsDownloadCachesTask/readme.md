This is a sandbox task for offline cache downloading.

# How to create the task
1. Open sandbox at https://sandbox.yandex-team.ru/
2. Press `Create task` button.
3. Write in `MAPS_DOWNLOAD_CACHES_TASK`
4. Press `Create`
5. Under `Task custom parameters` header, fill in your desired parameters, according to the [Inputs](#inputs) section.
6. Press `Run`
7. Wait for the task until it is in the Success status.
8. Go to the `Resources` tab, find the resource with Type = `MAPS_OFFLINE_CACHES_RESOURCE` and press on its ID number.
9. Press on the HTTP proxy link. Your browser will begin download the offline caches in a tar.gz archive.
10. You can find some hints about what to do with the archive in the [Working with the tar.gz archive](#working-with-the-targz-archive) section.

As an alternative to steps 2-4, you might want to clone an existing task with the type `MAPS_DOWNLOAD_CACHES_TASK`.

# Inputs
All of the task inputs are located under `Task custom parameters` header.
* `Layers`. Recommended: `vmap2fb,search2,driving` or `vnav2fb,search2,driving`.
* `Locale` (e.g. `ru_RU` or `en_US`).
* `Region IDs` separated by comma signs (",")
* `Countries (regex)` in the language you'd like to download it
* `Region names (regex)` in the language you'd like to download it
* `Legacy format`. Use legacy files emplacement format. See [Files emplacement](#files-emplacement) for more details
* `Time to live`. Do not confuse it with task's time to kill parameter!

You have to specify at least one of the three fields for region selection. If two or more fields for region selection are chosen, the task downloads regions that match any of the fields.

Country and region names must be in the language chosen in the Locale field. For example, if you like to download caches for all the regions of Turkey, then if `Locale == ru_RU`, you should write `Турция` in Countries field. If `Locale == en_US`, you should write `Turkey`.

Country and region names are Python regex fields. If you like to choose several, you should write it in this format: `(^First$|^Second$|^Third$|^Fourth$)`. Example: Countries == `(^France$|^Russia$|^Turkey$)` means that regions of France, Russia, and Turkey will be downloaded (if you chose `en_US` locale).

Beware of unwanted regions. For example, if you write Locale == `ru_RU` and Regions == `(Москва|Саха)`, you will get the following regions downloaded:
* Москва и Московская область
* Южно-Сахалинск
* Москва
* Республика Саха (Якутия)
* Сахалинская область

An example of correct regexes to download Moscow and Sakha (Yakutia) Republic is
```regex
(^Москва$|^Республика Саха \(Якутия\)$)
```
Full names of the regions are written, `(` and `)` symbols are escaped.

# What it does
1. Downloads region list from http://core-mobile-cacheinfo.maps.yandex.net/
2. Downloads metadata for regions matched by Region IDs or Countries or Region names.
3. Downloads the layers chosen by you in inputs.
4. Packs it all into `offline_cache.tar.gz`

# Working with the tar.gz archive
* To examine the file structrure of the archive, open the downloads directory in your terminal and type `tar -tf "offline_cache.tar.gz"`.
* To extract an archive, type `tar -xzf "offline_cache.tar.gz" mapkit`.

# Files emplacement
The result archive directory structure depends on the `Legacy format` check box.
Examples for layers: `driving,search2,vmap2fb` and locale: `ru_RU`:
`Legacy format` unchecked:
```
└── offline_caches
    ├── 10743
    │   ├── region.pb
    │   ├── driving.fb
    │   ├── search2.fb
    │   └── vmap2fb.fb
    └── 10745
        ├── region.pb
        ├── driving.fb
        ├── search2.fb
        └── vmap2fb.fb
```
`Legacy format` checked:
```
├── vmap2fb
│   ├── 10743_ru_RU
│   │   └── region.fb
│   └── 10745_ru_RU
│       └── region.fb
├── driving
│   ├── 10743_ru_RU
│   │   └── region.fb
│   └── 10745_ru_RU
│       └── region.fb
├── metadata
│   ├── 10743_ru_RU
│   │   └── region.pb
│   └── 10745_ru_RU
│       └── region.pb
└── search2
    ├── 10743_ru_RU
    │   └── region.fb
    └── 10745_ru_RU
        └── region.fb
```

# Troubleshooting directory contamination
Be careful when working with graphic explorer apps, such as macOS Finder app. It may contaminate the caches directories with files beginning with `.` which prevents offline caches from working in MapKit applications.

To check the existence of such files, type `find mapkit -name ".?*"`.

To remove the files you have found , type `find mapkit -name ".?*" | xargs -I {} rm -v "{}"`. This command will output the deleted files' names.

# Notes
`region_list_pb2.py` is made by protoc (libprotoc 2.6.1) from `arcadia/maps/doc/proto/yandex/maps/proto/offline-cache/region_list.proto`.
Its 10th line `from google.protobuf import descriptor_pb2` has been removed, so that `region_list_pb2.py` can pass py-flakes checks.

# Links
* https://st.yandex-team.ru/MAPSMOBCORE-7940
* Region ID database: https://geoadmin.yandex-team.ru/
