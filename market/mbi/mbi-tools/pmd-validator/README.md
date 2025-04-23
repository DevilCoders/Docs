Враппер над [PMD](https://pmd.github.io) для приложений на Java.

## Как использовать

```
RUN_JAVA_PROGRAM(
    ru.yandex.market.PmdValidateKt ${ARCADIA_ROOT}/[Путь к исходникам приложения]
    OUT_DIR ${BINDIR}/pmd/
    CLASSPATH market/mbi/mbi-tools/pmd-validator
)
```


