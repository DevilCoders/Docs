## Oracle_estimator

Скрипт генерации описания тикетов с оценкой для проекта миграции MBO из Oracle.

## Тикеты

- Основной тикет проекта [MCPROJECT-681](https://st.yandex-team.ru/MCPROJECT-681)
- [Удаление одиночных таблиц](https://st.yandex-team.ru/issues/409173)
- [Удаление кластеров таблиц](https://st.yandex-team.ru/issues/409174)
- [Миграция одиночных таблиц](https://st.yandex-team.ru/issues/409175)
- [Миграция миграция кластеров](https://st.yandex-team.ru/issues/409176)

## Как работать

### Структура папок и основные конфигурационные файлы
1)`/data` - обновляемые вручную и автоматом конфигурационные файлы, а именно:

`clusters.txt` - "нулевое" разбиение объектов по кластерам в начале проекта; не используется сейчас.

`objects.yaml`- основной конфигурационный файл для обновления статусов тикетов;

`oracle_size_data_%.csv` - перечитываемые автоматом данные о размере объектов в оракле.

`repositories.yaml` - список используемых репозиториев, для поиска использований в коде.

`reserved_tickets.txt`- сюда  записываются все созданные через oracle_estimator тикеты.

`usages_%Y_%m_%d.csv`- обвноляемый файл найденных использований объектов в аркадии и github,
хранится в sandbox и скачивается локально для обновления описаний тикетов.

2) `/sql` - поисковые скрипты, используемые для обновления данных из Оракла.

3) `/manual_usages_extract` - сюда выкачиваются и обновляются скрипты DDL, используются для поиска использований генерации `usages_%Y_%m_%d.csv`

### Типовой порядок использования oracle_estimator

#### Полный цикл обновления
1) Перечитать файлов `objects.yaml, oracle_size_data.csv, reserved_tickets.txt` и скриптов DDL для объектов из
   ПРОДА Оракла. На данном шаге в том числе в трекере автоматически могут создаваться новые тикеты для новых
   обнаруженных в Оракле объектов.
2) Перегенерить файл `usages.csv` c помощью `csearch` и выложить их в Sandbox.
3) Обновить тикеты, используя свежие файлов из п.1 и п.2.
4) Закоммитить файлы из п.1 в транк.

#### Обновление только objects.yaml и отдельных тикетов
1) Вручную внести изменения в `objects.yaml`.
2) Обновить отдельные тикеты, используя правки в `objects.yaml`.
3) Закоммитить `objects.yaml` из п.1 в транк.

### 1. Обновление objects.yaml, oracle_size_data.csv, reserved_tickets.txt и скриптов DDL
Команда `refresh-objects-info` используется для выкачивания из Oracle актуальной информации об объектах, генерации objects.yaml, oracle_size_data.csv, а также
автоматическом создании новых тикетов для новых найденных объектов в БД (за вычетом фильтров в скриптах `data/objects.sql` и `data/oracle_size_data.sql`).
Для новых объектов в треккере создаются тикеты-заглушки ("резервируются") - номера этих тикетов записываются в `data/reserved_tickets.txt` и `data/objects.yaml`
Полное описание этих тикетов моожно создать с помощью команды update-ticket (смотри описание ниже)

