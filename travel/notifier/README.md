# Travel.Notifier
## Система уведомлений Путешествий
### [Документация](https://docs.yandex-team.ru/travel/dev/notifier)

---

### CI

- [Конфигурация релизного процесса](./a.yaml)
- [Сборка архива](./api.pkg.json) с помощью `YA_PACKAGE`
- [Релизы в `NewCI`](https://arcanum.yandex-team.ru/ci/ticket/releases/timeline?dir=travel%2Fnotifier&id=travel-notifier-release)
- [Проект в Deploy](https://deploy.yandex-team.ru/projects/travel-notifier)

---

#### Разработка локально в `GoLand`

1. Копируем конфиг-файл, заполняем необходимые переменные:
    ```shell script
    cd ${ARCADIA}/travel/notifier
    cp ./config/api/config/config.development.yaml .
    vim config.development.yaml
    ```
2. Настраиваем `Build configuration`:
    1. `Run -> Edit configurations -> Add New Configuration -> Go Build`
    2. `Run kind: Directory`
    3. `Directory: ${ARCADIA}/travel/notifier/cmd/api`
    4. `Working directory: ${ARCADIA}/travel/notifier`
    5. `Environment variables`:
        - `CONFIG_PATH=config.development.yaml`
        - `DEPLOY_TVM_TOOL_URL=http://localhost:9005`
        - `TVMTOOL_LOCAL_AUTHTOKEN=********************************`
3. ```shell script
    cd ${ARCADIA}/travel/notifier
    ya make --yt-store --add-result=.go
   ```
4. `Run`/`Debug`
5. Опционально можно добавить еще одну `Build configuration` с запуском `${ARCADIA}/travel/notifier/tools/run-tvmtool.sh` и объединить её с основной конфигурацией в конфигурацию с типом `Compound`. Либо самостоятельно запускать `tvmtool` перед запуском приложения.
6. Для запуска некоторых тестов нужен локальный PostgreSQL. В `ya make -tt` он появляется по рецепту `INCLUDE(${ARCADIA_ROOT}/antiadblock/postgres_local/recipe/recipe.inc)`. Для запуска тестов в IDE нужно сделать:
    ```
    brew install postgres
    brew services start postgresql
    psql -c "CREATE DATABASE postgres"
    psql -d postgres
    ```

    ```
    postgres=# CREATE USER postgres WITH ENCRYPTED PASSWORD 'postgres';
    postgres=# grant all privileges on database postgres to postgres;
    ```
7. Работа со справочниками:
    Для локальной разработки нужно скачать и положить в `$DICTS_RESOURCES_PATH` (в `yaml` `dicts.resources_path`) необходимые protobuf-ы сгенерированные [этой Sandbox-таской](https://sandbox.yandex-team.ru/tasks?children=true&hidden=false&type=DUMP_RASP_DATA)
    Необходимые справочники можно посмотреть в [pkg.json](./api.pkg.json)
8. tvmtool:
    Для выписывания сервисных тикетов через tvm необходим локально запущенный tvmtool демон.
    В Deploy environment этот демон предоставляется автоматически и работает на порту lohalhost:2.
    Чтобы поднять его локально, см. здесь: https://wiki.yandex-team.ru/avia/dev/notifier/nastrojjka-tvm-/-tvmtool/

---

#### Полезные скрипты
| Script | Description |
|--------|-------------|
| [tools/make.sh](./tools/make.sh) | Собирает приложение и генерирует `*.pb.go` файлы |
| [tools/run-tests.sh](./tools/run-tests.sh) | `ya make --yt-store -tt` |
| [tools/run-dev.sh](./tools/run-tests.sh) | Запускает [`tools/make.sh`](./tools/make.sh) и запускает сервис локально |
| [tools/fix_ya_make.sh](./tools/fix_ya_make.sh) | `ya tool yo fix .` |
| [tools/format.sh](./tools/format.sh) | `ya tool go fmt ./...` |


#### Как ходить в тестинг с `TVM`
1. Выписываем тикет в обмен на свой SSH-ключ:
    - `ya tool tvmknife get_service_ticket sshkey --src 2025412 --dst 2025412`
2. Указываем полученный тикет в заголовке `X-Ya-Service-Ticket` grpc-запроса

- Пример для `grpcurl`:
 ```
grpcurl -v -plaintext -H 'X-Ya-Service-Ticket: $TICKET' $HOST:9001 grpc.health.v1.Health/Check
```

Также в `unstable`/`testing` можно получать с помощью grpcurl:
- Список сервисов: `grpcurl -v -plaintext $HOST:9001 list`
- Список методов сервиса: `grpcurl -v -plaintext $HOST:9001 list grpc.health.v1.Health`


#### Unified-Agent

- Конфиги лежат [здесь](./config/unified_agent/config)
- Чтобы обновить конфиг:
  - Из корня проекта выполняем

    ```ya upload --ttl inf -T OTHER_RESOURCE --tar config/unified_agent```
  - Переходим по полученному `Resource link`
  - Берем rbtorrent-ссылку на ресурс
  - Обновляем rbtorrent-ссылку для layer с конфигами в нужном stage в box `unified_agent`. [Пример для testing](https://deploy.yandex-team.ru/stages/travel-notifier-testing/edit/du-api/box-unified_agent)
  - Выкатываем новую версию stage

#### Логи в YT:
- [pretrip-render-log](./internal/service/pretrip/logging/renderlog/README.md)


#### Как добавить новый тип уведомления:
1. Добавляем новую структуру в [notification_type.go](./internal/models/notification_type.go)
2. Опционально (если есть подтипы) добавляем subtype в [notification_subtype.go](./internal/models/notification_subtype.go)
3. Добавляем сервис в директорию [internal/service](./internal/service). Можно смотреть на [pretrip](internal/service/pretrip). Сервис должен построить необходимые уведомления и запланировать их (сохранить в БД)
4. Если наше уведомление имеет `DispatchType = push` – добавляем `processor`. `processor` нужно зарегистрировать при создании `ProcessingService` [тут](https://a.yandex-team.ru/arc_vcs/travel/notifier/cmd/processor/main.go?rev=r9143647#L170). Процессор принимает на вход уведомление и должен решить, что с ним делать – отправлять, отменять, etc.
