---
title: CPA-платформа
---
# CPA-платформа

## Общая информация

### Чат поддержки

[Ссылка-приглашение](https://app.slack.com/client/T1B8NLW31/CDWRFEE4S)

Обсуждение общих вопросов, ошибок в работе платформы. Координация релизов

## Описание работы компонентов

* [Коллекторы](https://a.yandex-team.ru/arc_vcs/travel/cpa/collectors/README.md)
* [IPv4 proxy](https://a.yandex-team.ru/arc_vcs/travel/cpa/devops/ipv4-proxy/README.md)
* [Обработка данных](https://a.yandex-team.ru/arc_vcs/travel/cpa/data_processing/README.md)
* [Сверки для партнёрских отчётов](https://a.yandex-team.ru/arc_vcs/travel/cpa/data_check/reconciliation/README.md)

## Сборка и деплой

Это всё делает [ПОНЯбот](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/slack_forwarder/README.md)

## Запуск

Для начала нужно проверить в тестинге

Процессы запускаются в [sandbox_planner](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/sandbox_planner/README.md)
[План запуска](https://a.yandex-team.ru/arc_vcs/travel/hotels/devops/sandbox_planner/plan/cpa.yaml)
В качестве шаблона можно использовать существующий коллектор
Чтобы процесс запускался только в тестинге, нужно задать `enabled_prod: false`

После того, как коллектор запущен в тестинге, нужно убедиться в работоспособности конвейера. Данные обрабатываются последовательно по такой цепочке:

    collector -> logbroker/logfeller -> flow_app -> update_orders_incremental

Когда данные нового партнёра прошли по всему конвейеру и ничего не сломалось – можно запускать в проде

## Тестирование

Тестирование flow app описано [здесь](https://a.yandex-team.ru/arc_vcs/travel/cpa/tests/flow/README.md)

* тесты лежат в [tests](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/tests/lib)
* для тестирования понадобятся моки http-сервера, yt (для авиа-коллекторов) и logbroker, код находятся в [checkers.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/tests/lib/checkers.py)
* тест описывается в файле toml`, [например так](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/tests/lib/data/collectors/aviakassa/common_flow.toml)
    * **bin_path** – путь к исполняемому файлу, для коллекторов это всегда `travel/cpa/collectors_exec/collectors_exec`
    * **args** – список аргументов командной строки
    * **checkers** – перечень моков, используемых в тесте; каждому имени в checkers должен соответствовать ключ в корне файла, по которому лежит описание мока
        * **input** – входные данные
        * **output** – выходные данные

Формат входных данных зависит от типа мока

* **http**
    * **mime_type**
    * **responses** – список доступных ответов, ответ выбирается при соответствии path, args и headers по "и"
        * **path** – относительный путь запроса (по- умолчанию `'/'`)
        * **args** – словарь параметров, которые должны присутствовать в запросе (фактический набор параметров может быть больше)
        * **headers** – словарь заголовков, которые должны присутствовать в запросе (фактический набор заголовков может быть больше)
        * **data** – данные для ответа
        * **data_file** – если указан, то данные для ответа считаются из файла
        * **redirect_to** – относительный путь для редиректа
* **yt**
    * **{table_name}** – имя таблицы в тесте
        * **path** – путь к таблице
        * **data** – json-содержимое таблицы

Ожидаемые выходные данные в тестах коллекторов задаются только для logbroker

* **lb**
    * **topic** – топик lb, должен быть уникальным для каждого теста
    * **fields_to_skip** – поля, которые не нужно проверять
    * **expected** – ожидаемые данные


## Графики и алерты

Дашборды, графики и алерты хранятся в аркадии и выгружаются в Соломон с помощью
[solomon tool](https://a.yandex-team.ru/arc/trunk/arcadia/travel/devops/solomon)

[Графики CPA](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/solomon/graphs/cpa)

[Дашборд авиа](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/solomon/dashboards/travel-cpa-avia.yaml)

[Дашборд автобусов](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/solomon/dashboards/travel-cpa-buses.yaml)

[Дашборд отелей](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/solomon/dashboards/travel-cpa.yaml)

[Дашборд поездов](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/solomon/dashboards/travel-cpa-train.yaml)


Ссылки на дашборды в Соломоне:

[Дашборд авиа (тестинг)](https://solomon.yandex-team.ru/?project=travel&cluster=push_testing&service=cpa&dashboard=travel-cpa-avia&l.yt_proxy=hahn&b=1d&e=)

[Дашборд автобусов (тестинг)](https://solomon.yandex-team.ru/?project=travel&cluster=push_testing&service=cpa&dashboard=travel-cpa-buses&l.yt_proxy=hahn&b=1d&e=&autorefresh=y)

[Дашборд отелей (тестинг)](https://solomon.yandex-team.ru/?project=travel&cluster=push_testing&service=cpa&dashboard=travel-cpa&l.yt_proxy=arnold&b=1d&e=&autorefresh=y)

[Дашборд авиа (прод)](https://solomon.yandex-team.ru/?project=travel&cluster=push_prod&service=cpa&dashboard=travel-cpa-avia&l.yt_proxy=hahn&b=1d&e=)

[Дашборд автобусов (прод)](https://solomon.yandex-team.ru/?project=travel&cluster=push_prod&service=cpa&dashboard=travel-cpa-buses&l.yt_proxy=hahn&&b=1d&e=&autorefresh=y)

[Дашборд отелей (прод)](https://solomon.yandex-team.ru/?project=travel&cluster=push_prod&service=cpa&dashboard=travel-cpa&l.yt_proxy=arnold&b=1d&e=&autorefresh=y)

Алерты:

[Алерты для CPA](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/devops/solomon/alerts/cpa).

Для коллекторов авиа и поездов нужно создать новый канал нотификаций

## Рецепты

### Добавление партнёра в CPA-платформу

* написать [коллектор](https://a.yandex-team.ru/arc_vcs/travel/cpa/collectors/README.md) и тесты на него
* добавить обработчик в [data_processing/lib/order_processor.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/data_processing/lib/order_processor.py)
(подробнее [здесь](https://a.yandex-team.ru/arc_vcs/travel/cpa/data_processing/README.md))
* добавить тест по обработке заказа для партнёра
* запустить коллектор в тестинге и убедиться, что появились новые данные и не сломалось то, что работало раньше
* запустить коллектор в проде
* добавить графики на дашборд
* добавить алерты (при необходимости)

### Добавление поля в лэйбл

* Добавить поле в [соответствующий protobuf](https://a.yandex-team.ru/arc_vcs/travel/cpa/data_processing/README.md)

Если это Авиа-лэйбл, тебе не повезло. Нужно ещё:

* В [LabelFieldsAvia.java](https://a.yandex-team.ru/arc_vcs/travel/cpa/data_processing/flow/src/main/java/ru/yandex/travel/cpa/data_processing/flow/model/labels/LabelFieldsAvia.java)
добавить исходное поле из [avia-json-redir-log](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/avia-json-redir-log.json)
* В [LabelJsonDecoderAvia.java](https://a.yandex-team.ru/arc_vcs/travel/cpa/data_processing/flow/src/main/java/ru/yandex/travel/cpa/data_processing/flow/model/labels/LabelJsonDecoderAvia.java)
добавить запись этого поля в protobuf
* В [tests/flow/data.py](https://a.yandex-team.ru/arc_vcs/travel/cpa/tests/flow/data.py) добавить маппинг из имени поля
для avia-json-redir-log в имя поля для protobuf

Для выкатки изменений в прод нужно зарелизить [cpa-flow](http://travel-slack-forwarder.yandex.net:9098/component/cpa-flow)
и [travel-cpa-update-orders-incremental](http://travel-slack-forwarder.yandex.net:9098/component/travel-cpa-update-orders-incremental)


### Перечитать историю заказов

Перечитать историю заказов можно с помощью [collector_multiprocess_run](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/collector_multiprocess_run). Для того, чтобы заказы обрабатывались в очереди с низким приоритетом, он задаёт для коллекторов `--low-priority-order-processing`

### Повторная сборка старых заказов

[Обработка заказов](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/data_processing/README.md#обработка-заказов) происходит инкрементально. Обрабатываются только новые или изменённые заказы. Иногда может понадобиться обработать часть заказов повторно (например, при изменении алгоритма обработки). Для того, чтобы повторно обработать заказы нужно:

* Подготовить ключи заказов в таблице на YT. Расположение таблицы не важно. В таблице обязательно должны быть колонки ключа заказа (**partner_name**, **partner_order_id**)
* Запустить `travel/cpa/tools3 rebuild_orders` отдельно для `arnold` и `hahn` с параметрами
`--src-table {таблица с ключами заказов}`
`--dst-table //home/travel/{{env}}/cpa_flow/order_queue_slow`
* Дождаться окончания обработки. Можно следить на графике ([тестинг](https://solomon.yandex-team.ru/?project=travel&cluster=push_testing&service=cpa&yt_proxy=arnold&graph=travel-cpa-incremental-order-count&autorefresh=y&b=1h&e=), [прод](https://solomon.yandex-team.ru/?project=travel&cluster=push_prod&service=cpa&yt_proxy=arnold&graph=travel-cpa-incremental-order-count&autorefresh=y&b=1h&e=)) за значением *slow_not_processed*

### Как скрыть поле

Для некоторых бизнес-задач (например, партнёрская программа) нужны приватные данные пользователя. Чтобы ограничить доступ к приватным данным, *update_orders_incremental* сохраняет результаты работы в два набора таблиц, *публичные данные* и *приватные данные*. *Приватные данные* содержат весь набор полей, *публичные данные* не содержат приватных полей. Для того, чтобы поле считалось приватным, его нужно атрибуцировать. Если поле находится в основной части заказа (не в лейбле), в [модели заказа](https://a.yandex-team.ru/arcadia/travel/cpa/data_processing/lib/order_data_model.py) нужно задать для поля признак [hidden](https://a.yandex-team.ru/arcadia/travel/library/python/schematized/fields.py?rev=r9585306#L21). Если поле в лейбле, нужно для него задать опцию [HiddenField](https://a.yandex-team.ru/arcadia/travel/proto/cpa/proto_options/options.proto?rev=r9585306#L13) в proto, описывающем лейбл
