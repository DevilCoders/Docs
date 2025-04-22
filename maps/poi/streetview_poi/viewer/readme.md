Утилита для просмотра датасетов
===

Чтобы запустить, требуется сделать три вещи:
1. Требуется поставить YT Python API. Инструкция [здесь](https://wiki.yandex-team.ru/yt/userdoc/pythonwrapper/).
2. `pip install -r requirements.txt`
3. `python server.py`

## Help

```
~/arcadia/maps/poi/streetview_poi/viewer$ python server.py --help
usage: server.py [-h] [-p PORT] [-t INPUT_TABLE] [--per-page PER_PAGE]

Streetview dataset viewer

optional arguments:
  -h, --help            show this help message and exit
  -p PORT, --port PORT  http port to listen
  -t INPUT_TABLE, --input-table INPUT_TABLE
                        path to toloka dataset table on yt
  --per-page PER_PAGE   number of rows per page

```