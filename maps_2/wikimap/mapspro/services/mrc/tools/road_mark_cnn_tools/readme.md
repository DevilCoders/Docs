### Подготовка датасета:

python ./mask_ds_from_json.py <path_to_json> <images_folder> <tfrecord_folder>

path_to_json     - путь к json, полученному из толоки с классифицированными разметками на BirdView
images_folder    - путь к папке с фотографиями. Название файла <feature_id>.jpg (скрипт файлы не качает, скачать надо заранее)
tfrecord_folder  - папка куда положат два файла train.tfrecord и test.tfrecord. Фотографии раскладываются в тренировочный или
                   тестовый датасет случайным образом (вероятность попасть в тренировочный набор определяется параметром
                   TRAIN_PART)

### Подсчет статистики на тестовом наборе

python ./eval.py <path_to_graph> <path_to_test_tfrecord>