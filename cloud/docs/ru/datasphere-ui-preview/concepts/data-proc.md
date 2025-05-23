# Интеграция с Apache Spark™

С помощью интеграции {{ ml-platform-name }} с сервисом {{ dataproc-full-name }} вы можете производить вычисления на кластерах Apache Spark™. Вычисления производятся в сессиях, созданных с помощью [Apache Livy](https://livy.apache.org/).

## Кластер {{ dataproc-name }} {#cluster}

Вы можете использовать кластер, уже созданный в вашей подсети, или создать новый. Для корректной работы интеграции необходимо [настроить проект](#settings) и [назначить роли](#roles).

### Настройка проекта {{ ml-platform-name }} для работы с кластерами {{ dataproc-name }} {#settings}

Чтобы вы могли создавать кластеры {{ dataproc-name }} из {{ ml-platform-name }} или запускать уже существующие кластеры {{ dataproc-name }}, у проекта должны быть указаны:
* сервисный аккаунт, от имени которого будут производиться все операции с кластерами {{ dataproc-name }};
* подсеть, в которой будет создаваться или из которой будет подключаться уже существующий кластер {{ dataproc-name }}. {% if product == "yandex-cloud" %}В рамках интеграции доступны только подсети, созданные в зоне доступности `{{ region-id }}-a`.{% endif %}

Эти параметры необходимо [указать в дополнительных настройках проекта](../operations/data-proc-integration.md#settings).

{% include [subnet-create](../../_includes/subnet-create.md) %}

### Роли, необходимые для корректной работы с кластерами {{ dataproc-name }} {#roles}

* Для создания кластера {{ dataproc-name }} вам необходимо разрешение на сервисный аккаунт, от имени которого {{ ml-platform-name }} будет выполнять операции. Это разрешение входит в роли `iam.serviceAccounts.user`, `editor` и выше.
* Для управления кластерами {{ dataproc-name }} сервисному аккаунту необходимы роли:
  * `datasphere.admin` — для создания ресурсов в {{ ml-platform-name }};
  * `vpc.user` —  для доступа к сети, указанной в настройках проекта;
  * `mdb.admin` — для создания и использования кластеров {{ dataproc-name }};
  * `mdb.dataproc.agent` — для создания и использования кластеров {{ dataproc-name }}.

Подробнее об [управлении доступом](../security/index.md).

### Создание кластера из проекта {{ ml-platform-name }} {#notebook}

Особенности кластера, созданного из проекта {{ ml-platform-name }}:
* Кластер будет создан в каталоге с проектом и в подсети, указанной в настройках проекта.
* {{ ml-platform-name }} следит за временем жизни кластера и автоматически удаляет его после двух часов бездействия.

  Кластер {{ dataproc-name }} считается активным, если на нем производятся вычисления или если активен ноутбук в проекте с кластером. Ноутбук считается активным, если перерыв в вычислениях составляет менее 20 минут.

Подробнее о том, [как создать кластер из проекта](../operations/data-proc-integration.md#notebook).

### Создание кластера в сервисе {{ dataproc-name }} {#service}

Особенности кластера, созданного в сервисе {{ dataproc-name }}:
* Вы управляете жизненным циклом кластера.
* Для корректной работы необходима версия кластера {{ dataproc-name }} не ниже `1.3`, а также должны быть включены сервисы: `LIVY`, `SPARK`, `YARN` и `HDFS`.

Подробнее о том, [как создать кластер в сервисе](../operations/data-proc-integration.md#console).

## Вычислительные сессии {#session}

В кластере {{ dataproc-name }} ваш код выполняется в сессиях. Сессия хранит промежуточное состояние до тех пор, пока вы не удалите сессию или кластер. У каждого кластера есть сессия по умолчанию. Ее идентификатор равен идентификатору проекта.

Для управления сессиями используйте следующие команды:
* `%create_livy_session --host $host --id $id` — создание сессии;
* `%delete_livy_session $id` — удаление сессии.

### Запуск python-кода {#run-code}

Код запускается в ячейках с заголовком:

```
#!spark [--cluster <кластер>] [--session <сессия>] [--variables <переменная>].
```

Где:

* `<кластер>` — кластер Data Proc, на котором будут производиться вычисления. Может быть:
  * HTTP-ссылкой на Livy, например, `http://10.0.0.8:8998/`.
  * Именем кластера, созданного через интерфейс ноутбука.
  * Кластером {{ dataproc-name }} из настроек проекта в консоли управления, если параметр пропущен.
* `<сессия>` — идентификатор вычислительной сессии. Если параметр пропущен, используется сессия кластера {{ dataproc-name }} по умолчанию.
* `<переменная>` — переменная, импортированная в ячейку из ядра. Поддерживаемые типы: `bool`, `int`, `float`, `str`, `pandas.DataFrame` (преобразовывается в Spark DataFrame).