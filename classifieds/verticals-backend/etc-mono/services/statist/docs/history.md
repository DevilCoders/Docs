# Как перелить историю
- Создаем табличку в ыте с нужными данными:

  в _partition указываем что-то несуществующее, например, history

  в _offset – 0

  Стоит проверить, что схема в ыть-табличке соответствует схеме в кликхаусе.

  [Пример](https://yql.yandex-team.ru/Operations/YO_qKxJKfeF6hiGyofXmBY4zEbBHT5CI-5J55v9zrgg=)
- Ставим консольную утилиту от Tranfer Manager для переливки YT -> Clickhouse

  Можно собрать из аркадии самому или поставить
  из [deb-файла](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/_home/kusaeva/bin/yandex-copy-yt-to-clickhouse_1.0_amd64.deb) (
  спасибо @reimai). Achtung, версия из убунту-репозитория безнадёжно устаревшая и работать не будет, распаковывайте
  deb-ник через dpkg -i, мы не зря его собирали.

  [Документация](https://wiki.yandex-team.ru/transfer-manager/copy/yttoclickhouse/cliandexamples/)

- Смотрим, какие mat view висят на таблице с сырыми данными в кликхаусе:

  ```sql
  select database, name, arrayZip(dependencies_database, dependencies_table)
  from system.tables
  where database=XXX and name=YYY
  ```
  Если mat view нет – нам повезло, запускаем переливку (но скорее всего mat view будут).
  
  Если есть – тут момент, что на сырой табличке часто будет ttl, а на mat view его не будет или он будет другим.
  
  Поэтому при переливке истории с дня X по min(day) из сырой таблички, нужно будет подрезать mat view по этот день, чтобы данные не задублировались:
  
  ```sql
  ALTER TABLE [db.]table [ON CLUSTER cluster] DELETE WHERE day < min_day_from_raw_table
  ```
  
  В случае, если на таблице висит слишком много mat view, а история переливается для конкретного счетчика и подрезать все лениво, можно настроить переливку на отдельную таблицу, навесив аналогичный триггер с тем же таргетом на нее, или посчитать агрегаты на ыте и перелить уже их.
  
- Запускаем переливку
  
  Пример использования cli:
  
  ```
  copy_table_yt_to_clickhouse append --yt-cluster hahn -s //home/verticals/_home/reimai/ch_event_stat -d autoru_public.card_view_per_app_counter_day_old_stats  --ch-seed-host sas-g6e9074l8psxjed0.db.yandex.net --ch-http-port 8443 --ch-https --dbaas-token *** --ch-cluster MDB:test_vertis_ch_autoru_stats --ch-user autoru_stats --ch-password ***
  ```

## Полезности
  * [получить](https://docs.yandex-team.ru/cloud/mdb/cli) токен MDB
  * флаг __--reset-state__ запускает переливку заново, без него она пытается продолжиться. 
    copy_table_yt_to_clickhouse подготавливает данные для вставки по блокам, складывает их в ыть, и инсёртит оттуда, запоминая где остановилась.
    Если отменить начавшуюся переливку (поняли, что в запросе на подготовку данных ошибка), пересоздать табличку с данными под тем же именем, и продолжить, то без этого флага продолжат литься старые предподготовленные блоки.
  * при копировании больших таблиц обязательно стоит задавать [собственную директорию](https://wiki.yandex-team.ru/transfer-manager/copy/yttoclickhouse/transfermanager/#opciikopirovanijatablicy) для хранения стейта задачи и ttl для нее (по умолчанию там сутки)! В противном случае будет использован _//tmp_, а значит стейт задачи в любой момент может быть стерт. В таком случае прерванное копирование нельзя будет продолжить без потери целостности данных в КХ.
  Правда, патчить настройки умеет только сам transfer manager, при использовании консольной утилиты напрямую придется передать ей [полный конфиг](https://wiki.yandex-team.ru/transfer-manager/copy/yttoclickhouse/userdoc/#tonkienastrojjki).
  * Если переливка падает, так как не может залить на большинство хостов в шарде (один из хостов недоступен), можно поменять настройку ```per_shard_quorum = at_least_one```
   
