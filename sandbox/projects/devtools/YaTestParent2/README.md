# Отладка вносимых в задачу YA_TEST_PARENT_2 изменений

```
head_svn_revision=$(svn info svn+ssh://arcadia.yandex.ru/arc | /bin/grep "^Revision" | /bin/grep -o [0-9]*)
payload=$(echo '{"custom_fields": [{"name": "arcadia_url", "value": "arcadia:/arc/trunk/arcadia@{head_svn_revision}"}, {"name": "targets", "value": "devtools/dummy_arcadia/test/boost_test_exotic_platform/custom_test_module"}, {"name": "expected_test_info", "value": "{\"toolchain\":\"default-linux-x86_64-release\",\"tags\":[\"ya:force_sandbox\",\"sb:GENERIC\",\"sb:OSX_BIG_SUR\",\"ya:fat\"],\"suite_name\":\"unittest\",\"suite_hid\":123,\"owners\":{},\"requirements\":{},\"size\":\"large\",\"suite_id\":\"\"}"}]}' | sed -e "s#{head_svn_revision}#${head_svn_revision}#")
ya make -r && ./YaTestParent2 run --type YA_TEST_PARENT_2 --enable-taskbox "$payload"
```
