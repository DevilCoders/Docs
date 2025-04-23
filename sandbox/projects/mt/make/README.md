Задачи, необходимые для пайплайна сборки машинного перевода.

Проверка изменений в моделях:
* [CHECK_MTDATA](check_mtdata/README.md) - проверка валидности изменений, закоммиченных в [data.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/dict/mt/data.yaml).
* [EVAL_MTDATA](eval_mtdata) - оценка качества направлений, изменившихся в [data.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/dict/mt/data.yaml).

Обучение и оценка новых направлений:
* [PREPARE_NMT_RUN](prepare_nmt_run) - создание ветки эксперимента с генерацией изменений.
* [TRAIN_NMT](train_nmt/README.md) - запуск обучения перевода из указанной ветки.
* [EVAL_NMT](eval_nmt/README.md) - запуск обучения перевода из указанной ветки.

Другие:
* [DOWNLOAD_OPUS](download_opus) - скачивание корпусов с [Opus](https://opus.nlpl.eu/) на [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/mt/data/opus).
