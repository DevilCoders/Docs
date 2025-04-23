# Bazel rules

`Рул` – это декларативное описание набора действий с входами и выходами.

Основные рулы, которые мы используем:

1) `scala_library` – сборка scala-библиотеки. Подробнее в [rules_scala][rules_scala_link].

    Пример:
    ```
    scala_library(
        name = "statist", # имя таргета
        srcs = glob(["src/StatistClient.scala"]), # список файлов с исходным кодом
        visibility = ["//visibility:public"], # настройки видимости
        deps = [ # зависимости
            ":model", # зависимость от другого таргета по относительному пути
            "//schema-registry/proto/vertis/statist:api_model_scala_proto", # зависимость от другого таргета по абсолютному пути
            "@maven//:dev_zio_zio_2_13", # maven-зависимость, версия берется из maven_install.json
        ],
    )
    ```

2) `scala_binary` – сборка исполняемого jar из scala-кода. Подробнее в [rules_scala][rules_scala_link].

    Пример:
    ```
    scala_binary(
        name = "api", # имя таргета
        srcs = glob(["src/**/*.scala"]), # список файлов с исходным кодом
        main_class = "ru.yandex.vertis.general.bonsai.public_api.Main", # полное имя main-класса
        resource_strip_prefix = package_name() + "/resources",
        resources = glob(["resources/**/*"]), # список файлов с ресурсами
        visibility = ["//visibility:private"], # настройки видимости
        runtime_deps = [], # рантайм зависимости
        deps = [ # зависимости
            "//common/cache:api",
        ]
    )
    ```

3. `scala_image` – сборка docker-образа. Подробнее в [docker](docker.md).

    Пример:
    ```
    scala_image(
        name = "image", # имя таргета
        binary = ":public-api", # путь до scala_binary таргета
        jvm_flags = [ # дополнительные jvm-флаги
            "-Xms3g",
            "-Xmx3g",
        ],
        main_class = "ru.yandex.vertis.general.bonsai.public_api.Main", # полное имя main-класса
        service = "bonsai-api", # имя сервиса (будет в имени образа)
        visibility = ["//visibility:private"], # настройки видимости
    )
    ```

4. `shiva_service` – описание сервиса. Позволяет [локально](../run-service.md) запускать сервисы, а также автоматически прорастает в [CI-релизы](../../ci/intro.md).

    Пример:
    ```
    shiva_service(
        name = "service", # имя таргета
        binary = ":public-api", # путь до scala_binary таргета
        service_name = "bonsai-api", # имя сервиса из карты
    )
    ```

5. `owner_team` – описание команды владельцов. Подробности в настройках [CI](../../ci/codeowners.md).

    Пример:
    ```
    owner_team(
        name = "scala-common",
        abc_roles = ["vs_devtools:scala-common"],
        assign = 3, # по умолчанию 1
        ship = 1, # по умолчанию = assign
    )
    ```

6. `review_rule` – описание ревью-правила. Подробности в настройках [CI](../../ci/codeowners.md).

    Пример:
    ```
    review_rule(
        team = "//teams:scala-common",
        ship = 2,
        subpaths = ["grpc/**", "db/**", "!dashboards/**"],
    )
    ```

7. `prometheus_alert` – описание juggler-мониторинга по данным Prometheus. Подробности в настройках [мониторингов](../../operations/alerts/prometheus.md).

    Пример:
    ```
    prometheus_alert(
        name = "alive", # имя таргета для базеля
        alert_name = "ServiceAlive", # Имя алерта в прометеусе
        expression = """up{_service="my-service"} > 4""",
        for_duration = "5m",
        host = "my-service", # имя хоста для juggler'а
        summary = "", # Краткое описание метрики
        # Можно использовать плейсхолдер {{ $value }} для получение текущего значения метрики
        # или {{ $labels.<label>}} для получения label сработавшей метрики
        # https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/#templating
        tags = ["my-super-group"], # теги будут проброшены в juggler, если есть тег manual, то алерт будет проигнорен автоматикой.
        prod = True, # Генерировать алерт для продакшена
        test = False, # Генерировать алерт для тестинга
    )
    ```

8. `solomon_alert` – описание juggler-мониторинга по данным Solomon.

    Пример:
    ```
    solomon_alert(
        visibility = ["//visibility:public"],
        name = "alive", # имя алерта
        id = "alive", # id алерта в Solomon
        program = "...", # программа на языке Solomon
        group_by_labels = ["TopicPath"],
        annotations = {"text": "text", "tags": "tag1,tag2"},
        description = description, # описание проверки
        channels = ["verticals-backend-juggler"], # каналы для нотификаций
    )
    ```

[rules_scala_link]: https://github.com/bazelbuild/rules_scala
