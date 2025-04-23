# Библиотека для прогноза на основе torch

## Способ запуска на нирване

Все файлы библиотеки доставляются на машину с помощью ресурсов
(``library.python.resource``),
и на машине в облаке генерируется скрипт ``run_torch.py``, в начало которого
копируются все файлы библиотеки, указанные в функции ``import_resources``:

```python
from market.monetize.stapler.v1.tasks.torch import TorchTask
class MyTorchModelTask(TorchTask):
    # ...

    @staticmethod
    def import_resources():
        """
            List of resources to take source from for final torch_script (see tasks/torch.py)
        """
        return [
            "util.py",
            "target_transforms.py",
            "features_transforms.py",
            "losses.py",
            "nets.py",
            "feature_sets.py",
            "base_torch_model.py"
        ]
```
Все эти файлы должны быть добавлены как ресурсы в файле ``ya.make``:
```yamake
RESOURCE(
    data_preparation/torch_lib/util.py util.py
    data_preparation/torch_lib/target_transforms.py target_transforms.py
    data_preparation/torch_lib/features_transforms.py  features_transforms.py
    data_preparation/torch_lib/feature_sets.py feature_sets.py
    data_preparation/torch_lib/losses.py losses.py
    data_preparation/torch_lib/nets.py nets.py
    data_preparation/torch_lib/base_torch_model.py base_torch_model.py

)
```

## Как использовать
1. Определить нужный Loss в ``losses.py``, придумать ему короткое имя и
возвращать из функций ``get_loss_fn`` и ``get_epoch_loss_fn``

1. Определить нужную архитектуру сети в nets.py, придумать ей короткое имя
   и возвращать в функции ``get_network``

1. Определить нужные ``target_transform`` и ``features_transform``
   в ``target_transforms.py`` и ``features_transforms.py``,
   опять же придумать им имена, и добавить
   в словари ``feature_sets``, ``target_transforms``.

1. Создать объект модели и вызывать метод ``fit``
```python
    from ..torch_lib.base_torch_model import BaseTorchModel
    model = BaseTorchModel(
        net_type='МОЯ_СЕТКА', # можно взять 'l7' или 'dn1'
        loss='МОЙ_LOSS',      # можно взять 'rmse'
        loss_args={'ПАРАМЕТРЫ': 'LOSS'},
        target='НАЗВАНИЕ_ПОЛЯ_С_ТАРГЕТОМ',
        epochs=4,
        batch_size=3000,
        target_transform='МОЙ TT',
        feastures_transform='МОЙ FT',
    )
   train_loss, valid_loss = model.fit(train_dataset, valid_dataset)
````
1. Для сохранения модели на YT вызывать ``model.save_model_yt(yt_path)``

1. Для восстановления модели из файла на YT нужно создать модель и вызвать ``load_model_yt``:
````python
model = BaseTorchModel( ... )
model.load_model_yt(yt_path)
````

## Простой пример кода обучения

````python
from ..torch_lib.base_torch_model import BaseTorchModel
hyperp = {
    'net_type': 'dn1',
    'flt_feature_set': 'f1',
    'loss': 'rmse',
    'epochs': 6,
    'learn_rate': 0.001,
    'batch_size': 3000,
    'curve_step': 250000,
    'target_transform': 'log_1',
    'target': 'd7_avg_target',
    'target_dim': 1,
}
seed = 1234
model = BaseTorchModel(**hyperp)

for j in range(10):
    model.random_state = j + seed
    print(f"\n\nSTEP {j}")

    tr_loss, v_loss = model.fit(
        train_df, test_df,
        calc_metrics=False,
    )
    print(f"Last valid_loss = {v_loss}")
````

## Более сложный пример кода обучения персональной эластичности

   ```python
flt_feature_sets = {
    'base': ['rel_price'],
    'f1': ['rel_price', 'log_msku_r_d42_items']
}

cat_feature_sets = {
    'base': [
        ('msku', 0, 3), ('demand_class', 0, 3),
        ('prism_segment', 0, 3), ('cluster', 0, 3), ('province_name_hash', 0, 3)
    ],
    'c1': [
        ('msku', 0, 3), ('hid', 0, 3), ('model_name_hash', 0, 3), ('demand_class', 0, 3),
        ('prism_segment', 0, 3), ('cluster', 0, 3), ('province_name_hash', 0, 3),
        ('children_segment_hash', 0, 3), ('market_segment_hash', 0, 3),
        ('platform2_hash', 0, 3),
    ],
}

