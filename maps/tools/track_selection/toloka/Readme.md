###Основные скрипты

##from_yql_to_tsv

Скрипт, который	 берет таблицу с интересными треками и делает из нее файл в формате .tsv который можно загрузить в толоку

./to_tsv --help
```
Usage: to_tsv [OPTIONS]

  Make .tsv file to toloka from table with interesting tracks in YT(table with result of find_tracks utility)

Options:
  --filename TEXT   name of result
  --tablename TEXT  table with interesting tracks  [required]
  --help            Show this message and exit.
```

##export_from_toloka
Толокеры разметили треки, мы от них получили файл assigments.tsv, данные в толоку были загружены из таблицы X, мы хотим загрузить результат в таблицу Y и нам нужны только те треки в которых за один из двух треков"проголосовало" не меньше P% толокеров, тогда мы делаем 
```
./to_yql --filename assigments.tsv --exit-table Y --start-table X --selection P

./to_yql --help

Usage: to_yql [OPTIONS]

  Utility to download matched by tolokers tracks in YT

Options:
  --filename TEXT               .tsv file from toloka  [required]
  --output-segments-table TEXT  output segments-table  [required]
  --output-signals-table TEXT   output signals table  [required]
  --start-table TEXT            table with rows in toloka  [required]
  --quorum  FLOAT               what percentage of same answers do we need
  --help                        Show this message and exit.

```

###Вспомогательные скрипты

##results_converter

Если хочется посмотреь на размеченные толокерами треки, то можно сделать:
```
./tolokaview --tolokafile assigments.tsv --exit-dir directory --selection P
```

После этого в директории directory появятся файлики trc*, которые можно открывать в easyview, файл statistic в котором в строке i написано сколько толокеров за какой вариант ответили для трека trc[i] и файл new_toloka_file с той же информацией, но на которую можно смотреть в толоке, в этом случае все эти задания будут считаться контрольными с помеченным ответом полученным от толокеров.

```
./tolokaview --help

Usage: tolokaview [OPTIONS]

  Utility for view matched by tolokers tracks with toloka or easyview and
  get tolokers response statistics

Options:
  -tf, --toloka-file TEXT  file from toloka  [required]
  --output-dir TEXT        output directory  [required]
  --quorum FLOAT           what percentage of same answers do we need for show
                           track
  --help                   Show this message and exit.

```

##split_tasks
Иногда очень хочется в фале из толоки выделить только задания одного или нескольких типов из [основные, контрольные, обучающие]. Этот скрипт из одного файла для толоки делает другой оставляя только те типы заданий, которые нам нужны

```
./split --help

Usage: split [OPTIONS]

  Make file with only one from [main | control | train] tasks from big
  toloka file with all these types of tasks

Options:
  --input-f TEXT   [required]
  --output-f TEXT  [required]
  --main
  --train
  --control
  --help           Show this message and exit.
```
