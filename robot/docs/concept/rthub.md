# Устройство RTHUB

## Схема Real Time вычислений в облаке для документов (страниц, картинок, видео, хостов)

coming soon


## Описание процесса

{% cut "Процесс преобразования входных сообщений в выходные описывается таким конфигом" %}

```js
Channel {
    Input {
        // Как подключиться к входной очереди
        Source {
            Server: "sas.logbroker.yandex.net"
            Topic: "kwyt-zora-to-rthub-pages"
            LogType: ""
            Client: "rthub"
            MaxPartitions: 15
        }

        // Ограничивает число вычитанных из очереди сообщений, по которым пока не был получен ответ о записи в выходную очередь
        InflightLimit {
            ItemsCount: 1000
            ItemsSizeInBytes: 100000000
        }

        // Текущий формат сообщений от зоры — XObject-ы
        // https://a.yandex-team.ru/arc/trunk/arcadia/zora/xcalc/object/proto/object.proto
        // Этот флажок включает логику по их преобразованию в protobuf-ы — необходимо для purecalc-а.
        ConvertFromXObject: true
    }

    Yql {
        // Имя скрипта без суффикса .sql
        // Скрипты берутся из папки, указанной в свойстве YqlPath этого конфига
        Path: "WebPages"
        // Имя входящего protobuf-сообщения, должно быть описано в файле robot/kwyt/protos/queries.proto
        InputProto: "NKwYT.TRawDocument"
        // Имя исходящего protobuf-сообщения
        OutputProto: "NKwYT.TWebPagesItem"
    }

    Output {
        Yql {
            Path: "KwytPageExport"
            // Должно соответствовать OutputProto из внешнего Yql
            InputProto: "NKwYT.TWebPagesItem"
            // Формат сообщений, которые полетят в исходящую очередь Queue
            OutputProto: "NKwYT.TDocument"
        }

        Queue: {
            Server: "logbroker.yandex.net"
            Topic: "kwyt-rthub-pages-to-kwyt"
            LogType: ""
            MaxPartitions: 15
        }
    }
}

Limits {
    // Ограничивает суммарный размер всех исходящих очередей, нужно чтобы не вылететь по памяти
    OutputInflightLimit {
        ItemsCount: 10000
        ItemsSizeInBytes: 5000000000
    }
    // Если после сериализации размер выходного сообщения получится больше этой величины, то
    // сообщение не попадаёт в выходную очередь и просто выкидывается.
    MaxOutputMessageSize: 32000000
}

// Где искать файлы с ресурсами — аргументы функции FilePath в YQL
ResourcesPath: "data/resources"

// Где искать .so-шки с udf-ками
UdfsPath: "data/udfs"

// Где искать yql-запросы
YqlPath: "data/queries"

// Директория с .proto-файлами. Должна включать в себя все зависимости, достижимые по import-ам.
ProtoPath: "data/protos"

//перезапускать рабочие процессы с указанным периодом. Может быть полезно
//для борьбы с утечками памяти в udf-ках.
RecyclePeriodMinutes: 40

//таймаут на обработку одного сообщения. При превышении соответствующий
//рабочий процесс перезапускается, сообщение логируется и пропускается.
ExecutionTimeoutMillis: 10000

//Этот флажок включает режим, при котором считчики отдаются с дополнительной меткой
//instance, которая генерится уникально через захват файлового лока. Необходимость в
//этом возникает, когда на одной машине может быть запущено несколько экземпляров одной
//и тоже конфигурации rthub. Делать так по умолчанию неудобно, так как перестает
//работать дефолтная соломоновская агрегация по host-у.
MultipleInstancesOnSingleHost: true

//адреса реплик rthub-ного logbroker-балансера (robot/rthub/tools/lb_balancer). В отличие
//от стандартного балансера, учитывает лаг по партициям и рейт записи в них — чем
//больше лаг/рейт, тем меньше у партиции окажется соседей на воркере.
LogbrokerBalancerUrl: "http://man1-4518.search.yandex.net:30845"
LogbrokerBalancerUrl: "http://myt1-3194.search.yandex.net:30845"
LogbrokerBalancerUrl: "http://sas1-2491.search.yandex.net:30845"

//если сообщение обрабатывается дольше этого трешолда, оно будет учтено в счетчиках медленных
//сообщений (SlowMessagesCount, SlowestMessageDurationMillis). Кроме того, одно самое
//медленное из таких сообщений сохраняется в памяти каждого из рабочих
//процессов rthub в качетсве сэмпла. Команда curl "http://localhost:16392/report_slow_messages"
//сохранит все такие сообщения в лог и в файлик failed-messages, можно скачать
//этот файлик локально, запустить на нем rthub и изучить, в чем причина тормозов.
SlowMessagesThresholdMillis: 3000;
```

