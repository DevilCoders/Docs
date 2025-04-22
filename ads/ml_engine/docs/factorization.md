Движок _factorization_ предназначен для факторизации модели на произведение нескольких компонент:

<img src="https://latex.codecogs.com/png.latex?a(x) = a_1(x) \\cdot a_2(x) \\dots a_n(x)" />

Алгоритмы факторизации можно объединить в два основных семейства:
- покоординатный спуск (представлен режимами "reweighting" и "baselines"): последовательное обучение всех N компонент, в порядке их указания. На этапе обучения i-й модели все остальные фиксируются. Каждая из компонент аппроксимируется экспонентой от сырого прогноза модели;
- em-алгоритм (aka "wang"): модели обучаются параллельно, каждая из компонент аппроксимируется сигмоидой от сырого прогноза. В данном режиме можно факторизовывать только лишь на две компоненты.


## Пример конфига обучения

```
task_id: factorization_task
owner: username
mail_to: username@yandex-team.ru

engine: factorization

log: //home/bs/ml/logs/EFHFactorsYandexPremiumNS
last_log_date: 2021-06-22
days: 1

mode: reweighting

factorization:
    iterations: 5
    models:
        - qid_model
        - banner_model
    target: IsClick
    group_by:
        - HitLogID
        - Position
    split:
        by: HitLogID
        val_percent: 20
    tables:
        test:
            test_log_name:
                - //home/bs/ml/logs/EFHFactorsYandexPremiumNS/1d/2021-06-23

calc:
    revision: 8238308
    libraries:
        - ads/quality/simulate_auction_yt/pylib
    mappers:
        - Grep('r.FraudBits == 0')
    exec: |
        from yabs.matrixnet.factor import Lolita9Factors
    begin: |
        from math import log

qid_model:
    engine: tlm
    fit_args:
        algorithm: precond
        epochs: 1000
        lbfgs_curvature: 0
        lbfgs_m: 10
        learn_bias: 1
    factors_info:
        factors:
            - QID
        factor_types:
            QID: categorical
        tlm_factor_types:
            QID: categorical

banner_model:
    engine: catboost
    fit_args:
        loss: Logloss
        iterations: 40000
        lr: 0.44
        subsample: 0.9
    factors_info:
        factors: ['__formula__:Lolita9Factors']
        factor_types
            FLM1: mx
            FLM2: ignore
    init:
        type: constant
        params:
            value: 1
```

## Описание задачи факторизации

В поле **mode** указывается алгоритм факторизации (_reweighting_, _baselines_, _wang_).

Лог для обучения можно задать одним из трех способов:
- в поле **type**: в этом случае данные берутся из лога //home/bs/ml/logs/1d/{type}. Необходимо также определить поля **last_log_date** и **days**;
- в поле **log**. В данном случае также необходимо определить поля **last_log_date** и **days**;
- в поле **factorization->tables->input**. Здесь перечисляются списком полные пути до желаемых таблиц.

Ключевое поле, в котором описывается сама задача факторизации &ndash; **factorization**:

- Поле **target** определяет имя колонки, в которой лежит целевое значение (должно быть бинарным). Собственно, именно его и будет приближать комбинированный прогноз.
- В поле **models** перечисляются ключи, по которым можно найти описания моделей. Данное поле и определяет, на какие компоненты мы хотим разложить нашу модель.
- В поле **group_by** перечисляются колонки, по которым будет строиться ключ (способ адресации к строчке, по данному ключу будет происходить уникализация).
- В поле **split** описывается, каким образом мы будем разбивать исходную выборку на обучение и валидацию (по какому полю и в какой пропорции).
- В поле **tables->test** перечисляются тестовые логи, на которых мы также хотим посчитать метрики.

## Описание моделей (компонент)

- **engine** &ndash; движок, которым обучаем модель. Поддерживаемые движки: _catboost_, [_tlm_](https://wiki.yandex-team.ru/users/stepych/TLM/).
- **fit_args** &ndash; здесь описываются параметры обучения для данной модели.
- **factors_info** &ndash; здесь описываются используемые факторы, а также их типы.
- **init** &ndash; до того, как модель будет обучена, она будет прогнозировать стратегией, указанной в данной секции.

    <font color="red">Важно: </font> при использовании режима _wang_ необходимо проинциализировать все компоненты. При использовании режимов из семейства покоординатного спуска необходимо проинициализировать все компоненты, кроме первой.


## init-секция

Модель можно проинициализировать тремя способами:
- константой:
    ```
    type: constant
    params:
        value: 1
    ```
- полем
    ```
    type: field
    params:
        name: PositionCTRCorrection
    ```
- дампом из sandbox
    ```
    type: dump
    params:
        task_id: %%task_id%%
        last_log:date %%last_log_date%%
        activation: exp
    ```
  Поле **activation** может принимать два значения: _exp_ и _sigmoid_.
