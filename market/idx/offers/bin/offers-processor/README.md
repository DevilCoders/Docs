# offers-processor

## В первую очередь смотрим в Вики

- Подробная инструкция разработчика
  - https://wiki.yandex-team.ru/market/development/indexer/yt-genlogs/how-to/
- Верхнеуровневое описания проекта Генлоги в YT
  - https://wiki.yandex-team.ru/market/development/indexer/yt-genlogs/project-summary/

## О программе

Сюда переносим бизнес-логику из `offers-indexer`
- Всегда пишем в логи URL таблиц и операций в YT, не должно быть голых ID или хуже, их отсутствия
- Стараемся выдержать архитектуру: 1 главный маппер + N подготовительных этапов
- Большие сторонние данные нужно переносим через таблицы в YT
- Малые сторонние данные подгружаем в память маппера

## Пример запуска

С одной таблицей:
`./offers-processor --yt-proxy arnold --yt-token-path $HOME/.yt/token --yt-client-log-path yt_client.log --yt-input-table //home/market/testing/indexer/stratocaster/mi3/main/$GENERATION/offers/0000 --yt-output-dir //tmp/$LOGNAME --input-dir $HOME/offers_data --generation $GENERATION --yt-mapper-memory-mb 7000`

Со всеми таблицами одной директории:
`./offers-processor --yt-proxy arnold --yt-token-path $HOME/.yt/token --yt-client-log-path yt_client.log --yt-input-dir //home/market/testing/indexer/stratocaster/mi3/main/$GENERATION/offers --yt-output-dir //tmp/$LOGNAME --input-dir $HOME/offers_data --generation $GENERATION --yt-mapper-memory-mb 7000`

Замечания:
- подразумевается, что в переменной среды `GENERATION` хранится имя поколения, для которого нужно собрать генлоги
- в этих примерах директория `$HOME/offers_data` должна содержать все необходимые для запуска файлы данных
  - их актуальный список можно найти в переменной `INPUT_DATA` модуля `marketindexer/marketindexer/genlog.py`
- в одном запуске можно указать одну директорию и/или несколько таблиц
- есть еще опциональный параметр `--yt-small-bids-table` для работы с малыми ставками, см. код
