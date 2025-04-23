# ML Storage

Процессор для [ML Storage](https://a.yandex-team.ru/arc/trunk/arcadia/ads/emily/storage).

## Usage

```py
from ads.emily.storage.api.experiments.bigb import BigbExperimentsApi
from .dao import ExperimentsStorage

api = BigbExperimentsApi()

storage = ExperimentsStorage(experiments_api=api)

experiments = storage.get_experiments()
for experiment_id, experiment in experiments.items():
    pass
```
