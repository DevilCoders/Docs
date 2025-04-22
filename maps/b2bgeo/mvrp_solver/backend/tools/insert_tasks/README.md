```
usage: insert_tasks [-h] --psql-host PSQL_HOST [--psql-port PSQL_PORT] --psql-dbname PSQL_DBNAME --psql-user PSQL_USER
                    --psql-password PSQL_PASSWORD --num-rows NUM_ROWS [--apikey APIKEY]
                    [--task-statuses TASK_STATUSES] [--created CREATED]

Utility to import rows into tasks.tasks table. Beware using it in production.

optional arguments:
  -h, --help            show this help message and exit
  --psql-host PSQL_HOST
                        Postgresql host.
  --psql-port PSQL_PORT
                        Postgresql port. Default: 6432
  --psql-dbname PSQL_DBNAME
                        Postgresql dbname.
  --psql-user PSQL_USER
                        Postgresql user.
  --psql-password PSQL_PASSWORD
                        Postgresql password.
  --num-rows NUM_ROWS   Number of rows to insert into tasks.tasks table.
  --apikey APIKEY       Custom apikey for inserted tasks. Default: 7f963d7c-5fa8-48b9-8ce7-1e8796e0dc76
  --task-statuses TASK_STATUSES
                        Comma-separated task statuses to insert. 
                        Tasks are inserted using uniform distibution for statuses.
                        All possible values see here: https://a.yandex-team.ru/arc/trunk/arcadia/maps/b2bgeo/mvrp_solver/backend/async_backend/lib/types.h?rev=r8835817#L23
                        Default: completed
  --created CREATED     Value in isoformat (2021-11-18T17:04:15.934080)
                        to put in `created` and `activity` fields of tasks.tasks table.
                        Default: now() - 1day.
```

Example (add 50 rows to solver testing db):

```
./insert_tasks --psql-host `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o hosts` --psql-dbname `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o db_name` --psql-user `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o db_user` --psql-password `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o password` --num-rows 50
```