super_feature_sets = {
    'base': ['shuffled_rel_price_1', 'shuffled_rel_price_2']
}

hyperp = {
    'net_type': 'dn1',
    'flt_feature_set': 'f1',
    'cat_feature_set': 'c1',
    'super_feature_set': 'base',
    'loss': 'rmse',
    'epochs': 6,
    'learn_rate': 0.0003,
    'sample_num': 5000000,
    'batch_size': 6000,
    'curve_step': 250000,
    'target': 'target',
    'train_type': 'replace_first_by_super',
    'cat_dropout_ratio' : 0.03,
}

seed = 1234

if model is None:
    model = BaseTorchModel(**hyperp)
else:
    model.update(**hyperp)


for j in range(10):
    level = 0.99 if j < 4 else 0.995

    if j == 0:
        stop_valid_loss = None
    else:
        stop_valid_loss = (
            level * best_model.last_valid_loss if (best_model and best_model.last_valid_loss) else stop_valid_loss0
        )

    model.random_state = j + seed
    print(f"\n\nSTEP {j}")
    print(f"Failed_passes = {failed_passes}\n")
    print(f"Stop valid_loss = {stop_valid_loss}")

    tr_loss, v_loss = model.fit(
        train_df, test_df,
        calc_metrics=False, stop_valid_loss=stop_valid_loss
    )
    print(f"Last valid_loss = {v_loss}")

    if (
        best_model is None
        or best_model.last_valid_loss is None
        or best_model.last_valid_loss > model.last_valid_loss
    ):
        best_model = deepcopy(model)
        failed_passes = 0
    else:
        failed_passes += 1

    if model.train_samples > 50_000_000:
        break
   ```

## Описание основных параметров

Параметры задаются в конструкторе. Их можно обновлять с помощбю метода ``update``.
1. ``net_type`` – имя архитектуры сети, например, 'l5', 'l7', 'dn1', 'sn'.
   Важным шагом при обучении является нормализация фичей. Этот шаг встроен в предопределенные
   нейросети с помощью слоя DatasetNormalization, но для того, чтобы он сработал, при
   создании сети с помощью ``get_network`` необходимо передавать в первом аргументе трейн сет.
   Это и делается внутри ``BaseTorchModel.fit``.
1. ``loss`` – имя loss-функции. Есть много предопределенных функций:
    1. 'rmse' – классический MSELoss
    1. 'sq' – SmoothQLoss, сглаженный квантильный loss, в параметре ``loss_args`` нужно задать
       значения ``beta`` (сила сглаживания) и ``qx`` (квантиль),
    1. 'exp_sq' – ExpSmoothQLoss – это SmoothQLoss, который применяется к exp(target) и exp(predict).
    1. 'sw' – SmoothWapeLoss
    1. 'ex' – ExpectileLoss
    1. 'sl1' – SmoothL1Loss
    1. 'll' – BCEWithLogitsLoss
    1. 'v1a' – SmoothL1Loss + m * Bias, Bias = (target - predict).mean, m = 2 * qx - 1.
       При этом этот лосс адаптивный – сила сглаживания зависит от эпохи.
       В параметре ``loss_args`` нужно задать значения
       ``beta`` (конечной силы сглаживания),
       ``beta_wu`` (начальной силы сглаживания)
       и ``qx`` (квантиль).

1. ``loss_args`` – словарь с параметрами-loss функции
1. ``target`` – имя поля, в котором находится таргет
1. ``target_dim`` – размерность таргета (если > 1, то в таргете должен быть массив соответствующей  длины)
1. ``target_transform`` – имя target_transform
1. ``features_transform`` – имя features_transform
1. ``learn_rate``
1. ``flt_feature_set``
1. ``cat_feature_set``
1. ``super_feature_set``
1. ``epochs`` – сколько эпох обучать сетку (параметр конструктора)
1. ``train_type`` – хитрые методы обучения
    1. `replace_first_by_super` – режим для обучения персональной эластичности, когда мы обучаем
       покупки против покупок, в которых rel_price взят из чужих покупок. По сути происходит
       дополнение трейн бачей их копией, в которой первая фича заменяется на
       первую или вторую фичу из super-фичей и при этом у таргета (в этой копии) меняется знак.

    1. `shuffle_first` – происходит
       дополнение трейн бачей их копией, в которой первая фича шафлится и при этом
       у таргета (в этой копии) меняется знак.
