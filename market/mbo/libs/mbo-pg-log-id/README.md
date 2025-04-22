Очередь изменений через триггеры в БД
=========================

Мотивация
---------
Дешевый способ асинхронно обрабатывать изменения строк в таблице несколькими обработчиками.

Прямолинейный способ - modified_timestamp = now() не работает, т.к. таймстемп проставляется до момента коммита, и с точки зрения стороннего наблюдателя могут появляться строчки "в прошлом".

Принцип работы
--------------
В отдельной таблице создается и поддерживается последовательность изменений строк.

Таблица изменений содержит ключ совпадающий с ключом основной таблицы и уникальный id изменения.

При изменении сточки в основной таблице срабатывает триггер, который записывает в таблицу лога изменений null для соответствующего ключа.
Отдельный фоновый процесс пробегается по таблице изменений и заменяет null на уникальный id из сиквенса.

Обработчики могут получать новые изменения запросом:
```
select * from log_id_table where modified_seq_id > :last_processed_id
```

Как начать использовать
-----------------------
0. Добавить mbo-pg-log-id в зависимости проекта и подключить в liquibase xml
    - схема в которой будут лежать таблицы с логом изменений

      ```<property name="logid.schema" value="mdm_audit"/>```

    - создание схемы (если используется существующая, то не нужно)

      ```<include file="classpath:/migrations/log-id-sql/schema*.sql"/>```

    - общие функции для создания триггеров и таблиц

      ```<include file="classpath:/migrations/log-id-sql/log_id*.sql"/>```

1. Создание таблицы изменений и триггеров
В liquibase миграции прописать
```
   select mdm_audit.log_id_init_tables('schema', 'table');
   select mdm_audit.log_id_init_functions('schema', 'table');
   select mdm_audit.log_id_init_triggers('schema', 'table');
```

Второй вариант без foreign key с возможностью обработки удаленных записей
```
   select mdm_audit.log_id_init_tables_with_option_fk('schema', 'table', false);
   select mdm_audit.log_id_init_functions('schema', 'table');
   select mdm_audit.log_id_init_triggers('schema', 'table');
   select mdm_audit.log_id_init_delete_trigger('schema', 'table');
```

Будут созданы
    - таблица `{logid.schema}.log_id_{table}`
    - синквенс `{logid.schema}.log_id_{table}_seq`
    - триггеры after insert и update на таблицу `{schema}.{table}`
    - процедура для обновления modified_seq_id `{logid.schema}.log_id_{table}_update_seq(batch_size int)`
    - С `log_id_init_delete_trigger` еще будет создан тригер after delete на таблицу `{schema}.{table}` (работает только без foreign key на основную таблицу)

2. Создать бин PgLogIdService с настройками для своей таблицы и добавить в tms периодический запуск процедуры `PgLogIdService.updateModifiedSequence`.

3. Получать список измененных ключей через `PgLogIdService.getModifiedRecordsIdBatch` или `PgLogIdService.processUpdatedKeys`.

Подводные камни
---------------
1. В общем случае порядок modified_seq_id и modified_timestamp в данных не совпадают, погрешность - интервал запуска процедуры обновления modified_seq_id.
2. Часто меняющиеся строки будут обнулять modified_seq_id до того как обработчик их увидит.
3. Невозможно "пропустить" событие и обработать остальные. Т.е. любая ошибка с данными в обработке полностью останавливает всю очередь.

