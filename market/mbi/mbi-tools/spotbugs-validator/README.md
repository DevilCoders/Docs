Враппер над [Spotbugs](http://spotbugs.github.io) для приложений на Java.

## Как использовать

Добавить в ya.make приложения
```
DEPENDS(market/mbi/mbi-tools/spotbugs-validator)

SET(SPOTBUGS_OUT ${BINDIR}/spotbugs/out)

RUN_JAVA_PROGRAM(
    ru.yandex.market.spotbugs.SpotbugsValidateKt ${ARCADIA_BUILD_ROOT}/market/mbi/mbi-health-api/mbi-health-api.jar
    OUT_DIR ${SPOTBUGS_OUT}
    IN ${ARCADIA_BUILD_ROOT}/market/mbi/mbi-health-api/mbi-health-api.jar
    CLASSPATH market/mbi/mbi-tools/spotbugs-validator
)
```
