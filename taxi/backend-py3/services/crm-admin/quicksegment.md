Quicksegment
====

# Описание

Quicksegment позволяет описывать логику формирования сегмента для разных типов кампаний.
Схемы настраиваются через [админку фильтров](https://campaign-management-unstable.taxi.tst.yandex-team.ru/settings/quick-segments/User/0.291/filter_schema)
и состоят из трех разделов:
  - Table catalog (table_schema) - описание input таблиц и связей между ними
  - Логика формирования сегмента (filter_schema) - описание фильтров, по которым выбираются данные (страна, город, и т.п.)
  - Input параметры (input_schema) - отображение настроек фильтров кампании на стороне фронта (типы полей, описание, расположение и т.п.)

По сути, table_schema отчечает за SQL from и join clauses, а filter_schema -
where and having clauses.

Основной код для работы со схемами находится [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/backend-py3/services/crm-admin/crm_admin/quicksegment),
a оригинальный репозиторий с описаниями формата и набором инструментов для отладки - [здесь](https://github.yandex-team.ru/mnozdrachev/table-catalog)

## Примеры схем

### table_schema

```yaml
tables:
  - name: main
    path: //path/to/main
    select:
      - entity_id
      - features.value

  - name: features
    path: //path/to/features

root_table: main

graph:
  - how: inner
    left: main
    right: features
    keys: entity_id
```

### filter_schema

```yaml
filters:
  - id: first
    where: >
      main.entity_id is not null

  - id: second
    enabled-if: ${var} is not null
    where: >
      features.prop = ${var}

  - id: main
    where: >
      %{first}
      and %{second}

targets:
  - main

extra_columns:
  - if: ${var} is not null
    then: features.prop
```

Самый неочевидный параметр в этой схеме - это `targets` - это roots всех независимых
extresion trees в фильтрах. Target - это root filter id для sub-query.

Sub-queries определяются исключительно структурой table_schema. Sub-query
root table (anchor) - это:
  - root table
  - таблицы с group by clause
  - таблицы приджойненные через semi/anti join.

Все фильтры принадлежащие одной anchor table должны быть явно объеденены
в одно выражение ('main' filter в примере). Не может быть больше одного
target для одной anchor table.

В идеале, тот список должен вычился автоматически, но сейчас он явно указывается
руками.

### SQL

Схемы выше приводят к SQL запросу:
```sql
SELECT __features__prop AS prop,
       __features__value AS value,
       entity_id
  FROM main
 INNER JOIN (
        SELECT KEY AS __features__key,
               prop AS __features__prop,
               value AS __features__value
          FROM features
       ) AS features
    ON main.entity_id = features.__features__entity_id
 WHERE (main.entity_id IS NOT NULL)
   AND (__features__prop = ${var})
```


# API and Versions

Quicksegment API описано в [quicksegment.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/backend-py3/services/crm-admin/docs/yaml/api/quicksegment.yaml).

У сохраненных конфигов есть некоторая система версионирования. Каждый набор
схем (table_schema + filter_schema + input_schema) имеет общую версию.

Версия соcтотит из двух числе major version and minor version. Мы считаем,
что разные major версии примерно соответсвуют разным веткам и могут
использоваться для разных целей (мажорное обновление логики,
ветка для тестеров, ветка для разработки и т.п.).

К каждой кампании привязана определенная major version конфигов,
и при расчетах всегда испольщуется последняя minor версия
(соответсвующая major версии).  Кампания создается с major version
из `CRM_ADMIN_SETTINGS.QuicksegmentSettings.default_version`
и в проде это параметр не может быть в дальнейшем изменен.


# Query Builder

Точка входа для qs - это [query builder](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/backend-py3/services/crm-admin/crm_admin/quicksegment/query_builder.py?rev=r8413775#L801).


# Debugging

Логи можно посмотреть примерно так:
[link](https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(time:(from:now-1h,to:now))&_a=(query:(language:kuery,query:'ngroups%3Ataxi_crm-admin%2A%20and%20stq_task_id%3Acampaign_116%2A')))

В логах можно найти
  * command line arguments: <br>
    `INFO: running ['spark-submit-yt', '--deploy-mode=cluster', '--proxy=hahn',...`
  * generated SQL query: <br>
    `INFO: quicksegment query: SELECT ...`
  * variables: <br>
    `INFO: variables: {'country': ['br_russia'], 'node_id': ['br_saintpetersburg'],...`
  * link to the driver logs: <br>
    `INFO: driver stdout: http://.../logPage/...`
  * driver status link: <br>
    `INFO asking task status: http://.../v1/submissions/status/...`
