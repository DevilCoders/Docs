Утилита предназначена для получения features в окрестности пересечения границ административно-территориальных единиц
с участками дороги.

Предварительно следует подготовить две таблицы с геометриями в YT.

1. Таблица с геометриями ЕATД (геометрии ЕАТД на момент написания утилиты задавались в виде MultiPolygon). Для этого
можно использовать, например такой YQL запрос:

```sql

INSERT INTO hahn.`temp/maps_mrc/ad_geom` WITH TRUNCATE
SELECT
    geom_table.shape as geom
FROM hahn.`home/maps/core/garden/stable/ymapsdf/latest/cis1/ad` AS ad_table
FULL JOIN hahn.`home/maps/core/garden/stable/ymapsdf/latest/cis1/ad_geom` AS geom_table USING (ad_id)
WHERE ad_table.level_kind BETWEEN 2 AND 4;
```

2. Таблица с геометриями участков дорог (на момент написания утилиты - Polyline)

```sql
INSERT INTO hahn.`temp/maps_mrc/rd_geom` WITH TRUNCATE
SELECT
    shape as geom
FROM hahn.`home/maps/core/garden/stable/ymapsdf/latest/cis1/rd_el`
WHERE fc <= 5;
```

После этого можно вызвать утилиту:

```
 ./extract_features_on_intersection --mrc-config <???> --input1 //temp/maps_mrc/ad_geom --input2 //temp/maps_mrc/rd_geom --filter ./full_dataset_ids.txt --output ./results.txt
```