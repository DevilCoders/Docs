# Binary Road classifier
[MAPSMRC-559](https://st.yandex-team.ru/MAPSMRC-559)

## Model

Classifier uses __AlexNet__ architecture with the following graph:


Tensor graph:
* Tensor("mul:0", shape=(?, 224, 224, 3), dtype=float32)
* Tensor("conv1/conv1:0", shape=(?, 56, 56, 32), dtype=float32)
* Tensor("pool1:0", shape=(?, 27, 27, 32), dtype=float32)
* Tensor("conv2/conv2:0", shape=(?, 27, 27, 48), dtype=float32)
* Tensor("pool2:0", shape=(?, 13, 13, 48), dtype=float32)
* Tensor("conv3/conv3:0", shape=(?, 13, 13, 64), dtype=float32)
* Tensor("conv4/conv4:0", shape=(?, 13, 13, 64), dtype=float32)
* Tensor("conv5/conv5:0", shape=(?, 13, 13, 48), dtype=float32)
* Tensor("pool5:0", shape=(?, 6, 6, 48), dtype=float32)
* Tensor("fc1/fc1:0", shape=(?, 256), dtype=float32)
* Tensor("fc2/fc2:0", shape=(?, 256), dtype=float32)
* Tensor("y/MatMul:0", shape=(?, 2), dtype=float32)

After `fc1` and `fc2` layers dropout is used.

Model uses batch normalization with parameters described below.

## Dataset
Training dataset for _road_ and _not road_ classes contains 86,000 images each.

Validation dataset for _road_ and _not road_ classes contains 10,000 images each.

There are 2 forms of datasets:
* Initial (raw) dataset: [traning dataset (raw)](https://nirvana.yandex-team.ru/data/fc66f3b1-2373-421d-9d51-4e1039f6a077) and [testing dataset (raw)](https://nirvana.yandex-team.ru/data/52ec3697-29f8-4d6f-8857-20d88c448775)
* Equalized dataset produced from raw by applying histogram equalization to every image: [traning dataset (equalized)](https://nirvana.yandex-team.ru/data/5cd7c8f3-876a-4123-83cc-b2cb1763cc30) and [testing dataset (equalized)](https://nirvana.yandex-team.ru/data/0dc7b04b-d61e-46d9-9b9a-097db448c397)

Dataset uses:
* _road_ images are taken from our MDS database
*  _not road_ images are taken from [Open Images Dataset](https://github.com/cvdfoundation/open-images-dataset#download-full-dataset-with-google-storage-transfer)

## Learning
Nirvana operation used for tranining:
[Road binary classifier v0.40](https://nirvana.yandex-team.ru/operation/cd730ed1-ab4c-4165-b6af-8b2c35aeabda)

Last used learning parameters:
```
{
    "lr_base": 0.001,               # Base learning rate
    "lr_decay_rate": 0.96,
    "lr_decay_times": 4,
    "lr_decay_staircase": true,
    "optimizer": "Adam",
    "momentum": 0.9,                # Parameter for MomentumOptimizer
    "adam_beta1": 0.9,              # -|
    "adam_beta2": 0.999,            #  -> Parameters for AdamOptimizer
    "adam_epsilon": 0.1,            # -|
    "iter_cnt": 2000000             # Number of total iterations for traning
    "log_step": 1000,
    "validate_on_n_log": 10,
    "batch_size": 64,
    "validation_batch_size": 256,
    "cross_validation": false,
    "cross_validation_folds": 5,
    "data_split": 1,                # Percent of data to use for training
    "keep_prob": 0.5,               # Dropout keep probability
    "use_batch_norm": true,
    "bn_epsilon": 0.001,
    "bn_decay": 0.9,
    "random_state": null,           # value for numpy.random.seed
    "shuffle_data": false,          # weather to shuffle the data loaded from disk
}
```
