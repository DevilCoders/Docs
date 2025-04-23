Враппер над [ktlint](https://ktlint.github.io/).

## Как использовать

```
RUN_JAVA_PROGRAM(
    ru.yandex.market.ktlint.KtlintWrapperKt
    OUT_DIR ${KTLINT_OUT}
    CLASSPATH market/mbi/mbi-tools/ktlint
    CWD ${ARCADIA_ROOT}/market/путь_до_приложения
)
```
