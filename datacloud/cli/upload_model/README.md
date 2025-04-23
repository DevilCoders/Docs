# Upload Model

Консольная утилита для раскатки нового бинарника модели в прод. 

## Выполняет следующие действия:
- Из входной таблицы подготавливает батч для batch_monitoring
- Загружает бинарник модели с локальной машины в нужное место на YT и выставляет симлинк на него
- Добавляет строчку в [api_models_config](https://yt.yandex-team.ru/hahn/navigation?path=//home/x-products/production/config/datacloud/api-models-config&offsetMode=key) на YT
- Добавляет строчку в [score_path](https://ydb.yandex-team.ru/db/ydb-ru/impulse/production/xprod-scoring-api-db/browser/score_api/config/score_path) в YDB
- Добавляет партнеру internal доступ до нового скора в таблице [partner_scores](https://ydb.yandex-team.ru/db/ydb-ru/impulse/production/xprod-scoring-api-db/browser/score_api/config/partner_scores)

## Важно помнить:
- В raw таблице вашего тикета таргет должен быть **строго** бинарный
- yql token можно положить в переменную окружения **YQL_TOKEN** или вместо вашего ключа от yt в `~/.yt/token`

## Параметры бинарника
- `-h, --help` Вызвать хэлп
- `-p <PARTNER_ID>, --partner-id <PARTNER_ID>` <Required> (например bank_mega_capital, sberkoff)
- `-s <SCORE_NAME>, --score-name <SCORE_NAME>` <Required> Score name (например bmc_aml_xprod_1103, sberkoff_xprod_889_20180508)
- `-l LOCAL_BINARY, --local-binary LOCAL_BINARY` <Required> Path to local binary (**путь на локальной машине!**)
- `-c MODEL_CLASS, --model-class MODEL_CLASS` <Required> Model class (может быть PredictModel или PredictProbaModel; определяет, делать predict или predict_proba)
- `-f LIST_OF_FEATURES, --features LIST_OF_FEATURES` <Required> Features (например `DSSMFeatureBase400 ClusterFeatureBase767`; **порядок важен!**)
- `r PATH_TO_RAW, --path-to-raw PATH_TO_RAW` Path to raw table for batch prepare (можно не указывать)
- `-a AUC_THRESH, --auc-thresh AUC_THRESH` AUC threshold for batch monitoring (по умолчанию 0.6)
- `-i HIT_THRESH, --hit-thresh HIT_THRESH` Hit threshold for batch monitoring (по умолчанию 0.6)
- `-t TARGET, --target TARGET` Target field name for batch monitoring (по умолчанию "target")
- `-y YT_BINARY_NAME, --yt-binary-name YT_BINARY_NAME` YT binary name (имя бинарника на YT; по умолчанию совпадает с именем локального файла)
- `--not-active` Раскатить модель, но сделать ее неактивной
- `--save-info` При раскатке сохранять фичи и другую сопутствующую информацию (полезно, например, для tcs)
- `--cookie-sync-on` Будет ли партнер пользоваться cookie-sync (добавляет хэш от cid в раскатываемый скор)
- `--transfer-off` Выключить регулярную отгрузку скора на YDB
