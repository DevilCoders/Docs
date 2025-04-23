# QR Image Decoder

Утилита, использующая декодер QR кодов Ya для декодинга изображений.

## I/O
**На входе** подаётся файл со списком изображений для парсинга.
```text
frame1.jpeg
frame2.jpeg
```

**На выходе** - JSON с кодами на каждом изображении
```json
[
  {
    "file": "frame1.jpeg",
    "codes": [
      "12345678",
      "qweqwe"
    ]
  },
  {
    "file": "frame2.jpeg",
    "codes": [
    ]
  }
]
```

## Запуск скрипта
После запуска `ya make` мы получаем бинарный скрипт, который можно запускать локально.

Для запуска привожу пример скрипта запуска из коммандной строки:
```shell
./qr_image_decoder -i filelist_qr.txt -o result_decoding.json
```

Результат скрипта - `json` в указанный файл в следующем виде:
```json
{
  "/home/ilinvalery/dh2mp_16mm2/frame_00001.png": [
    "K20-01B1",
    "K19-02A2"
  ],
  "/home/ilinvalery/dh2mp_16mm2/frame_00002.png": [
    "K20-01B1"
  ],
  "/home/ilinvalery/dh2mp_16mm2/frame_00003.png": [
    "K20-01B1"
  ]
}
```
