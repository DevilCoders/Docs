# Папка с данными для запуска Inventory MVP APP (Python version)

Текущая структура каталога `data` следующая, позволяет запускать тесты и запускать проект на Jetson:

```
.
├── decoder
│   ├── config.yaml
│   ├── detect.caffemodel
│   ├── detect.prototxt
│   ├── sr.caffemodel
│   ├── sr.prototxt
│   └── test_decode_image.png
├── detector
│   ├── config.yaml
│   ├── pltdet_train_v2.3.1_512.pb
│   ├── pltdet_train_v2.3.4_256.pb
│   ├── test_detect_image.jpeg
│   ├── test_image_2.jpeg
│   └── test_image_vis.jpeg

├── gt_dataset
│   ├── ride_left_backward
│   ├── ride_left_forward
│   ├── ride_right_backward
│   └── ride_right_forward
└── results
```
