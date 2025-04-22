## simple-runner.template.py

Runner for simple tools for local run.

Usage example:

```
GENERATE_SCRIPT(
    TEMPLATE ${ARCADIA_ROOT}/travel/hotels/devops/starter/simple-runner.template.py
    CUSTOM_PROPERTY appName gen_logfeller_parser_pojo-get_schema
    CUSTOM_PROPERTY mainClass ru.yandex.travel.gen_logfeller_parser_pojo.get_schema.Main
    OUT get_schema.py
)
```


## starter.template.py

Runner for server java applications.

Usage example:

```
GENERATE_SCRIPT(
    TEMPLATE ${ARCADIA_ROOT}/travel/hotels/devops/starter/starter.template.py
    OUT ${BINDIR}/bin/api.py
    CUSTOM_PROPERTY appName travel-api
    CUSTOM_PROPERTY mainClass ru.yandex.travel.api.Application
)
```
