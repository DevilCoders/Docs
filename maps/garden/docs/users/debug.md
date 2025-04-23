# Как отлаживать огородные модули

Чтобы ловить ошибки на этапе написания кода, нужно иметь хорошие юнит-тесты.
В Огороде есть библиотека для локального запуска YT, YQL, Postgres, S3 MDS для тестов.
Подробнее на отдельной [странице](tests.md).

Для тестирования модуля со всеми задачами в боевом режиме на продакшн данных используется функциональность экспериментов.
Подробнее на отдельной [странице](experiments.md).

После того как задача отработала в боевом режиме, информация о ней попадает в Перф.
В Перфе есть ссылки на лог задачи в S3 и на операцию в YT.
Если задача выбрасывает исключение, то оно будет перехвачено и записано в лог вместе со стектрейсом.
Подробнее про исключения на отдельной [странице](module-exceptions.md)

Если задача работает долго, то можно:

* посмотреть `stderr` на странице операции в YT
* подключиться по ssh к контейнеру с операцией и запустить gdb через [job-shell](https://yt.yandex-team.ru/docs/problems/jobshell_and_slowjobs.html#zapusk-job-shell)

Для выполнения этих действий нужно вступить в группу [garden-users](https://yt.yandex-team.ru/hahn/groups?groupFilter=garden-users).

## Локальный запуск задач

Есть возможность запустить локально почти любую задачу (см. ограничения ниже) и подать ей на вход реальные данные.

Шаг 1: соберите бинарный модуль и сгенерируйте болванку конфига для запуска:

```
cd maps/garden/modules/<module_name>/bin
ya make
./<module_name> generate_config <TaskName> [<region1>,<region2>,<region3>]
```

Будет сгенерирован файл `<TaskName>.json`.
При повторных запусках команды `generate_config` файл не будет перезаписываться.

Если задача относится к reduce-модулю и принимает на вход ресурсы из разных регионов,
то можно передать список регионов через запятую.

Шаг 2: заполните болванку конфига реальными данными.

В секции `demands` укажите пути к таблицам с данными,
ссылки на скачивание файлов и другие свойства ресурсов.

В секции `creates` укажите пути к таблицам, которые нужно создать,
или имена файлов, которые будут сохранены локально.

{% note warning %}

Будьте осторожны и не указывайте пути в тестинге или продакшене Огорода.

{% endnote %}

В секции `environment_settings` укажите дополнительные поля, которые нужны для работы задачи,
но которых не хватает в настройках, которые используются [по умолчанию](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/libs/module_rpc/task_runner.py?rev=r7829378#L40).

Шаг 3: запустите задачу:

```
./<module_name> run_task <TaskName> <path to config>
```

{% note info %}

Если задача работает с YT-таблицами или запускает YQL-запросы,
то необходимо настроить токены согласно документации этих сервисов.

Также для некоторых задач может понадобится переменная окружения `YT_PROXY=hahn`.

Если задача использует environment-dependent конфиги, которые зашиты в модуль,
то необходимо выставить переменную окружения `ENVIRONMENT_NAME`.

{% endnote %}

### Ограничения

Не все задачи можно запустить таким образом.

Поддерживаемые типы ресурсов на входе:

* `BuildParamsResource`
* `FileResource`
* `DirResource`
* `PythonResource`
* `RemoteDirResource`
* `YtFileResource`
* `YtTableResource`
* `YtSourcePathResource`

Поддерживаемые типы ресурсов на выходе:

* `FileResource`
* `DirResource`
* `PythonResource`
* `YtFileResource`
* `YtTableResource`

Ресурс может быть обёрнут в `OptionalResource`.

Если хотя бы один из ресурсов задачи не поддерживается, то инструмент не даст запустить задачу.

Если задача имеет не уникальное имя `displayed_name`, то будет запущена задача, которая была добавлена первой в `TaskGraphBuilder`.

Если нужно запустить конкретную задачу с неуникальным именем класса (например, `YqlTask`), то необходимо переопределить у неё `displayed_name`.

### Внешние ресурсы

Некоторые задачи могут принимать на вход ресурсы, которые объявлены в других бинарных модулях.

Для локального запуска такой задачи необходимо явно указать типы всех внешних ресурсов.

Объявите словарь `<resource_name>: <resource_type>` и передайте его в функцию `run_module` в `main.py`. Пример:

```python
input_resources = {
    "src_altay_out": YtSourcePathResource
}

def main():
    run_module("<module_name>", fill_graph, input_resources)
```

Если задача относится к reduce-модулю и принимает на вход ресурсы из разных регионов,
то можно объявить функцию, которая будет генерировать аналогичный словарь. Пример:

```python
def input_resources(regions)
    return {
        "table_" + region + "_" + vendor: YtTableResource
        for region, vendor in regions
    }

def main():
    run_module("<module_name>", fill_graph, input_resources)
```

Для модулей, которые потребляют `ymapsdf` можно взять за образец такую функцию:

```python
def input_resources(regions):
    result = {}
    for region, vendor in regions:
        for table_name in INPUT_TABLE_NAMES:
            resource_name = name_conventions.get_full_resource_name(
                resource_namer.YT_YMAPSDF_FINAL_STAGE.resource_name(table_name),
                region,
                vendor)
            result[resource_name] = yt_plugin.YtTableResource
    return result
```

### Отладка

Задачи можно отлаживать с помощью `ya tool gdb` во время локального запуска.

Предварительно необходимо отключить обрезание символов:

* либо в `ya.make` вписать `ENABLE(NO_STRIP)`
* либо собрать модуль командой `ya make -DNO_STRIP=yes`

Пример запуска отладчика:
```bash
ya tool gdb --args ./ymapsdf run_task ComputeBldAddrTask ComputeBldAddrTask.json
$ run
```

Точка останова в файле:
```
$ break /home/alexbobkov/arc/arcadia/maps/garden/modules/ymapsdf/lib/parent_finder/bld_addr_final.cpp:252
```

Точка останова в начале функции:
```
$ break computeBldAddr
```

Можно смотреть отдельно стек функций на Питоне:
```
$ py-bt
```

Временно эта команда не работает под 3м Питоном (<https://st.yandex-team.ru/DEVTOOLS-6661>).

Подробнее про GDB: <https://abv.at.yandex-team.ru/583>

Документация по GDB: <http://sourceware.org/gdb/current/onlinedocs/gdb/>

Документация по отладке Питона в GDB: <https://devguide.python.org/gdb/>

### Профилирование C++ кода

#### `ya profile` (Google Performance Tools)

Предварительно необходимо собрать модуль командой:
```bash
ya make --build=profile
```

Пример запуска:
```bash
ya profile --format=callgrind ./ymapsdf run_task ComputeBldAddrTask ComputeBldAddrTask.json
```

В папке `profile` будет файл в формате `kcachegrind`.

Подробнее: <https://wiki.yandex-team.ru/yatool/profile/>

Документация по gperftools: <https://github.com/gperftools/gperftools>

#### `ya tool perf`

Предварительно необходимо собрать модуль командой:
```bash
ya make --build=profile
```

Пример запуска:
```bash
ya tool perf record -F 250 -g --proc-map-timeout=10000 ./ymapsdf run_task ComputeBldAddrTask ComputeBldAddrTask.json
ya tool perf script > out.perf
```

Если `perf` не запускается, то возможно нужно разрешить запуск из-под обычного пользователя:
```bash
sudo sh -c 'echo 1 > /proc/sys/kernel/perf_event_paranoid'
```

Посмотреть результат можно командой:
```bash
ya tool perf report --call-graph graph --tui
```

Либо сконвертировать результат во Flame Graph:
```bash
~/arc/arcadia/contrib/tools/flame-graph/stackcollapse-perf.pl > out.perf-folded < out.perf
~/arc/arcadia/contrib/tools/flame-graph/flamegraph.pl out.perf-folded > out.svg
```

Подробнее: <https://clubs.at.yandex-team.ru/arcadia/18242>

#### Poor man's profiler

С помощью простого скрипта можно в цикле снимать стеки и на выходе получить Flame Graph:
<https://loudhorr.at.yandex-team.ru/101>

### Профилирование Python кода

Код на Питоне можно профилировать с помощью `py-spy`.
Он работает с аркадийным Питоном, если модуль собран с `NO_STRIP` (см. выше).

`py-spy` написан на Rust, так что его можно собрать самостоятельно с помощью `cargo`.
Либо можно использовать уже собранный бинарник `/usr/local/bin/py-spy` на разработческой машине `wicket`.

Пример запуска:
```bash
/usr/local/bin/py-spy record -o profile.svg ./ymapsdf run_task MakeFtPermalinkTask MakeFtPermalinkTask.json
```

Результат будет в виде Flame Graph.

Документация по py-spy: <https://github.com/benfred/py-spy>

Ещё про профилирование Питона: <https://torkve.at.yandex-team.ru/4076>


## Локальная отладка джобы из MR-операции

Некоторые задачи запускают MR-операции, и иногда джобы падают на каких-то данных.

YT позволяет скачать входные файлы для джобы и запустить её локально.

В логах таски нужно найти `operation_id` упавшей операции, и на вкладке `Jobs` выбрать нужный `job_id`.

Локально запустить команду
```bash
ya tool yt job-tool prepare-job-environment <operation_id> <job_id>
```

Эта команда создаст директорию (назовём её `job-dir` для удобства) и скачает туда все нужные файлы.
В том числе бинарник модуля в директорию `job-dir/sandbox`.

Запустить джоб можно командой `job-dir/run.sh`.

Запустить джоб под отладчиком можно командой `job-dir/run_gdb.sh`.
Рекомендуется иметь алиас `alias gdb="ya tool gdb"`.

После исправления бага можно собрать новую версию бинарного модуля, подложить в директорию с джобом
и запустить для проверки
```
ya make -r
cp <module_name> job-dir/sandbox
job-dir/run.sh
```

Подробнее: <https://wiki.yandex-team.ru/yt/userdoc/jobtool/>
