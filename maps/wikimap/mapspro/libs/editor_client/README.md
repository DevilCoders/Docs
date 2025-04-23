# editor-client library

Simple wrapper to ease basic HTTP requests to maps-wiki-editor backends.
To use create client Instance class object and call apropriate methods.
Instance stores database token returned by updates.
Backed errors are wrapped into editor_client::ServerException class object


Usage example :

```cpp
#include <maps/wikimap/mapspro/libs/editor_client/include/instance.h>

Y_UNIT_TEST(test_get_object_exception)
{
    Instance instance(BACKEND_URL, SOME_USER_UID);
    try {
        instance.getObjectById(1);
        UNIT_FAIL("Didn't get ERR_MISSING_OBJECT from editor backend.");
    } catch (const ServerException& ex) {
        UNIT_ASSERT_VALUES_EQUAL(ex.status(), ERR_MISSING_OBJECT);
    }
}
```

Add this to your **ya.make** PEERDIR file:

```
maps/wikimap/mapspro/libs/editor_client
```
