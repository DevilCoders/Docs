## Yawn+Multiclass
### Подготовка среды
1. `pip3 install -r requirements.txt`
2. Скачать данные [трейна](https://yc.yandex-team.ru/folders/foo6afjbeudn66li09nu/storage/buckets/taximl-datasets?key=signalq%2Fdatasets%2Fyawn%2F) и [валидации](https://yc.yandex-team.ru/folders/foo6afjbeudn66li09nu/storage/buckets/taximl-datasets?key=signalq%2Fgolden-set%2Fdata%2F) (нужны все файлы). Файлы **трейна** поместить в папку `local-data`
3. Для запуска обучения (в рабочей директории должны содержаться скачанные файлы):
```
python3 ml/projects/projects/signalq/learning/face_actions/yawn/training.py --train_h5 local-data/train.h5 --train_csv local-data/train.csv --val_h5 val.h5 --val_csv val.csv --epochs 30 --bs 128 --nw 16 --lr 0.001 --save_path tcn.onnx
```
## Запуск инференса модели мультикласса
[ссылка на модель](https://s3.mds.yandex.net/taxi-ml/signalq/models/face_actions/face_actions_model.onnx)
`python3 ml/projects/projects/signalq/learning/face_actions/inference.py --model_path=face_actions_model.onnx --vid_path=local/480p/yawn-5773.mp4`
