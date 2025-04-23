## Быстрый старт

### Начало работы

1. Всё ниже поисходит в namespace `default`
2. Зайдите в саппорт чат, скажите, что вы хотите нами пользоваться

### Пишем protobuf с сообщениями – контрактом тасклета

1. Делаем proto_library как обычно

    {% cut "Скелет:" %}
    ```proto
    syntax = "proto3";

    package tasklet_examples;

    option go_package = "a.yandex-team.ru/tasklet/experimental/examples/proto;taskletexamples";

    message TestInput {
    string branch = 1;
    }

    message TestOutput {
    int result = 1;
    }
    ```
    {% endcut %}

2. Ставим PEERDIR из [/tasklet/registry/common](https://a.yandex-team.ru/arcadia/tasklet/registry/common/ya.make) на свою библиотеку

### Пишем тасклет

1. Делаем каталог, описываем там `PY3_PROGRAM` / `GO_PROGRAM` / `JAVA_PROGRAM` как обычно
2. Создаём t.yaml с описанием и спецификацией

    {% cut "Скелет:" %}
    ```YAML
    meta:
    name: Foo
    description: "Bar"
    namespace: default
    owner: abc:YOUR_ABC_GROUP
    spec:
    naive_schema:
        input_message: tasklet_examples.TestInput
        output_message: tasklet_examples.TestOutput
    executor:
        type: binary
    container:
        cpu_limit: 1000
        ram_limit: 1GB
        workdir:
        type: hdd
        space: 100MB
    ```
    {% endcut %}

3. `ya tool tasklet tasklet create`
4. `ya make -r`
5. `ya tool tasklet build upload --build-schema <your binary file>` – получаем build id
6. `ya tool tasklet label create godemo`
7. `ya tool tasklet label move godemo --to ${build_id}`
8. `ya tool tasklet run godemo input_file.json -i json` – подаём на вход JSON, который CLI сконвертирует в protobuf за нас

## Готовые примеры {#samples}
- [Пример тасклета на Python](https://a.yandex-team.ru/arcadia/tasklet/experimental/tests/tasklets/dummy_tasklet)
- [Пример тасклета на Java](https://a.yandex-team.ru/arcadia/tasklet/experimental/tests/tasklets/dummy_java_tasklet)
- [Пример тасклета на Go](https://a.yandex-team.ru/arcadia/tasklet/experimental/tests/tasklets/dummy_go_tasklet)
