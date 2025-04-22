# avia-search-results-queue-producer

Сервис для наполнения очереди из результатов опроса партнеров (aka "писчий"<sup><a href="https://a.yandex-team.ru/arc_vcs/library/python/errorboosterclient/errorboosterclient/logbroker.py?rev=242e866357a9f9e014cd8ce579091a48ef356a48#L143">[1]</a></sup>)
Как работает:
1. Сервис читает сообщение (`qid`) из logbroker-topic `/avia/$environment/ticket-daemon/processed-qid`
2. Получает из YDB результаты по полученному `qid` 
3. Распаковывает
4. Перекладывает в protobuf. [proto-spec](https://a.yandex-team.ru/arc_vcs/travel/avia/library/proto/search_result/v1/result.proto)
5. Записывает полученный protobuf в очередь `/avia/$environment/search-results-queue`

---

### CI

- [Конфигурация релизного процесса](./a.yaml)
- [Сборка архива](./pkg.json) с помощью `YA_PACKAGE`
- __TODO:__ Релизы в `Release Machine` 
- [Проект в Deploy](https://deploy.yandex-team.ru/projects/avia-search-results-queue-producer)

---

#### Разработка локально в `GoLand`

1. Копируем конфиг-файл, заполняем необходимые переменные:
    ```shell script
    cd ${ARCADIA}/travel/avia/search_results_queue_producer
    cp ./config/search_results_queue_producer/config/config.development.yaml .
    vim config.development.yaml
    ```
2. Настраиваем `Build configuration`:
    1. `Run -> Edit configurations -> Add New Configuration -> Go Build`
    2. `Run kind: Directory`
    3. `Directory: ${ARCADIA}/travel/search_results_queue_producer/cmd/search_results_queue_producer`
    4. `Working directory: ${ARCADIA}/travel/search_results_queue_producer`
    5. `Environment variables`:
        - `CONFIG_PATH=config.development.yaml`
4. ```shell script
    cd ${ARCADIA}/travel/search_results_queue_producer
    tools/make.sh
   ```
5. `Run`/`Debug`
6. Работа со справочниками:
    Для локальной разработки нужно скачать и положить в `$DICTS_RESOURCES_PATH` (в `yaml` `dicts.resources_path`) необходимые protobuf-ы сгенерированные [этой Sandbox-таской](https://sandbox.yandex-team.ru/tasks?children=true&hidden=false&type=DUMP_RASP_DATA)
   Необходимые справочники можно посмотреть в [pkg.json](./pkg.json)
   

---

#### Полезные скрипты
| Script | Description |
|--------|-------------|
| [tools/make.sh](./tools/make.sh) | Собирает приложение и генерирует `*.pb.go` файлы |
| [tools/run-tests.sh](./tools/run-tests.sh) | `ya make --yt-store -tt` |
| [tools/run-dev.sh](./tools/run-tests.sh) | Запускает [`tools/make.sh`](./tools/make.sh) и запускает сервис локально |
| [tools/fix_ya_make.sh](./tools/fix_ya_make.sh) | `ya tool yo fix .` |
| [tools/format.sh](./tools/format.sh) | `ya tool go fmt ./...` |
