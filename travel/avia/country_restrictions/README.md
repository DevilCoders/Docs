# Country restrictions

Сервис для обработки ограничений по странам, регионам и т. д. с разных источников.

[Ссылка на wiki](https://wiki.yandex-team.ru/avia/dev/services-table/country-restrictions/)

## Деплой
https://a.yandex-team.ru/projects/ticket/ci/releases/timeline?dir=travel%2Favia%2Fcountry_restrictions&id=regular-release

## Разработка

### Преамбула

* По умочанию вся информация пишется и на `hahn`, и на `arnold`
* Если нужен только `hahn`, в `./bin/bin` нужно дополнительно передавать `--yt-proxies hahn`
* Если хочется создать структуру вручную, можно взять формат папок из `//home/avia/data/country-restrictions`

### Вначале

1. Убедиться, что в `~/.yt/token` есть токен для YT. Если нет, то поставить его или при вызове `./bin/bin` каждый раз
передавать `--yt-token <your_token>`
2. Собрать текущее: `ya make`
3. Подготовить свою директорию: `./bin/bin create-bp --base-path //home/avia/dev/<your_folder>/country-restrictions`
4. Если используется PyCharm, выполнить `ya ide pycharm` в корне проекта
5. Если используется PyCharm, то `File` > `Invalidate Caches...` > `Invalidate and restart`

### Тестирование

1. Собрать: `ya make`
2. Протестировать: `ya make -t`
3. Очистить свои директории: `./bin/bin yt-clear --base-path //home/avia/dev/<your_folder>/country-restrictions`
4. Запустить парсеры: `./bin/bin combined --base-path //home/avia/dev/<your_folder>/country-restrictions --sandbox-token <SANDBOX_TOKEN>`
5. Перейти по url из вывода терминала и убедиться, что всё хорошо

## Локальный запуск

Делается через `./bin/bin <command> <options>`.

Помощь: `./bin/bin --help`

### Команды

|Имя|Описание|
|---|---|
|`source-parser <paser_name>`| Запустить определенный парсер. Текущие парсеры: `serp`, `assessors`, `inline_admin`|
|`aggregator`| Запустить аггрегатор (имеем где-то таблицы источников, хотим итоговый вывод)|
|`combined`| Запустить и парсеры, и аггрегатор|
|`yt-clear`| Очистить директорию проекта в YT. Не сделает ничего, если указанный через `--base-path` путь не является папкой разработчика|
|`create-bp`| Сформировать пути в YT, если они не сущестсвуют. Не сделает ничего, если указанный через `--base-path` путь не является папкой разработчика|

### Опции

|Имя|Описание|Обязательная / Default|Пример|
|---|---|---|---|
|`--environment`|Окружение|`testing`|`testing` OR `production`|
|`--version`|Версия структуры выходных данных|`1`|`1`|
|`--base-path`|Путь к корню данных проекта|Обязательная|`//home/avia/dev/<your_folder>/country-restrictions`|
|`--yt-token`|Токен в YT|Берется из env или из файла в системе|`AQAD-xxx`|
|`--yt_proxies`|Кластеры YT|`hahn,arnold`|`hahn`|
|`--solomon-token`|Токен в solomon|`None`|`AQAD-xxx`|
|`--sandbox-token`|Токен в solomon|Обязательная для непосредственно запусков парсеров|`AQAD-xxx`|

## Архитектура

### Парсеры

Иерархия начиная от `AbcParser`

`ToYtTableParser(AbcParser)` - парсим в YT таблицу. Перед началом считывает данные из результирующей таблицы, если она
есть и перезаписывает новыми при необходимости.

`YtTablesToYtTableParser(ToYtTableParser)` - из n YT таблиц одного формата в YT таблицу.

`PipelineParser(AbcParser)` - последовательно применить парсеры.

### Метрика

Непосредственно хранит данные. Создавать вручную не надо, нужно делать это через фабрики - `MetricType`.
Добавлять дополнения и исключения нужно тоже через фабрики.

Список всех актуальных метрик есть на [wiki](https://wiki.yandex-team.ru/avia/dev/services-table/country-restrictions/#tekushhiemetriki).
При добавлении новых обновить страницу.

### MetricType

Иерархия начиная с `MetricType`.

Фабрика для создания метрик. Хранит в себе все строковые литералы, связанные с метриками.

Также умеет в создание дополнений и исключений к метрикам.

## Метрики

### Виды метрик

1. Общие (`total`, `null`, `updated`) x (`geo`, `metrics`, `cells`)

   Всего 9 метрик соломона. Отправка в `lib/parsers/to_yt_table_parser.py`

   | Метрика соломона  | Описание |
   | ----------------- | --- |
   | `updated_geo`     | геопозиции с хотя бы одним обновлением ячейки |
   | `updated_metrics` | метрики с хотя бы одним обновлением ячейки |
   | `updated_cells`   | обновленные ячейки |
   | `null_geo`        | геопозиции, где все ячейки пустые |
   | `null_metrics`    | метрики, где все ячейки пустые |
   | `null_cells`      | пустые ячейки |
   | `total_geo`       | всего геопозиций |
   | `total_metrics`   | всего метрик |
   | `total_cells`     | всего ячеек |

2. Говорящие о конфликтах между метриками.

   Например: туризм невозможен, но можно поехать с вакциной.

   Детальнее тут: `lib/parsers/metric_corectness_validators.py`

### Положение

| Название | Значение |
| -------  | --- |
| Проект   | `avia` |
| Кластер  | `country_restrictions_{testing,production}` |
| Сервис   | `country_restrictions` |
