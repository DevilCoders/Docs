# DWH

Table of Contents
=================

   * [DWH](#dwh)
      * [Релиз](#релиз)
         * [Новый релиз в RM](#новый-релиз-в-rm)
         * [Новая версия в RM](#новая-версия-в-rm)
         * [Выкладка](#выкладка)
      * [Отчёты](#отчёты)
         * [DWH-200](#dwh-200)
            * [Агрегация](#агрегация)
            * [Сборка](#сборка)
         * [DWH-397](#dwh-397)
         * [DWH-512](#dwh-512)
      * [Экспортёр](#экспортёр)
         * [Стратегии](#стратегии)
         * [Трансфер на кластеры](#трансфер-на-кластеры)
         * [Трансфер мапнод на кластеры](#трансфер-мапнод-на-кластеры)
      * [Инфраструктура](#инфраструктура)
         * [URI](#uri)
      * [Мировые константы](#мировые-константы)
      * [Тесты](#тесты)
      * [Локальный запуск экспорта в YT](#локальный-запуск-экспорта-в-yt)
         * [Подготовка](#подготовка)
         * [Переменные окружения](#переменные-окружения)
         * [Хинты](#хинты)
         * [Запуск (python)](#запуск-python)
         * [Запуск (binary)](#запуск-binary)
      * [Обновление mncloselib](#обновление-mncloselib)
         * [Разархивация](#разархивация)
         * [Архивация](#архивация)
         * [Проверка установки в virtual environment](#проверка-установки-в-virtual-environment)
      *  [Кроссвалидация](#кроссвалидация)

Проект DWH(Data Warehouse) включает в себя:
* Отчёты [DWH-200](#dwh-200), DWH-276, [DWH-397](#dwh-397)
* Экспортёр из данных Биллинга в YT
* Некую наколеночную инфраструктуру для работы с YT, YQL и ST из [luigi](https://github.com/spotify/luigi)
* Мировые константы для расчётов
* Какие-то тесты ко всему этому
* Веб-сервис с API для удалённого запуска задач

## Релиз

### Новый релиз в RM

Идём в релизную машину:

- https://rm.z.yandex-team.ru/component/dwh

Нажимаем `Pre release`.

### Новая версия в RM

Идём в релизную машину:

- https://rm.z.yandex-team.ru/component/dwh/merge_rollback

Далее:

- Выбираем ветку (выпадающий список `Branches`) в правой половине экрана (`Merge`)
- Указываем номера ревизий в поле `Revisions`
- Нажимаем кнопку `RUN`

После этого будет создана новая версия существующего релиза.


### Выкладка

- Кондукторный пакет: [yb-dwh](https://c.yandex-team.ru/packages/yb-dwh)
- Timeline: [dwh](https://timeline.paysys.yandex-team.ru/pipe/projects/deploy/release/new/deploy-start-release-dwh)

## Отчёты

### DWH-200
Общий отчет для финансовой и управленческой отчетности с информацией по вознаграждению партнерам РСЯ за внутреннюю рекламу.
В отчете есть 3 блока данных:
* Вознаграждение партнерам РСЯ за внутреннюю рекламу
* Вознаграждение по договорам дистрибуции
* Детализация выручки маркета

Что получается и откуда берутся данные можно посмотреть [тут](https://wiki.yandex-team.ru/Balance/TZ/dwh-internaladreward/)

Выполняется в 3 подхода: агрегация, сборка агрегата awaps, сборка отчета.
Пускается 3 раза в месяц: 1-го (нулевая (forecast) фаза), 2-го или 3-го (первая фаза) и 15-го (вторая фаза). Даты могут слегка сдвигаться в будущее.

#### Агрегация
```bash
/usr/bin/dwh/run_with_env.sh -m luigi \
--module grocery.dwh-200-business DWH200Aggregation \
--local-scheduler \
[--month 'YYYY-MM'] [--force] [--no-mnclose] [--cooked] [--simple] [--with-boost {nirvana/cloud/without}] [--sample] [--output-path 'path']
```
Параметр | Допустимые значения | Описание
------------ | -------------|---------------
month | 'YYYY-MM' | Период за который необходимо запустить предыдущий расчёт. По умолчанию прошлый месяц
force | flag | Запустить полную пересборку отчёта
no-mnclose| flag | Не проверять задачу в графе MNClose при запуске отчета. Нужно для запуска 2-й фазы отчета после закрытия
cooked | flag | использовать для сборки cooked-chevent логи баннерокрутилки. По умолчанию используются chevent и undochevent логи. Полезно при сборке 2 фазы отчета и при пересборке агрегата за прошлые периоды
simple | flag | использовать "простой" способ определения суммы события до отката (без использования полей eventcost_beforeundo, только незафроженные клики). По факту не прижился и не используется. Значение по умолчанию - не использовать
with-boost | flag | Использовать дополнительные вычислительные ресурсы за счёт облачной квоты/квоты в Нирвана/не использовать
sample | flag | агрегировать не за весь месяц, а только за четвёртый день месяца
output-path | flag | Куда сгружать агрегат. По умолчанию в 'dwh/business-{month}'


#### Awaps
```bash
/usr/bin/dwh/run_with_env.sh -m luigi  \
--module grocery.dwh_200_awaps VideoAwapsDsp \
--local-scheduler \
[--month 'YYYY-MM'] [--force] [--with-boost {nirvana/cloud/without}] [--workers N] [--phase {ForecastPhase/FirstPhase/FullPhase}] [--mnclose MNCLOSE_TASK]
```

Параметр | Допустимые значения | Описание
------------ | -------------|---------------
month | 'YYYY-MM' | Период за который необходимо запустить предыдущий расчёт. По умолчанию прошлый месяц
phase | {ForecastPhase/FirstPhase/FullPhase} | Фаза закрытия. Не влияет на логику расчёта. Для ForecastPhase партнерские акты берутся из отдельного места
force | flag | Запустить полную пересборку отчёта
no-mnclose| flag | Не проверять задачу в графе MNClose при запуске отчета. Нужно для запуска 2-й фазы отчета после закрытия
mnclose | str | Идентификатор задачи, которую нужно проверять в закрытие
workers | int | Количество воркеров, которое можно запустить при расчете. Имеет смысл указать 4, так как части отчета могут выполняться параллельно. По умолчанию 1

#### Сборка

```bash
/usr/bin/dwh/run_with_env.sh -m luigi \
--module grocery.dwh-200-v2 DWH200 \
--local-scheduler \
--phase {ForecastPhase/FirstPhase/FullPhase} \
[--month 'YYYY-MM'] [--force] [--s3] [--no-mnclose] [--mnclose MNCLOSE_TASK]  [--no-excel] [--no-db] [--sample] [--suffix] [--calc-yan] [--calc-distr]
```

Параметр | Допустимые значения | Описание
------------ | -------------|---------------
month | 'YYYY-MM' | Период за который необходимо запустить предыдущий расчёт. По умолчанию прошлый месяц
phase | {ForecastPhase/FirstPhase/FullPhase} | Фаза закрытия. Не влияет на логику расчёта. Для ForecastPhase партнерские акты берутся из отдельного места во всем пайплайне. Влияет на суффикс названия результа
force | flag | Запустить полную пересборку отчёта
no-mnclose| flag | Не проверять задачу в графе MNClose при запуске отчета. Нужно для запуска 2-й фазы отчета после закрытия
mnclose | str | Идентификатор задачи, которую нужно проверять в закрытие
no-excel | bool, default True | Не сохранять в результат в excel
no-db | flag | Не сохранять результат в ДБ
sample | flag | Выполнять сэмплирование промежуточных результатов в pandas процессинге. Результаты семплирования сохранятся в ```/etc/dwh/{processname}-{stagenum:02d}-{name}-{stagename}.pcl```
suffix | str | Добавить суффикс к названию результата
calc-yan | bool | Считать РСЯ, по умолчанию true, для выключения нужно указать ```--calc-yan=false```
calc-distr | bool | Считать Дистрибуцию, по умолчанию true, для выключения нужно указать ```--calc-distr=false```

### DWH-397
Отчёт детализации актов директа разрезом площадок. Подробнее [тут](https://st.yandex-team.ru/DWH-391).

Потребитель [Комдеп Аналитики](https://staff.yandex-team.ru/departments/yandex_biz_com_analytics/)

Очёт строит помесячные агрегаты и перерасчитывает их в случае изменения исходных данных.

```bash
/usr/bin/dwh/run_with_env.sh -m luigi \
--module grocery.dwh-397 DWH397 \
--local-scheduler \
[--start_month 'YYYY-MM']
[--end_month 'YYYY-MM']
[--with-boost cloud/nirvana/without]
[--workers X]
```

Параметр | Допустимые значения | Описание
------------ | -------------|---------------
start_month | 'YYYY-MM' | С какого месяца надо пробовать делать перерасчёт. По умолчанию полгода назад
end_month | 'YYYY-MM' | Каким месяцем заканчивать пробовать делать перерасчёт. По умолчанию этот месяц
with-boost | cloud/nirvana/without | Использовать дополнительные вычислительные ресурсы за счёт облачной квоты, гарантированного пула, не использовать
workers | number | количество одновременно работающих воркеров luigi, если не указано - то 1 worker

**Внимание**: ```start_month``` и ```end_month``` трактуются как границы левого полуинтервала.

### DWH-512
Отчет детализации актов по общему счету и боидам по заказам Директа

```bash
/usr/bin/dwh/run_with_env.sh -m luigi \
--module grocery.dwh-512 DWH512 \
--local-scheduler \
[ --start-month 'YYYY-MM'] \
[--end_month 'YYYY-MM'] \
[ --workers N] \
[--with-boost cloud/nirvana/without] \
```

Параметр | Допустимые значения | Описание
------------ | -------------|---------------
start_month | 'YYYY-MM' | С какого месяца надо пробовать делать перерасчёт. По умолчанию полгода назад
end_month | 'YYYY-MM' | Каким месяцем заканчивать пробовать делать перерасчёт. По умолчанию этот месяц
with-boost | cloud/nirvana/without | Использовать дополнительные вычислительные ресурсы за счёт облачной квоты, гарантированного пула, не использовать
workers | number | количество одновременно работающих воркеров luigi, если не указано - то 1 worker

**Внимание**: ```start_month``` и ```end_month``` трактуются как границы левого полуинтервала.

## Экспортёр

Занимается выгрузкой таблиц Биллинга в YT. Параметры экспорта по таблицам хранятся в [узле экспорта](https://bunker.yandex-team.ru/dwh/prod/export) в бункере, а хинты для отображения оракловых типов данных в ытёвые в его подузлах.
И то и то подтягивается динамически по мере необходимости.

```bash
/usr/bin/dwh/run_with_env.sh -m luigi \
--module grocery.yt_export YTExport \
--local-scheduler \
--tables '[table1,table2,...]' \
[ --targets '{"table1": "//path/to/table1/target/", ...}'] \
[ --transfer-to-clusters '["hahn","freud","arnold"]']
[ --update_id update_id] \
[ --meta_dict ...]
[ --workers N]
```

Параметр | Допустимые значения | Описание
------------ | -------------|---------------
tables | Список из таблиц описаных в [бункере](https://bunker.yandex-team.ru/dwh/prod/export) | Какие таблицы экспортировать. Гарантируется, что все таблицы из списка будут либо выгружены все вместе, либо не выгружены вовсе.
targets | Dict[table -> path] | Пути до мапнод, куда выгружать соответствующие таблицы. По умолчанию это домашняя мапнода определяемая конфигом / имя таблицы
update_id | iso datetime до микросекунд | Идентификатор версии выгрузки. Выгрузка происходит, только если update_id выгруженного не совпадает с указаным. По умолчанию это iso datetime до микросекунд от прямо сейчас
transfer-to-clusters | List[cluster] | Список кластеров, на которые нужно выгрузить данные. Если в списке есть несколько кластеров, то все сначала будет выгружено на Hahn, потом будут запущены задачи YtTransferTask для выгрузки на остальные кластеры из списка
meta_dict | Словарь метаданных экспорта | См. бункер. По умолчанию ничего и словарь тянется из бункера.
workers | number | количество одновременно работающих воркеров luigi, если не указано - то 1 worker

### Стратегии
Стратегия определяет как именно будет выгружена таблица. На данный момент существуют следующие стратегии выгрузки

Стратегия | Первичная выгрузка | Последующие
------------ | ------------- | -----
export | Выгрузить полностью в одну таблицу | Выгрузить накопившиеся изменения и влить их в ранее выгруженное
small | Выгрузить полностью в одну таблицу | Если были изменения, то выгрузить полностью в одну таблицу
monthly | Выгрузить полностью с разбивкой по месяцам | Выгрузить накопившиеся изменения последних 2 месяцев и влить их в соответствующие таблицы
shagren | Выгрузить полностью с разбивкой по месяцам | Перевыгрузить месяца в которых, судя по simple_log, были обновления

### Трансфер на кластеры
Запускает задачи по синхронизации выгруженных таблиц между кластерами. Использует [Transfer Manager](https://wiki.yandex-team.ru/transfer-manager/).
На выгрузку каждой таблицы ставится отдельная задача в Transfer Manager. Выгружаются только те таблицы, update_id которых меньше, чем update_id источника.

```bash
/usr/bin/dwh/run_with_env.sh -m luigi \
--module grocery.yt_export YTTransferTask \
--sources '["//path/to/table1","//path/to/table2"]' \
--destinations '["//new/path/to/table1","//new/path/to/table2"]' \
--from-cluster SOURCE_CLUSTER_NAME \
--to-cluster TARGET_CLUSTER_NAME \
--local-scheduler \
[--only-new] \
[--workers N]
```

Параметр | Допустимые значения | Описание
------------ | -------------|---------------
sources | List["path1","path2"...] | Для каких таблиц нужно сделать задачи на синхронизацию между кластерами
destinations | List["path1","path2"...] | Пути до таблиц, куда нужно синхронизировать таблицы-источники
from-cluster | hahn | Название кластера, с которого необходимо синхронизировать таблицы
to-cluster | hahn | Название кластера, с которого необходимо синхронизировать таблицы
only-new |  | Проверить и выгрузить только обновленные/измененные таблицы. Проверка осуществляется по update-id таблиц
workers | number | количество одновременно работающих воркеров luigi, если не указано - то 1 worker

### Трансфер мапнод на кластеры

Запускает задачи по синхронизации мапнод между кластерами. Рекурсивно проходит по указанным мапнодам и создает задачи TransferManager.

```bash
/usr/bin/dwh/run_with_env.sh -m luigi \
--module grocery.yt_export YTMapNodeTransferTask  \
--from-mapnode '["//path/to/mapnode"]' \
--from-cluster SOURCE_CLUSTER_NAME \
--to-cluster TARGET_CLUSTER_NAME \
--local-scheduler \
[--only-new] \
[--running-task-limit NNN] \
[--workers N]
```

Параметр | Допустимые значения | Описание
------------ | -------------|---------------
from-mapnode | List["path1","path2"...] | Мапнода, для которой нужно сделать задачи на синхронизацию между кластерами. Передается списком значений
from-cluster | hahn | Название кластера, с которого необходимо синхронизировать таблицы
to-cluster | hahn | Название кластера, с которого необходимо синхронизировать таблицы
only-new |  | Проверить и выгрузить только обновленные/измененные таблицы. Проверка осуществляется по update-id таблиц
running-task-limit | NNN | Параметр количество одновременно запущенных задач в TransferManager. Параметр трансфер менеджера, по умолчанию 100
workers | number | количество одновременно работающих воркеров luigi, если не указано - то 1 worker

### Обновление MV

## Инфраструктура
Большая часть кода оформлена в виде luigi.Task-ов, которые можно вызывать из Python с помощью [luigi.build](https://luigi.readthedocs.io/en/stable/running_luigi.html#running-from-python-code)

### URI
uri таблицы
```
base/con:schema.table
```
uri чанка
```
base/con:schema.table@chunk_field_name[from,to]:type
```
Чтобы из uri сделать пригодный для работы объект можно воспользоваться OracleExportable.exportable_from_uri или конструкторами его наследников.

## Мировые константы

## Тесты

Выставить переменные окружения
```bash
export INSTANT_CLIENT_HOME=/opt/oracle/instantclient_XX_X/
export BALANCE_BO_PASSWORD=XXX
export META_BO_PASSWORD=XXX
export ST_TOKEN=XXX
export S3_KEY_ID=XXX
export S3_SECRET_KEY=XXX
export YT_TOKEN=XXX
export YQL_TOKEN=XXX
```

Запуск юнит-тестов:
```bash
ya make -t
```

Запуск регрессии (может занять много времени, более 20 минут):
```bash
ya make -ttt
```

Запуск регрессии через sandbox
- Перейти на страницу https://sandbox.yandex-team.ru/scheduler/699029/view
- Нажать "Run once"
- Подробное описание механизмов: https://wiki.yandex-team.ru/users/mrevgen/dwh-regression-sandbox/

## Локальный запуск экспорта в YT

### Подготовка

```bash
$ python3 -m venv venv
$ source venv/bin/activate
$ pip install -r requirements.txt
```

### Переменные окружения

- `DWH_CONF_PATH` - конфиг для всего приложения. Дефолт: `/etc/dwh/conf.yaml`
- `DWH_SECRET_PATH` - конфиг с токенами. Дефолт: `/etc/yandex/balance-common/dwh-secret.cfg.yml`
- `MNCLOSE_PATH` - конфиг для подключения к mnlose. Дефолт: `/etc/yandex/balance-common/mnclose-conn.cfg.xml`
- `WORLD_CONSTS_PATH` - файлик с константами. Чтобы иметь возможность отличать REWARD_TYPE_GROSS от DIRECT_DSP да и вообще писать так вместо непонятных магических единиц. Дефолт: `/usr/bin/dwh/world_consts.yaml`
- `DWH_ENV_PATH` - конфиг для типа окружения. Дефолт: `/etc/yandex/environment.type`
- `ORACLE_CONFIG_PATH` - директория с конфигами к бд. Дефолт: `/etc/yandex/balance-common`

### Хинты

Если не хочется работать в бункере, можно держать хинты локально:

```
$ cat ./conf/local/hints/t_act_internal.json
{
        "partition_key": "",
        "dst": "",
        "modified": "",
        "full_key": [],
        "columns": [
                {
                        "name": "amt_w_nds",
                        "type": "float"
                },
                {
                        "name": "amt",
                        "type": "float"
                },
                {
                        "name": "amt_w_nds_rub",
                        "type": "float"
                },
                {
                        "name": "amt_rub",
                        "type": "float"
                }
        ]
}
```

### Логирование

Для корректного логирования при локальном запуске требуется дополнительно передавать параметр `--logging-conf-file conf/local/logging.conf`

### Запуск (python)

При установленном ``envbox`` переменные окружения могут быть взяты из ``.env`` файлов автоматически,
поэтому вручную можно их не выставлять.

```bash
$ python -m luigi --module grocery.wc A --local-scheduler --myparam "some"


$ python -m luigi --logging-conf-file /conf/local/logging.conf \
        --module grocery.yt_export YTFullExportTaskV2 \
        --uri "meta/meta_1:bo.v_opt_2015_acts" \
        --yt-path //home/balance/dev/yb-ar/acts/201905 \
        --update-id "`date +%s%N`" \
        --local-scheduler
```

### Запуск (binary) на dev/test сервере

Сборка бинарника и запуск делается одним скриптом:

```bash
$ cat run.sh
#!/usr/bin/env bash
source /etc/oraprofile
export PYTHONPATH=""
export LUIGI_CONFIG_PATH="/etc/dwh/luigi.cfg"

trap '>&2 echo "Killed from outer space"; exit 1' SIGTERM

ya make && \
    WORLD_CONSTS_PATH=./conf/remote/usr/bin/dwh/world_consts.yaml \
    ./src/dwh/grocery/run/run $@

$ sh run.sh -m luigi --module grocery.dcs.export.ovi PrepareCheckData --local-scheduler --workers 2
```
### Запуск (binary) локально

Сборка бинарника и запуск делается одним скриптом:

```bash
$ ya make && ./src/dwh/grocery/run/run -m luigi --module grocery.wc A --local-scheduler --myparam "some"

$ ya make &&
  LUIGI_CONFIG_PATH=./conf/remote/etc/dwh/luigi.dev.cfg \
  WORLD_CONSTS_PATH=./conf/remote/usr/bin/dwh/world_consts.yaml \
  DWH_CONF_PATH=./conf/remote/etc/dwh/conf.dev.yaml \
  DWH_SECRET_PATH=./conf/local/dwh-secret.yaml \
  DWH_ENV_PATH=./conf/local/environment.type \
  ORACLE_CONFIG_PATH=./conf/local \
  MNCLOSE_PATH=./conf/local/mnclose.xml \
  ./src/dwh/grocery/run/run -m luigi --module grocery.reputter Reputter --local-scheduler --workers 12
  --logging-conf-file ./conf/local/logging.conf --reput '["v_payment","v_person"]' --exclude '["v_person"]'
```


### Кроссвалидация

[DWH-772](https://st.yandex-team.ru/DWH-772)

* Граф в нирване для вычисления метрик находится по пути [/billing/dwh/metrics/crossvalidations](https://nirvana.yandex-team.ru/flow/3c142abe-f162-45a5-98fc-208acec81dc3/c8a99c3e-eb12-490c-9871-4ccd9fdb67d2/graph)
* Solomon-сервис [balance-reports_dwh_crossvalidation](https://solomon.yandex-team.ru/admin/projects/balance-reports/services/balance-reports_dwh_crossvalidation)
* В каталоге нирваны /billing/dwh/metrics запущены две реакции, отдельно для кластеров YT hahn и arnold
* Вот здесь посмотреть сами метрики https://monitoring.yandex-team.ru/projects/balance-reports/explorer/queries?q.0.s=%7Bproject%3D%22balance-reports%22%2C%20service%3D%22dwh_crossvalidation%22%2C%20cluster%3D%22Push%22%7D&refresh=60&range=1d&normz=off&colors=auto&type=auto&interpolation=linear&dsp_method=auto&dsp_aggr=default&dsp_fill=default&vis_labels=off&vis_aggr=avg

* Агрегаты https://juggler.yandex-team.ru/aggregate_checks/?project=dwh&query=host%3Ddwh.prod%26service%3Dcrossvalidation_*
* Описание проверок в MaC `$ARCADIA_ROOT/paysys/sre/tools/monitorings/configs/dwh/stable/dwh.py`

Чтобы создать новую проверку надо:
* Создать новый кубик в нирване с текстом YQL-запроса, который:
  * Имеет набор полей
    * `sensor` - название метрики (их сейчас две: `"too_big_too_small"`, `"sums_divergence"`)
    * `prefix` - YT-путь ко всем таблицам баланса, задается в глобальных параметрах, скорее всего `"home/balance/prod"`
    * `dir1` - YT-путь относительно `prefix`, где находятся данные с которыми сравниваемся
    * `dir2` - YT-путь относительно `prefix`, где находятся данные которые сравниваем (у `"too_big_too_small"` - пусто, сам с собой сравниваем)
    * `slice` - доп. информация, имя поля, в разрезе которого выполнялось сравнение, либо пустота
    * `value` - значение метрики типа `Double`
  * В котором каждая строчка - метрика; на данный момент все запросы возвращают лишь одну строчку;
  * не будет падать, если таблиц за какой-то месяц не окажется на YT (например, на Арнольд не выгружается `yb-ar/acts`). Для этого, например, с функцией `RANGE` используется хинт `WITH SCHEMA`: тогда, если список нужных таблиц пустой, селектим как будто из одной пустой таблицы.
* Расположить его внизу графа и прикрепить к `Prepare final query`
* В предпоследнем кубике в конце убрать символ `;` и заменить на `UNION ALL` обязательно добавив 2 пробела в конце, чтобы все правильно склеилось
* Если это новый `sensor`:
  * Обновить настройки в MaC, добавив новый вызов `_get_crossvalidation_multialert` внутри функции `checks`, правильно подобрав пороги срабатывания


### B2B-тестирование
[DWH-771](https://st.yandex-team.ru/DWH-771)

B2B-тестирование запускается, когда изменяется одна из следующих задач:
* DWH-724
* DWH-671
* DWH-397
* DWH-512

Тогда из пулл-реквеста в Teamcity автоматически запускается измененная задача. Агрегаты строятся на продовых данных, но кладутся в специально создаваемую для ПР'а папку в YT:
`//home/balance/dev/dwh/agg_compare/pr_<pr_number>`
По дефолту запускается на `hahn`. Чтобы запустить на другом кластере, нужно остановить текущий запуск в Teamcity и на [странице билда](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Billing_DWH_BuildAggregates), нажать справа сверху многоточие возле `Run`, во вкладке `Parameters` заполнить параметр `arc.pr_id` и изменить `cluster` на нужный.

После того, как агрегаты построились, запускается задача, сравнивающая полученный агрегат в папке ПР'а и "настоящий" агрегат в проде. Дифф между таблицами складывается в артефакты билда Teamcity в двух версиях -- короткой и полной.
В диффе остаются только колонки, в которых есть различия между продовой и dev-таблицей. Если таких колонок мало (<=5), слева выводятся колонки из prod-таблицы, справа -- из dev-таблицы. Если колонок больше 5, строки выводятся друг под другом.

Если открыть дифф в браузере у него, скорее всего, будет сбита кодировка, которую нужно поменять на этой открытой странице (пока с этим ничего не получается сделать).

Наличие строк в диффе необязательно значит, что изменение в задаче сломало ее логику.
Часто получаемые различия:
 * Разница в `client_name` -- например, было 'Рога и Копыта', а стало -- 'ООО "Рога и копыта"'. Скорее всего, просто изменился справочник с последнего обновления агрегата в проде;
 * Только новые строки в dev-таблице -- агрегат в проде не успел обновиться;
 * будет дополняться...

Кроме того, в папку ПР'а на YT в подпапку `diff` складываются еще две таблицы: строки, которые есть только в prod-таблице и строки, которые есть только в dev-таблице, отсортированные по каждой колонке. Иногда из них тоже можно извлечь какую-то полезную информацию.
