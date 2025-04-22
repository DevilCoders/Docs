Сейчас переименование, удаление и патчинг данных в поставке не автоматизированы.
Вот какие движения нужно для них совершить:

# Переименование

* перестать писать, дождаться пока все пайпы прочтут
* опционально переименовать таблички, подробности ниже

* вмёржить новую версию
* удалить старые внутренние lb топики тестинг/прод, это можно сделать из [ui](https://logbroker.yandex-team.ru/logbroker/accounts/vertis/broker?page=browser&type=directory&browserFilter=&consumerFilter=&metricsFrom=1657534063641&metricsTo=1657620463641&sortOrder=%22default%22) чтобы заодно убедиться что топики никто не читает, или через cli:
```
logbroker -s logbroker.yandex.net schema remove topic '/vertis/broker/prod/client-topics/full/topic/path'
```
* удалить лб-консьюмеров для lb, kafka, ch и transducer (у yt один на всех консьюмер, у остальных +- один на поставку)
* удалить артефакты в [реакторе](https://reactor.yandex-team.ru/browse?selected=2959084)

Записанные данные сами не переедут. Если их нужно сохранить, можно переименовать таблицы в yt и ch перед выкаткой новой версии:
* yt:
```
    ya tool yt move src_path dst_path
```
* ch (если поменяли имя таблицы):
```
    //опционально создать новую базу
    create database new_db on cluster '{cluster}'

    //получить список мат вью старой таблицы
    select arrayMap(t -> concat (tupleElement(t, 1), '.', tupleElement(t, 2)), arrayZip(dependencies_database, dependencies_table)) from system.tables where database = 'old_db' and name = 'old_table'

    //переименовать таблицу
    rename table old_table to new_table on cluster '{cluster}'

    //пересоздать все мат вью, сами они не перенесутся
    //так можно делать только если у mat view указана таблица TO, неявная таблица будет дропнута вместе со вью
    //для неявных таблиц можно, например, перелить всё в явную (но вообще их лучше не использовать)
    drop view mat_view on cluster '{cluster}'
    create materialized view new_db.mat_view on cluster '{cluster}' to new_db.existing_table as select ... from new_db.new_table

    //таблицу с оффсетами надо потранкейтить (удалить все данные, чтобы начать читать новый топик заново)
    truncate table new_db.new_table_offset_view on cluster '{cluster}'
```

# Удаление

* дропнуть конфиг, вмёржить, подождать пока доедет

* удалить старые внутренние lb топики тестинг/прод, это можно сделать из [ui](https://logbroker.yandex-team.ru/logbroker/accounts/vertis/broker?page=browser&type=directory&browserFilter=&consumerFilter=&metricsFrom=1657534063641&metricsTo=1657620463641&sortOrder=%22default%22) чтобы заодно убедиться что топики никто не читает, или через cli:
```
logbroker -s logbroker.yandex.net schema remove topic '/vertis/broker/prod/client-topics/full/topic/path'
```
* удалить лб-консьюмеров для lb, kafka, ch и transducer (у yt один на всех консьюмер, у остальных +- один на поставку)
* удалить артефакты в [реакторе](https://reactor.yandex-team.ru/browse?selected=2959084)
* опционально удалить данные
  * ыть-таблицы
```
    ya tool yt remove src_path
```

  * сh-таблицы и их вью:
```
    select arrayMap(t -> concat (tupleElement(t, 1), '.', tupleElement(t, 2)), arrayZip(dependencies_database, dependencies_table)) from system.tables where database = 'autoru_public' and name = 'event':
    drop table x on cluster '{cluster}'
```

  * kafka-топик (в железной кафке, в mdb топик дропают владельцы сервиса через тикет в VASUP)
  * исходящий lb-топик, проверить что его не читают

# Патчинг

Самое проблемное мероприятие, нужно несовместимо изменить схему или пофиксить неправильные значения, есть варианты:

с конвертацией на отправителе:

* создать новую поставку, отправлять в неё уже правильные данные (или с несовместимой схемой)
* старые данные либо перепослать, либо перелить своими скриптами (плохой вариант, потому что обычно это yql там другах схема)

наш вариант:

* завести новую поставку (таска миграции не работает in-place)
* написать конвертер для битых данных (yson -> yson, что неудобно, приходится yson парсить)
* руками собрать uber-jar, залить в ыть
* написать конфиг миграции (сохранять ли сортировку, дни, пути), выкатить в прод
* дождаться завершения, убрать конфиг миграции

хороший вариант:

пока отсутствует
