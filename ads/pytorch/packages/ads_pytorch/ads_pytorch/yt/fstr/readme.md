Как пользоваться?

в ~/.bashrc добавить удобную команду

```bash
alias torch_fstr='ADS_PYTORCH_BUILD_DIR=~/torch_build_dir/ python ~/arcadia/ads/pytorch/packages/ads_pytorch/ads_pytorch/nirvana/wrapper.py /dev/null --entry_point ads_pytorch.yt.fstr.entry_point'
```

Дальше запускаем локально командой
```
CUDA_VISIBLE_DEVICES=3 torch_fstr --conf <путь к конфигу проверки>.json --out <папка с результатами проверки>
```

Json конфиг проверки (пример 1) c автоматическим выводом таблицы и списка факторов:
```json
{
  "model_yt_dir": "//home/ads/ltp/users/jruziev/online_learning/experiments/spynet_v5/v2_lclick_v2_simplebowrvCEsmall6_2_d0.001_s0.001/model"
}
```

Json конфиг проверки (пример 2) c автоматическим выводом таблицы (num_batches можно и не указывать):
```json
{
  "model_yt_dir": "//home/ads/ltp/users/jruziev/online_learning/experiments/spynet_v5/v2_lclick_v2_simplebowrvCEsmall6_2_d0.001_s0.001/model",
  "factors": [
    "BannerID__minshows",
    "OrderID"
  ],
  "num_batches": 1000
}
```

Json конфиг проверки (пример 3):
```json
{
  "model_yt_dir": "//home/ads/ltp/users/jruziev/online_learning/experiments/spynet_v5/v2_lclick_v2_simplebowrvCEsmall6_2_d0.001_s0.001/model",
  "tables": {
    "train": {
      "name": "//home/ads/ltp/users/jruziev/nomzod/v2_extended3/spynet_clickshows_lclick.train.batch",
      "lower_key": "202111051700",
      "upper_key": "202111051955"
    },
    "test": {
      "name": "//home/ads/ltp/users/jruziev/nomzod/v2_extended3/spynet_clickshows_lclick.val.batch",
      "lower_key": "202111052100",
      "upper_key": "202111060000"
    }
  },
  "factors": [
    "BannerID__minshows",
    "OrderID"
  ]
}
```

Иногда нужно перемешивать группу факторов целиком. Например, в трансформере SeqLen и последовательность нужно вместе перемешивать.
Json конфиг проверки (пример 4), группы факторов:
```json
{
    "model_yt_dir": "//home/advquality/users/sbkarasik/TsarPyTorchBkoPclick/models/model_v2_banner_bow_sample",
    "num_batches": 1000,
    "factors": [
        "UserRegionID",
        "ImageAvatarsEmbeddingI2T",
        [  // описание группы факторов, список из двух элементов: название группы, факторы
            "BigBQueryTransformer",  // название, влияет только на имя ключа в итоговом dict с метриками
            [  // факторы в группе 
                "BigBQueryTexts",
                "BigBQuerySelectTypes",
                "BigBQueryFactors",
                "BigBQuery_SeqLen"
            ]
        ]
    ]
}
```

Чтобы запустить на нирване, нужно собрать ads/pytorch/packages/ads_pytorch/ads_pytorch/yt/fstr/run и вызвать его с конфигом:
```bash
ya make -r && ./run --conf <conf.json>
```

Пример <conf.json>:
```json
{
  "model_yt_dir": "//home/ads/ltp/users/jruziev/online_learning/experiments/spynet_v5/v2_lclick_v2_simplebowrvCEsmall6_2_d0.001_s0.001/model",
  "factors": [
    "BannerID__minshows",
    "OrderID"
  ],
  "num_batches": 1000,
  "nirvana": {
        "quota": "ads-deep-learning",
        "project": "jruziev_torch",
        "yt_pool": "ads-research",
        "yt_proxy": "hahn",
        "secret": "jruziev_ml_engine_app_token"
    }
}
```

*Note*: сейчас в `vh` поломана поддержка `project`, вместо этого используйте `workflow_ns_id`.
[Подробнее про workflow_ns_id](https://a.yandex-team.ru/arc/trunk/arcadia/nirvana/valhalla/docs/reference/run_kwargs.md#workflow_ns_id=). Пример:
```json
{
    "model_yt_dir": "//home/advquality/users/sbkarasik/TsarPyTorchBkoPclick/experiments/model_v2_may/ads_pytorch_embeddings",
    "num_batches": 1000,
    "nirvana": {
        "quota": "ads-deep-learning",
        "workflow_ns_id": 11203579,
        "yt_pool": "ads-research",
        "yt_proxy": "hahn",
        "secret": "sbkarasik_ml_engine_app_token"
    },
    "factors": [
        "UserRegionID",
        [
            "DocumentHistoryTransformer",
            [
                "DocumentHistoryTitles",
                "DocumentHistoryFactors",
                "DocumentHistory_SeqLen"
            ]
        ]
    ]
}
```
