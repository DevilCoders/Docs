# PLT Detector->Decoder pipeline on one image

## Запуск скрипта

После запуска `ya make` мы получаем бинарный скрипт, который можно запускать локально.

Перед запуском скрипта необходимо подготовить данные В примере ниже указанной папке `/home/ilinvalery/pltdet_test/`:

```
.
├── pltDetectorConfig.json
├── plt_det_v1.pb
└── test_image_2codes.jpg
```

### Обычный запуск (вывод в консоль)

Пример скрипта запуска из коммандной строки:

```shell
./one_image_registrator -d /home/ilinvalery/pltdet_test/ -i /home/ilinvalery/pltdet_test/test_image_2codes.jpg
```

Результат скрипта - `json` в `stdout` поток в следующем виде:

```json
{
  "/home/ilinvalery/pltdet_test/test_image_2codes.jpg": [
    {
      "Box": {
        "Left": 861.185,
        "Top": 612.63,
        "Width": 123.786,
        "Height": 110.886
      },
      "Score": 0.478862,
      "RecognitionResult": "PLT10398",
      "CodeType": "PLT"
    },
    {
      "Box": {
        "Left": 746.843,
        "Top": 43.8536,
        "Width": 114.492,
        "Height": 116.957
      },
      "Score": 0.474238,
      "RecognitionResult": "PLT10395",
      "CodeType": "PLT"
    }
  ]
}
```

## Запуск с отправкой JSON на конкретный endpoint

Пример скрипта запуска из коммандной строки:

```shell
./one_image_registrator -d /home/ilinvalery/pltdet_test/ -i /home/ilinvalery/pltdet_test/test_image_2codes.jpg --send-api --url http://127.0.0.1:8080/test_view
```

В данном случае результат в виде JSON отправится на указанный endpoint в виде POST запроса. В консоли будет сообщение об
успешной отправки данных:

```bash
Result was successfully sent to http://127.0.0.1:8080/test_view
```

## Конфиг

Для использования скрипта необходимо наличие обученной сети и конфига файла. Конфиг `pltDetectorConfig.json` выглядит
следующим образом:

```json
{
  "NetworkParams": {
    "GraphFilePath": "plt_det_v1.pb",
    "ImageSize": 256,
    "HeadName": "pltlabels"
  },
  "RuntimeParams": {
    "NumInterThreads": 1,
    "NumIntraThreads": 4,
    "DeviceId": -1,
    "AllowSoftPlacement": true,
    "AllowGrowth": true
  },
  "FilteringParams": {
    "ConfidenceThreshold": 0.3,
    "NmsThreshold": 0.3,
    "MaxOutputSize": 5,
    "UseCorrection": true
  }
}
```

## Материалы для запуска

1. Для простоты использования рекомендуется скачать tar архив с тестируемыми данными:
   https://sandbox.yandex-team.ru/resource/3181445694/view
2. Для теста можно локально развернуть python сервер (предварительно установив `aiohttp`).
   Ресурс: https://sandbox.yandex-team.ru/resource/3181625778/view

