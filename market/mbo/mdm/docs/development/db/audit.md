# Аудит в МДМ

[Теория для слабаков, давайте сразу к примерам в YQL!](#yql)

Аудитом мы называем *историю изменений данных* в МДМ. Как мастер-система, мы обязаны предоставлять такую информацию для решения рабочих задач:
- Анализ качества данных "было" vs "стало"
- Поиск причин проблем
- Восстановление данных в случае порчи
- Построение отчётности по работе операторов смежных компонент

{% note info "Другой аудит" %}

В реальном мире аудитом называют проверку предприятия или учреждения на соответствие установленным государственным или международным стандартам. Это не имеет никакого отношения к обсуждаемому здесь аудиту. Но так уж исторически сложилось, что две разных вещи называют одним термином.

{% endnote %}

## Старый аудит

"Старым" аудитом мы называем историю изменений таблиц, хранящихся в PostgreSQL. В Yt он доступен по пути [//home/market/production/mbo/mdm/audit/mdm_audit_archive](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mbo/mdm/audit/mdm_audit_archive).

Схема:

change_type (string) | changes (yson) | context (string) | entity_key (string) | entity_type (string) | event_id (uint64) | event_timestamp (string)
:---|:---|:---|:---|:---|:---|:---
Тип изменения, один из `INSERT`, `UPDATE` или `DELETE` | Сами изменения, см. ниже описание формата | Имя треда или обработчика события. Позволяет понять, какой процесс в коде сделал изменение | Ключ сущности. Если ключ составной, то стыкуется через пробел, например, ключ SSKU будет выглядеть как `12345 my-shop-sku` | Тип сущности, например, маппинг, MasterData или ReferenceItem. Полный список будет указан ниже | Внутренний ID события аудита, почти никогда не нужен | Время изменения в UTC

**Формат колонки changes**

Зависит от `change_type`.

{% list tabs %}

- INSERT

  В `changes` будет лежать конвертированная в Yson добавленная строка таблицы. Например, так будет выглядеть добавленная MasterData:

  ```yson
  {
    "data" = {
        "datacampMasterDataVersion" = 1765641708705525425;
        "gtins" = [
            "4601164003133"
        ];
        "manufacturerCountry" = [];
        "shelfLife" = {
            "time" = 1;
            "unit" = "YEAR"
        };
        "shelfLifeComment" = #;
        "vat" = 7;
    };
    "is_uploaded_to_yt_arnold" = %false;
    "is_uploaded_to_yt_hahn" = %false;
    "modified_timestamp" = "2022-02-09T07:50:12.160114";
    "msku_import_status" = %false;
    "msku_import_ts" = "2000-01-01T00:00:00";
    "shop_sku" = "00000408112";
    "supplier_id" = 3892448;
    "version" = 1
  }
  ```

  Если бы вы, скажем, захотели достать все GTIN-ы, добавленные с определённой даты, то YQL могла бы выглядеть так:

  ```sql
  select changes.data.gtins from hahn.`//home/market/production/mbo/mdm/audit/mdm_audit_archive`
  where
    entity_type = 'ваш тип сущности'
    and event_timestamp > 'ваша_дата';
  ```

- UPDATE

  В `changes` будет лежать конвертированная в Yson изменённая строка таблицы, причём только те поля, что реально изменились. Все изменённые поля превращаются в массивы длины два. В нулевом элементе массива будет лежать версия поля "до", а в первом элементе массива - "после". Например, так будет выглядеть изменённый маппинг:

  ```yson
  {
    "eox_timestamp": [
        "2022-04-22T12:35:23.178856",
        "2022-04-22T13:17:24.567572"
    ],
    "mapping_source": [
        "MBOC_API",
        "DATACAMP"
    ],
    "update_stamp": [
        1037295743,
        null
    ]
  }
  ```

  Здесь мы видим, что свойство маппинга `eox_timestamp` изменилось со значения `2022-04-22T12:35:23.178856` на значение `2022-04-22T13:17:24.567572`, а свойство `mapping_source` изменилось с `MBOC_API` на `DATACAMP` и так далее. Если бы вы, скажем, захотели достать все маппинги, которые потрогал Datacamp с определённой даты, то YQL могла бы выглядеть так:

  ```sql
  select entity_key, changes from hahn.`//home/market/production/mbo/mdm/audit/mdm_audit_archive`
  where
    entity_type = 'ваш тип сущности'
    and Yson::ConvertToString(changes.mapping_source[1]) = 'DATACAMP'
    and event_timestamp > 'ваша_дата';
  ```

  {% note warning %}

  Ещё раз подчёркиваем, что в случае `UPDATE` в аудит попадают только фактически изменившиеся поля. Поэтому в примере выше нельзя написать `select changes.supplier_id, changes.shop_sku from ...`, ибо этих полей там не будет и `supplier_id` с `shop_sku` для всех update-ов будут равны `null`.

  {% endnote %}

- DELETE

  В `changes` будет лежать конвертированная в Yson удалённая строка таблицы. Например, так будет выглядеть удалённый параметр SSKU:

  ```yson
  {
    "bools" = [];
    "datacamp_master_data_version" = 1761033679095929100;
    "is_processed" = %false;
    "mdm_param_id" = 101;
    "numerics" = [];
    "options" = [];
    "shop_sku" = "1260772";
    "source_id" = "923547";
    "source_type" = "SUPPLIER";
    "source_updated_ts" = "2021-12-20T17:01:00";
    "ssku_silver_transport" = "DATACAMP";
    "strings" = [
        "Китай"
    ];
    "supplier_id" = 923547;
    "updated_ts" = "2021-12-21T15:40:24.274602";
    "xsl_name" = "manufacturerCountry"
  }
  ```

  Если бы вы, скажем, захотели достать все страны производства, удалённые с определённой даты, то YQL могла бы выглядеть так:

  ```sql
  select changes.strings from hahn.`//home/market/production/mbo/mdm/audit/mdm_audit_archive`
  where
    entity_type = 'ваш тип сущности'
    and Yson::ConvertToString(changes.xsl_name) = 'manufacturerCountry'
    and event_timestamp > 'ваша_дата';
  ```

{% endlist %}

## Новый аудит

Это интегрированные в Yt-хранилища таблички, автоматически заполняемые при любых существенных апдейтах. Всегда лежат рядом с обычными таблицами, но имеют суффикс `snapshot`. Например, для таблицы [MSKU](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/mdm/storage/msku_gold) имеется соответствующая [snapshot-табличка](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/market/production/mdm/storage/msku_gold_snapshot).

Схема:

event_id | mdm_id | mdm_entity_type_id | mdm_entity | version_from
:---|:---|:---|:---|:---
ID события аудита. Чаще всего не нужно, но позволяет отличить одно событие сохранения от другого | ID сущности в БМДМ. Проще всего вычислить его по [индексной таблице](yt_storage.md#mdm_id) | ID типа сущности из [Конструктора](https://mdm.market.yandex-team.ru/constructor/mdm-entity-types/0) | Изменения "после" (без "до") в формате [Entity](yt_storage.md#entity), см. ниже подробности | Таймштамп в UTC в миллисекундах с точным временем изменения

**Формат изменений**

Как и со старым аудитом, зависит от типа изменения — создание, обновление или удаление. Разница лишь в том, что в новом аудите нет явной колонки с указанием типа операции, но это можно понять по самой сущности.

{% list tabs %}

- Создание

  В `mdm_entity` будет лежать полноценная сущность, ничем не отличающаяся от "оригинала" в основной таблице.

- Обновление

  В `mdm_entity` будет лежать сущность версии "после" (то есть свежая, фактически сохраняемая). Однако из неё будут исключены поля, не имеющие существенных изменений.

  Например, пусть у нас есть сущность "до":

  ```json
  {
      "mdm_entity": {
          "mdm_id": 2356823142,
          "mdm_entity_type_id": 1042432961,
          "mdm_attribute_values": {
              "12345": {
                  "mdm_attribute_id": 12345,
                  "values": [ { "string": "Красный" }, { "string": "Синий" }, { "string": "Зелёный" } ]
              },
              "67890": {
                  "mdm_attribute_id": 67890,
                  "values": [ { "numeric": "3.14159265" } ]
              },
              "102030": {
                  "mdm_attribute_id": 102030,
                  "values": [ { "int64": 9000 } ]
              }
          }
      }
  }
  ```

  и её пересохранили с небольшими изменениями:

  ```json
  {
      "mdm_entity": {
          "mdm_id": 2356823142,
          "mdm_entity_type_id": 1042432961,
          "mdm_attribute_values": {
              "12345": {
                  "mdm_attribute_id": 12345,
                  "values": [ { "string": "Пурпурный" }, { "string": "Синий" } ]
              },
              "67890": {
                  "mdm_attribute_id": 67890,
                  "values": [ { "numeric": "3.14159265" } ]
              },
              "102030": {
                  "mdm_attribute_id": 102030,
                  "values": [ { "int64": -32 } ]
              }
          }
      }
  }
  ```

  Тогда в аудит запишется сущность только с изменёнными полями:

  ```json
  {
      "mdm_entity": {
          "mdm_attribute_values": {
              "12345": {
                  "mdm_attribute_id": 12345,
                  "values": [ { "string": "Пурпурный" }, { "string": "Синий" } ]
              },
              "102030": {
                  "mdm_attribute_id": 102030,
                  "values": [ { "int64": -32 } ]
              }
          }
      }
  }
  ```

  На примере видно, что неизменные поля идентификаторов сущности, равно как и нетронутый параметр `67890` в аудит не попали. Но что будет, если атрибут вообще удалили? В таком случае мы запишем пустой атрибут, а в поле метаинформации укажем ему флажок `deleted = true`.

  ```json
  {
      "mdm_entity": {
          "mdm_attribute_values": {
              "12345": {
                  "mdm_attribute_id": 12345,
                  "mdm_update_meta": {
                      "deleted": true
                  }
              }
          }
      }
  }
  ```

- Удаление

  В `mdm_entity` будет лежать сущность с флагом удаления в метаинформации верхнего уровня.

  ```json
  {
      "mdm_entity": {
          "mdm_id": 2687969106,
          "mdm_update_meta": {
              "deleted": true,
              "from": 1647694039885,
              "to": 1649314303110
          }
      }
  }
  ```

  В данном случае `version_to` указывает на дату смерти объекта.

{% endlist %}

---

**Существенность изменений**

Поскольку данный вариант аудита пишется только в разрезе фактических существенных изменений, неплохо было бы определить, а что именно мы считаем существенным.

- Сущность создаётся или удаляется целиком
- Добавился или удалился атрибут
- Изменилось значение простого (не `STRUCT`) атрибута

  *Если атрибут мультизначный, то существенным считается как качественное обновление хотя бы одного из значений, так и количественные изменения. Изменение порядка тоже считается существенным.*

- Изменились тип или ID источника в `MdmSourceMeta` у атрибута
- Изменилась вложенная `STRUCT` в атрибуте-контейнере

  *В этом случае ко вложенной entity будут рекурсивно применены те же правила построения diff-а, что и к обычной "внешней" сущности. Таким образом, в аудите все вложенные сущности тоже являют собой неполные diff-ы лишь с фактическими изменениями.*

## Аудит MBO

Аудит офферов Категорийного Интерфейса и карточек MSKU из MBO. Доступен [здесь](https://mbo.market.yandex-team.ru/ui/audit). В целом, достаточно интуитивен, но есть тонкости:

- Указывайте корректные даты в "Начало" и "Конец периода". Иногда настройка по умолчанию чудит и указывает противоречивые даты в 0 дней.
- Всегда переключайте "Системные свойства" в активное положение. Многие МДМ-атрибуты имеют свойство "Служебные", и потому не попадают в стандартную выдачу.
- В колонке `ID: ID объекта | S: Источник` по индикатору источника можно понять, какая подсистема внесла изменения. Для МДМ там есть отдельный источник и он будет отображаться явно как `S: MDM`.
- Если страница не открывается или чудит, возможно у вас не хватает прав. Запросить их можно по [форме](https://wiki.yandex-team.ru/market/sluzhba-kataloga/MBO/).

## Хрестоматия YQL-щика {#yql}

В шапку ко всем запросам рекомендуется прописать:

```
use hahn;
PRAGMA AnsiInForEmptyOrNullableItemsCollections;
pragma yson.DisableStrict;
pragma simplecolumns = 'true';
```

### Электрум SSKU (master_data)

**Аудит:** старый
**entity_type:** `master_data`
**Пример entity_key:** `465852 000064.космо-енот1`

{% cut "Что происходило с SSKU" %}

```sql
select * from hahn.`home/market/production/mbo/mdm/audit/mdm_audit_archive`
where entity_type = 'master_data' and entity_key = '465852 022753.2211100115-50-L'
order by event_id desc
limit 500;
```

[YQL](https://yql.yandex-team.ru/Operations/YmLgDJfFt6kXkA4R6xK3g-DViFfU1HEksvYEhBOfhPU=)

{% endcut %}


{% cut "1P SSKU с большими квантами с определённой даты" %}

```sql
select * from hahn.`home/market/production/mbo/mdm/audit/mdm_audit_archive`
where entity_type = 'master_data'
  and entity_key like '465852%'
  and Yson::ConvertToInt64(coalesce(changes.data.quantumOfSupply[1], changes.data.quantumOfSupply)) > 1
  and event_timestamp > '2022-04-15T00:00:00.000000Z'
order by event_id desc
limit 500;
```

[YQL](https://yql.yandex-team.ru/Operations/YmLnA9JwbG6XRAelyxC4t5qaT7du5TrzItyg4-JNbcE=)

{% endcut %}


### Золото SSKU (reference_item)

**Аудит:** старый
**entity_type:** `reference_item`
**Пример entity_key:** `465852 000064.космо-енот1`

{% cut "Что происходило с золотом SSKU" %}

```sql
select *
from hahn.`home/market/production/mbo/mdm/audit/mdm_audit_archive`
where entity_type = 'reference_item'
  and entity_key = '465852 022753.2211100115-50-L'
order by id desc
limit 500;
```

[YQL](https://yql.yandex-team.ru/Operations/YmLlXdJwbG6XRARZfM99_EROrMxLB04cWzGuIv1AwBM=)

{% endcut %}

{% cut "Изменения ОСГ в варке золота за период" %}

```sql
select cast(String::SplitToList(entity_key, ' ')[0] as Uint32) as supplier_id,
       String::SplitToList(entity_key, ' ')[1] as shop_sku
from hahn.`home/market/production/mbo/mdm/audit/mdm_audit_archive`
where entity_type = 'reference_item'
  and change_type = 'UPDATE'
  and event_timestamp > '2022-03-14T10:46:00.000000Z'
  and event_timestamp < '2022-03-15T13:10:00.000000Z'
  and ToBytes(changes) like '%rsl%'
  and context like 'SskuGoldWorker%'
limit 500;
```

[YQL](https://yql.yandex-team.ru/Operations/YmLltNJwbG6XRAUNi8a5n_5in2qTNvmuCuNjPLGcBIY=)

{% endcut %}

### Маппинги

**Аудит:** старый
**entity_type:** `mappings_cache`
**Пример entity_key:** `465852 000064.космо-енот1`

### Рубильники

**Аудит:** старый
**entity_type:** `storage_key_value`
**Пример entity_key:** `sskuGoldRequeueFailed`

### Поставщики

**Аудит:** старый
**entity_type:** `supplier`
**Пример entity_key:** `465852`

{% cut "Что происходило с партнёром" %}

```sql
select *
from hahn.`home/market/production/mbo/mdm/audit/mdm_audit_archive`
where entity_type = 'supplier'
  and entity_key = '4418468'
order by id desc
limit 500;
```

[YQL](https://yql.yandex-team.ru/Operations/YlVmRq5OD5h1_qkXQyAsdXUHVqsdOah6oT3JJQD-FHw=)

{% endcut %}

### Категорийные настройки

**Аудит:** старый
**entity_type:** `category_param_value`
**Пример entity_key:** `1003092 13`

Пояснение к ключу: 13 - это ID атрибута в старом МДМ, его можно посмотреть в [Конструкторе](https://mdm.market.yandex-team.ru/constructor/mdm-entity-type/1), нажав на внешнюю связь атрибута. Поле "Внешний id" и будет искомым числом.

### Серебро SSKU

**Аудит:** новый
**Таблица:** `home/market/production/mdm/storage/ssku_silver_snapshot`

### MSKU

**Аудит:** новый
**Таблица:** `home/market/production/mdm/storage/msku_gold_snapshot`
