# get_schema

## Add new log

To add new log schema generation add following generation to `ya.make` of this project for each log file.

```yamake
RUN_JAVA_PROGRAM(
    ru.yandex.travel.gen_logfeller_parser_pojo.generator.Main
    --class <canonical name of your log record class>
    --out-file ${BINDIR}/generated/<log-name>
    OUT_DIR ${BINDIR}/generated
    CLASSPATH travel/hotels/tools/gen_logfeller_parser_pojo/generator <PEERDIR of yout class project>
)
```

Params:

- `<canonical name of your log record class>` - full name of your class with package. Example: `ru.yandex.travel.api.endpoints.hotels_portal.SuggestLogRecord`.
- `<log-name>` - name of your log record class. Must not contain spaces. Should be human readable. Example: `travel/api/suggest-log`.
- `<PEERDIR of yout class project>` - path to project with record class in Arcadia. Example: `travel/api`.

Do not forget to add description and generation


## Generate schema for log

```shell script
ya make . &&  ./get_schema.py --log <log-name> --out-file <path/to/out/file>
```

Will write generated schema for `<log-name>` to `<path/to/out/file>`.


## Known logs

### travel/api/hotels-suggest-log

Travel API hotel suggest log

Update schema:

```shell script
ya make . && ./get_schema.py --log travel/api/hotels-suggest-log --out-file ${ARCADIA_ROOT}/logfeller/configs/parsers/travel-api-hotels-suggest-log.json
```

### travel/api/hotels-suggest-choice-log

Travel API hotel suggest choice log

Update schema:

```shell script
ya make . && ./get_schema.py --log travel/api/hotels-suggest-choice-log --out-file ${ARCADIA_ROOT}/logfeller/configs/parsers/travel-api-hotels-suggest-choice-log.json
```

### travel/api/hotels-happy-page-log

Travel API hotel happy page log

Update schema:

```shell script
ya make . && ./get_schema.py --log travel/api/hotels-happy-page-log --out-file ${ARCADIA_ROOT}/logfeller/configs/parsers/travel-happy-page-log.json
```