{% endcut %}



Каждый channel (их может быть один или более) имеет входную очередь, основной yql скрипт, и один или более output-ов. На каждый output опционально можно использовать свой yql скрипт, в котором выбрать только нужные поля или добавить дополнительную фильтрацию с помощью WHERE. Входящие сообщения обрабатываются последовательно: сначала основным yql-скриптом и, если он вернул результат, к нему дополнительно применяется скрипт из output-а.

YQL-скрипт должен предоставить данные для всех полей из OutputProto, в противном случае purecalc ругается при компиляции. В сообщении об ошибке будет выведен suggested protobuf — это тот OutputProto, который purecalc ожидает увидеть при данном InputProto. Его можно использовать, чтобы не писать эти протобуфы руками: укажите в OutputProto имя пустого протобуфа, дождитесь ошибки и скопируйте suggested protobuf в queries.proto

Исходящие протобуф-сообщения для экономии трафика жмутся ZLib-ом перед отправкой. При чтении для распаковки нужно воспользоваться утиловым классом TZLibDecompress с параметром StreamType::ZLib.

## Как запускать

Рекоммендуемый способ запуска — утилита [LocalRthub](https://wiki.yandex-team.ru/robot/rthub/local-rthub).


{% cut "Также можно воспользоваться старой инструкцией" %}

Зайдите в Аркадии в **robot/rthub** и соберите через `ya make`. Для работы rthub нужны собранные .so-шки c udf-ками и соответствующие ресурсные файлы. Все необходимое содержится в пакете **robot/rthub/packages/rthub_pages_full_package.json**. Его можно собрать локально командой 
```js
(bash) ya package rthub_pages_full_package.json --sandbox-download-protocol=skynet
```

или скачать результат уже [собранной таски](https://sandbox.yandex-team.ru/tasks?page=1&pageCapacity=20&type=BUILD_RTHUB_PACKAGE&forPage=tasks&desc_re=RTHUB__PAGES&recipients=). Полученный tar-архив нужно распаковать:
```js
(bash) 
tar -I pigz -xvf <whatever>.tar.gz -C ./
```
и положить папку **data** из него рядом с rthub.

* Для профилирования/отладки можно собрать свои версии .so-шек в разделе **robot/rthub/yql/udfs** и подложить их в папку **data/udfs**. yql-скрипты так же, по умолчанию, берутся из папки **data** (подпапка **yql** в ней). Чтобы скопировать измененные .so/.sql в папку **data** можно воспользоваться скриптом `./scripts/deploy-local.sh`.

Для этого выкачиваем из боевой очереди тестовый набор данных такой командой: 
```js

(bash) 
./tools/pq_tool --cmd pull --config --topic zora--pages conf/conf-production/pages.pb.txt --limit 1000
```

Параметром limit задается количество сообщений, которые нужно скачать.  Данные сохраняются в human readable формате в папке **data/pq**, можно на них смотреть глазами. Путь для сохранения файлов можно изменить с помощью параметра `--directory`.
* запускаем на скачанных данных rthub такой командой:
```js
(bash) ./rthub --config conf/conf-production/pages.pb.txt --input-directory data/pq --output-directory data/pq &>rthub.log
```

В input-directory нужно указать то место, куда были скачаны данные на предыдущем этапе. Результат будет помещен в output-directory, в файлик с именем выходной очереди из config.pb.txt.
Если это не получилось сделать, попробуйте также в `conf/conf-production/pages.pb.txt` удалить `CpuOversubscription: 2` и изменить `InstanceStateFilePath:` на локальную директорию `./webcache`, чтобы не срабатывали verify.

* за процессом можно следить по счетчикам. По умолчанию они доступны по http на порту 16392. Если rthub запускается на разработческом сервере, можно прокинуть ssh туннель:
```js
(bash)ssh -L 16392:localhost:16392 <host name>
```
и наблюдать за ними локально из браузера по адресу **http://localhost:16392/rthub**. 
Если при запуске rthub указать параметр `--print-counters`, то финальные значения счетчиков будут выведены в stdout в виде сериализованного протобуфа.
* Другой способ проверить работоспособность скриптов/udf-ок — запустить rthub на тестовом потоке данных из pq. Для этого нужно передать параметр `--test-mode`:
```js
(bash)
./rthub --config conf/conf-production/pages.pb.txt --test-mode &>rthub.log
```
Результат работы сохраняется в папку data/pq, где можно посмотреть на него глазами.
* при запуске rthub можно указать параметр --dump-error-messages, тогда в stdout попадут все сообщения (входные и выходные), по которым были ошибки (udf-ка заполнила значение Error)
* по умолчанию при запуске с `--input-directory` процесс rthub завершается сразу после обработки всех входящих сообщений. Если указать `--poll-input-directory true`, то процесс не завершится, а будет периодически проверять входящую папку на наличие новых сообщений и обрабатывать их. Это может быть полезно для автотестов.

{% endcut %}


## Как запускать на YT
RTHub умеет запускать yql-скрипты на кластере YT в режиме обычных map-операций. Это может быть удобно, если логика скриптов или udf-ок изменилась и нужно пересчитать предыдущие результаты:
```js
(bash)
./tools/yt_run/yt_run --config conf/conf-batch/pages.pb.txt --data-package ./pages.data.tar.gz

```
В конфиге должна быть определена секция Yt:
```js
Channel {
    Input {
        Source {
            //имя таблицы на yt — zora--pages
            Ident: "zora"
            LogType: "pages"
            //Server может быть полезен для тестирования скриптов локально, через logbroker и тестового клиента
            Server: "man.logbroker.yandex.net"
            Client: "rthub-test"
        }
        InflightLimit {
            ItemsCount: 10000
            ItemsSizeInBytes: 100000000
        }
        ConvertFromXObject: true
    }
    Yql {
        Path: "WebPages"
        InputProto: "NKwYT.TDocument"
        OutputProto: "NKwYT.TWebPagesItem"
    }
    Output {
        Yql {
            Path: "JupiterPageBatchExport"
            InputProto: "NKwYT.TWebPagesItem"
            OutputProto: "NKwYT.TJupiterBatchItem"
        }
        Queue: {
            //имя выходной таблиц — rthub--jupiter
            Ident: "rthub"
            LogType: "jupiter"
        }
    }
}
Yt {
    //имя сервера yt
    Server: "banach"
    //папка, из которой будут браться входные и выходные таблицы
    BasePrefix: "//home/antispam/users/bikulov/rthub"
}
```
Имена таблиц должны совпадать с именами топиков, как в примере выше. Таблицы должны быть строго типизированными, protobuf-схема должна совпадать с форматом соответствующих топиков.

В `--data-package` нужно указать путь до архива, содержащего папки resources, libraries, udfs и queries. Инструмент скопирует его в рабочий каталог мап-операции, разархивирует и положит содержимое в папку **data**. Имя 'data' для этой папки для простоты прибито в коде гвоздями: предполагается, что в конфиге используются пути по умолчанию до udf-ок и всего остального. Для pages.pb.txt этот архив можно получить с помощью [этой таски](https://sandbox.yandex-team.ru/tasks?page=1&pageCapacity=20&type=BUILD_RTHUB_UDFS_PACKAGE&forPage=tasks). Вы также можете вручную [перепаковать описанным образом результат](https://sandbox.yandex-team.ru/tasks?page=1&pageCapacity=20&type=BUILD_FULL_WEB_RTHUB_PACKAGE&hidden=true&children=true&forPage=tasks).

## Добавление новых UDF
Код новых UDF должен располагаться в **arcadia/rthub/yql/udfs**.

Если UDF'ка должна выкатываться с каким-либо из существующих пакетов, ее нужно добавить в соответствующий package. Например, cписок udf, которые входят в package pages, находится тут:
```js
arcadia/robot/rthub/packages/full_web_udfs/ya.make
```
Если UDF использует какие-либо внешние файлы данных, то необходимо добавить их в ya.make ресурсов нужного package'а [тут](https://a.yandex-team.ru/arc_vcs/robot/rthub/packages/resources), после чего прописать, куда должен попасть ресурс внутри package'а в json-описании package'а. Для pages — это [rthub_pages_full_package.json](https://a.yandex-team.ru/arc_vcs/robot/rthub/packages/rthub_pages_full_package.json). 

`ya.make` в **pages_2**, по сути, является продолжением списка ресурсов из `ya.make` в **pages**. Разделение появилось из-за проблем со сборкой в dist-build'е.

Пример:
```js
(json)
        {
            "destination": {
                "path": "/data/resources/"
            },
            "source": {
                "path": "robot/rthub/packages/resources/pages_2/cruelty.dssm",
                "type": "BUILD_OUTPUT"
            }
        },
```


{% note warning %}

Если ресурс используется udf'кой и в pages и в pages-fresh, нужно его прописать и в [rthub_pages_full_package.json](https://a.yandex-team.ru/arc_vcs/robot/rthub/packages/rthub_pages_full_package.json), и в [rthub_pages_fresh_full_package.json](https://a.yandex-team.ru/arc_vcs/robot/rthub/packages/rthub_pages_fresh_full_package.json), а так же в [rthub_kwyt_viewer_full_package.json](https://a.yandex-team.ru/arc_vcs/robot/rthub/packages/rthub_kwyt_viewer_full_package.json), т.к. kwyt_viewer тоже может запускать эту udf'ку.

{% endnote %}

Можно прописать ресурс напрямую в json-описание package'а, но в этом случае ресурс не будет обновляться автоматически:
```js
(json)
{
   "source": {
       "type": "SANDBOX_RESOURCE",
       "id": 426790131,
       "path": "titles.lst"
   },
   "destination": {
       "path": "/data/resources/"
   }
 }
```

Приоритетный способ хранения файлов данных — sandbox-ресурс.

## Обновление ресурсов для UDF
Раз в день запускается [sandbox-задача](https://testenv.yandex-team.ru/?screen=job_history&database=rthub-trunk&job_name=UPDATE_RTHUB_RESOURCES), которая перезаливает все ресурсы, имя которых начинается с YQL_UDF_, и которые прописаны в [https://a.yandex-team.ru/arc_vcs/robot/jupiter/delivery/scripts/extfiles.py](https://a.yandex-team.ru/arc_vcs/robot/jupiter/delivery/scripts/extfiles.py). После чего она коммитит новые id в ya.make'и package'ей в [https://a.yandex-team.ru/arc_vcs/robot/rthub/packages/resources](https://a.yandex-team.ru/arc_vcs/robot/rthub/packages/resources).
Для автоматического обновления ресурсов нужно их прописать в [extfiles.py](https://a.yandex-team.ru/arc_vcs/robot/jupiter/delivery/scripts/extfiles.py), указав, откуда брать файлы в vcs или какой sandbox-ресурс использовать.

## Локальное тестирование
После внесения изменений в код/запросы/данные нужно запустить локальный тест для соответствующего package.
Для pages тест живёт здесь: [arcadia/robot/rthub/test/pages](https://a.yandex-team.ru/arc/trunk/arcadia/robot/rthub/test/pages).

Запускается вот так: 
```js
(bash)
ya make -Ar <путь_до_теста>
```

## Тесты в Review
В ревью в плашке автоматом запускаются только MEDIUM (на небольшом кол-ве тестовых данных) тесты.
LARGE тесты нужно запускать вручную.

## Как катить прод

Инстансы RTHub'а подняты в Nanny.
Есть инстансы для:
* [rthub-pages](https://nanny.yandex-team.ru/ui/#/services/catalog/rthub-pages/)
* [rthub-pages-fresh](https://nanny.yandex-team.ru/ui/#/services/catalog/rthub-pages-fresh/)
* [rthub-pages-fresh-mini](https://nanny.yandex-team.ru/ui/#/services/catalog/rthub-pages-fresh-mini/)
* [rthub-hosts](https://nanny.yandex-team.ru/ui/#/services/catalog/rthub-hosts/)
* [rthub-sitemaps](https://nanny.yandex-team.ru/ui/#/services/catalog/rthub-sitemaps/)
* [rthub-appdocs](https://nanny.yandex-team.ru/ui/#/services/catalog/rthub-appdocs/)
* [rthub-images](https://nanny.yandex-team.ru/ui/#/services/catalog/rthub-images/)
* [rthub-images-fresh](https://nanny.yandex-team.ru/ui/#/services/catalog/rthub-images-fresh/)

Деплой осуществляется с помощью Release Machine (далее RM) в  [этом проекте](https://rm.z.yandex-team.ru/component/rthub). Прочитать о Release machine можно на [Wiki](https://wiki.yandex-team.ru/releasemachine/).

Сначала все сборки выкатываются на prestable, и если там всё хорошо,далее на production.
Инстанс rthub-pages-fresh-mini существует для проверки работоспособности rthub-pages-fresh на основном потоке на 2 машинах, чтобы исключить риски.

Последовательность действий для отвода новой релизной ветки и её деплоя:
1. По нажатию на кнопку **Pre release** появляется форма, в которой нужно указать ревизию отвода (номер ветки задаётся автоматически), и далее нажать **Pre release**.
2. В течении нескольких минут будет отведена новая ветка, и она появится в интерфейсе RM (страницу проекта нужно будет обновить в браузере).
3. Сборки билдов для все типов инстансов запустятся автоматом, а так же тесты для них. Соответствующие джобы будут видны в интерфейсе RM на вкладке Job Results, если слева выбрать новый бранч.
4. После того как все билды и тесты завершились успешно можно начать их деплой на prestable. Для этого, выбрав нужный бранч в RM, нажать **Release**, в открывшейся форме выбрать нужный тип инстанса с суффиксом `_PRESTABLE` и нажать **Release**. Так нужно сделать для всех типов инстансов, которые нужно зарелизить.
5. Прогресс выкатки можно наблюдать на соответствующей странице инстанса в Nanny.
6. Для релиза в production, необходимо выполнить те же действия, что и для prestable, но в форме релиза выбрать инстансы с суффиксом `_STABLE`.

Есть возможность задеплоить всё вручную через интерфейс Nanny.
Билды собираются с помощью Sandbox-таска [BUILD_RTHUB_PACKAGE](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=BUILD_RTHUB_PACKAGE&created=14_days).
Типы ресурсов:
* RTHUB_PAGES_FULL_PACKAGE
* RTHUB_PAGES_FRESH_FULL_PACKAGE
* RTHUB_HOSTS_FULL_PACKAGE
* RTHUB_SITEMAPS_FULL_PACKAGE
* RTHUB_APP_DOCS_FULL_PACKAGE
* RTHUB_IMAGES_FULL_PACKAGE
Соответствующий инстансу ресурс нужно заменить на вкладке Files в Nanny и нажать `Save`.

## Troubleshooting
* Если в процессе работы скрипта/udf-ки возникает segfault, текущее сообщение сохраняется в файлик failed-messages рядом с бинарником rthub. С помощью этого файлика можно воспроизвести проблему локально примерно так:
```js
(bash)
cp ./failed-messages ./data/rthub--pages
./rthub --input-directory ./data --output-directory ./data --config ./conf/conf-production/pages.pb.txt
```

* Сохранение в failed-messages происходит изнутри рабочего процесса через подписку на сигналы. Некоторые сигналы (например, SIGKILL от oom killer-а) нельзя поймать таким образом, поэтому на такой случай есть отдельный механизм. Когда рабочий процесс завершается по сигналу, обрабатываемое им в данный момент сообщение попадает как есть в файлик failed-message-X, где X — номер рабочего процесса. Новые падения удаляют предыдущие. Этот файлик можно превратить в обычный текстовый формат такой командой:
```js
(bash)
./tools/convert_format/convert_format conf/conf-prestable/turbo-parser-worker.pb.txt NKwYT.TContentPluginsData ./failed-message-0 single-compressed-binary data/pq/rthub--turbo-pages text
```

* При запуске rthub в gdb необходимо указать путь к udf файлам:
```js
(bash)
(gdb) set solib-search-path /path/to/udfs/folder
```
Путь /path/to/udfs/folder должен быть или абсолютный или начинаться с ~. Также для отладки обычно удобно бывает оставить треды вместо процессов и ограничиться только одним из них. Для этого в конфиге нужно добавить это:
```js
UseProcesses: false
Limits {
    WorkerThreadsCount: 1
}
```

## Счетчики
Есть несколько групп счетчиков, отражающих работу разных компонент.
* **type=subscribers** — обработка входного потока из [pq](https://solomon.yandex-team.ru/?project=kwyt&cluster=rthub-pages&service=cloud&l.type=subscriber)s. Можно фильтровать по **name** — имени входящего топика, а также **host** — имени машины и **cluster** — сумме показателей со всех машин.
* **ActivePartitions** — число прослушиваемых на данный момент партиций
* **BatchSize** — число сообщений во входящей пачке сообщений
* **InflightInputBytesCount** — суммарный размер в байтах, вычитанных из данного входного топика сообщений, по которым еще не было получено подтверждение о записи результата в исходящий топик и, соответственно, оффсет по этим сообщениям еще не закоммичен во входящий топик. Это число ограничивается параметром конфига `InflightLimit.ItemsSizeInBytes`, при превышении чтение будет тормозиться. Чем больше значение этого параметра, тем больше сообщений logbroker, обрабатывающий исходящий поток, сможет уместить в один fsync, и тем выше пропускная способность.
* **InflightInputMessagesCount** аналогичный показатель, измеренный в количестве сообщений
* **InflightOutputBytesCount** показывает для данного топика размер в байтах исходящих сообщений, еще не записанных в исходящий топик.
* **InflightOutputMessagesCount** аналогично в штуках
* **InputBytesCount** рейт чтения в байтах
* **InputMessagesCount** рейт чтения в штуках
* **InputContention** число превышений InflightLimit, позволяет отследить, не упираемся ли мы в него
* **OutputBytesCount** рейт формирования исходящего потока в байтах для данного входного топика
* **OutputMessagesCount** аналогично в штуках
* **TotalInflightOutputBytesCount** суммарный размер в байтах еще не записанных исходящих сообщений по всем топикам. Ограничивается параметром конфига OutputInflightLimit.ItemsSizeInBytes, при превышении чтение будет тормозиться. Это ограничение полезно чтобы просто не вылететь по памяти, так как освобождение происходит только после получения подтверждения о записи.
* **TotalInflightOutputMessagesCount** аналогично в штуках
* **TotalOutputContention** число превышений OutputInflightLimit, позволяет отследить, не упираемся ли мы в него
* **type=channels** — запуск [yql-запросов](https://solomon.yandex-team.ru/?project=kwyt&cluster=rthub-pages&service=cloud&type=channels), где **name** — имя yql-скрипта.
* **ChannelYqlErrorMessages** количество сообщений с непустым полем Error. Обычно в этом поле собираются ошибки со всех использованных udf.
* **ChannelYqlProcessErrorsRate** эксепшны, случившиеся при выполнении yql-скрипта
* **Min/Max/Average/Percentile** характеристики времени выполнения скрипта
* **InputMessageSize** размер одного входящего сообщения
* **TotalMin, TotalMax** ... вся обработка сообщения внутри channel-а, заканчивая отправкой (но не ожиданием результата) в исходящие топики
* **type=channel_outputs**, отправка сообщений в исходящие топики https://solomon.yandex-team.ru/?project=kwyt&cluster=rthub-pages&service=cloud&type=channel_outputs, name — имя Output-а, образованное от имени основного скрипта и имени исходящего топика.
* **ChannelOutputYqlErrorMessages...ChannelOutputYqlProcessRate** аналогично channel, характеризуют выполнение yql-запросов, навешенных на Output-ы
* **OutputMessageSize** размер одного исходящего сообщения
* **SendAverage**, **SendErrorsRate**, **SendMin**, **SendPercentile**, **SendRate** характеризуют результат отправки исходящего сообщения
* **TooBigOutputMessagesCount** — исходящие сообщения, размер которых превышает MaxOutputMessageSize. Такие сообщения сейчас просто отбрасываются.
* **type=system** — общие счетчики процесса [rthub](https://solomon.yandex-team.ru/?project=kwyt&cluster=rthub-pages&service=cloud&type=system).
  * **CpuUserTime** — использование cpu в секундах. Если процессор один, и он занят на 100%, то за 15 секунд (интервал опроса соломоном) будет 15 единиц, на единицу времени будет 1, если 4 процессора — то 4.
* **CpuSystemTime** — аналогично, время, которое проводим в ядре.
* **Initialized** — число работающих экземпляров процесса rthub.
* **MajorPageFaults** page fault-ы, требующие обращения к диску.
* **NonvolContextSwitches** — переключения контекста по инициативе планировщика ядра.
* **VolContextSwitches** — переключения контекста по инициативе самого потока (sleep, io wait).
* **RSS** — объем резидентной памяти. Может существенно превышать фактическое использование памяти, ограничиваемое настройками gencfg через porto-контейнеры, например если один и тот же файлик замаплен много раз через mmap. Реальное использование памяти можно посмотреть через графики в gencfg. [Привер](https://gencfg.yandex-team.ru/trunk/hosts/myt1-0619.search.yandex.net).
* **Uptime** — число секунд, прошедших с момента старта процесса.
* **Vsize** — объем виртуальной памяти.
* **type=logbroker_balancer** — [мониторинг логброкера](https://solomon.yandex-team.ru/?project=kwyt&cluster=rthub-pages&service=cloud&type=logbroker_balancer). Поддержание оптимального распределения воркеров-процессов rthub между разными дц, с которых идет чтение. Учитывается рейт записи в каждый дц и величина накопленного лага. **name** — доменное имя логброкера в конкретном дц.
* **Active** — дц, с которого идет чтение в данный момент.
* **ActualWorkersCount** — реальное число воркеров на каждом из дц. Получается чтением ручки pull/offsets.
* **EstimatedWorkersCount** — число воркеров, которое в идеале должно быть на данном дц, учитывая текущий рейт и лаг.
* **Failed** — упавший дц, признается таковым если pull/offsets не срабатывает за определенное число попыток. Если активный дц признается упавшим, то в течение двух минут rthub переключится на другой дц.
* **LackedWorkers** — ограничения MaxPartitions в конфиге не позволяют читать все имеющиеся партиции, данный счетчик показывает, сколько воркеров не хватает.
* **RedundantWorkers** — если число воркеров больше, чем суммарное число партиций, данный счетчик показывает разницу. Это может стать актуально, если выпадут один или несколько дц.
* **Local** — в данный момент мы читаем с локального логброкера, то есть rthub запущен в том же дц.
* **PullOffsetsFailures** — число фейлов при вызове pull/offsets.
* **Rate** — оценка рейта записи в дц, полученная путем анализа pull/offsets.
* **SwitchesCount** — количество переключений между разными логброкерами.
* **TotalLag** — суммарный лаг по топику, полученный из pull/offsets.
* **Uptime** — число секунд, прошедшее после последнего переключения между дц.

