# Утилита анализа использования квоты

Утилита для измерения потребления CPU и RAM по таскам LOGOS и yt-операциям пользователя. Имеет три режима работы: формирование отчёта по таскам,
запущенным на dev-графе, мониторинг потребления квоты в Grafana, а так же формирование отчёта для любых yt-операций, сгруппированных по тегам.

## Как пользоваться

Общая структура запуска выглядит так:

`./monitor_quota [OPTIONS] COMMAND [ARGS]...`,

где `[OPTIONS]` &ndash; аргументы, общие для обоих режимов работы:

* `--workdir` &ndash; путь к директории на YT, куда будут сохранены промежуточные результаты работы. По умолчанию &ndash; `//home/ads/logos/monitoring`.
* `--start-date` &ndash; время в формате `Y-m-d H:M`&ndash; момент времени, **с** которого будет происходить фильтр операций. По умолчанию &ndash; неделю назад.
* `-d`, `--days` &ndash; количество дней, которые следует отсчитать от настоящего момента и принять за начальный момент времени. Может быть полезна, если требуются операции за последние n дней,
и прописывать `--start-date "Y-m-d H:M"` как-то лень.
* `-h`, `--hours` &ndash; аналогичная опция для часов. Можно комбинировать с `--days`. `--start-date` игнорируется, если его случайно указать вместе с `-d, -h`.
* `--finish-date` &ndash; время в формате `Y-m-d H:M`&ndash; момент времени, **до** которого будет происходить фильтр операций. По умолчанию &ndash; момент запуска.
* `--help` &ndash; показать примерно то же, что написано тут, и выйти.

`COMMAND` &ndash; непосредственно режим работы:
* `dev-report` &ndash; отчёт по таскам на dev.
* `graphite-report` &ndash; мониторинг потребления квоты.
* `report-tags` &ndash; отчёт по всем yt-операциям пользователя, сгруппированным по тегам.

#### Отчёт по таскам на dev

Собирает за заданный промежуток времени все таски, запущенные пользователем на dev, и выводит отчёт потребления CPU/RAM примерно в следующем виде:
```
2020-10-01T19:54:29.039 JoinBannerToEFHFactorsTask
User time: 2020-09-30 08:00:00
Release ID: test_banner_join_no_drop
CPU days: 2.34 (3.44 in prod)
GiB days: 8.96 (8.64 GiB in prod)

2020-10-01T19:54:37.340 JoinBannerToEDHFactorsTask
User time: 2020-09-30 08:00:00
Release ID: test_banner_join_no_drop
CPU days: 1.24 (1.18 in prod)
GiB days: 2.78 (2.74 GiB in prod)
```

Специфические опции для `dev-report`:
* `--user` &ndash; пользователь, по которому происходит фильтрация. По умолчанию &ndash; запустивший команду.
* `--disable-prod-diff` &ndash; по умолчанию рядом с результатом выводится также потребление ресурсов продовой версией этого таска. Данные достаются из таблички `{--workdir}/logos_prod_tasks`.
Данный флаг отключает сравнение с продом.

#### Мониторинг потребления квоты в Grafana

Высчитывает статистику потребления ресурсов по дням и отправляет отчёт в Graphite.

Специфические опции для `graphite-report`:

* `--upload-to-graphite` &ndash; отправить данные в Graphite.
* `--graphite-namespace` &ndash; часть пути для отправки данных в Graphite. Итоговые пути формируются как `one_day.{--graphite-namespace}.by_pool_project_state_child` и `one_day.{--graphite-namespace}.limits_by_pool`. По умолчанию &ndash; `ads_quality_logos.monitoring.quota`.

Если не указан `--workdir`, то будет использована `//home/ads/logos/monitoring`.

#### Отчёт по всем операциям

Собирает за заданный промежуток времени все операции, запущенные пользователем, группирует их по указанным тегам и выводит отчёт потребления CPU/RAM. Если тег в операции отсутствует, ему будет присвоено значение `unknown`. Пример вывода:

```angular2html
tag1: 1
tag2: two
CPU days: 0.97
Operation number: 1.00
User time: 0.26
GiB days: 4.25

tag1: one
tag2: two
CPU days: 2.09
Operation number: 2.00
User time: 0.52
GiB days: 12.20

tag1: unknown
tag2: unknown
CPU days: 4.71
Operation number: 2.00
User time: 3.92
GiB days: 10.63

```

Специфические опции для `report-tags`:
* `--user` &ndash; пользователь, по которому происходит фильтрация. По умолчанию &ndash; запустивший команду.
* `--tags` &ndash; теги, по которым группируются операции.

