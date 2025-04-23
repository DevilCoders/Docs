# wiki-unittest library

Has various fixtures that bring up a local postgres server with applied migrations and useful methods to obtain pgpool3::Pool&.

Usage example 1:

```cpp
#include <yandex/maps/wiki/unittest/localdb.h>

Y_UNIT_TEST(test_something)
{
    unittest::MapsproDbFixture fixture;

    auto txn = fixture.pool().masterWriteableTransaction();
}
```

Usage example 2:

```cpp
#include <yandex/maps/wiki/unittest/arcadia.h>

WIKI_FIXTURE_TEST_CASE(test_something, unittest::MapsproDbFixture)
{
    auto txn = pool().masterWriteableTransaction();
}
```

Usage example 3 (not recommended until IGNIETFERRO-960 is done):

```cpp
#include <yandex/maps/wiki/unittest/arcadia.h>

Y_UNIT_TEST_F(test_something, unittest::ArcadiaDbFixture)
{
    auto txn = pool().masterWriteableTransaction();
}
```

Tests should be run in a container with Postgres packages installed.
Migrations should be accessible by the tests.

Add this to your **ya.make** file:

```
DATA(arcadia/maps/wikimap/mapspro/migrations/migrations)

TAG(ya:fat ya:force_sandbox)
REQUIREMENTS(container:513446773)
```
