## Сервис для объединения заказов в поездки (aka путешествия aka trips)
### Компоненты
#### API
GRPC-API для фронта (через TravelAPI)
#### Processor
Компонента, отвечающая за формирование и сохранение сущности `Trip` на основе заказов пользователя
#### Collector
Компонента, отвечающая за:
  - сбор событий создания и изменения заказа из различных источников:
    - `travel-orders`
    - `travel-cpa`
    - ???
  - уведомление `Processor` об этих событиях
### Запуск в dev окружении:
`$component = api | collector | processor`
0. Инициализировать конфиги
    ```shell
    ./tools/init_configs.sh
    ```
1. Заполнить все секреты в конфиге нужной компоненты
    ```
    vim ./dev/$component.config.yaml
    ```
2. ```shell
   ./tools/run-dev-$component.sh
   ```

#### Разработка в `GoLand`
0. Простая инициализация проекта:
    ```shell
    cd ${ARCADIA}
    ya ide goland ${ARCADIA}/travel/komod/trips/
    ```
1. Для работы нужно сгенерировать нужные proto:
   ```shell
   ./tools/make.sh
   ```
2. Скачать справочники:
    ```shell
    ./tools/download_dicts.sh
    ```
3. Копируем конфиг-файл, заполняем необходимые переменные:
   ```shell
   ./tools/init_cofigs.sh
   vim ./dev/$component.config.yaml
   ```
4. Настраиваем `Build configuration`:
    1. `Run -> Edit configurations -> Add New Configuration -> Go Build`
    2. `Run kind: Directory`
    3. `Directory: ${ARCADIA}/travel/komod/trips/cmd/$component`
    4. `Working directory: ${ARCADIA}/travel/komod/trips`
    5. `Environment variables`:
        - `CONFIG_PATH=./dev/$component.config.yaml`

3`Run`/`Debug`


#### Ещё немного про запуск и разработку

Для отладки лучше создать свою БД в YDB и пользоваться ей
https://ydb.yandex-team.ru/docs/quickstart#kak-sozdat-svoyu-bd

#### Проблемы с CGO
- полечить 	`imports github.com/DataDog/zstd: invalid input file name "_cgo_gotypes.go"` при запуске мне помогал флаг CGO_ENABLED=0

#### Проверить API через grpcurl

Список доступных функций: `grpcurl -plaintext localhost:9001 describe`

#### local TVM

- Нужно настроить tvmtool ([wiki](https://wiki.yandex-team.ru/avia/dev/services-table/notifier/nastrojjka-tvm-/-tvmtool/))
- Перед запуском установить переменные окружения:
  - `DEPLOY_TVM_TOOL_URL=http://localhost:9005`
  - `TVMTOOL_LOCAL_AUTHTOKEN=...`
- Получить user-ticket:
  - `echo '$BLACKBOX_OAUTH' | ya tool tvmknife get_user_ticket oauth --tvm_id 2025412`


#### Отправка заказов из оркестратора в очередь на процессинг
- Зайти на инстанс `collector` в нужном окружении
- ```shell
  cd collect_orders
  vim ./configs/config.$YANDEX_ENVIRONMENT_TYPE.yaml
  CONFIG_PATH=/collect_orders/configs/config.$YANDEX_ENVIRONMENT_TYPE.yaml ./collect_orders
  ```


#### Апдейт конфига Unified Agent
1. Заливаем конфиги в Sandbox
    ```shell
    ya upload --ttl inf -T OTHER_RESOURCE --tar ./configs/unified_agent
    ```
2. Обновляем в Ya.Deploy stage версию ресурса с конфигом на новую


#### Обновление схемы YT-логов:
- [processing-events-log](./internal/processor/eventslogger/README.md)
