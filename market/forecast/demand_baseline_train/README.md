# Трэйн бейзлайна прогноза (Подрайверный прогноз)


## graph_generator CLI
```
Usage: ./graph_generator [OPTIONS]

Options:
  --calculator TEXT     calculator_app file name  [required]
  --secret_name TEXT    Nirvana secret_name with credentials to call Nirvana
                        API  [required]

  --pool TEXT           YT pool name  [required]
  --quota TEXT          Nirvana quota name  [required]
  --yt_token TEXT       Nirvana API token  [required]
  --proxy TEXT          YT proxy [hahn, arnold...]  [default: hahn]
  --workflow_guid TEXT  Nirvana workflow GUID
  --log_level TEXT      graph_generator logging level  [default: INFO]
  --mode TEXT           Run mode  [default: dev]
  --root TEXT           root
  --today TEXT          today
  --help                Show this message and exit.
```

## lib

Либы

## bin

Бинари

## CI/CD
- [Проект в аркадии](https://a.yandex-team.ru/projects/alpaca/ci/releases/timeline?dir=market%2Fforecast%2Fdemand_baseline_train&id=demand-baseline-train-release)
    - [CI/CD config](https://a.yandex-team.ru/arc_vcs/market/forecast/demand_baseline_train/a.yaml)

## Nirvana
Проект в Nirvana:
- dev
    - https://nirvana.yandex-team.ru/flow/bf9ac108-92bb-4d4c-9d95-04f8bf03c58b/a98aeddb-3c5f-4383-9d63-a5ae53789979/graph
- prod
    - draft:
        - https://nirvana.yandex-team.ru/flow/a26c2180-25fd-4fd6-896a-fda447cf85c5/7c368add-8e26-4d31-881e-4ee10ddca0d1/graph
    - reactor:
        - https://nirvana.yandex-team.ru/flow/bb713500-8251-4ce5-968b-280ede19bd6a/ea2f2f19-f4c4-45b8-b8a7-b932e3f80756/graph
## Reactor
Реакция запуска графа
- https://nirvana.yandex-team.ru/browse?selected=8769205


## Требования к коду

### Таска torch_model_training.py не должна содержать ничего кроме обучения модели
Т.к. это требовательный к GPU код, то его не так просто отлаживать, таким образом любое усложнение этого участка кода ведет к драмматическому росту трудозатрат на отладку.

### Весь фича инжениринг должен происходить в spark_data_preparation.py
Отчасти вытекает из пункта выше.
На таком объеме датасета процессинг в пандасе значительно замедляет обучение
В torch_model_training датасет для экономии времени поднимается по сути сразу в numpy, который без изменений нарезается на батчи-тензоры

### Все драйвера должны иметь shape = (N, 1) т.е. быть векторами а не матрицами
Драйвера-матрицы побуждают делать one_hot'ы и усложняют сериализацию драйверов
Если есть необходимость сделать драйвер на уровне пересечения, то стоит на уровне spark_data_preparation.py ввести индекс для каждой пары на основе сортировки, для воспроизводимости.
Пример - category_weekofyear_index

### Для каждой промежуточной таблицы, участвующей в расчете должен быть заведен резолвер класс
Если этого не сделать, то есть риск посадить хардкод и, например, перезатирать прод тестовыми запусками

### Все идентификаторы должны начинаться с нуля


