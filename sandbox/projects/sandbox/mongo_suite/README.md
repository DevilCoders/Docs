## Mongo backup

Бэкапы делаются ежедневно ночью планировщиком на *SECONDARY* серверах.
Для наименьшего воздействия на работоспособность серверов и упрощения синхронизации, бекап выполняются на одном хосте,
где расположены все шарды монги, включая конфигурацию сервера, в [скрытом режиме](https://docs.mongodb.com/manual/core/replica-set-hidden-member/)
(используются только для репликаций, участвуют в голосовании, не могут стать *PRIMARY*).

Если таких хостов несколько, то они чередуются.
Если таких хостов нет, то возможен вариант бэкапа с нескольких *SECONDARY* серверов с синхронизацией через ZooKeeper,
  однако он устарел, не имеет многих особенностей и не рекомендуется к использованию.

Бэкапы публикуются в S3 в специальный бакет **sandbox-backup** в папку под именем `mongo_backup-<timestamp>`,
  где **timestamp** имеет вид `Y%m%d_%H%M%S` (например, `20210611_071015`).
По умолчанию, время жизни бэкапов - 14 дней.

### Task SERVICE_MONGO_BACKUP

Основная задача для бэкапа монги. Задача определяет хосты, запускает бэкаперы,
  мониторит процесс и может выполнять некоторые дополнительные действия над базой.

**SERVICE_MONGO_BACKUP** должна выполняться на sandbox сервере для доступа к mongos.

#### Workflow

* Убедиться, что балансер выключен;
* Получить shard map через ручку sandbox'а `/service/status/database/shards`
    и отфильтровать хосты по нужным критериям (*SECONDARY*, *hidden* и т.п.);
* Запустить одну или несколько задач-бэкаперов на хостах с репликами и ожидать их завершения;
* Если необходимо, запустить восстановление по свежему бэкапу;
* Включить балансер до 7 утра и потом выключить;
* Запустить тесты бэкапа.

Тесты и восстановление на данный момент не работают, пользоваться этими опциями не стоит.

#### Parameters

Для управления фильтрацией шардов и хостов имеются три параметра:
* `run_on_single_host (bool: True)` - делать бэкап только на хостах с полным набором шардов,
    если таких хостов нет, задача упадёт с ошибкой;
* `use_hidden_shards (bool: True)` - запускать бэкап только на скрытых репликах;
* `blacklist (str)` - список хостов, запрещенных для использования.

Для конфигурирования процесса бэкапа есть ещё два параметра (передаются в дочерние задачи):
  * `do_fsync (bool: True)` - перед началом бэкапа делать `fsync` (дамп на диск данных из памяти) с блокировкой;
  * `use_mongodump (bool: True)` - для бэкапов использовать `mongodump`,
      в противном случае бэкап будет собран прямо с файлов на диске
      (только если включены `run_on_single_host` и `do_fsync`).

### Task SERVICE_MONGO_BACKUPER

Внутренняя задача бэкапа монги. Задача подготавливает окружение, делает дамп и выгружает его в MDS.

**SERVICE_MONGO_BACKUPER** выполянется непосредственно на сервере с нужными шардами.
Запуск вручную не предполагается, задача должна запускаться в рамках **SERVICE_MONGO_BACKUP**.

#### Workflow

* Задача принимает список шардов для бэкапа (по-хорошему, там должны быть перечислены все шарды базы)
    и проверяет, что они действительно всё ещё *SECONDARY*
* Если `do_fsync` включён, то каждая реплика делает `fsync` с блокировкой записи на время бэкапа;
* Если `use_mongodump` включён, то для каждого шарда поочереди вызывается `mongodump --oplog --archive`
    с перенаправлением вывода на компрессор **pixz**;
  иначе для каждой папки в `mongodb_path` (по-умолчанию `/ssd/mongodb`)
    вызывается `tar -c` с компрессией через **pixz** (количество папок должно совпадать с количеством шардов);
* Если `do_fsync` включён, отпускаем блокировку через `fsyncUnock()`;
* Папка `mongo_backup-<timestamp>` со всеми архивами публикуется в S3 в специальный бакет **sandbox-backup**
    и оформляется как ресурс типа **SANDBOX_SHARD_GROUP_BACKUP**.
