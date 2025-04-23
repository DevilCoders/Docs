Описание задачи
===============

Задача дамп схемы базы mysql в Sandbox ресурс.
Задача бинарная, чтобы ее загрузить в локальную песочницу в консоли:
```bash
cd arcadia/sandbox/projects/avia/dump_mysql/
ya make --checkout
sandbox upload_binary dump_mysql --enable-taskbox --attr released=stable --attr task_type=AVIA_DUMP_MYSQL
```

Для заливки в большой sandbox:
```bash
cd arcadia/sandbox/projects/avia/dump_data/
ya make --checkout
./dump_mysql upload --owner AVIA --attr released=stable --attr task_type=AVIA_DUMP_MYSQL
```

Задаче требуется ресурс с пакетом mysql. В локальный sandbox можно загрузить так:

```bash
ya upload --skynet --type=AVIA_MYSQL_PACKAGE --sandbox-url="http://<url for your sandbox>:13337" --user=guest <mysql tar>
```
