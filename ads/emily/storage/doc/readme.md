# ML Storage 

Стандартизированное хранилище моделей

[Документация](https://logos.yandex-team.ru/docs/ml_logos/storage/about.html)

**Формат:** [models.json](./models.json)

## API Экспериментов

**Формат ответа:** [experiments.json](experiments.json)

### Интерфейс API экспериментов

```py
# api/experiments/base.py

class ExperimentsBaseApi:

    @abstractmethod
    def get_experiments_ids(self) -> ExperimentIDListResponse:
        """ Gets experiment ids list """
        raise NotImplementedError

    @abstractmethod
    def get_experiment(self, experiment_id: str) -> ExperimentResponse:
        """ Gets experiment by id """
        raise NotImplementedError

```

### Пример реализации API экспериментов

```py
# api/experiments/__init__.py

from .base import ExperimentsBaseApi, ExperimentResponse

class ExperimentsApi(ExperimentsBaseApi):

    def get_experiments_ids(self) -> ExperimentIDListResponse:
        id_list = fetch_experiment_ids()  # some logic
        return id_list

    def get_experiment(self, experiment_id: str) -> ExperimentResponse:
        experiment_dict = fetch_experiment(experiment_id)  # some logic
        return ExperimentResponse.load({'data': experiment_dict})  # validation
```

## API Факторов

**Формат ответа:** [factors.json](factors.json)

### Интерфейс API факторов

```py
# api/factors/base.py

class FactorsBaseApi(BaseModelStorageApi):

    @abstractmethod
    def get_model_factors(self, model_id: str, key: str = None) -> FactorResponse:
        raise NotImplementedError
```

### Пример реализации API факторов

```py
# api/factors/__init__.py

from .base import FactorsBaseApi, FactorResponse


class FactorApi(FactorsBaseApi):

    def get_model_factors(self, model_id: str, key: str = None) -> FactorResponse:
        factors = fetch_factors_by_model_id_key(model_id, key)  # some logic
        return FactorResponse.load({'data': factors})  # validation

```
