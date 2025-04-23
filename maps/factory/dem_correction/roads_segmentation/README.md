Здесь находятся тулы для обучения нейронной сети для сегментации дорог на спутниковых снимках:
- data_gen -- тул для генерации обучающего датасета
- train -- тул для запуска обучения

## Формат датасета

Датасет хранится в формате  [TFRecord](https://www.tensorflow.org/tutorials/load_data/tfrecord) и представляет собой бинарный файл, в котором последовательно записаны protobuf-сообщения [tensorflow.Example](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/libs/tf/tensorflow/core/example/example.proto?rev=3997277#L88).

Каждый из `tensorboard.Event` в датасете содержит пару изображений одинакового размера: `sat` -- 3-канальное изображение спутникового снимка, `mask` -- 1-канальное изображение визуализации дорог.
```
{
    features {
        feature {
            key: "sat"
            value { bytes_list {
                value: "JPEG image"
            }}
        }
        feature {
            key: "mask"
            value { bytes_list {
                value: "JPEG image"
            }}
        }
}
```

## Генерация датасета

Тул для генерации датасета находится в директории `data_gen`, принимает на вход geojson-файл с полигонами регионов, для которых нужно сгенерировать датасет. В качестве источника спутниковых снимков используется опубликованный растровый тайловый спутниковый слой Яндекса.  Поддерживаются два варианта источников масок дорог:
- каартографические данные из YMASPDF (из YT-таблиц)
- из растрового тайлового слоя визуализации автомобильных треков

Пример запуска:
```
./datagen/data_gen --locations moscow.geojson --out moscow_gps_17.dataset --zoom 17 --roads-source gps
```

## Обучение сети

### Структура сети

![Структура сети Unet](https://jing.yandex-team.ru/files/dolotov-e/unet.png)

Для нахождения дорог используется сеть, описанная в статье U-Net: Convolutional Networks for Biomedical Image Segmentation (Unet, https://arxiv.org/pdf/1505.04597.pdf).

Сеть Unet состоит из 4 стадий со свертками, после которых следуют слои с max pooling. Это позволяет снизить размер изображения в 16 раз. За четвертой стадией следуют еще две свертки. После этих сверток изображение начинает увеличиваться при помощи deconvolutinal слоев в 2 раза. После каждого увеличения выполняются еще две свертки. Особенностью архитектуры Unet является то, что к результату каждого deconvolution слоя присоединяется результат одной из первых четырех стадий. В конце выполняется свертка с ядром 1x1 и количеством каналов k, где k - число различных классов объектов.

Общая ошибка сети - сумма ошибок на всех ветках. Ошибка на одной ветке считается следующим образом:

![Функция ошибки](https://jing.yandex-team.ru/files/dolotov-e/iou_1.png)

![Функция ошибки](https://jing.yandex-team.ru/files/dolotov-e/iou_2.png)


Процедура обучения поддерживает сохранение промежуточных состояний, она дружественна к перезапускам.
Также реализована возможность сохранения лога обучения в формате Tensorboard.

### Локальный запуск

Сборка:

`ya make -r`

Запуск:

`./train --train-config config.yaml --dataset-path ../data_gen/birulevo.dataset  --snapshot-path snapshot --model-path model.gdef --epoch-end 2 train_inside_yt`

### Запуск на YT на GPU

Сборка:

`ya make -r -DTENSORFLOW_WITH_CUDA=1 -DCUDA_VERSION=10.1 -DNO_DEBUGINFO`

Запуск:

`LD_LIBRARY_PATH=~/cuda_libs/lib64/:~/cuda_libs/lib64/stubs/ ./train --train-config config.yaml --dataset-path ../data_gen/moscow_gps_17.dataset --epoch-end 200  --model-path //tmp/quoter/road_segmentation/model --snapshot-dir //tmp/quoter/road_segmentation/snapshots --summary-logs-dir tb_logs train_over_yt -d //tmp/quoter/road_segmentation --gpu-count 4`

### Визуализация процесса обучения в tensorboard

Установка
`sudo apt-get install pip`
`pip install tensorflow`

Запуск:
```
TB_HOME=`pip show tensorboard | grep Location | cut -f2 -d' '`
python ${TB_HOME}/tensorboard/main.py --logdir tb_logs
```
