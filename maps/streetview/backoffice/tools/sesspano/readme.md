# sesspano - Интеллектуальное построение связей панорам

## Назначение

    Построение связей панорам с помощью машинного обучения. Основные функции:
    * построение связей с использованием встроенной модели Catboost;
    * создание датасета для обучения модели Catboost или её применения;
    * создание easyview-файлов приматчивания панорам к графам (дорожному и пешеходному).

## Как запускать (sesspano -h)

    Usage: sesspano <input_dir> [<output_dir>] [options]

      <input_dir>   should contain session xml files and possibly reference.tsv
      <output_dir>  will contain links.tsv and other output files
                    if omitted, <input_dir> is used

    Allowed options:
      -h [ --help ]         produce help message
      -a [ --age ] arg (=6) overlapped age in months
      -d [ --dataset ]      create dataset.cd/.tsv and dataset_links.tsv possibly
                            using reference.tsv (zero labels if not provided)
      -e [ --easyview ]     create <graph_code>.ev files to debug graph matching

## Примеры запуска

    sesspano -h
    sesspano /path/to/work/dir -de
    sesspano /path/to/input/dir /path/to/output/dir -d -e

## Входные данные

    В <input_dir> должны содержаться файлы с сессиями в формате XML: <session_name>.xml
    Если нужен датасет для обучения модели, следует положить файл reference.tsv
    со связями из базы в формате TSV ("src\_filename\\tdst\_filename\\n").

## Выходные данные

    В <output_dir> после окончания работы программы будут помещены следующие файлы:

    * links.tsv - результируюшие связи, в формате TSV.

    Если указана опция -d [ --dataset ], то будут созданы следующие файлы:

    * dataset.tsv - датасет для обучения модели CatBoost;
    * datacet.cd - описания колонок датасета;
    * dataset\_links.tsv - все связи датасета в формате TSV.

    Если указана опция -e [ --easyview ], то будут созданы следующие файлы:

    * <graph_code>.ev - easyview-файл с результатами приматчивания к графу для определённого графа и дистанции связывания.

