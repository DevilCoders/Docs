## Collect resources recipe
This recipe allows to collect all resources in test cwd.

### Usage
Add the following include to the tests's ya.make:

    SET(COLLECT_RESOURCES path/to/res_1 path/to/res_2 ...)
    INCLUDE(${ARCADIA_ROOT}/ads/yacontext/apps/yacofast/tests/collect_resources/recipe.inc)

path/to/res_i is supposed to be UNION or PACKAGE.
