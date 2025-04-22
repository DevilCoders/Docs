# Trains.SearchApi

Точка входа для предзаказной части Поездов.
Поиск для travel-api и колдунщик.

---

# Links
- [Конфигурация релизного процесса](./a.yaml)
- [Сборка архива](./pkg.json) с помощью `YA_PACKAGE`
- [Wiki](https://wiki.yandex-team.ru/travel/wizards/projects/train-wizard-api-go/)
- [Релизы в `NewCI`](https://arcanum.yandex-team.ru/ci/trainbus/releases/timeline?dir=travel%2Ftrains%2Fsearch_api&id=search-api-release)
- [Проект в Deploy](https://deploy.yandex-team.ru/projects/trains-search-api)
- [Танкер](https://tanker.yandex-team.ru/project/travel-backend?branch=master)

# Разработка
- [Локальный swagger](http://127.0.0.1:9002/swagger/)
- Обновить схему логфеллера
```shell
export a=<path to arcadia root>
cd $a/travel/trains/search_api/api
$a/contrib/tools/protoc/bin/protoc --descriptor_set_out=$a/logfeller/configs/parsers/travel-trains-search_api-search_log.desc -I$a -I$a/contrib/libs/protobuf -I$a/travel/proto/ -I$a/contrib/libs/googleapis-common-protos -I$a/contrib/libs/protobuf/src --include_imports --include_source_info -I. ./search_api_service.proto
```

# Как катить?
- Запускаем новый релиз [тут](https://arcanum.yandex-team.ru/ci/trainbus/releases/timeline?dir=travel%2Ftrains%2Fsearch_api&id=search-api-release)
- Чтобы выкатить нужно прожать кнопку необходимого стейджа на текущем графе релиза

# Как запустить?
- секреты для справочников лежат в [rasp-common-testing](https://yav.yandex-team.ru/secret/sec-01cmw91jcrtk5fpvjq0ev9wdnx/explore/versions)
- остальные секреты получаем из [trains-common-testing](https://yav.yandex-team.ru/secret/sec-01f3td8gjk2espct0f2djg53sm/explore/versions)
```shell
export SEARCH_API={{path to search_api}}

cp $SEARCH_API/docker/search_api/config.development.yaml $SEARCH_API/
vim $SEARCH_API/config.development.yaml

ya make -r $SEARCH_API
CONFIG_PATH=$SEARCH_API/config.development.yaml $SEARCH_API/cmd/search_api/search_api
```

# Style checking
Для автоформатирования проекти используется следующий список комманд
```shell
ya style $SEARCH_API    # автоформатирование с импортами

ya tool yo fix $SEARCH_API       # автогенерация ya.make и */gotest
                                 # к сожалению не уберает лишнее,
                                 # так что немного нужно поправить
```

# Solomon
Для начала нужно верно разложить переменные -> [quickstart](https://a.yandex-team.ru/arc/trunk/arcadia/travel/devops/solomon#quickstart)

В README все команды запускаются с флагом -n (подавление изменений). Для применения дифа нужно убрать флаг

### Собрать тулзу
```shell
ya make -r $ARCADIA/travel/devops/solomon/
export SOLOMON=$ARCADIA/travel/devops/solomon/solomon
```

### Подтянуть текущее состояние solomon в код
```shell
# dashboard
$SOLOMON -n dashboards --service=search_api pull

# graphs
$SOLOMON -n graphs --service=search_api pull
```

### Отправить текущую конфигурацию в solomon (ALARM!!! перетрет изменения в solomon'е)
```shell
# dashboard
$SOLOMON -n dashboards --service=search_api push

# graphs
$SOLOMON -n graphs --service=search_api push

# alerts
$SOLOMON -n alerts --alert=search_api/5xx push
$SOLOMON -n alerts --alert=search_api/http-panics push
$SOLOMON -n alerts --alert=search_api/http-timings push
$SOLOMON -n alerts --alert=search_api/loading-cache-fails push
$SOLOMON -n alerts --alert=search_api/logbroker-lag push

```


# TemplatesDumper
Тулза для проверки шаблонов seo-страниц и их дампа из танкера в s3
[Документация по работе с шаблонами](https://docs.yandex-team.ru/travel/services/trains/seo-pages)
[Код дампера](./cmd/templates_dumper)

## Локальный запуск
Локально удобно запускать с тем же config.development.yaml, что и search-api, поправив там настройки seo.s3... и tanker-oauth-token.
Собираем, запускаем cmd/templates_dumper.

## Запуск в sandbox
Создаем новую задачу TRAINS_DUMP_TEMPLATES, выбираем Environment из testing/production, запускаем.

## Работа в sandbox
В sandbox запускается с помощью задачи TRAINS_DUMP_TEMPLATES.
Бинарная sandbox-задача [TRAINS_DUMP_TEMPLATES](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/rasp/TrainsDumpTemplates) при выполнении
ищет последний released ресурс типа TRAVEL_TRAINS_TEMPLATES_DUMPER_PACKAGE, распаковывает его и
запускает с правильными настройками в зависимости от параметра задачи Environment, выводит лог в Info задачи.

## Сборка
### TRAINS_DUMP_TEMPLATES
Собрать бинарную sandbox-задачу можно:
- в sandbox [DEPLOY_BINARY_TASK](https://docs.yandex-team.ru/sandbox/dev/binary-task#deploy-binary-task)
- локально на Linux (на mac-os не сработает)
```shell
cd $A/sandbox/projects/rasp/TrainsDumpTemplates
ya make
./TrainsDumpTemplates run --type TRAINS_DUMP_TEMPLATES -o RASP --attr task_type=TRAINS_DUMP_TEMPLATES --create-only
```

### TRAVEL_TRAINS_TEMPLATES_DUMPER_PACKAGE
TRAVEL_TRAINS_TEMPLATES_DUMPER_PACKAGE это tarball архив search_api.
Когда исправили логику рендера шаблонов, изминили поля структур для seo-страниц, или поправили фильтры, то
нужно собрать и зарелизить новую версию ресурса TRAVEL_TRAINS_TEMPLATES_DUMPER_PACKAGE.

Собираем локально и загружаем в sandbox:
```shell
cd $A/travel/trains/search_api
ya package --yt-store --tar --target-platform=Linux --ttl inf --sandbox --upload-resource-type TRAVEL_TRAINS_TEMPLATES_DUMPER_PACKAGE --owner=RASP --upload pkg.json
```

Тыкаем релиз testing в sandbox, проверяем. Когда пришло время тыкаем релиз stable.
