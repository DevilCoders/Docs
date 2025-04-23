# ml_enigine_transfer

Скрипт перекладывает модели формата ML_ENGINE_DUMP в формат ML_STORAGE_DUMP. 

usage:

```sh
ya make -r --yt-store
./transfer <path> --fetch-models
```

__path__ - это директория, где лежат дампы матрикснетов. По дефолту имеет значение "__models__". Если дампов нет, нужно запустить фечтер дампов с помощью флага __--fetch_models__, тогла по пути __path__ будут скачены дампы всех продовых матрикснетов.
