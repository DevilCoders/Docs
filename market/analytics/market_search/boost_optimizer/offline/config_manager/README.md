## config manager

Python>=3.6

### main:
* main_get_new_boosts - получить список новых бустов из менеджерского конфига

### Тесты
Из папки запустить `python -m pytest`

### Запустить локально
`python main.py
    --manager-file="test_data/boost_config.json"
    --production-file="test_data/booster.json"
    --type-map-file="test_data/type_map.json"
    --production-config-save-file="test_data/production_result.json"
    --new-boosts-save-file="test_data/new_boosts.json"
`
