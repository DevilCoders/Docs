# Варианты записи логов

## Stdout и Stderr стартового контейнера {#stdout_stderr}

Вариант [активируется](standard-mechanism.md#activation) через UI или в yaml-спецификации workload'a ([proto-спецификация](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r8782046#L777)):

{% note warning %}

Автоматическая отгрузка `stdout` и `stderr` осуществляется только для **стартового контейнера workload'a**.
Отгрузку из созданных в процессе функционирования дополнительных процессов необходимо осуществлять [самостоятельно](#libs).

{% endnote %}

### Ограничение на длину сообщения {#limit-length}

В данный момент ограничение на длину строки сообщения – `1 Мб`.

При превышении ограничения сообщение будет разбито на отдельные записи размером `1 Мб` каждая (кроме последней части).

### Формат логов {#format}

В stdout/stderr можно писать логи как в обычном plain-text формате, так и в виде структурированного JSON, см. [раздел Формат логов](format.md#format).

### Перенаправление логов в файлы {#log-redirect}

Перенаправление логов (например флагом `-Xloggc` для java-приложений) допустимо в любые файлы, за исключением `/dev/stdout, /dev/stderr` и линков на них.

### Служебные лог-файлы для хранения `stdout` и `stderr` в контейнере {#stdout_stderr_files}

При включенной поставке логов `stdout` и `stderr` записываются без какой-либо предобработки в служебные файлы:

* `<box_chroot>/porto_log_files/<workload_id>_stdout.portolog`
* `<box_chroot>/porto_log_files/<workload_id>_stderr.portolog`

{% note warning %}

Пути могут поменяться в будущем.

{% endnote %}

#### Ротация лог-файлов {#rotation}

Pod agent автоматически ротирует указанные файлы, если размер превышает `80Мб`.

Отрезается 20% от текущего размера, то есть размер после ротации будет в диапазоне `64-80Мб`

#### Использование лог-файлов пользователем {#logfiles-use}

Из указанных файлов разрешено чтение в пользовательских целях:
- чтение логов в консоли;
- поставка логов в сторонние системы.

{% note warning %}

Данные файлы нельзя удалять или править со стороны пользователя — это сломает механизм отгрузки логов.

{% endnote %}

## Клиенты для Unified Agent {#libs}

### Java {#java}

* [Инструкция](https://docs.yandex-team.ru/unified_agent/libraries/java)
* [Артефакты для проектов вне Аркадии](http://artifactory.yandex.net/artifactory/yandex_media_releases/ru/yandex/unified_agent_java_client/).

#### Logback аппендер {#logback}

* [Использование appender](https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/java/logback/USAGE.md).
* [Пример](https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/java/logback/CONFIGURATION.md) конфигурирования appender и описание параметров.
* [Артефакты для проектов вне Аркадии](http://artifactory.yandex.net/artifactory/yandex_media_releases/ru/yandex/unified_agent_java_client_logback/).

#### Log4j аппендер {#log4j}

* [Использование appender](https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/java/log4j2/USAGE.md).
* [Пример](https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/java/log4j2/CONFIGURATION.md) конфигурирования appender и описание параметров.
* [Артефакты для проектов вне Аркадии](http://artifactory.yandex.net/artifactory/yandex_media_releases/ru/yandex/unified_agent_java_client_log4j2/).

### C++ {#c-pluss}

* [Инструкция](https://docs.yandex-team.ru/unified_agent/libraries/cpp)
* Код бэкенда логгера: [https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/cpp/yd_logger/yd_backend.h](https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/cpp/yd_logger/yd_backend.h)
* Примеры использования: [https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/cpp/examples/ua_yd_logger/main.cpp](https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/cpp/examples/ua_yd_logger/main.cpp)

### Python {#python}

* [Инструкция](https://docs.yandex-team.ru/unified_agent/libraries/python)
* Код логгер хэндлера: [https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/python/yd_handler.py](https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/python/yd_handler.py)
* Примеры использования: [https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/python/examples/ua_yd_logger/__main__.py](https://a.yandex-team.ru/arc/trunk/arcadia/logbroker/unified_agent/client/python/examples/ua_yd_logger/__main__.py)