Oracle_estimator c командой `refresh-objects-info` использует для подключения к Oracle используется библиотеку [cx_Oracle](https://oracle.github.io/python-cx_Oracle/)
Для работы этой библиотеки потребуется вручную установить библиотеки Oracle:
- [Инструкция для Linux](https://oracle.github.io/odpi/doc/installation.html#linux)
    1. Скачать zip-архив `instantclient-basic-linux.x64-21.1.0.0.0.zip`
    2. Создать директорию `/opt/oracle/`
    3. Распаковать архив в `/opt/oracle/` - создастся директория `instantclient_21_1`
    4. Установить `libio` - для Ubuntu надо устанавливать `libaio1` вместо `libaio`, для MacOS `libio` не требуется
    5. Выполнить команду (при этом версия instantclient может отличаться у вас)
        ```sh
        export LD_LIBRARY_PATH=/opt/oracle/instantclient_21_1:$LD_LIBRARY_PATH
        ```
    6. Скачать файл [etcd.yml](https://github.yandex-team.ru/cs-admin/datasources-ng/blob/master/production/etcd.yml) в директорию `~/arc/github/cs-admin/datasources-ng`

Для обновления `objects.yaml` и дампа `oracle_size_data` наберите:

```sh
ya make . && ./estimator refresh-objects-info
```

При работе этой команды

Если возникает ошибка `cx_Oracle.DatabaseError: ORA-24454: client host name is not set` выполнить [команду](https://dba.stackexchange.com/a/167479):
```sh
sudo /bin/bash -c "echo '127.0.1.1 ${HOSTNAME}' >> /etc/hosts"
```

Если возникает ошибка `cx_Oracle.DatabaseError: ORA-00936: missing expression`, можно попробовать пропустить поиск внутренних SQL с помощью ключа `--skip-inner-sql`.

### 2. Работа с usages.csv

Для обновления списка использований объектов в описании тикетов oracle_estimator готовит таблицу usages.csv.
Этот файл можно сгенерировать с помощью специальной команды или скачать из sandbox готовый (ранее сгенерированный и загруженный).

#### Генерация файла usages.csv
Файл usages.csv формируется в формате объекты - ссылки на использования до строки.
Для этого происходит выкачивание кода из аркадии и гитхаба из репозитариев, указанных в `data/repositories.yaml` во временную локальную папку.
Затем генерация индекса через `cindex`. А затем поиск использований для каждого объекта из `data/objects.yaml` через `csearch` с записью резульататов в новый файл `data/usages_%Y_%m_%d.csv`
Для быстрой генерации необходимо
1. Установить go ([инструкция](https://golang.org/doc/install))
2. Установить csearch ([репозиторий](https://github.com/google/codesearch))
3. Выполнить команду
   ```shell script
   ya make && ./estimator generate-usages-csearch
   ```
Используя дополнительный флаг `--only-in-strings` можно ограничить поиск использований только внутри строк, ограниченных символами '' или "".
Это может быть полезно для поиска использований для частотных таблиц по сгенерированному файлу.
   ```shell script
   ya make && ./estimator generate-usages-csearch --only-in-strings
   ```
#### Поиск использований по usages.csv
 - Получить список уникальных использований `CATEGORY` и `CATEGORY_NAME` в коде:
    ```shell script
    egrep -w 'CATEGORY|CATEGORY_NAME'  data/usages_2022_04_12.csv |  egrep -v '(.sql|changelog.xml|oracle_estimator)'  | awk -F',/var.*https' '{print $1" https"$2}'| less
    ```
 - Получить список файлов (классов) с использованиями `CATEGORY` и `CATEGORY_NAME` в коде:
    ```shell script
    egrep -w 'CATEGORY|CATEGORY_NAME'  data/usages_2022_04_12.csv |  egrep -v '(.sql|changelog.xml|oracle_estimator)'  | awk -F',/var.*https' '{print $1" https"$2}'| awk -F '\\?#|#' '{print $1}' | sort -u  | less
    ```
 - Получить количество файлов (классов) с использованиями `CATEGORY` в коде:
    ```shell script
    egrep -w 'CATEGORY|CATEGORY_NAME'  data/usages_2022_04_12.csv |  egrep -v '(.sql|changelog.xml|oracle_estimator)'  | awk -F',/var.*https' '{print $1" https"$2}'| awk -F '\\?#|#' '{print $1}' | sort -u  | wc -l | less
    ```

#### Использование готового файла usages.csv из Sandbox

**В связи с тем, что генерация usages на основе csearch достаточно быстрая, рекомендуется использовать ее**

Тем не менее, если по каким-то причинам не получается сгенерировать usages локально, можно по прежнему использовать готовые файлы.

~~Рассчет использований таблиц занимает достаточно много времени, поэтому целесообразно использовать готовые файлы с рассчтеами.~~

Для загрузки файлов в sandbox понадобится получить токен на страничке https://sandbox.yandex-team.ru/oauth/token .
После получения токена его рекомендуется положить в файл `~/.sandbox/token`

Для того, чтобы загрузить сгенерированный usages файл в sandbox нужно выполнить команду:
```shell script
ya upload \
  --token $(cat ~/.sandbox/token) \
  --ttl 60 \
  --owner MARKET \
  --description "MBO tables usages uploaded by $(whoami) at $(date -u --rfc-3339=seconds)" \
  --attr mbo_tables_usages=True -- \
  ./data/usages_$(date +"%Y_%m_%d").csv
```
Не рекомендуется менять атрибуты и ttl, чтобы загруженные файлы можно было найти, и чтобы они автоматически удалялись через 60 дней.

Загруженные файлы можно найти в sandbox по [ссылке поиска](https://sandbox.yandex-team.ru/resources?owner=MARKET&type=OTHER_RESOURCE&limit=20&attrs=%7B%22mbo_tables_usages%22%3Atrue%7D&created=1_month)


### 3. Обновление описания тикетов
Для обновления описания тикетов необходимо вызвать команду:

```sh
ya make. && ./estimator update-ticket --usages-file="./data/usages_$(date +"%Y_%m_%d").csv" --tickets <TICKET-ID-1> <TICKET-ID-2>
```
Закрытые тикеты не будут обновляться по умолчанию, для их принудительного обновления нужно использовать флаг:
```sh
--update-closed
```
### Обновить описание всех тикетов

Для обновления описания тикета необходимо вызвать команду:

```sh
ya make. && ./estimator update-ticket --usages-file="./data/usages_$(date +"%Y_%m_%d").csv" --all-schemas --all-objects --big-tables-ticket
```

Для вновь найденных объектов в Оракле (после шага 1 `refresh-objects-info`) - нужно выполнить `update-ticket` хотя бы раз, чтобы поменять описание заглушку.

Используйте эту функциональность с осторожностью.


#### Альтерантивные репозитории

Для поиска по другим репозиториям, можно указать любой другой файл, вместо `./data/repositories.yaml` с аналогичной структурой.
Сделать это можно с помощью параметра `--repositories-file="path/to/another/file"`.
Репозитории будут склонированы во временную папку и по ним будет выполнен поиск объектов из `objects.yaml`.

### Startrek token

Для обновления описания тикетов необходимо получить Startrek API token [по ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5f671d781aca402ab7460fde4050267b).
Подробнее см [документацию  Startrek API](https://wiki.yandex-team.ru/tracker/api/).

Этот токен необходимо положить в файл `~/.st/token`.

### Dry run

Для проверки генерации можно воспользоваться флагом `--dry-run`, который выведет сгенерированное описание в консоль.

Пример:

```sh
ya make. && ./estimator update-ticket  --tickets MBO-31550 --dry-run
```


## Дополнительные возможности oracle_estimator

### Печать таблицы для burndown графика

```shell script
ya make. && ./estimator burndown-csv
```

Или

```shell script
ya make. && ./estimator burndown-csv --dates 2021-08-01 2021-08-03 ...
```

Если надо за укказанные дни


### Получение списка зависимостей по DDL
```shell
ya make. && ./estimator build-graph --root ROOT
```
ROOT в формате `<object_type>.<object_owner>.<object_name>`, например, `view.site_catalog.v_mp_map`

* Параметр `--depth N` - отвечает за глубину DFS поиска по построенному графу. По умолчанию `N = -1`, что означает максимальную глубину поиска
* Параметр `--use-tickets` - если указан, добавляет зависимость между объектами в одном тикете, если не указан — не учитывает тикеты при построении зависимостей
* Параметр `--ignore-finished` - если указан, при построении зависимостей игнорирует объекты со статусом MIGRATED и DELETED, если не указан — использует все объекты

* Параметры `--print-objects`, `--print-tickets`, `--print-filenames` отвечают за информацию, выводимую в результате работы скрипта
   * Если указан `--print-objects` выводит имена зависимых объектов в формате `<object_type>.<object_owner>.<object_name>`
   * Если указан `--print-tickets` выводит id тикетов, в которых найдены зависимые объекты
   * Если указан `--print-filenames` выводит имена файлов, в которых найдены зависимые объекты
   * Если указаны все 3 или ни одного — выводит полную информацию

### Перегенерация json'а по DDLкам

Все файлы DDL файлы перестраиваются в массив объектов следующего вида:
```json
{
        "filename": "manual_usages_extract/some_file_name.sql",
        "keys": [
            "<object_type>.<object_owner>.<object_name>",
            "<object_type>.<object_owner>.<object_name>",
            ...
        ]
}
```
В `keys` указываются все объекты использующиеся в файле

Перегенерация usages.json (в keys будут записаны все объекты):
```shell
ya make. && ./estimator generate-usages-json
```

Перегенерация usages_ignore_finished.json (в keys будут записаны все объекты, кроме объектов в статусе DELETED и MIGRATED):
```shell
ya make. && ./estimator generate-usages-json --ignore-finished
```

Т. к. генерация основана на файле objects.yaml при изменениях статусов объектов в objects.yaml следует перегенерировать и usages_ignore_finished.json, а при добавлении/удалении объектов в objects.yaml следует перегенерировать и usages.json
