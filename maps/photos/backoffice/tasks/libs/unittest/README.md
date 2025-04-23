Tests should be run in a container with Postgres packages installed.
Also ```create_db``` binary should be available.

Add this to your **ya.make** file:

```
INCLUDE(${ARCADIA_ROOT}/maps/photos/backoffice/tasks/libs/unittest/recipe.inc)
```
