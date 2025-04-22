PostgreSQL Queries Executor
===========================

Quick Start
-----------
```
./psql-exec postgresql://user:password@host:port/db --command "SELECT version();"
```


Purpose
-------
This tool is useful in the following two scenarious:
- A query must be executed on a node without `psql`. This tool can be used
  without installation, just copy it to the home directory.
- A query execution time is of interest. This tool is able to run the same query
  several times and then report the median execution time.


Output Format
-------------
The format is compatible with Yandex Wiki markup, therefore query execution
output can be easily used in the wiki, tracker, etc: it must be inserted
in between the start `#|` and the stop table `|#` symbols.
