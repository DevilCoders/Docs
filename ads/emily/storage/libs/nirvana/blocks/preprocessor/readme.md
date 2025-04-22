# ML Storage Preprocessor

Препроцессор для обработки моделей ML_ENGINE перед загрузкой в ML Storage.

## Usage

```bash
# help
./preprocessor -h

# process
./preprocessor --path data.tar.gz --key vw_apc_model --version 2020-12-10T11:00:00 --model-bin-src matrixnet.info

# output data.tar.gz
```

## Structure

```bash
# Input
# data: data.tar.gz

data/
    <ml_engine_dump>

# process

data -> unpack -> build meta -> compress -> data.tar.gz

# Output
# data: data.tar.gz

data/
    dump/
        <ml_engine_dump>
    meta/
        meta.json
    model/
        model.bin  # matrixnet.info
```
