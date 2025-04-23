GP -> YT
========

Ссылка на [кубик в Nirvana](https://nirvana.yandex-team.ru/alias/operation/dmp-gp-yt).


## Конфигурация кубика

* **Source GP table path** – что копируем (полное имя таблицы вместе со схемой)
* **Target YT table path** – полный путь на YT Hahn куда копируем данные. Если данные партиционированы, то путь станет папкой, в которой будут лежать партиции.
* **If table exists** – что делать, если на момент запуска кубика таблица уже существует:
  - *drop and recreate* – перезатереть
  - *append* – добавить записи в конец. Не поддерживается, если выбран **Partition Scale** отличный от *No partitioning*
* **Schema of the target YT table** – схема результирующей таблицы на YT. Далее поговорим о ней поподробнее.
* **Name of the column, used for partitioning** – колонка, по которой надо партиционировать данные. Если не задана, то данные будут литься в одну таблицу.
* **Partition Scale** – период партиционирования. Может быть **day**, **month** или **year**.
* **First date of the period to replicate** – Дата, начиная с которой нужно перелить данные.
  Работает только в режиме партиционирования. Эта дата должна совпадать с началом партиции.
  Выборка производится по полю партиционирования.
* **Last date of the period to replicate** – Дата, до которой (включительно) нужно перелить данные.
* **Optimize For** – режим оптимизации: **scan** (по-умолчанию) или **lookup**.
* **Compression Level** – режим сжатия данных, по-умолчанию средний, с использованием **zlib_9** кодека.
* **GPTransfer** – Через какой GPTransfer запускать переливку. Влияет на Greenplum базу, из которой
  будет производиться выборка данных. Этот параметр нужен больше для тестирования, так как позволяет
  образаться к тестовой базе Butthead. По-умолчанию: **Ritchie**.
* **dmp-config.yaml** – секретный конфиг с токенами.

### Права доступа на таблицу в Greenplum

Для переливаемой таблицы нужно выдать грант на селект для `robot-taxi-stat`

```sql
grant select on <your table name> to "robot-taxi-stat"
```

### Схема YT-таблицы

**Schema of the target YT table** – это список полей и их типов в результирующей таблице. Перечислить этот список придется вручную в виде JSON'а, где каждая запись имеет два ключа: **name** (имя таблицы) и **type** (тип).

Пример:

```json
[
    {
        "name": "utc_created_dttm",
        "type": "datetime",
        "required": true,
        "sort_order": "asc"
    },
    {
        "name": "age",
        "type": "int64",
        "required": true,
        "sort_order": "desc"
    },
    {
        "name": "height",
        "type": "double"
    }
]
```

[Вот тут](https://wiki.yandex-team.ru/dmp/archive/development/projectinfo/typing/#mappingtipov) есть хорошая статья от Платформы на тему соответствия типов между GP и YT.

### Обязательные поля

Помимо **type**, для поля можно так же указывать **required: True**, если оно обязательно.

### Сортировка по ключу

Если на выходе нужно получить отсортированную таблицу (например потому что из неё будет быстрее работать выборка),
то следует колонки, которые будут входить в ключ, поместить в схему в том порядке, в котором они должны идти
в ключе, а к самим колонкам добавить поле, указывающее на порядок сортировки:

* **sort_order="ascending"**
* **sort_order="descending"**

Вместо **ascending** и **descending** можно использовать алиасы **asc** и **desc**.

{% note warning %}

На данный момент сортировка работает только для режима перезаписи таблиц.
В режиме **append** кубик сортировать не умеет.

{% endnote %}

### Конфиг с токенами

**dmp-config.yaml** – должен содержать токены для доступа к YT и GP и иметь следующую структуру:
```yaml
yt:
    yt_token: AQAD-...

greenplum:
    default_connection: ritchie

    connections:
        ritchie:
            user: <username>
            password: AQAD-...
```

Токены должны соответствовать пользователю, указанному в пункте **user**.

Если хотите настроить этот кубик для своего пользователя, то [тут](https://oauth.yt.yandex.net/)
можно взять свой **YT token**, а [тут](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=833bfb16b4ca43408e2ed077f1893601) - **GP token**.

Полученный JSON нужно добавить в Нирвану с типом **Private Key** (не Token):

![](https://jing.yandex-team.ru/files/art/creating-dmp-config.png)

## Колонки с типом Datetime

В YT схеме вы можете указать такие типы данных, как **datetime**, **date** или **timestamp**.

Если колонка на Greenplum имеет тип **TIMESTAMP WITHOUT TIME ZONE** то по умолчанию, операция будет считать,
что в колонке лежит время в таймзоне **UTC**. Если это не так,
то нужно прописать правильную таймзону, передав в опции кубика **column_settings** словарь типа такого:

```json
{
   "msk_created_at": {
       "default_timezone": "Europe/Moscow"
   }
}
```

Для колонок, имеющих в Greenplum тип **DATE**, перевод из одной таймзоны в другую невозможен,
но иногда может быть необходимо сделать колонку, в которой будет дата по московскому времени:

{% note warning %}

Из-за некоторых особенностей DataLens ваши отчёты будут строиться по данным в UTC таймзоне.
Если нужно сделать отчет, который выбирает данные по московскому времени, то нужно заранее на Greenplum
создать колонку с типом **DATE** и поместить в него именно дату по московскому времени а не по UTC.
Как это сделать, имея обычный **TIMESTAMP**, [описано на вики](https://wiki.yandex-team.ru/dmp/platform/dmpsuite/datetime/#chtozhedelat).

{% endnote %}

## Маленькие хитрости

### Генерация списка колонок для схемы целевой таблицы

Для генерации списка колонок и их типов можно использовать код ниже.

{% note warning %}

Обязательно уберите последнюю запятую у последней строки.

{% endnote %}

```sql
select
  column_name, data_type, udt_name, numeric_precision , numeric_precision_radix,
  '{"name":"'||column_name||'", "type":"'||
     case
       when udt_name in ('text','varchar')   then 'string'
       when udt_name in ('int2','int4')      then 'int32'
       when udt_name in ('int8','int32')     then 'int64'
       when udt_name in ('numeric')          then 'double'
       when udt_name in ('float8','numeric') then 'double'
       when udt_name in ('bool')             then 'boolean'
       when udt_name in ('timestamp','timestamptz') then 'datetime'
       when udt_name in ('date')             then 'date'
     else
       udt_name
     end||'"'
     ||case when is_nullable='NO' then ', "required":"true"},' else '},' end
   as Schema_of_the_target_YT_table
from
  information_schema.columns c
where 1=1
  and table_schema = $your_schema
  and table_name   = $your_table
order by ordinal_position
```


## Возможные проблемы

### Permission denied for table
```
message='Task not valid: Permission denied for table ... in robot-taxi-stat@gpdb-pgbouncer-gptransfer.taxi.yandex.net:5432/ritchie Greenplum'
```

Для GPTransfer существует отдельный робот по имени `robot-taxi-stat`.
Нужно предоставить ему права на доступ к переливаемой таблице (т.е. прописать `GRANT SELECT ON ... TO "robot-taxi-stat"`)

Вторая причина – у `robot-taxi-stat` нет прав доступа к схеме с таблицами
[закажите через IDM](https://idm.yandex-team.ru/reports/roles#rf=1,rf-role=noEnV6sb#user:robot-taxi-stat@taxi-dwh-idm-integration/greenplum_analyst/greenplum_schema_access(fields:();params:()),f-role-id=64162411,f-is-expanded=true,f-status=all,f-system-type=all,rf-expanded=noEnV6sb) права на чтение.

### Got internal exception

```
message='Got internal exception in the Gptransfer: error when connecting to gpfdist'
...
process_uuid='a3353fb6-75ac-478b-805b-5de0070fb19d'
```

Велика вероятность, что проблема **в несоответствии типов** полей
между YT и GP. Используйте код из раздела "Генерация списка колонок для схемы целевой таблицы",
чтобы починить типы колонок в схеме.

Чтобы проверить это наверняка:

1. Заходим в [Кибану](https://kibana.taxi.yandex-team.ru/app/kibana#/).
2. Вместо **Lucene** (справа от строки поиска) указываем **KQL**.
3. Вместо **yandex-taxi-*** указываем **taxi-dwh-***.
5. В строке поиска вводим `application: gptransfer AND process_uuid: <uid из сообщения об ошибке>`
6. Жмём кнопку **Update** и смотрим в логах, в чем была проблема.

# ChangeLog

## 0.1.7

Просто пересборка операции после перемещения кода вверх по дереву папок.

## 0.1.6

Теперь операция помечена, как non-deterministic, чтобы не использовать по умолчанию данные из кэша.

## 0.1.5

В этой версии была добавлена поддержка **Datetime**, **Date** и **Timestamp** колонок на YT.
Достаточно указать один из этих типов в опции **yt-schema**. Подробнее, смотрите раздел **Колонки с типом Datetime**.

Обратно-несовместимые изменения:

* Теперь **Last date of the period** должна быть меньше или равна текущей дате.
  Раньше, если дата оказывалась в прошлом, это могло приводить к падениям
  переливки данных в GPTransfer.
* Опция **yt_schema** была переименована в **yt-schema**. После апгрейда Надо будет заполнить его заново,
  перенеся значение из предыдущего запуска операции.

## 0.0.5

* В этой версии в режиме drop таблицы заменяются "транзакционно".
  То есть, во время пока данные переливаются, доступна старая версия таблицы,
  а в конце происходит переключение на новую версию данных.
* Добавлена поддержка партиционирования.
* Выбор периода данных для обновления.
* Теперь можно задавать режим оптимизации:
  * scan (по-умолчнанию);
  * lookup.
* Возможность создавать сортированые таблицы на YT.
* Так же, появилась возможность указывать уровень сжатия.
  По-умолчанию используется средний.
* И была добавлена поддержка `required` полей.

## 0.0.4

Первая версия куба в ведении DMP.
