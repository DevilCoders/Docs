# dbutil-tests

Модуль лежит отдельно от dbutil, чтобы не склеиваться в idea без `--separate-test-modules`.
Иначе, в проекте генерируется циклическая зависимость:
```
direct/libs-internal/dbutils/ut
-> direct/libs-internal/testing/dbutil-testutils/ut
-> direct/libs-internal/testing/dbutil-reviewed-testutils/ut
-> direct/libs-internal/dbutil/ut
```
