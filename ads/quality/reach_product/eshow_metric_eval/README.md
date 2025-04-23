# Offline-метрики EShow-моделей на одном наборе данных

Строит Nirvana-граф для оценки качества работы EShow-моделей, обученных на разных наборах данных. Написано аналогично [eshow_graph_launcher](https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/reach_product/eshow_graph_launcher).

Основные аргументы:
+ `--conf` – путь к конфигу, можно использовать таски eshow_graph_launcher;
+ `--resource-id` – Resource ID модели в Sandbox, можно указывать несколько через `,`;
+ `--experiments-id` – ID эксперимента, будет взята последняя (по атрибуту `last_log_date`) модель из Sandbox;
+ `--ab-testids` – testids AB-эксперимента, будет взята последняя (по атрибуту `last_log_date`) модель из Sandbox;
+ `--use-pools` – путь к подготовленному обучающему набору данных;
+ `--use-yql-pool` – путь к подготовленной YQL выборке, будут посчитаны `RSYAFactors`, `QID` и `train/test split`;
+ `--timestamp` – timestamp правой границы для сбора данных;
+ `--train-days` – число дней (период) сбора данных, назад от `timestamp`;
+ `--train-folds`, `--val-folds` – train/test соотношение данных;
+ `--multi-target` – если опция активирована, будет добавлена бинаризация таргета [0, 1] -> {0, 1};
+ `--plot-eshow-hist` – если опция активирована, будет построена HTML EShow-гистограма (Plotly);
+ `--nirvana-secret` – имя секрета в SecretsNirvana;
+ `--project-code` – код проекта в Nirvana, в котором будет построен граф;
+ `--graph-name` – название workflow;
+ `--no-start` – если опция активирована, граф будет построен в Draft-режиме, иначе сразу запустится;

Пример запуска:

`./eshow_metric_eval --conf tasks/EShow_Media_LClick_BannerID_UniqID_QSoftMax.yml --nirvana-secret aberezniker_ml_engine_app_token --timestamp 1614546000 --no-start --project-code berezniker_junk --resource-id 2001817727,2001817727 --train-days 28 --plot-eshow-hist`
