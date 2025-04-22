# Amenities mapping codegen

Генерирует маппиги для различных удобств для партнеров.
Также генерирует маппинги для общего кода в папке `feeders/lib/model`

## Запуск

```shell script
ya make -t . && ./amenities_mapping_codegen
```

## Запуск для одного партнера

```shell script
ya make -t . && ./amenities_mapping_codegen [partner]
```
