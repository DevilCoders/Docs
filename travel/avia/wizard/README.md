# Колдунщик авиабилетов

### Как начать разрабатывать:
1. Установить `Arc VCS` через `Self Service`
2. [Смонтировать корень Аркадии](https://arc-vcs.yandex-team.ru/docs/setup/arc/install.html#podkliuchenie-rabochego-dereva) в `$GOPATH/src/a.yandex-team.ru`
3. Открыть `$ARCADIA_ROOT` в `GoLand`
4. Добавить в `Exclude` все директории кроме:
	* `travel/avia/wizard`
	* `travel/avia/lib`
	* `vendor`
	* `library/go`
5. Добавить конфигурацию `Go Build` в `Run configurations`:
    * `Run kind: Directory`
    * `Directory: $ARCADIA_ROOT/travel/avia/wizard/cmd/wizard`
    * `Working directory: $ARCADIA_ROOT/travel/avia/wizard`
    * `✅Run after build`
    * Положить (`Copy-Paste`) содержимое файла `$ARCADIA_ROOT/travel/avia/wizard/cmd/wizard/environment.env`
    в `Environment -> Browse`, заполнив значения для необходимых переменных.
    * [Сгенерировать прото-файлы](#generate-proto)
6. Работа со справочниками:
   Нужно скачать и положить в `$REFERENCE_RESOURCES_PATH` (в `yaml` `referenses.resources.path`) необходимые protobuf-ы сгенерированные [этой Sandbox-таской](https://sandbox.yandex-team.ru/tasks?children=true&hidden=false&type=AVIA_DUMP_DATA&limit=20)
   Необходимые справочники можно посмотреть в [pkg.json](./pkg.json)


После этого должен заработать `Run`/`Debug` из `GoLand`

### Локальный запуск
Нужно выставить переменные окружения перед запуском `./cmd/wizard/wizard`.

    AVIA_WIZARD_LOG_PATH=./logs
    AVIA_WIZARD_YDB_CLUSTER=ydb-ru-prestable.yandex.net:2135
    AVIA_WIZARD_YDB_DATABASE=/ru-prestable/ticket/testing/search_results
    AVIA_WIZARD_BACKEND_BASE_URL=http://backend.testing.avia.yandex.net
    YDB_TOKEN=!!!SECRET!!!
    QLOUD_LOGGER_STDOUT_PARSER=text
    CACHE_SANDBOX_RESOURCES=1
    AVIA_WIZARD_MAX_STATIC_REQUEST_DURATION=10000s
    AVIA_WIZARD_MAX_DYNAMIC_REQUEST_DURATION=10000s
    AVIA_WIZARD_TICKET_DAEMON_API_BASE_URL=http://ticket-daemon-api.testing.avia.yandex.net
    AVIA_WIZARD_SANDBOX_REQUEST_TIMEOUT=5m
    AVIA_WIZARD_DEBUG_LOG_RESPONSE_JSON=0
    AVIA_WIZARD_SENTRY_DSN=
    AVIA_WIZARD_SANDBOX_OAUTH_TOKEN=!!!SECRET!!!
    AVIA_WIZARD_MAX_VARIANTS_INFO_REQUEST_DURATION=5s
    CGO_ENABLED=0
Копируем конфиги
    ```
    cp ./docker/config/wizard/config.development.yaml ./dev/wizard.config.yaml
    ```

Запуск
    ```shell
    ./tools/run.sh
    ```

#### Разработка в `GoLand`
1. Скачать справочники:
    ```shell
    ./tools/download_dicts.sh
    ```
2. Настраиваем `Build configuration`:
    1. `Run -> Edit configurations -> Add New Configuration -> Go Build`
    2. `Run kind: Directory`
    3. `Package path: a.yandex-team.ru/travel/avia/wizard/cmd/wizard`
    4. `Directory: ${ARCADIA}/travel/avia/wizard`
    5. `Working directory: ${ARCADIA}/travel/avia/wizard`
    6. `Environment variables`:
        - `CONFIG_PATH=./dev/wizard.config.yaml`


### Запуск тестов
1. Из Goland: добавить конфигурацию `Go Test` в `Run configurations`:
    * `Test framework: gotest`
    * `Test kind: Directory`
    * `Directory: $ARCADIA_ROOT/travel/avia/wizard/tests`
    * `Working directory: $ARCADIA_ROOT/travel/avia/wizard/tests`
2. Через `ya make`:
    ```
    cd $ARCADIA_ROOT/travel/avia/wizard
    ya make -tt
    ```

### Генерация ya.make файлов
```shell script
bash $ARCADIA_ROOT/travel/avia/wizard/bin/yo_fix_wizard.sh
```

### Generate proto
```shell script
bash $ARCADIA_ROOT/travel/avia/wizard/bin/make_and_generate_proto.sh
```

### Стенды на ПР
Как работает автоматика сдендов на ПР можно прочитать и поправить на wiki:

https://wiki.yandex-team.ru/avia/dev/stand-on-pr/

### Работа с геобазой
* Локально в IDE заставить её работать не получится. Для сборки проекта в GoLand нужно отключить `Preferences -> Go -> Build tags & Vendoring -> CGO Support`
* Актуальный ресурс можно взять в https://sandbox.yandex-team.ru/resources?type=GEODATA6BIN_STABLE
* Текущую версию ресурса в проде можно посмотреть в окружении Qloud

### Описание

#### Ручки

- [WizardHandler](https://a.yandex-team.ru/arcadia/travel/avia/wizard/pkg/wizard/handlers/wizard.go#L21) \
В него ходит поиск. В этой ручке мы логируем бизнесовые метрики

- [VariantsInfoHandler](https://a.yandex-team.ru/arcadia/travel/avia/wizard/pkg/wizard/handlers/variants_info.go#L19) \
В него ходит наша фоновая таска с запросами по популярным направлениям и строит фиды для маркетинга. В ней мы
не логируем запросы так как по ним не нужна аналитика
