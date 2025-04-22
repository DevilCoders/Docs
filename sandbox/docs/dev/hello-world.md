# Hello World

В этом разделе мы с нуля создадим простейшую задачу для Sandbox. Перед началом убедитесь, что:

* Вы установили все основные инструменты разработки и получили исходные коды Аркадии, как описано в разделе [быстрый старт](/devtools/intro/quick-start-guide).
* Вы ознакомились с основными понятиями Sandbox в предыдущих разделах данной документации.

Для того чтобы создать новую задачу в Sandbox нужно выполнить несколько шагов:

1. Все исходные коды задач Sandbox хранятся в едином репозитории в каталоге [sandbox/projects](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects).
**Создаем каталог задачи** внутри него:

    ```bash
    ~/arcadia/sandbox/projects$ mkdir -p my_project/my_test_task
    ```

    {% note warning %}

    Внутри `sandbox/projects` задачи складываются в подкаталоги, каждый из которых соответствует одному проекту. Создавать новые задачи в корне `sandbox/projects` запрещено (хотя многие старые задачи по-прежнему находятся там). Вместо `my_project` в команде выше следует указать каталог вашего проекта, например, `media`, `market` и так далее.

    {% endnote %}


2. Положить **исходный код задачи на Python** в файл `__init__.py` в новом каталоге (`sandbox/projects/my_project/my_test_task/__init__.py`):

    ```python
    import logging
    from sandbox import sdk2


    class MyTestTask(sdk2.Task):

        def on_execute(self):
            logging.info("Hello, world!")

    ```

    {% note warning %}

    Имя класса задачи (в [CamelCase](https://en.wikipedia.org/wiki/Camel_case)) преобразуется в ее [тип](../tasks.md#type) (в [SNAKE_CASE](https://en.wikipedia.org/wiki/Snake_case)) и должно быть уникально среди всех классов задач. Например, `MyTestTask` преобразуется в `MY_TEST_TASK`.

    {% endnote %}


3. Создать файл **ya.make** в том же каталоге:

    ```bash
    ~/arcadia/sandbox/projects/my_project/my_test_task$ cat ya.make
    SANDBOX_PY23_TASK()

    OWNER(
        your-login # Ваш логин на Staff или имя группы из https://a.yandex-team.ru/arc/trunk/arcadia/groups
    )

    PY_SRCS(
        __init__.py
    )

    END()
    ```

4. Вы можете организовывать произвольную иерархию каталогов с задачами. При этом необходимо, чтобы во всех промежуточных каталогах, где не объявлена задача, лежал пустой `__init__.py` и вот такой **ya.make**:

    ```bash
    ~/arcadia/sandbox/projects/my_project$ cat ya.make
    PY23_LIBRARY()

    OWNER(
       your-login
    )

    PY_SRCS(
       __init__.py
    )

    PEERDIR(
        sandbox/projects/my_project/my_test_task # добавление зависимости на новую библиотеку
    )

    END()

    RECURSE(
        my_test_task # подключение к автоматической сборке всего содержимого новой директории
    )
    ```

    Если вы создаете задачу в каталоге вашего проекта, такой файл **ya.make** обычно уже есть в наличии.
    Вам нужно только добавить туда сведения о новом каталоге `my_test_task`.
    Если вы создаете новый каталог для нового проекта, то сведения нужно добавлять в [sandbox/projects/ya.make](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/ya.make)

5. [Создать пулл-реквест](/devtools/src/arc/workflow#workflow) в единый репозиторий с внесенными изменениями:

    ```bash
    $ arc co -b new-branch-for-new-sandbox-task
    $ arc commit -m 'Hello world Sandbox task'
    $ arc pr create --push
    ```

    При проверке пулл-реквеста будет выполнен набор тестов, проверяющих, что задача имеет правильный синтаксис.

6. Для того чтобы информация об изменениях в задачах появилась в Sandbox, требуется некоторое время после вливания пулл-реквеста.
    Обычно это занимает не больше 5-10 минут.

7. Теперь можно собрать исполняемый файл с задачей:

    ```bash
    ~/arcadia/sandbox/projects/my_project/my_test_task$ ya m
    ```

    затем [получить OAuth-токен для доступа в Sandbox](https://docs.yandex-team.ru/sandbox/dev/binary-task#cli-auth)

    и запустить собранный файл:

    ```bash
    ~/arcadia/sandbox/projects/my_project/my_test_task$ ./my_test_task run
    ```

    так же можно [запустить](../tasks.md#new-task) задачу с типом `MY_TEST_TASK` без сборки и убедиться, что в [лог](../tasks.md#logs)-файл `common.log` будет выведено `Hello, world!`.
