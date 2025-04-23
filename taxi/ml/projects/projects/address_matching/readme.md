Current Flow of Training and Deploying Address Matcher:

1. Collect initial dataset like `//home/taxi_ml/dev/cc_address_matching/dataset-2022-04` with [YQL](https://yql.yandex-team.ru/Operations/Yl_9Xrq3k_zTCSNbcwjQeczkpuuoxg3ewigk9kJibjU=)
2. Perform data preparation with `data/pipeline.sh`
3. Launch `train.py` as `python -m projects.address_matcher.train`
4. Deploy new resource to [plotva](https://a.yandex-team.ru/arc_vcs/taxi/backend-py3/services/taxi-plotva-ml/taxi_plotva_ml/api/taxi_order_by_phone_match_address_v1.py)