##### Как добавить теги

Для `yt.wrapper`, `yql` и `tabtools` можно добавить теги следующим образом:

```python
import logos.libs.clients as clients
import yabs.conf


# Указываем теги и их значения
annotation = {
    "tag1": "one",
    "tag2": "two",
}

# yt.wrapper client
yt = clients.GlobalYt(
    config={
        "spec_defaults": {
            "annotations": annotation,
        },
    },
).get_client()

# yql client
yql = clients.GlobalYql(
    additional_attributes=annotation,
).get_client()

# tabtools
mr_conf = yabs.conf.update(basename="mapreducelib")
mr_conf.mapreducelib.options.yt_spec.annotations = annotation
```

## Примеры

```
$ YT_PROXY=hahn ./monitor_quota --start-date 2020-09-29\ 00:00 dev-report

$ YT_PROXY=hahn ./monitor_quota -d 1 -h 12 dev-report --user npytincev --disable-prod-diff

$ YT_PROXY=arnold ./monitor_quota --workdir //home/ads/logos/monitoring graphite-report --upload-to-graphite --graphite-namespace ads_quality_logos.monitoring.quota.grafana_by_clusters.arnold

$ YT_PROXY=hahn ./monitor_quota -d 2 report-tags --tags script_name --tags user_time

$ YT_PROXY=hahn ./monitor_quota report-tags --tags script_name --user npytincev
```

## На что стоит обратить внимание

1. При подготовке отчёта по dev время работы сильно зависит от заданного промежутка времени. Если интересует какой-то конкретный таск, то рекомендуется ограничить период времени в пару часов,
во время которого таск гарантированно отработал, чтобы утилита работала порядка нескольких секунд.
1. Чтобы информация о продовых ресурсах доставалась как можно быстрее, регулярный процесс фильтрует полный архив операций и сохраняет продовые операции в нашу табличку каждые два часа. Поэтому, если информации о проде нет, хотя должна быть,
есть вероятность, что таблица просто не успела обновиться – повторите попытку через некоторое время.
1. Чтобы не утяжелять таблицу с отфильтрованными запусками на проде, хранятся запуски только за последние две недели. По этой причине не стоит запускать на деве операции за слишком старую дату: их будет не с чем сравнивать.

## Алгоритм работы

#### Отчёт по таскам на dev

Вначале происходит фильтрация по пользователю, имени проекта и времени запуска. При этом используется высокоуровневый интерфейс
[`iterate_operations`](https://docs.yandex-team.ru/yt/api/python/python_wrapper#op_job_commands), так как на разумном (порядка нескольких тысяч)
количестве операций он позволяет добиться многократного прироста скорости выполнения по сравнению с грепом через YQL. Далее мы группируем данные по имени таска и времени запуска на Нирване с точностью до миллисекунд,
суммируя CPU/GiB-дни.

#### Мониторинг потребления квоты в Grafana

В случае мониторинга **продовых тасков** запускается YQL-запрос, фильтрующий нужные операции из [логов YT](https://yt.yandex-team.ru/hahn/navigation?path=//sys/operations_archive/ordered_by_id)
по пользователю, пулу и времени запуска (по умолчанию -- не старше недели).

Из "тяжёлых" колонок (таких, как `spec`, `full_spec`, `progress`) извлекаются нужные поля (лимиты CPU, RAM, суммарное время работы джобов и другие). Для каждой операции суммарное время работы джобов
(которое за счёт параллельного выполнения в общем случае не равно настенному времени работы этой операции) умножается на лимит CPU/RAM и делится на время работы операции.
Таким образом получается некоторая усреднённая величина потребления ресурсов данной операции в секунду. Потреблённые ресурсы пропорционально распределяются по часам: для каждого часа, который
пересекается с промежутком работы операции, усреднённое потребление CPU/RAM умножается либо на 3600 секунд, если операция проработала весь час, либо на остаток секунд,
если операция началась/закончилась в течение этого часа. Результаты, соответствующие каждому часу одного дня, группируются и суммируются, получая таким образом потребление ресурсов за день.
После этого данные группируются по имени скрипта, пользователю, состоянию и др. и загружаются в Graphite.

#### Отчёт по всем операциям

Операции фильтруются по пользователю и времени запуска с помощью [`iterate_operations`](https://docs.yandex-team.ru/yt/api/python/python_wrapper#op_job_commands), далее мы группируем данные по тегам, суммируя CPU/GiB-дни.

