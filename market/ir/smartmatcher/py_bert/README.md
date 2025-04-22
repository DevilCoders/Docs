# Smart Matcher

## FastText

#### Run on Nirvana with YT checkpoint saving

```bash
cd $SOURCE_CODE_PATH
export PYTHONPATH=$PWD
export VECTORS_PATH=$INPUT_PATH/vectors.bin
export WANDB_BASE_URL=http://sovetnik-analytics01hd.market.yandex.net:11000

python train_fasttext.py \
    --gpus=1 \
    --filename=$VECTORS_PATH \
    --save_dir=//home/sovetnik/seeall/smartmatcher/checkpoints \
    --save_to_yt=True \
    --logs_dir_name=$OUT_LOGS_PATH \
    --num_workers=30 \
    --max_epochs=100 \
    --m_samples_per_category=100 \
    --batch_size=1000 \
    --check_val_every_n_epoch=5 \
    --precision=32 \
    --deterministic=True \
    --benchmark=True \
```


#### Run on Nirvana with Local checkpoint saving

```bash
cd $SOURCE_CODE_PATH
export PYTHONPATH=$PWD
export VECTORS_PATH=$INPUT_PATH/vectors.bin
export WANDB_BASE_URL=http://sovetnik-analytics01hd.market.yandex.net:11000

python train_fasttext.py \
    --gpus=1 \
    --filename=$VECTORS_PATH \
    --save_dir=$TMP_OUTPUT_PATH \
    --logs_dir_name=$OUT_LOGS_PATH \
    --num_workers=30 \
    --max_epochs=100 \
    --m_samples_per_category=100 \
    --batch_size=1000 \
    --check_val_every_n_epoch=5 \
    --precision=32 \
    --deterministic=True \
    --benchmark=True \
```

## BERT

#### Run on Nirvana with YT checkpoint saving

```bash
cd $SOURCE_CODE_PATH
export PYTHONPATH=$PWD
export WANDB_BASE_URL=http://sovetnik-analytics01hd.market.yandex.net:11000

python train_bert.py \
    --gpus=1 \
    --bert_dir $INPUT_PATH/ \
    --batch_size 240 \
    --max_length 128 \
    --save_dir=//home/sovetnik/seeall/smartmatcher/checkpoints \
    --save_to_yt=True \
    --logs_dir_name=$OUT_LOGS_PATH \
    --num_workers=30 \
    --max_epochs=100 \
    --m_samples_per_category=100 \
    --batch_size=1000 \
    --check_val_every_n_epoch=5 \
    --precision=32 \
    --deterministic=True \
    --benchmark=True \
    --distributed_backend dp \
```


#### Run on Nirvana with Local checkpoint saving

```bash
cd $SOURCE_CODE_PATH
export PYTHONPATH=$PWD
export WANDB_BASE_URL=http://sovetnik-analytics01hd.market.yandex.net:11000

python train_bert.py \
    --gpus=1 \
    --bert_dir $INPUT_PATH/ \
    --batch_size 240 \
    --max_length 128 \
    --save_dir=$TMP_OUTPUT_PATH \
    --logs_dir_name=$OUT_LOGS_PATH \
    --num_workers=30 \
    --max_epochs=100 \
    --m_samples_per_category=100 \
    --batch_size=1000 \
    --check_val_every_n_epoch=5 \
    --precision=32 \
    --deterministic=True \
    --benchmark=True \
    --distributed_backend dp \
```

### For loading model's state stored on YT from previous runs, use the 'yt_checkpoint' flag:

```bash
python train_fasttext.py \
    --yt_checkpoint=//home/sovetnik/seeall/smartmatcher/checkpoints/...
```

## SplitBERT для переноса в YNMT
весь код с логикой формирования - в файле `ynmt_example.py` (код вне файла не нужен)
Версии библиотек:
transformers==3.0.2
torch==1.6.0
(код работает также и с версией торча выше, 1.7.1)
Подготовка: нужно скачать обычную модель с конфигом (для инициализации) и распаковать архив в папку data/
Ссылка на дату в нирване: [тык](https://nirvana.yandex-team.ru/data/7bbd832b-e0e2-4bf0-a878-5cf50e37486a)
И скачать обученные веса из нирваны в бинарном виде и положить  data/trained_weights.bin
ссылка: [тык](https://nirvana.yandex-team.ru/data/9eafc8c0-1145-4f3e-a260-0352488f287b)

Запуск:
```bash
export YT_TOKEN=<...>
export YT_PROXY=hahn.yt.yandex.net

python ynmt_example.py --bert_path data/ --state_path data/trained_weights.bin
```
После чего в `infer_results.json` будут записаны входы и выходы берта для отладки.

Про структуру кода:
Класс `SplitBert` содержит в себе две подмодели и общуюу логику графа исполнения

Функция `collate_splitbert_inference` - сбор в батче объектов (с формированием масок и паддингов). 
Токенизация происходит в `SplitYTPairsDataset`. Тут важно обратить внимание на то, что в каждой из последовательностей есть  CLS-токены в начале, и они без убирания подаются (после конкатенации) в общую шапку. Но классификация делается только по первому cls-токену, второй болтается сам по себе.
