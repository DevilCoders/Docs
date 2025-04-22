# Toloka TSV to YT dataset converter

## Запуск
После сборки при помощи `ya make` утилиты, вы получите `toloka2yt` бинарь. Для его запуска используйте следующее:

```bash
./toloka2yt --config example_config.yaml
```

## Конфиг
Пример конфига представлен в `example_config.yaml`. Для наглядности, далее приводится конфиг с комментариями
```yaml
yt_cluster: arnold # Кластер (прокси)
yt_folder: //home/ymbot_dataset_keeper/dataset_05_22 # Папка на YT для сохранения данных
yt_table_name: test_script # Название таблицы в YT
yt_table_rewrite: true # Перезаписать существующий файл, если существует такой
yt_batch_size: 100 # Объём батча записи в YT
upload_mode: dataset # Режим записи - записать tsv или же преобразовать данные в датасет с бинарным изображением.
image_rescale: # Делать ли изменение размера в режиме записи dataset
  do: true # Флажок, который отвечает за рескейл
  width: 256 # Новая ширина изображения
  height: 256 # Новая высота изображения
toloka_files_tsv: # Пути к файлам для загрузки в YT
  - ./data/sample_1.tsv
  - ./data/sample_2.tsv
ignore_files_tsv: # Пути к файлам c system:itemId, которые стоит игнорировать при загрузке датасета
  - ./data/list_bad_samples_05_22_1.tsv
  - ./data/list_bad_samples_05_22_2.tsv

```
