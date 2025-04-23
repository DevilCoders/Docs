# mockEnrichment

## enrichEntities – переиспользование сущностей и фейк незаданных параметров
Позволяет избежать простыни при установки состояния мока.

Пример:

Без хелпера будет что-то вроде

data=
```json
[
{"entity": "product", "id": "1", "vendor": {"id": "1", "someprop": "val"}},
{"entity": "offer", "wareid": "ololo", "vendor": {"id": "1", "someprop": "val"}}
]
```

С хелпером:
collections=
```json
{
    "entities": {
        "vendor": {
            "1": {"id": "1", "someprop": "val"}
        }
    }
}
```

data=
```json
[
{"entity": "product", "id": "1", "vendor": {"id": "1"}},
{"entity": "offer", "wareid": "ololo", "vendor": {"id": "1"}}
]
```

Вывод будет аналогичен выводу без хелпера, плюс будут зафейканы (если не переопределены в collections или data) 
обязательные и опциональные поля (случайным образом).

Дескриптор:
enrichEntities(collections, data, dataSchema, formatResolver = defaultFormatResolver, entityDecorator = null)

Аргументы:
* collections коллекция базовых сущностей, которую применить к items.
* data денонармализованная структура которую нужно обогатить в соотв со схемой.
* dataSchema схема для нормализации items.
* formatResolver резолвер, возвращающий микроформат по entity type
* entityDecorator ф-ция которая применяется к каждой денормализованной сущности, перед мержом
