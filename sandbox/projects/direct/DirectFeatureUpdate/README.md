# DirectFeatureUpdate

Локальный запуск:
```shell
ya make
./direct-feature-update run --enable-taskbox --owner DIRECT --create-only '{"custom_fields": [{"name": "ticket", "value": "DIRECT-000"}, {"name": "feature_name", "value": "test_feature"}, {"name": "feature_description", "value": "Example description"}, {"name":"binary_executor_release_type", "value":"custom"}]}'
```
