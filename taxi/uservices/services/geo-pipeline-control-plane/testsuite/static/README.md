When updating db_* files, ensure that json is dumped with sort_keys=True and
without space. 
```
data['version'] = 3
data['config'] = json.dumps(json.load(open(f'/tmp/MY_FILE_WITH_CONFIG.json', 'r')), separators=(',', ':'),indent=None, sort_keys=True)
json.dump(data, open('./db_geo_pipeline_configs_test.json', 'w'), sort_keys=True, separators=(',', ':'))
```
That is because inside service, we write in mong with ToStableString.
If json is equal, but serialization is not - e.g. you wrote it without
sort_keys=True, then service will fail edit_pipeline tests

Also, leave previous versions of config in this file, this way you can tets
that previous versions continue to work. This ensures smooth rollout of
next config version
