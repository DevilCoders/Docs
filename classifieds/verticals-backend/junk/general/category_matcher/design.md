# Админка для матчинга категорий

## Задачи
Для фидов необходим маппинг категорий + тегов чужого формата (avito, market) на наши категории.
В общем виде это можно представить как отображение `category + {key1: value1, key2: value2} -> [generalCategoryId]`, 
где `key1`, `key2` – произвольные теги из чужого фида, а `[generalCategoryId]` – набор идентификаторов категорий в Я.Объявлениях.

Примеры (Авито):
1) category="Товары для компьютера", tags={"GoodsType": "Блоки питания"} -> ["bloki-pitaniya-1_Iy38bu"]
2) category="Одежда, обувь, аксессуары", tags={"GoodsType": "Женская одежда", "Apparel": "Брюки"} -> ["bryuki-dlya-zhenshchin_Cv3xqY"] 
3) category="Красота и здоровье", tags={"GoodsType": "Медицинские изделия"} -> ["pribory-i-aksussuary_lsNv9V", "dezinficiruuschie-sredstva_4st2q9"]

## Основные сценарии
- работа с матчингами (создание, редактирование, удаление, листинг)
- экспорт в YT/s3
- кросс-валидации с bonsai (подсвечивать маппинги, указывающие на симлинки или заархивированные категории)
- саджест для категорий general по имени
- саджест существующих категорий
- саджест существующих тегов и их значений
- работа с тегами (создание, редактирование, удаление, листинг)
- работа со значениями тегов (создание, редактирование, удаление, листинг)

### API
[gRPC](../../schema-registry/proto/general/category_matcher/api.proto)

### Экспорт в YT
Периодически экспортируем таблицу `avito_mapping` в YT и s3.
Раскладка в виде json, не плоская. Набор колонок тот же, что и в исходной таблице.

### Кросс-валидации с bonsai
Процесс использует снепшот каталога bonsai.
По таблице `mapping_inverted` проверяем все категории и формируем отчет.

## Хранение
В качестве базы используем PostgreSQL

`category` - таблица с категориями
  - namespace: enum {avito, market} - тип фида, для которого делается маппинг
  - category: text - название категории

`tag` – таблица с тегами. В ключе отображения могут использоваться только они.
  - namespace: enum {avito, market} - тип фида, для которого делается маппинг
  - name: text – имя тега
  - count: integer – число маппингов с таким тегом в пределах неймспейса
  PK (namespace, name)
  
`tag_value` – таблица со значениями тегов. В ключе отображения могут использоваться только они.
  - namespace: enum {avito, market} - тип фида, для которого делается маппинг
  - name: text – имя тега
  - value: text - значение тега
  - count: integer – число маппингов с таким тегом в пределах неймспейса
   PK (namespace, name)  
  
`mapping`
  - namespace: enum {avito, market} - тип фида, для которого делается маппинг
  - category text
  - tags hstore
  - generalCategoryId text[]
  PK (namespace, category, tags)
  
`mapping_inverted`
  - generalCategoryId text
  - category text
  - tags hstore
  PK (generalCategoryId, namespace, category, tags)  
    