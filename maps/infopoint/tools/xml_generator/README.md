XML generator
=============

Tool for generation valid xml file for import into infopoint from simple csv files

During the generation events can be merged into one if they have intersection in tags
and distance between them is less or equal than specified radius

`process_csv.sh` script simplifies generation on folders with predefined structure (e.g. test\_events)

```
<data dir>
├── data
│   └── <csv files in format lat;lon;tags;description>
└── <optional exclude file to filter points>
```

After generation resulting xml shoud be uploaded as corresponding sandbox resourse

```
ya upload --ttl=inf --attr=infopoint_xml_import=<id> <generated_xml>
```

For process of importing this data in infopoint please check infopoint [documentation](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infopoint#documentation)

