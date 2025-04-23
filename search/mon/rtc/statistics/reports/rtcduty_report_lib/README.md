# RTCDutyReporter

## What for?

Библиотека для генерации еженедельного отчёта RTCDUTY,
который обсуждается на встрече по передаче дежурств RTC.

## How is working?
Отчёт формируется на основе jinja-шаблона и запросов в Трекер.

Криты/Блокеры и Проблемы/Доработки выгружаются вне зависимости
от статуса, за прошедшую неделю с момента запуска **reporter**'а.
Тикеты для таблицы "Проблемы/Доработки" выгружаются по тэгу **duty_report_review**,
и попадают в отчёт, если тег был проставлен менее чем за неделю
до запуска **reporter**'а.

Тикеты с просроченным SLA выгружаются в отчёт только если они
в статусе "В работе" или "Команда разработки". Далее они сначала
сортируются по статусу, а потом по команде разработки.

Команды разработки определяются по тэгам вида "Team:<Tag>" и составляются на основе
таблицы https://rtc.yandex-team.ru/docs/support/responsibility

В **reporter** выгружаются из YAML-файла формата:
```
- {responsible: <staff-login1>, Team: <Tag1>}
- {responsible: <staff-login2>, Team: <Tag2>}
```
На данный момент файл нужно заполнять вручную,
автоматической генерации нет. Последняя актуальная версия файла находится вместе с либой.

Все тикеты, в которых не задан или задан некорректно тэг
отгружаются в **Team: Other**.

## Requirements

Для работы репортера необходимы стандартные модули Python и сам Python версии 3.6+(используются f-string)
```
os, datetime, yaml, jinja2, logging
```

И [яндексовый модуль](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/startrek_python_client)
с python'овским Startrek-client'ом.

## How to use?
В python3 cli:
```
from rtcduty_report import RtcDutyReporter
RtcDutyReporter(report_template_file_path="<путь к файлу с шаблоном отчёта>", responsible_file_path="<путь к файлу с командами и ответственными>", st_token="<токен для образения в API Startrek>"  support_queue="<Имя очереди в которой будем искать тикеты>", report_queue="<Имя очереди, в которой создастся результирующий отчёт>").generate_report()
```

Через Sandbox:
1. Если необходимо, собрать бинарник таски https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/rtcbutler/CreateRtcdutyReport с помощью задачи ##DEPLOY_BINARY_TASK##. Пример: https://sandbox.yandex-team.ru/task/1131201335
2. Релизнуть успешно собранный бинарь в необходимый стейджинг (testing/stable).
2. Запустить получившуюся Binary Task ##GENERATE_RTCDUTY_REPORT##. В полях прописать параметры, которые необходимы для работы таски:
```
Token for usage Startrek API (yav st_token)   -   токен для похода в Стартрек, расположенный в YaV. Токен в YaV должен быть указан с ключом ST_TOKEN.

ST Queue that will be searched for tickets (support_queue) - очередь, в которой будут парситься тикеты для отчёта.

ST Queue to wich will be sended report (report_queue) - очередь, в которой будет сгенерирован тикет с отчётом.

Svn url for arc with revision. (arcadia_head) - ветка репозитория, откуда будем забирать конфиги и JSON'ы для работы таски. 
Установлена в ##arcadia:/arc/trunk/arcadia##

Relative path in Arcadia to file with Jinja2 template of report (template_file) - относительный путь от ветки до jinja-шаблона отчёта.
По-умолчанию: search/mon/rtc/statistics/reports/rtcduty_report_lib/report_template.jinja

Relative path in Arcadia to YAML-file with defenition Team - Responsible for team (responsible_file) - относительный путь от ветки до YAML-файла с таблицой ответственных по командам.
По-умолчанию: search/mon/rtc/statistics/reports/rtcduty_report_lib/responsibles

Relative path in Arcadia to Summon Message file (summon_file) - относительный путь от ветки до файла с текстом призыва ответственных за команды в отчёт.
По-умолчанию:  search/mon/rtc/statistics/reports/rtcduty_report_lib/summon_message


Binary task executor
Release type of binary executor resource (binary_executor_release_type) - бинарник таски из какого стейджинга использовать.(см. пункт 2)
По-умолчанию: stable
```
