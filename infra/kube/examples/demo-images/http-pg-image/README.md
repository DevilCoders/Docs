# REST Application with postgres storage

Simple application showing access log stored in postgres.

Run application:

* Set env vars:
    ```
    PGHOST=<hostname>
    PGPORT=5432
    PGUSER=postgres
    PGPASSWORD=postgres
    PGDATABASE=postgres
    ```
* Build `go build -o server`
* Run `./server`
