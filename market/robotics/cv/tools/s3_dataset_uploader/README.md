# S3 Dataset Uploader

Инструмент для загрузке изображений/файлов из папки в S3. Поддерживает регулярки.

Пример использования:
```bash
 ./s3_dataset_uploader \
     --bucket mr-toloka-images \
     --key-id <key_id> \
     --secret-key <secret_key> \
     --folder-upload "/Users/ilinvalery/Developer/parsed/*/*/*.jpeg" \
     --folder-aws PLTDataset0522/all_frames_jpeg
```

Скрипт считывает файлы по указанной маске и загрузит их в указанный бакет в указанную папку. Прогресс отслеживается при помощи `tqdm`
