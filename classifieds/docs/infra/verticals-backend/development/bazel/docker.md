# Как собирается докер базелем

Для сборки докер образа используются рулы из [rules_docker].  
Эти правила не используют (обычно) докер для сборки образа, поэтому не требуют его наличие при сборке.

При запуске таргета с образом он соберется и запушится в локальный докер демон.  
При этом его имя будет получено из имени таргета.
Например, таргет `//general/gateway/app:image` будет иметь имя образа `bazel/general/gateway/app` и версию `image`.  
Т.е. для запуска надо использовать строку `bazel/general/gateway/app:image`.  
В дальнейшем этот образ можно потегать и запушить в удаленный репозиторий.

## Настройки образа
Для приложений на scala лучше всего использовать макрос `scala_image` объявленный в файле `tools/defaults.bzl`.
Для него нужно указать имя бинарника, который будет запущен. 
Из этого бинарника будут наследованы настройки main_class, jvm_flags и args.
Также макрос объявляет несколько дефолтов (jvm флаги, базовый образ с последней jvm), которые при необходимости можно переопределить.

## Параметры запуска
Входной точкой в образ является скрипт [entrypoint.sh].

Он поддерживает несколько аргументов:
```
# --debug               Launch the JVM in remote debugging mode listening
# --debug=<port>        to the specified port or the port set in the
#                       DEFAULT_JVM_DEBUG_PORT environment variable (e.g.
#                       'export DEFAULT_JVM_DEBUG_PORT=8000') or else the
#                       default port of 5005.  The JVM starts suspended
#                       unless the DEFAULT_JVM_DEBUG_SUSPEND environment
#                       variable is set to 'n'.
# --main_advice=<class> Run an alternate main class with the usual main
#                       program and arguments appended as arguments.
# --jvm_flag=<flag>     Pass <flag> to the "java" command itself.
#                       <flag> may contain spaces. Can be used multiple times.
# --jvm_flags=<flags>   Pass space-separated flags to the "java" command
#                       itself. Can be used multiple times.
# --print_javabin       Print the location of java executable binary and exit.
```

Так же несколько переменных окружений влияют на его поведение:
`JVM_FLAGS` – дополнительные параметры для запускаемой jvm
`JVM_DEBUG_PORT` – порт, на котором нужно запустить дебаггер
`DEFAULT_JVM_DEBUG_SUSPEND=n` – чтобы не ждать подключения дебаггера на старте приложения
`JAVA_STUB_DEBUG` – выполнить произвольные bash код перед запуском скрипта. Например, `set -x` чтобы включить дебаг в bash.
`PRINT_JAVABIN=1` – напечатает путь до бинарника java и выйдет.
`MAIN_ADVICE` – переопределить main класс, который будет запущен. Оригинальный main класс будет передан первым аргументом.

[rules_docker]: https://github.com/bazelbuild/rules_docker
[entrypoint.sh]: https://a.yandex-team.ru/arc_vcs/classifieds/verticals-backend/tools/docker/entrypoint.sh