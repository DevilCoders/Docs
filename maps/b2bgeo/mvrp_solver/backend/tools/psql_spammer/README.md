```
usage: psql_spammer [-h] --psql-host PSQL_HOST [--psql-port PSQL_PORT] --psql-dbname PSQL_DBNAME --psql-user PSQL_USER --psql-password PSQL_PASSWORD [--threads THREADS] [--query-per-thread QUERY_PER_THREAD] [--delay DELAY] --query
                    QUERY

Utility to spam db with queries in multiple threads.

optional arguments:
  -h, --help            show this help message and exit
  --psql-host PSQL_HOST
                        Postgresql host.
  --psql-port PSQL_PORT
                        Postgresql port. Default: 6432.
  --psql-dbname PSQL_DBNAME
                        Postgresql dbname.
  --psql-user PSQL_USER
                        Postgresql user.
  --psql-password PSQL_PASSWORD
                        Postgresql password.
  --threads THREADS     Number of threads. Default: 1.
  --query-per-thread QUERY_PER_THREAD
                        Number of queries for each thread to send. Default: 10.
  --delay DELAY         Delay between two consecutive queries within one thread in seconds. Default: 0.01
  --query QUERY         Query to spam.
```

Example (send 100 queries per each of 10 threads with delay of 0.01s to solver testing db):
```
./psql_spammer --psql-host `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o hosts` --psql-dbname `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o db_name` --psql-user `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o db_user` --psql-password `ya vault get version sec-01ddnqwb7gjh51xjnskedf8yxc -o password` --threads 10 --query-per-thread 100 --delay 0.01 --query "SELECT uuid FROM tasks.tasks WHERE status = 'queued' ORDER BY created LIMIT 1 FOR UPDATE SKIP LOCKED;"

```
