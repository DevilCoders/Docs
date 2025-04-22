## Javac Annotation Processing Tool

Java-программа, которая позволяет генерировать java код, проксируя вызов javac-препроцессору с указанием класса-процессора.

Может быть использована в сборке проекта ya make'ом. Для этого в ya.make проекта следует добавить следующую конфигурацию:

```
RUN_JAVA_PROGRAM(
    ru.yandex.market.apt.JavacAnnotationProcessingTool
    -processor <fully qualified processor class name>
    -output_directory <directory where generated code should be saved>
    <list of directories with sources for code generation>

    OUT_DIR <the same as output_directory>
    CLASSPATH
    market/jlibrary/javac-apt
    <any other modules that need to be in classpath for code generation>
)
```

При этом то, что указано в OUT_DIR должно быть так же указано в JAVA_SRCS вашего проекта, иначе RUN_JAVA_PROGRAM не будет запущена.

Рабочий пример может быть найден в проекте [LMS](https://a.yandex-team.ru/arc/trunk/arcadia/market/logistics/logistics-management-service).
