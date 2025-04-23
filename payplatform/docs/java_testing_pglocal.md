Библиотека pglocal
==================

Библиотека позволяет запустить локальный `postgres` кластер для использования в тестах. На данный момент из коробки предоставляется:

- Запуск сконфигурированного postgresql сервера
- Возможность запуска `postgresql` кластера с одним мастером и 1-N реплик
- Интеграция с `micronaut`

Конфигурация
------------

Конфигурация задается в конфиге `micronaut`:

```yaml
local-pg:
  user: testuser # Имя пользователя, который будет обращаться к базе
  pg-version: v12 # Необходимая версия postgresql. Возможные значения: v12
  migrations: # Параметры миграций. Можно указать только один из двух вариантов
    resource-folder: path # Путь к папке миграций в classpath
    folder: path # Путь к папке миграций на диске
  cluster: # В данной секции описываются инстансы кластера
    master: # Имя инстанса (может быть любое, единственное требование: не должно быть инстансов с одинаковым именем)
      port: ${random.port} # Порт, который будет слушать инстанс
      role: master # Роль инстанса. Возможные значения: master, slave.
    slave:
      port: ${random.port}
      role: slave
    ...
    slaveN:
      ...
```

{% note warning %}

В кластере обязательно должен быть объявлен один мастер.

{% endnote %}

Использование
-------------

Для использования модуля необходимо подключить его в качестве зависимости в ya.make теста и настроить annotation processors.

```yamake
INCLUDE(${ARCADIA_ROOT}/payplatform/java/test.inc) # подключаем общие зависимости и параметры сборки

PEERDIR(
    payplatform/java/testing/pglocal
)

# настраиваем annotation processors
ANNOTATION_PROCESSOR(
    io.micronaut.annotation.processing.TypeElementVisitorProcessor
    io.micronaut.annotation.processing.AggregatingTypeElementVisitorProcessor
    io.micronaut.annotation.processing.PackageConfigurationInjectProcessor
    io.micronaut.annotation.processing.BeanDefinitionInjectProcessor
    io.micronaut.annotation.processing.ServiceDescriptionProcessor
)
```

Для того чтобы база была поднята перед запуском тестового класса необходимо задать имя базы:

```java
import io.micronaut.context.annotation.Property;
import io.micronaut.test.annotation.MicronautTest;

import static ru.yandex.payments.testing.pglocal.micronaut.PgLocalConfiguration.DB_NAME_PROPERTY;

@MicronautTest
@Property(name = DB_NAME_PROPERTY, value = "mydbname") // mydbname - имя базы, которая будет создана перед запуском теста
class MyTest {
}
```

{% note warning %}

Одну и ту же базу нельзя переиспользовать из разных тестовых классов. Если тестам требуется взаимодействовать с одной базой, то поместите их в один класс.

{% endnote %}

Обновление postgres
-------------------

В случае необходимости добавить новую версию postgres требуется выполнить следующие шаги:

- Запустить скрипт [build_sandbox_pg_artefacts.sh](https://a.yandex-team.ru/arc/trunk/arcadia/payplatform/java/testing/pglocal/scripts/build_sandbox_pg_artefacts.sh), заменив версию postgres в переменной `PG_VERSION` на необходимую.
- Добавить новую версию в `enum` `Version`.
- Добавить ссылки на архивы новой версии, полученные из вывода скрипта, в мапу `PG_URL` класса `BinarySandboxSource`.
