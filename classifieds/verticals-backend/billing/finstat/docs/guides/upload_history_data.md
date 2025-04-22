# Дока для разработчиков биллинга. Как налить исторические данные.
## Заливка исторических данных AutoruDealers

Данная инструкция копирует [общую](https://a.yandex-team.ru/arc_vcs/classifieds/verticals-backend/etc-mono/services/statist/docs/history.md),
с уточнениями для финстаты

### Подготовка

- Установить утилиту copy_table_yt_to_clickhouse.
  Либо собрать из аркадии либо из
  [deb пакета](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/_home/kusaeva/bin/yandex-copy-yt-to-clickhouse_1.0_amd64.deb).
  В вики можно найти другие способы установки, но там могут старые версии, не поддерживающие нужные параметры.

  Чтобы не собирать под mac из аркадии можно завести виртуалку
  [здесь](https://st.yandex-team.ru/createTicket?queue=VASUP&_form=62708) и запустить переливку на ней.

- Получить OAuth-токен сохранить его в ~/.yt/token

  Для этого пройти по [ссылке](https://oauth.yt.yandex.net/), нажать Give me my token и дать разрешение.
  Там сразу будет команда для сохранения токена в ~/.yt/token

- Скопировать файл
  [settings.json](https://a.yandex-team.ru/arc/trunk/arcadia/transfer_manager/copy_yt_to_clickhouse/settings/settings.json)

  в settings.json использовать такие настройки, чтобы данные в кликхаус наливались медленнее.
  Иначе нагрузка на кликхаус может оказаться слишком большой, и он сложится.
  "threads_per_host": 1
  "lock_shard_timeout": 120,
  "insert_block_timeout": 120,
  "too_many_parts_pause": 45

- В скопированном settings.json заменить параметр tasks_base_path на свою собственную директорию в yt.
  В противном случае будет использован //tmp , а значит, стейт задачи в любой момент может быть стерт.

### Конвертация

1. Запустить запрос конвертирующий лог билинга во временную yt таблицу с данными финстаты

   Например [запросы собирающие данные для autoru](../../../../services/dealer_finstat_writer/docs)

   Перед запуском настроить параметры:

   - **source** - таблица billing_operation_event, надо поправить путь
     с учетом окружения, для которого делается заливка (test или prod)

   - **target** - временная таблица, можно указать любой путь, куда есть
     права на запись в yt. Каждый запуск запроса пересоздает эту таблицу с нуля.

2. Выполнить команду
   <details>
     <summary>для тестинга</summary>

      ```
      copy_table_yt_to_clickhouse append \
        --yt-cluster hahn \
        -s {temp_table} \
        -d finstat.autoru_dealers_events \
        --ch-seed-host sas-5nizh11m9j7wx59k.db.yandex.net \
        --ch-http-port 8443 \
        --ch-cluster MDB:finstat_test \
        --ch-https \
        --dbaas-token {oauth token} \
        --ch-user finstat \
        --ch-password {password}
        --settings {path_to_setting.json}
      ```
   </details>
   <details>
      <summary>для прода</summary>

      ```
      copy_table_yt_to_clickhouse append \
        --yt-cluster hahn \
        -s {temp_table} \
        -d finstat.autoru_dealers_events \
        --ch-seed-host sas-6at2s57lhropgr7m.db.yandex.net \
        --ch-http-port 8443 \
        --ch-cluster MDB:finstat_prod \
        --ch-https \
        --dbaas-token {oauth token} \
        --ch-user finstat \
        --ch-password {password}
        --settings {path_to_setting.json}
      ```
   </details>

   Параметры
    - **{oauth token}** - полученный ранее OAuth-токен
    - **{password}** - значение password из секрета ([тестинг](https://yav.yandex-team.ru/secret/sec-01fjkb1jnq68fz64d3wxhzpa8c/explore/versions),
         [прод](https://yav.yandex-team.ru/secret/sec-01fjkbb8r34s53mf9391c2n68f))
    - **{temp_table}** - временная таблица target из пункта 1
    - **{path_to_setting.json}** - путь до скопированного [settings.json](https://a.yandex-team.ru/arc/trunk/arcadia/transfer_manager/copy_yt_to_clickhouse/settings/settings.json) с настроенным tasks_base_path

    **дополнительно**

    флаг --reset-state запускает переливку заново, без него она пытается продолжиться.
    copy_table_yt_to_clickhouse подготавливает данные для вставки по блокам, складывает их в ыть,
    и инсёртит оттуда, запоминая где остановилась. Если отменить начавшуюся переливку
    (поняли, что в запросе на подготовку данных ошибка), пересоздать табличку с данными
    под тем же именем, и продолжить, то без этого флага продолжат литься старые
    предподготовленные блоки.
