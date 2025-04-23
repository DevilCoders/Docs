# Библиотека для обучения Catboost модели

### Как использовать:
- Сохраните ваш токен от нирваны в переменную окружения `NIRVANA_API_TOKEN`
- Добавьте в `peerdir` папку `maps/analyzer/pylibs/train_catboost`
- Создайте параметры катбуста (класс `CatboostParams` в `catboost_params.py`)
- Запустите функцию `train`. Переменная `yt_token` - название секрета с YT токеном в нирване. Модель будет загружена по пути, которую вы передали в параметр `model_dst_path`.


### Пример использования в `maps/analyzer/toolkit/repl`:

```ipython
In [1]: import maps.analyzer.pylibs.train_catboost as train

In [2]: from nirvana_api.blocks.catboost import CatboostLearningMethod  # need to set loss function

In [3]: learn_table = '//home/maps/jams/dev/users/gotocoding/small_tsv_table'; \
   ...: column_description = '0\tAuxiliary\n1\tLabel\n2\tDocId\n3\tAuxiliary\n'; \
   ...: yt_token = 'yt-token-gotocoding'; \
   ...: model_dst_path = '//home/maps/jams/dev/users/gotocoding/tmp_cb_model';

In [4]: p = train.CatboostParams(cpu_guarantee=1700, learning_rate=0.01, bootstrap_type=train.BootstrapType.Bernoulli, subsample=0.5, loss_function=CatboostLearningMethod.Regression.RMSE, gpu_type=train.GpuType.LAST, use_best_model
   ...: =True, border_count=128, ttl=14400, depth=6, has_time=True, iterations=10000, seed=42, random_strength=0, fstr_type=train.FstrType.PredictionValuesChange)

In [5]: train.train(learn_table=learn_table, column_description=column_description, learn_params=p, model_dst_path=model_dst_path, yt_token=yt_token)
INFO:nirvana_api.highlevel_api:Flow link: https://nirvana.yandex-team.ru/flow/9001de02-b673-47f7-95da-368728095596/graph
INFO:nirvana_api.highlevel_api:Flow was created
INFO:nirvana_api.highlevel_api:Validate flow: ok
INFO:nirvana_api.highlevel_api:Start flow: e6a202f7-8ae8-40cf-8dd0-8e8bd42360c0
INFO:nirvana_api.highlevel_api:Running flow: status undefined, progress 0.0, message None
INFO:nirvana_api.highlevel_api:Running flow: status running, progress 0.333333333333, message Finished 1/3.
INFO:nirvana_api.highlevel_api:Running flow: status running, progress 0.666666666667, message Finished 2/3.
INFO:nirvana_api.highlevel_api:Running flow: status completed, progress 1.0, message Finished 3/3.
INFO:nirvana_api.highlevel_api:End flow: {'status': u'completed', 'blocks': [], 'started': u'2019-11-21T17:36:19+0300', 'completed': u'2019-11-21T18:02:02+0300', 'workflowInstanceId': u'e6a202f7-8ae8-40cf-8dd0-8e8bd42360c0', 'result': u'success', 'progress': 1.0, 'message': u'Finished 3/3.', 'details': u'Waiting: 0 / Running: 0 / Succeeded: 3 / Failed: 0 / Cancelled: 0 / Skipped: 0'}
```
