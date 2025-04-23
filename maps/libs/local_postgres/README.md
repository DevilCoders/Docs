# local_postgres library

Allows to bring up a local postgres server to use in unittests.

Usage example:

```cpp
#include <maps/libs/local_postgres/include/instance.h>

Database database;
database.createExtension("postgis");
database.executeSql("SELECT * FROM table");

pqxx::connection conn(database.connectionString());
```

Tests should be run in an environment with postgres available.

To bring up postgres you should add this to your **ya.make** file

```
SIZE(MEDIUM)
INCLUDE(${ARCADIA_ROOT}/maps/pylibs/recipes/postgres/recipe.inc)
```

Legacy way(FAT tests):
```
INCLUDE(${ARCADIA_ROOT}/maps/libs/local_postgres/recipe.inc)
```

Container details: https://wiki.yandex-team.ru/maps/dev/core/wikimap/mapspro/unittest-lib/#kontejjnerspostgresom1186370448
