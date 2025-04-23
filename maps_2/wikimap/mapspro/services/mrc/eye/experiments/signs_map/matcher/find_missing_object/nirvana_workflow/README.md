Описание графа Нирваны для обучения catboost-модели предсказания видимости знака на фото.

Как запустить:
```
ya make
VH3_PROFILE=./profile.yaml  ./train_predict_cluster_visibility run train_catboost_model
```
Эта команда запустит граф на опубликованных версиях операций, если же нужно запустить граф на версии операции с локальными изменениями, надо дополнительно выставить переменную окружения `VH3_DEV=1`.


Arcadia ci operations publishing tasks: https://a.yandex-team.ru/projects/maps-core-nmaps-mrc/ci/actions/launches?dir=maps%2Fwikimap%2Fmapspro%2Fservices%2Fmrc%2Feye%2Fexperiments%2Fsigns_map&id=auto-pack-nirvana-operations
