### Биндинги к [`time_estimator`](/arc/trunk/arcadia/maps/libs/time_estimator)

Позволяют получить названия факторов по ModelConfig. Используются в [`train_model`](/arc/trunk/arcadia/maps/analyzer/sandbox/eta_prediction/train_model) для построения column_description.


Пример:
```python
config = PyModelConfig.from_file('model_config.meta')
feature_names = get_feature_names(config)
```
