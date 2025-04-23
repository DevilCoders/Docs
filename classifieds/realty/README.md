Realty backend
==============

[Документация](https://wiki.yandex-team.ru/realty/)

[Quick start](https://wiki.yandex-team.ru/realty/backend/quick-start/)

## Некоторые code conventions
 * [Обработка ошибок](https://wiki.yandex-team.ru/realty/backend/how-to-make-apis/)
 * Использовать [java.time предпочтительно](https://wiki.yandex-team.ru/realty/backend/realty-rent/chasovye-pojasa-i-vremja/)

## Запуск
[Настроить идею](https://wiki.yandex-team.ru/realty/backend/idea-tuning/)
[Настроить maven](https://github.com/YandexClassifieds/maven-settings)

Например, компиляция шедулера
```
./gradlew realty-seller-scheduler:compileScala
```

Запустить по зеленой стрелочке в Main

### Проблемы, которые могут возникнуть при запуске
##
#### Q:
```
Cannot start service, error during initialization
com.typesafe.config.ConfigException$Missing: seller-core.development.conf
@ file:/Users/dengbn/my/realty/realty-seller/realty-seller-core/target/classes/seller-core.development.conf: 30:
No configuration setting found for key 'realty.api.billing'
```
#### A:
Попробовать создать копию файла `realty-extdataloader-core.development.template.properties` без `.template` ->
`realty-extdataloader-core.development.properties`
Попробовать создать копию файла `realty-common.development.template.properties` без `.template` ->
`realty-common.development.properties`
##
#### Q:
```
java: package sun.misc does not exist
java: cannot find symbol
  symbol: class SignalHandler
java: cannot find symbol
  symbol:   class Signal
  location: class ru.yandex.realty.application.HupSignalHandler
```
#### A:
Снять галочку `Use '--release' option for cross-compilation (Java 9 and later)` в
**Build, Execution, Deployment > Compiler > Java Compiler**.

NOTE: Причина в использовании внутреннего API из модуля `jdk.unsupported` в `ru.yandex.realty.application.HupSignalHandler`

    jdeps -jdkinternals realty-common/target/classes/ru/yandex/realty/application/HupSignalHandler.class
    HupSignalHandler.class -> jdk.unsupported
    ru.yandex.realty.application.HupSignalHandler      -> sun.misc.Signal                                    JDK internal API (jdk.unsupported)
    ru.yandex.realty.application.HupSignalHandler      -> sun.misc.SignalHandler                             JDK internal API (jdk.unsupported)

    Warning: JDK internal APIs are unsupported and private to JDK implementation that are
    subject to be removed or changed incompatibly and could break your application.
    Please modify your code to eliminate dependence on any JDK internal APIs.
    For the most recent update on JDK internal API replacements, please check:
    https://wiki.openjdk.java.net/display/JDK8/Java+Dependency+Analysis+Tool

    JDK Internal API                         Suggested Replacement
    ----------------                         ---------------------
    sun.misc.Signal                          See http://openjdk.java.net/jeps/260
    sun.misc.SignalHandler                   See http://openjdk.java.net/jeps/260
