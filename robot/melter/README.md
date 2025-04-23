# SaaS 2.0 @ Jupiter

## Инструкция по настройке и эксплуатации

### Инструменты

Ниже в инструкции будут использоваться альясы на следующие инструменты

1. [big_rt_cli] –– тулза для создания и настройки цезарных очередей
1. [yt_dynamic_tables] –– тулза для настройки PlutoniumFS (рабочей директории воркера)
1. [melter](./) –– сам воркер

### Настройка входной Цезарной очереди для инкрементального обновления индекса для SaaS 2.0

1. Создаем Цезарную очередь для потоковой поставки данных для варки индексов

    ```bash
    big_rt_cli queue create <queue path> --max-ttl 3d --shards <shards count>
    ```

    Параметр `--max-ttl` указывает на гарантированный срок жизни строк в YT-таблицах. Разумно его указывать в пределах от 2 до 3-х дней.

2. Настраиваем консьюмера, через который будут читать данные из Цезарной очереди

    ```bash
    big_rt_cli consumer create <queue path> <consumer name> --ignore-in-trimming 0
    ```

    Метаданные консьюмера создаются в `<queue path>/<consumer name>`. Метаданные представляют из себя таблички с оффсетамии по каждому из шардов в очереди.

3. Далее мы донастраиваем очередь пользовательскими атрибутами. Настройка необходима для интеграции инструментов SaaS 2.0 с Цезарной очередью. Взято из примера [plutonium/examples/yt_static_tables_file_system_dynamic_queue_erf_chunks](https://arcanum.yandex-team.ru/arc_vcs/search/plutonium/examples/yt_static_tables_file_system_dynamic_queue_erf_chunks).

    ```bash
    # Установка через атрибут информации о протобуфах в очереди
    yt set <queue path>/@allowed_proto_types "[\"NMelter::TMelterQueueItem\";]"

    # Если при записи в очередь протобуфы упаковались по несколько штук в одну строку, то нужно выставить значение "[\"enable_frame_unpacker\";]". В общем случае в атрибут пишем пустой список.
    yt set <queue path>/@queue_format_flags "[]"
    ```

    `NMelter::TMelterQueueItem` –– это тип данных (протобуфа), которые будут поступать в очередь.

4. <details><summary>* Опциональный пункт по загрузке данных в очередь.</summary>
    Далее можно загрузить в очередь тестовые данные, взяв их с дампа теста [callisto_mercury_test]. Скачиваем данные таблицы. Вставляем строки на кластер.

    ```bash
    cat <queue-content> | yt insert --format '<format=pretty>yson' <queue path table>
    ```

    Be ware! По умолчанию YT не партиционирует строки между все таблетами, но это можно сделать самому написав небольшой python-скрипт, который случайным образом проставлять каждой строке `$tablet_index`

    Пример:

    ```python
    #!/usr/bin/env python

    import cyson
    import sys
    import random

    TABLETS_CNT = 64

    if __name__ == "__main__":
        with open("./tmp/queue2", "w") as out_f:
            with open("./tmp/queue", "r") as in_f:
                input_ = cyson.list_fragments(cyson.InputStream.from_fd(in_f.fileno()), process_table_index=True)
                output_ = cyson.OutputStream.from_fd(out_f.fileno())

                writer = cyson.Writer(
                    output_,
                    format="pretty",
                    mode="list_fragment"
                )

                writer.begin_stream()

                for record in input_:
                    record["$tablet_index"] = random.randint(0, TABLETS_CNT - 1)
                    writer.write(record)

                writer.end_stream()
    ```

    </details>

### Настройка рабочей директории воркера с файловой системой SaaS 2.0

1. Создание рабочей директории воркера

    ```bash
    yt_dynamic_tables create-tables --yt-dir <working_dir path>
    ```

2. Инициализации шардов SaaS 2.0 для файловой системы.

    ```bash
    yt_dynamic_tables init-shards --yt-dir <work dir> --yt-proxy arnold --state-id-generator iso8601 --schema <tablets mapping schema>
    ```

    Для каждого шарда будет создана отдельная map node для [распределенных блокировок](https://yt.yandex-team.ru/docs/description/locking/cypress_as_locking_service). Когда стартует демон, то берется блокировка каждым отдельным воркером. Блокировка определяет шард, который будет наливать воркер.

    Помимо этого для каждого неймспейса проинициализируется начальное состояние (смотри табличку `<working_dir>/current_state`) и служебный файл `__modifications_queue_offset__`, в котором будут храниться оффсеты модификаций очереди по каждому из стейтов.

    Для каждом шарда SaaS 2.0 создается служебный файлик в **WorkerFS** с изначальными оффсетами очереди по обрабатываемым таблетам.

    Подробнее с логикой можно ознакомиться в [исходниках](https://arcanum.yandex-team.ru/arc_vcs/search/plutonium/tools/yt_dynamic_tables/init_shard.cpp?rev=r8941010#L72).

3. Опционально можно создать директорию для локов `garbage_collector`:

    ```bash
    yt create -r map_node <work_dir>/gc_locks/main
    ```

### Настройка табличек контроллеров

Таблички контроллеров должны создаваться автоматически. Мап ноды лучше создать руками для каждой из инсталляций: https://jing.yandex-team.ru/files/sikalov/2022-03-23T12:47:09Z.51e82b9.png

Стоит удостовериться, что флажок для автоматического создания табличек проставлен: https://arcanum.yandex-team.ru/arc/trunk/arcadia/search/plutonium/deploy/core/proto/config.proto?rev=r9092913#L57

**Attention!!** после создания табличек нужно запустить скрипт по выставлению ttl и инициализации табличек _notify/notify_positions_ у табличек chunk ctrl с помощью скрипта [prepare_chunkctrl_tables.sh](./utils/prepare_chunkctrl_tables.sh):

```
./prepare_chunkctrl_tables.sh   //home/callisto/melter/ctrl/sas/chunkctrl_kvrs
./prepare_chunkctrl_tables.sh   //home/callisto/melter/ctrl/vla/chunkctrl_kvrs
./prepare_chunkctrl_tables.sh   //home/callisto/melter/ctrl/man/chunkctrl_kvrs
```

Без этого chunkctrl будет работать некорректно.

### Полный скрипт настройки

```bash
#! /usr/bin/env bash

set -x

big_rt_cli=$HOME/arc/arcadia/ads/bsyeti/big_rt/cli/big_rt_cli
yt_dynamic_tables=$HOME/arc/arcadia/search/plutonium/tools/yt_dynamic_tables/yt_dynamic_tables
melter=$HOME/arc/arcadia/robot/mercury/tools/melter/melter

SHARDS_CNT=64
MELTER_DIR=//home/melter
QUEUE_PATH=$MELTER_DIR/rt_index
WORKDIR_PATH=$MELTER_DIR/work_dir
TABLETS_MAPPING_PATH=configs/worker/<schema mapping>
CONSUMER_NAME=melter_consumer
WORKERS_CNT=32

# Attention! Configure for your own case
export YT_PROXY=dione.man.yp-c.yandex.net:27589
export YT_USER=root


$big_rt_cli queue create $QUEUE_PATH --max-ttl 3d --shards $SHARDS_CNT
$big_rt_cli consumer create $QUEUE_PATH $CONSUMER_NAME --ignore-in-trimming 0

yt set $QUEUE_PATH/@allowed_proto_types "[\"NMelter::TMelterQueueItem\";]"

# Attention! Check that you use packer writing to caesar queue
yt set $QUEUE_PATH/@queue_format_flags "[\"enable_frame_unpacker\";]"

$yt_dynamic_tables create-tables --yt-dir $WORKDIR_PATH
$yt_dynamic_tables init-shards --yt-dir $WORKDIR_PATH --state-id-generator iso8601us --schema $TABLETS_MAPPING_PATH
```

### Генерация конфигов

```bash
# Скрипты генерации моно найти в ya.make
ya make configs
```

## Запуск воркера

### Для одного стрима (namespace)

```console
# Note that -c/--config/--config-json/--config-text are different options, you need exactly --cfg
melter Daemon --cfg <config path>
```

### Для нескольких стримов (с одной машины в несколько процессов)

```bash
#! /usr/bin/env bash

# Configurable variables
CONFIG_PATH="./configs/worker/worker-config.pb.txt.gen"
WORKER_LOGS_DIR="./melter-logs"
WORKER_BIN="./impl/worker/worker"
YT_PROXY=arnold
WORKERS_CNT=32

# Trap handler
trap 'pkill -P $$' SIGINT

mkdir -p $WORKER_LOGS_DIR

for workerId in $(seq 0 $(($WORKERS_CNT - 1))); do
    YT_PROXY=$YT_PROXY YT_USER=$YT_USER $WORKER_BIN Daemon --cfg $CONFIG_PATH >$WORKER_LOGS_DIR/melter.$workerId.out 2>$WORKER_LOGS_DIR/melter.$workerId.err &
done

tail -f $WORKER_LOGS_DIR/melter.0.err &

wait
```

## Тестирование воркера

[Тесты](./test/worker/) на воркер фактически являются E2E. При запуске используется подготовленный снепшот со всеми необходимыми табличками на YT. В тесте прогоняется процессинг воркера входной очереди и формируется RuntimeFS SaaS 2.0. Документы с их лампами дампятся с помощью [специального принтера](./utils/melter_printer/main.cpp) из RuntimeFS и диффуется с каноническими данными.

### Обновление входной очереди для теста

Для обновления тестового контента очереди тестового снепшота при обновлении кода в меркуриальном воркере можно запустить [каллистовский тест](../mercury/test/callisto_test/) и сдампить оттуда очередь `//home/jupiter/mercury/RtIndexQueue/queue`:

```bash
ya download sbr:<id test snapshot data> --output=test_snapshot
YT_PROXY=<local YT proxy under test> yt select-rows '[$tablet_index], value, codec from [//home/jupiter/mercury/RtIndexQueue/queue]' --format="<format=binary>yson" > test_snapshot/rt_index/queue
ya upload --skynet test_snapshot
```

[big_rt_cli]: https://arcanum.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/cli
[yt_dynamic_tables]: https://arcanum.yandex-team.ru/arc_vcs/search/plutonium/tools/yt_dynamic_tables
[yt]: https://yt.yandex-team.ru/docs/api/cli/cli
[melter]: ./
[callisto_mercury_test]: ../../test/callisto_test
